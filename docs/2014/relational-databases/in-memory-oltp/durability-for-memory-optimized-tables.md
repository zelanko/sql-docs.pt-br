---
title: Durabilidade para tabelas com otimização de memória | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: d304c94d-3ab4-47b0-905d-3c8c2aba9db6
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: fb0f2dec6ac7ad68a6a1aa1de8d4734f99559b54
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/28/2020
ms.locfileid: "78175939"
---
# <a name="durability-for-memory-optimized-tables"></a>Durabilidade de tabelas com otimização de memória
  [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] fornece a durabilidade completa para tabelas com otimização de memória. Quando uma transação que modificou uma tabela com otimização de memória é confirmada, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (como faz em tabelas baseadas em disco), garante que as alterações sejam permanentes (sobreviverão uma reinicialização do banco de dados), contanto que o armazenamento subjacente esteja disponível. Há dois principais componentes de durabilidade: log de transações e persistência das alterações de dados para armazenamento em disco.

## <a name="transaction-log"></a>Log de Transações
 Todas as alterações feitas nas tabelas baseadas em disco ou tabelas duráveis com otimização de memória são capturadas em um ou mais registros de log de transações. Depois da confirmação de uma transação, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] grava os registros de log associados com a transação no disco antes de comunicar ao aplicativo ou à sessão de usuário que a transação foi confirmada. Isso garante que as alterações feitas pela transação sejam duráveis. O log de transações para tabelas com otimização de memória está totalmente integrado ao mesmo fluxo de log usado por tabelas baseadas em disco. Essa integração permite que operações existentes de backup, recuperação e restauração do log de transações continuem funcionando, sem exigir etapas adicionais. No entanto, como o [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] pode aumentar significativamente a taxa de transferência de transações de sua carga de trabalho, será necessário verificar se o armazenamento de log de transações está configurado adequadamente para controlar os requisitos de aumento de E/S.

## <a name="data-and-delta-files"></a>Arquivos delta e de dados
 Os dados nas tabelas com otimização de memória são armazenados como as linhas de dados de forma livre que são vinculadas por meio de um ou mais índices de memória, na memória. Não há nenhuma estrutura de página para linhas de dados, como as usadas para tabelas baseadas em disco. Quando o aplicativo está pronto para confirmar a transação, o [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] gera os registros de log para a transação. A persistência de tabelas com otimização de memória é feita com um conjunto de dados e arquivos delta usando um thread em segundo plano. Os dados e os arquivos delta estão localizados em um ou mais contêineres (com o mesmo mecanismo usado para dados FILESTREAM). Esses contêineres são mapeados para um novo tipo de grupo de arquivos, chamado de grupo de arquivos com otimização de memória.

 Os dados são gravados nesses arquivos de maneira estritamente sequencial, o que minimiza a latência do disco na rotação da mídia. Você pode usar vários contêineres em discos diferentes para distribuir a atividade de E/S. Os arquivos delta e de dados em vários contêineres em discos diferentes aumentarão o desempenho de recuperação quando os dados forem lidos nos arquivos delta e de dados em disco, na memória.

 Um aplicativo não pode acessar diretamente arquivos delta e de dados. Todas as leituras e gravações de dados usam dados na memória.

### <a name="the-data-file"></a>O arquivo de dados
 Um arquivo de dados contém linhas de uma ou mais tabelas com otimização de memória que foram inseridas por várias transações como parte das operações INSERT ou UPDATE. Por exemplo, uma linha pode ser de uma tabela com otimização de memória T1 e a linha seguinte pode ser da tabela com otimização de memória T2. As linhas são acrescentadas ao arquivo de dados na ordem das transações no log de transações, tornando o acesso aos dados sequencial. Isso permite uma taxa de transferência de E/S significativamente melhor em comparação com a E/S aleatória. Cada arquivo de dados é dimensionado aproximadamente para 128MB para computadores com mais memória que 16GB e 16MB para computadores com menos que ou igual a 16GB. Quando o arquivo de dados estiver cheio, as linhas inseridas por novas transações serão armazenadas em outro arquivo de dados. Com o tempo, as linhas de tabelas com otimização de memória duráveis são armazenadas em um de mais arquivos de dados e em cada arquivo de dados que contém linhas de um intervalo não contíguo, mas contíguo de transações. Por exemplo, um arquivo de dados com o carimbo de data/hora de confirmação de transação no intervalo de (100, 200) tem todas as linhas inseridas por transações com o carimbo de data/hora de confirmação maior que 100 e menor que ou igual a 200. O carimbo de data/hora de confirmação é um número que aumenta de forma monotônica atribuído a uma transação quando está pronto para confirmação. Cada transação tem um carimbo de data/hora de confirmação exclusivo.

 Quando uma linha é excluída ou atualizada, ela não é removida, nem alterada no local no arquivo de dados, mas as linhas excluídas são rastreadas em outro tipo de arquivo: o arquivo delta. As operações de atualização são processadas como uma tupla de operações de exclusão e inserção para cada linha. Isso elimina a E/S aleatória no arquivo de dados.

### <a name="the-delta-file"></a>O arquivo delta
 Cada arquivo de dados é emparelhado com um arquivo delta que tem o mesmo intervalo de transações e rastreia as linhas excluídas inseridas por transações nesse intervalo. Estes arquivos de dados e delta são chamados de Par de Arquivos de Ponto de Verificação (CFP) e são a unidade da alocação e deslocamento, bem como a unidade de operações de Mesclagem. Por exemplo, um arquivo delta correspondente ao intervalo de transações (100, 200) armazenará as linhas excluídas que foram inseridas por transações no intervalo (100, 200). Assim como os arquivos de dados, o arquivo delta é acessado sequencialmente.

 Quando uma linha é excluída, ela não é removida do arquivo de dados, mas uma referência a ela é anexada ao arquivo delta associado ao intervalo de transações em que essa linha de dados foi inserida. Como a linha de dados a ser excluída já existe no arquivo de dados, o arquivo delta armazena apenas as informações de referência `{inserting_tx_id, row_id, deleting_tx_id }` e segue a ordem do log transacional das operações de exclusão ou atualização originais.

## <a name="populating-data-and-delta-files"></a>Populando arquivos de dados e delta
 Os arquivos de dados e delta são populados por um thread em segundo plano chamado de ponto de verificação offline. Esse thread lê os registros do log de transações gerados por transações confirmadas em tabelas com otimização de memória e anexa informações sobre as linhas inseridas e excluídas em arquivos delta e de dados apropriados. Diferentemente das tabelas baseadas em disco, nas quais páginas de dados/índice são liberadas com E/S aleatória quando o ponto de verificação é realizado, a persistência da tabela com otimização de memória é uma operação em segundo plano contínua. Vários arquivos delta são acessados, pois uma transação pode excluir ou atualizar qualquer linha que foi inserida por qualquer transação anterior. As informações de exclusão sempre são anexadas no final do arquivo delta. Por exemplo, uma transação com um carimbo de data/hora de confirmação de 600 insere uma linha nova e exclui linhas inseridas por transações com um carimbo de data/hora de confirmação de 150, 250 e 450, conforme mostrado na imagem a seguir. As quatro operações de E/S de arquivo (três para linhas excluídas e uma para as linhas recentemente inseridas) são operações somente de acréscimo nos arquivos delta e de dados correspondentes.

 ![Registros de leitura de log para tabelas com otimização de memória.](../../database-engine/media/read-logs-hekaton.gif "Registros de leitura de log para tabelas com otimização de memória.")

## <a name="accessing-data-and-delta-files"></a>Acessando arquivos delta e de dados
 Os pares de arquivos de dados e delta são acessados quando as situações a seguir ocorrem.

 Thread de ponto de verificação offline esse thread anexa inserções e exclusões a linhas de dados com otimização de memória para os pares de arquivos Delta e de dados correspondentes.

 Operação de mesclagem a operação mescla um ou mais pares de arquivos Delta e de dados e cria um novo par de arquivos Delta e de dados.

 Durante a recuperação de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] falha quando o é reiniciado ou o banco de dados é colocado online novamente, o dado com otimização de memória é populado usando os pares de arquivos Delta e de dados. O arquivo delta atua como um filtro para as linhas excluídas ao ler as linhas do arquivo de dados correspondente. Como cada par de arquivos delta e de dados é independente, esses arquivos são carregados paralelamente para reduzir o tempo necessário para popular os dados na memória. Depois que os dados forem carregados na memória, o mecanismo OLTP na memória aplicará os registros de log de transações ativos ainda não cobertos pelos arquivos de ponto de verificação para que os dados com otimização de memória sejam concluídos.

 Durante a operação de restauração, os arquivos de ponto de verificação OLTP na memória são criados a partir do backup de banco de dados e um ou mais backups de log de transações são aplicados. Assim como na recuperação de pane, o mecanismo OLTP na memória carrega os dados na memória paralelamente para minimizar o impacto no tempo de recuperação.

## <a name="merging-data-and-delta-files"></a>Mesclando arquivos delta e de dados
 Os dados de tabelas com otimização de memória são armazenados em um ou mais pares de arquivos delta e de dados (também denominados pares de arquivos de ponto de verificação ou CFP). Os arquivos de dados armazenam linhas inseridas e os arquivos delta referenciam linhas excluídas. Durante a execução de uma carga de trabalho OLTP, enquanto as operações DML atualizam, inserem e excluem linhas, novos CFPs são criados para persistir as novas linhas e a referência às linhas excluídas é anexada aos arquivos delta.

 Os metadados de todos os CFPs fechados anteriormente e atualmente ativos são armazenados em uma estrutura de matriz interna referenciada como a matriz de armazenamento. É uma matriz de tamanho finito (8.192 entradas) de CFPs. As entradas na matriz de armazenamento são ordenadas pelo intervalo de transações. Os CFPs na matriz de armazenamento (junto com o final do log) representam todo o estado em disco necessário para recuperar um banco de dados com tabelas com otimização de memória.

 Com o tempo, com as operações DML, o número de CFPs cresce fazendo a matriz de armazenamento alcançar a capacidade, que apresenta os seguintes desafios:

-   Linhas excluídas.  As linhas excluídas permanecem no arquivo de dados, mas são marcadas como excluídas no arquivo delta correspondente. Essas linhas não são mais necessárias e serão removidas do armazenamento. Se as linhas excluídas não foram removidas de CFPs, elas usarão o espaço desnecessariamente e tornarão o tempo de recuperação mais lento.

-   Matriz de armazenamento cheia. Quando são alocadas 8.000 entradas na matriz de armazenamento (192 entradas na matriz são reservadas para que as mesclagens existentes disputem ou permitam que você faça mesclagens manuais), nenhuma nova transação DML pode ser executada em tabelas duráveis com otimização de memória. Somente as operações de ponto de verificação e mesclagem podem consumir as entradas restantes. Isso assegura que as transações DML não preencham a matriz e que algumas entradas na matriz sejam reservadas para mesclar os arquivos existentes e reclamar espaço na matriz.

-   Sobrecarga de manipulação da matriz de armazenamento. Os processos internos procuram na matriz de armazenamento operações como localizar o arquivo delta para anexar informações sobre uma linha excluída. O custo dessas operações aumenta com o número de entradas.

 Para ajudar a evitar essas ineficiências, os CFPs fechados mais antigos são mesclados, com base em uma política de mesclagem descrita abaixo, para que a matriz de armazenamento seja compactada para representar o mesmo conjunto de dados, com um número reduzido de CFPs.

 O tamanho total da memória de todas as tabelas duráveis em um banco de dados não deve exceder 250 GB. As tabelas duráveis que usam até 250 GB de memória irão, supondo operações de inserção, exclusão e atualização, exigir na média 500 GB de espaço de armazenamento. Os 4.000 pares de arquivos delta e de dados no grupo de arquivos com otimização de memória são necessários para oferecer suporte a 500 GB de espaço de armazenamento.

 As sobrecargas de curto prazo na atividade do banco de dados pode causar atrasos no ponto de verificação e nas operações de mesclagem, o que aumentará o número de pares de arquivos delta e de dados. Para acomodar picos de sobrecarga de curto prazo na atividade de banco de dados, o sistema de armazenamento poderá alocar até 8.000 pares de arquivos delta e de dados até um total de 1TB de armazenamento. Quando o limite é atingido, nenhuma nova transação será permitida no banco de dados até que as operações de ponto de verificação recuperem o atraso. Se o tamanho de tabelas duráveis na memória exceder 250GB por longos períodos de tempo, há uma possibilidade de atingir o limite de 8.000 pares de arquivo.

 A operação de mesclagem utiliza como entrada um ou mais CFPs fechados adjacentes (denominados a origem da mesclagem) com base em uma política de mesclagem definida internamente e produz um CFP resultante, chamado destino de mesclagem. As entradas em cada arquivo delta dos CFPs de origem são usadas para filtrar linhas do arquivo de dados correspondente para remover as linhas de dados que não são necessárias. As linhas restantes nos CFPs de origem são consolidadas em um CFP de destino. Após a conclusão da mesclagem, o CFP de destino de mesclagem resultante substitui os CFPs de origem (origens de mesclagem). Os CFPs de origem de mesclagem passam por uma fase de transição antes de sua remoção do armazenamento.

 No exemplo abaixo, o grupo de arquivos da tabela com otimização de memória tem quatro pares de arquivos delta e de dados no carimbo de data/hora 500 que contém dados de transações anteriores. Por exemplo, as linhas no primeiro arquivo de dados correspondem a transações com carimbo de data/hora superior a 100 e inferior ou igual a 200; alternativamente representados como (100, 200]. O segundo e terceiro arquivos de dados apresentam menos de 50% de utilização após a contagem das linhas marcadas como excluídas. A operação de mesclagem combina esses dois CFPs e cria um novo CFP que contém transações com carimbo de data/hora superior a 200 e inferior ou igual a 400, que é o intervalo combinado desses dois CFPs. Você vê outro CFP com intervalo (500, 600] e o arquivo delta não vazio do intervalo de transações (200, 400] mostra que a operação de mesclagem pode ser realizada junto com atividades transacionais, incluindo a exclusão de mais linhas dos CFPs de origem.

 ![O diagrama mostra o grupo de arquivos de tabela com otimização de memória](../../database-engine/media/storagediagram-hekaton.png "O diagrama mostra o grupo de arquivos de tabela com otimização de memória")

 Um thread de segundo plano avalia todos os CFPs fechados usando uma política de mesclagem e, em seguida, inicia uma ou mais solicitações de mesclagem para os CFPs de qualificação. Essas solicitações de mesclagem são processadas pelo thread de ponto de verificação offline. A avaliação da política de mesclagem é feita periodicamente e também quando um ponto de verificação é fechado.

### <a name="sssql14-merge-policy"></a>[!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]Mesclar política
 
  [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] implementa a seguinte política de mesclagem:

-   Uma mesclagem será agendada se dois ou mais CFPs consecutivos puderem ser consolidados, após a contagem das linhas excluídas, para que as linhas resultantes possam caber em 1 CFP do tamanho ideal. O tamanho ideal do CFP é determinado desta forma:

    -   Se um computador tiver memória menor ou igual a 16 GB, o arquivo de dados será de 16 MB e o arquivo delta será de 1 MB.

    -   Se um computador tiver memória maior de 16 GB, o arquivo de dados será de 128 MB e o arquivo delta será de 16 MB.

-   Um único CFP pode ser automesclado caso o arquivo de dados exceda 256 MB e mais da metade das linhas serão excluídas. Um arquivo de dados poderá ficar com mais de 128 MB se, por exemplo, uma única transação ou várias transações simultâneas inserirem ou atualizarem grandes quantidades de dados, forçando o arquivo de dados a crescer além de seu tamanho ideal porque uma transação não pode se estender por vários CFPs.

 Veja alguns exemplos que mostram os CFPs que serão mesclados na política de mesclagem:

|CFPs de origem adjacentes (% de utilização)|Seleção de mesclagem|
|-------------------------------------------|---------------------|
|CFP0 (30%), CFP1 (50%), CFP2 (50%), CFP3 (90%)|(CFP0, CFP1)<br /><br /> O CFP2 não será escolhido, pois tornará o arquivo de dados resultante maior que 100% do tamanho ideal.|
|CFP0 (30%), CFP1 (20%), CFP2 (50%), CFP3 (10%)|(CFP0, CFP1, CFP2). Os arquivos são escolhidos a partir da esquerda.<br /><br /> O CTP3 não será escolhido, pois tornará o arquivo de dados resultante maior que 100% do tamanho ideal.|
|CFP0 (80%), CFP1 (30%), CFP2 (10%), CFP3 (40%)|(CFP1, CFP2, CFP3). Os arquivos são escolhidos a partir da esquerda.<br /><br /> O CFP0 é ignorado, pois se combinado com o CFP1, o arquivo de dados resultante será maior que 100% do tamanho ideal.|

 Nem todos os CFPs com o espaço disponível se qualificam para mesclagem. Por exemplo, se dois CFPs adjacentes apresentarem 60% de utilização, eles não estarão qualificados para mesclagem e cada um desses CFPs terá 40% do armazenamento não usado. No pior caso, todos os CFPs terão 50% de utilização, uma utilização do armazenamento de apenas 50%. Embora as linhas excluídas possam existir no armazenamento porque os CFPs não se qualificam para mesclagem, essas linhas talvez já tenham sido removidas da memória pela coleta de lixo na memória. O gerenciamento de armazenamento e de memória é independente da coleta de lixo. O armazenamento ocupado pelos CFPs ativos (nem todos os CFPs estão sendo atualizados) pode ser até 2 vezes maior do que o tamanho de tabelas duráveis na memória.

 Se necessário, uma mesclagem manual pode ser executada explicitamente chamando [Sys. sp_xtp_merge_checkpoint_files &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-merge-checkpoint-files-transact-sql).

### <a name="life-cycle-of-a-cfp"></a>Ciclo de vida de um CFP
 Transição de CPFs por vários estados antes de poderem ser desalocados. A qualquer momento, os CFPs estarão em uma das seguintes fases: PRECREATED, UNDER CONSTRUCTION, ACTIVE, MERGE TARGET, MERGED SOURCE, REQUIRED FOR BACKUP/HA, IN TRANSITION TO TOMBSTONE e TOMBSTONE. Para obter uma descrição dessas fases, veja [sys.dm_db_xtp_checkpoint_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql).

 Após a contagem do armazenamento ocupado pelos CFPs em diversos estados, o armazenamento geral ocupado pelas tabelas com otimização de memória duráveis poderá ser muito maior do que 2 vezes o tamanho das tabelas na memória. A [&#41;DMV. dm_db_xtp_checkpoint_files &#40;Transact-SQL](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql) pode ser consultada para listar todos os CFPS no grupo de arquivos com otimização de memória, incluindo sua fase. A transição de estados de CFPs de MERGE SOURCE para TOMBSTONE e por fim a coleta de lixo pode demorar cinco pontos de verificação, com cada ponto de verificação seguido por um backup de log de transações, caso o banco de dados esteja configurado para o modelo de recuperação completa ou bulk-logged.

 Você pode forçar manualmente o ponto de verificação seguido pelo backup de log para acelerar a coleta de lixo, mas isso adicionaria 5 CFPs vazios (5 pares de arquivos de dados/delta com o arquivo de dados de tamanho de 128 MB). Nos cenários de produção, os backups automáticos de pontos de verificação e log ocorrem como parte da estratégia de backup que executará a transição perfeita de CFPs por essas fases, sem a necessidade de nenhuma intervenção manual. O impacto do processo de coleta de lixo é que os bancos de dados com tabelas com otimização de memória podem ter um tamanho de armazenamento maior em comparação com seu tamanho na memória. Não é raro para CFPs serem até quatro vezes o tamanho das tabelas com otimização de memória duráveis em memória.

## <a name="see-also"></a>Consulte Também
 [Criando e gerenciando armazenamento para objetos com otimização de memória](creating-and-managing-storage-for-memory-optimized-objects.md)


