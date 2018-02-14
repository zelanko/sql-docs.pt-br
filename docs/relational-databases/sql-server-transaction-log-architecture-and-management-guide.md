---
title: "Guia de arquitetura e gerenciamento de log de transações do SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 01/05/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: relational-databases-misc
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transaction log architecture guide
- guide, transaction log architecture
- vlf
- transaction log guidance
- vlfs
- virtual log files
- virtual log size
- vlf size
- transaction log internals
ms.assetid: 88b22f65-ee01-459c-8800-bcf052df958a
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: cd276306b5fd40dd41602a573a2eb152ef5a6dda
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="sql-server-transaction-log-architecture-and-management-guide"></a>Guia de arquitetura e gerenciamento do log de transações do SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Todo banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tem um log de transações que registra todas as transações e modificações feitas no banco de dados a cada transação. O log de transações é um componente crítico do banco de dados e, se houver uma falha do sistema, será necessário que o log de transações retorne seu banco de dados a um estado consistente. Este guia fornece informações sobre a arquitetura física e lógica do log de transações. A compreensão da arquitetura pode melhorar sua efetividade na administração de logs de transações.  

  
##  <a name="Logical_Arch"></a> Arquitetura lógica de log de transações  
 O log de transações do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] opera de forma lógica como se o log de transações fosse uma cadeia de caracteres de registros de log. Cada registro de log é identificado por um LSN (número de sequência de log). Cada registro de log novo é gravado no final lógico do log com um LSN maior que o do registro antes da gravação. Os registros de log são armazenados em sequência consecutiva conforme são criados. Cada registro de log contém a ID da transação a que pertence. Para cada transação, todos os registros de log associados com a transação são vinculados individualmente em uma cadeia usando ponteiros de retrocesso que aceleram a reversão da transação.  
  
 Os registros de log para modificações de dados registram a operação lógica executada ou as imagens anteriores e posteriores dos dados modificados. A imagem anterior é uma cópia dos dados antes da execução da operação; a imagem posterior é uma cópia dos dados após a execução da operação.  
  
As etapas para recuperar uma operação dependem do tipo de registro de log:  
  
-   Log da operação lógica  
  
    -   Para avançar a operação lógica, é executada a operação novamente.  
  
    -   Para reverter a operação lógica, é executada a operação lógica inversa.  
  
-   Log da imagem anterior e posterior  
  
    -   Para avançar a operação lógica, é aplicada a imagem posterior.  
  
    -   Para reverter a operação lógica, é aplicada a imagem anterior.  
  
São registrados muitos tipos de operações no log de transações. Essas operações incluem:  
  
-   O início e o término de cada transação.  
  
-   Toda modificação de dados (inserção, atualização ou exclusão). Isso inclui mudanças por procedimentos armazenados do sistema ou instruções DDL (linguagem de definição de dados) para qualquer tabela, inclusive tabelas do sistema.  
  
-   Toda extensão e alocação ou desalocação de página.  
  
-   Criando ou descartando uma tabela ou um índice.  
  
 Operações de reversão também são registradas. Cada transação reserva espaço no log de transações para verificar se há espaço de log suficiente para oferecer suporte a uma reversão causada por uma instrução de reversão explícita ou se um erro for encontrado. A quantidade de espaço reservada depende das operações executadas na transação, mas geralmente é igual à quantidade de espaço usada para registrar cada operação. Esse espaço reservado é liberado quando a transação é concluída.  
  
<a name="minlsn"></a> A seção do arquivo de log do primeiro registro de log que deve estar presente para uma reversão bem-sucedida em todo o banco de dados para o registro de log da última gravação é chamada de parte ativa do log ou *log ativo*. Essa é a seção do log necessária para uma recuperação completa do banco de dados. Nenhuma parte do log ativo pode ter sido truncada. O [LSN (número de sequência de log)](../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) desse primeiro registro de log é conhecido como **LSN de recuperação mínima (*MinLSN*)**.  
  
##  <a name="physical_arch"></a> Arquitetura física de log de transações  
O log de transações em um banco de dados mapeia um ou mais arquivos físicos. Conceitualmente, o arquivo de log é uma cadeia de caracteres de registros de log. Fisicamente, a sequência de registros de log é armazenada com eficiência no conjunto de arquivos físicos que implementam o log de transações. Deve haver, no mínimo, um arquivo de log para cada banco de dados.  
  
O [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] divide cada arquivo de log físico internamente em vários VLFs (arquivos de log virtuais). Os arquivos de log virtuais não têm tamanho fixo e não há número fixo de arquivos de log virtuais para um arquivo de log físico. O [!INCLUDE[ssDE](../includes/ssde-md.md)] escolhe o tamanho dos arquivos de log virtuais dinamicamente enquanto está criando ou estendendo os arquivos de log. O [!INCLUDE[ssDE](../includes/ssde-md.md)] tenta manter um pequeno número de arquivos virtuais. O tamanho dos arquivos virtuais depois que um arquivo de log for estendido é a soma do tamanho do log existente com o tamanho do incremento do arquivo novo. O tamanho ou o número de arquivos de log virtuais não pode ser configurado nem definido por administradores.  

> [!NOTE]
> A criação de VLF (arquivos de log virtuais) segue este método:
> - Se o próximo crescimento for menor que 1/8 do tamanho físico do log atual, crie 1 VLF que abranja o tamanho do crescimento (começando com [!INCLUDE[ssSQL14](../includes/sssql14-md.md)])
> - Se o próximo crescimento for maior que 1/8 do tamanho atual do log, use o método pré-2014:
>    -  Se o crescimento for menor que 64 MB, crie 4 VLFs que abranjam o tamanho do crescimento (por exemplo, para um crescimento de 1 MB, crie quatro VLFs de 256 KB)
>    -  Se o crescimento for de 64 MB a 1 GB, crie 8 VLFs que abranjam o tamanho do crescimento (por exemplo, para um crescimento de 512 MB, crie oito VLFs de 64 MB)
>    -  Se o crescimento for maior que 1 GB, crie 16 VLFs que abranjam o tamanho do crescimento (por exemplo, para um crescimento de 8 GB, crie dezesseis VLFs de 512 MB)

Se os arquivos de log ficarem grandes, em diversos incrementos pequenos, eles terão muitos arquivos de log virtuais. **Isso pode reduzir a velocidade de inicialização do banco de dados e também das operações de backup e restauração de log.** Por outro lado, se os arquivos de log forem definidos para um tamanho grande com poucos ou apenas um incremento, eles terão poucos arquivos de log virtuais muito grandes. Para obter mais informações de como estimar corretamente as configurações **tamanho necessário** e **crescimento automático** de um log de transações, consulte a seção *Recomendações* de [Gerenciar o tamanho do arquivo de log de transações](../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md#Recommendations).

É recomendável que você atribua aos arquivos de log um valor de *tamanho* próximo ao tamanho final necessário, usando os incrementos necessários para alcançar uma distribuição de VLF ideal e também ter um valor de *growth_increment* relativamente grande. Consulte a dica abaixo para determinar a distribuição ideal de VLF para o tamanho atual do log de transações. 
 - O valor *size*, conforme definido pelo argumento `SIZE` de `ALTER DATABASE`, é o tamanho inicial do arquivo de log.
 - O valor *growth_increment* (também conhecido como valor de crescimento automático), conforme definido pelo argumento `FILEGROWTH` de `ALTER DATABASE`, é a quantidade de espaço adicionada ao arquivo sempre que um novo espaço é necessário. 
 
Para obter mais informações sobre os argumentos `FILEGROWTH` e `SIZE` de `ALTER DATABASE`, consulte [Opções de arquivo e grupo de arquivos de ALTER DATABASE &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md).

> [!TIP]
> Para determinar a distribuição ideal de VLF para o tamanho atual do log de transações de todos os bancos de dados em uma instância determinada e os incrementos de crescimento necessários para alcançar o tamanho necessário, consulte este [script](http://github.com/Microsoft/tigertoolbox/tree/master/Fixing-VLFs).
  
 O log de transações é um arquivo embrulhado. Por exemplo, considere um banco de dados com um arquivo de log físico dividido em quatro VLFs. Quando o banco de dados é criado, o arquivo de log lógico começa no início do arquivo de log físico. Novos registros de log são adicionados no final do log lógico e expandem para o final do log físico. O truncamento de logs libera quaisquer logs virtuais cujos registros apareçam todos na frente do número mínimo de sequência de recuperação do log (MinLSN). O *MinLSN* é o número de sequência de log do registro de log mais antigo que deve estar presente para o êxito de uma reversão de todo o banco de dados. O log de transações no banco de dados de exemplo pareceria semelhante ao apresentado na ilustração a seguir.  
  
 ![tranlog3](../relational-databases/media/tranlog3.gif)  
  
 Quando o final do log lógico alcança o final do arquivo de log físico, os novos registros de log são adicionados no início do arquivo de log físico.  
  
![tranlog4](../relational-databases/media/tranlog4.gif)   
  
 Esse ciclo repete-se indefinidamente, desde que o final do log lógico nunca alcance o início do log lógico. Se os registros de log antigos forem truncados com frequência suficiente para sempre deixar espaço suficiente para todos os registros de log novos criados através do próximo ponto de verificação, o log nunca estará completo. Contudo, se o final do log lógico não alcançar o início do log lógico, ocorrerá uma das duas coisas:  
  
-   Se a configuração de `FILEGROWTH` estiver habilitada para o log e houver espaço disponível no disco, o arquivo será estendido na quantidade especificada no parâmetro *growth_increment* e os novos registros de log serão adicionados à extensão. Para obter mais informações sobre a configuração de `FILEGROWTH`, consulte [Opções de arquivo e grupo de arquivos de ALTER DATABASE &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md).  
  
-   Se a configuração de `FILEGROWTH` não estiver habilitada ou se o disco que estiver mantendo o arquivo de log tiver menos espaço livre do que a quantidade especificada em *growth_increment*, será gerado um erro 9002. Consulte [Solução de problemas em um log de transações completo](../relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md) para obter mais informações.  
  
 Se o log contiver diversos arquivos de log físico, o log lógico percorrerá todos os arquivos de log físico antes de voltar ao início do primeiro arquivo de log físico. 
 
> [!IMPORTANT]
> Para obter mais informações sobre o gerenciamento do tamanho do log de transações, consulte [Gerenciar o tamanho do arquivo de log de transações](../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md).
  
### <a name="log-truncation"></a>Truncamento do log  
 O truncamento de log é essencial para impedir o preenchimento do log. O truncamento de log exclui arquivos de log virtuais inativos do log de transações lógicas de um banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , liberando espaço no log lógico para reutilização pelo log de transações físicas. Se um log de transações nunca foi truncado, eventualmente, ele preencherá todo o espaço em disco alocado para seus arquivos de log físicos. No entanto, para que o log possa ser truncado, deve ocorrer uma operação ponto de verificação. Um ponto de verificação grava as páginas modificadas na memória atualmente (conhecidas como páginas sujas) e as informações do log de transações de memória em disco. Quando o ponto de verificação é executado, a porção inativa do log de transações é marcada como reutilizável. Depois disso, a porção inativa pode ser liberada por meio do truncamento de log. Para obter mais informações sobre pontos de verificação, consulte [Pontos de verificação de bancos de dados &#40;SQL Server&#41;](../relational-databases/logs/database-checkpoints-sql-server.md).  
  
 As ilustrações seguintes mostram um log de transações antes e depois do truncamento. A primeira ilustração mostra um log de transações que nunca foi truncado. Atualmente, quatro arquivos de log virtuais estão em uso pelo log lógico. O log virtual inicia à frente do primeiro arquivo de log virtual e termina em log 4 virtual. O registro de MinLSN está em log 3 virtual. O log 1 virtual e o log 2 virtual contêm apenas registros de log inativos. Estes registros podem ser truncados. O log 5 virtual ainda está sem-uso e não é parte do log lógico atual.  
  
![tranlog2](../relational-databases/media/tranlog2.gif)  
  
 A segunda ilustração mostra como o log aparece depois de ser truncado. Log 1 virtual e log 2 virtual foram liberados para reutilização. O log lógico agora inicia no começo do log 3 virtual. O log 5 virtual ainda está sem-uso e não é parte do log lógico atual.  
  
![tranlog3](../relational-databases/media/tranlog3.gif)  
  
 O truncamento de log ocorre automaticamente após os seguintes eventos, exceto quando atrasado por alguma razão:  
  
-   No modelo de recuperação simples, depois de um ponto de verificação.  
-   No modelo de recuperação completa ou bulk-logged, depois de um backup de log, se um ponto de verificação tiver acontecido desde o backup prévio.  
  
 O truncamento de log pode ser atrasado por uma variedade de fatores. No caso de uma demora longa em truncamento de log, o log de transações pode ficar cheio. Para obter informações, consulte [Fatores que podem atrasar o truncamento de log](../relational-databases/logs/the-transaction-log-sql-server.md#FactorsThatDelayTruncation) e [Solução de problemas de um log de transações cheio &#40;Erro 9002 do SQL Server&#41;](../relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md).  
  
##  <a name="WAL"></a> Log de transações write-ahead  
 Esta seção descreve a função do log de transações write-ahead no registro de modificações de dados no disco. O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usa um algoritmo WAL (log write-ahead), que garante que nenhuma modificação de dados seja gravada no disco antes de o registro de log associado ser gravado no disco. Isso mantém as propriedades ACID de uma transação.  
  
 Para entender como o log write-ahead funciona, é importante saber como os dados modificados são gravados em disco. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mantém um cache de buffer em que ele lê páginas de dados quando dados precisam ser recuperados. Quando uma página é modificada no cache do buffer, não é gravada imediatamente de volta no disco. Em vez disso, a página é marcada como *suja*. Uma página de dados pode ter mais de uma gravação lógica feita antes de ser gravada fisicamente no disco. Para cada gravação lógica, um registro de log de transações é inserido no cache de log que registra a modificação. Os registros de log devem ser gravados no disco antes de a página suja associada ser removida do cache do buffer e gravada no disco. O processo de ponto de verificação examina o cache do buffer periodicamente para buffers com páginas de um banco de dados especificado e grava todas as páginas sujas no disco. Os pontos de verificação economizam tempo durante uma recuperação posterior, pois criam um ponto em que todas as páginas sujas são gravadas no disco.  
  
 A gravação de uma página de dados modificada do cache do buffer no disco é chamada de liberação de página. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tem uma lógica que impede que uma página suja seja removida antes do registro de log associado ser gravado. Os registros de log são gravados no disco quando as transações são confirmadas.  
  
##  <a name="Backups"></a> Backups de log de transações  
 Esta seção apresenta conceitos sobre como fazer backup e restaurar (aplicar) logs de transações. Nos modelos de recuperação completa e de recuperação com log de operações em massa é necessário fazer backups de rotina de logs de transações (*backups de log*) para recuperar dados. É possível fazer backup do log enquanto qualquer backup completo está em execução. Para obter mais informações sobre os modelos de recuperação, consulte [Fazer backup e restaurar bancos de dados do SQL Server](../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md).  
  
 Para poder criar o primeiro backup de log, você deve criar um backup completo, como um backup de banco de dados ou o primeiro de um conjunto de backups de arquivo. A restauração de um banco de dados usando apenas backups de arquivo pode tornar-se complexa. Portanto, recomendamos que, assim que possível, você inicie com um backup de banco de dados. Assim, é necessário fazer backup de log de transações regularmente. Isto não só minimiza a exposição à perda de trabalho, como também habilita o truncamento do log de transações. Normalmente, o log de transações é truncado após todos os backups de log convencionais.  
  
> [!IMPORTANT]
> Recomendamos fazer backups de log com frequência suficiente para dar suporte a seus requisitos empresariais, especificamente, a tolerância à perda de trabalho que pode ser causada por um armazenamento de log danificado. A frequência apropriada para fazer backups de log depende de tolerância à exposição à perda de trabalho, equilibrada por quantos backups de log é possível armazenar, administrar e, potencialmente, restaurar. Pense no [RTO](http://wikipedia.org/wiki/Recovery_time_objective) e [RPO](http://wikipedia.org/wiki/Recovery_point_objective) necessários ao implementar sua estratégia de recuperação e, especificamente, na cadência de backup de log.
> Fazer um backup de log a cada 15 a 30 minutos deve ser o bastante. Se o seu negócio requer que você reduza ao mínimo a exposição à perda de trabalho, considere fazer backups de log com mais frequência. Backups de log mais frequentes têm a vantagem adicional de aumentar a frequência de truncamentos de log, resultando em arquivos de log menores.  
  
> [!IMPORTANT]
> Para limitar o número de backups de log que você precisa restaurar, é essencial fazer backup dos dados com frequência. Por exemplo, convém programar um backup de banco de dados completo por semana e backups de diferenciais de banco de dados diariamente.  
> Mais uma vez, pense no [RTO](http://wikipedia.org/wiki/Recovery_time_objective) e [RPO](http://wikipedia.org/wiki/Recovery_point_objective) necessários ao implementar sua estratégia de recuperação e, especificamente, na cadência de backup completo e diferencial de banco de dados.

Para obter mais informações sobre backups de log de transações, consulte [Backups de log de transações &#40;SQL Server&#41;](../relational-databases/backup-restore/transaction-log-backups-sql-server.md).
  
### <a name="the-log-chain"></a>A cadeia de logs  
 Uma sequência contínua de backups de log é denominada *cadeia de logs*. Uma cadeia de logs começa com um backup completo do banco de dados. Normalmente, uma cadeia de logs nova será iniciada apenas quando for feito backup do banco de dados pela primeira vez ou, depois que o modelo de recuperação for trocado de recuperação simples para recuperação completa ou recuperação com log de operações bulk-logged. A menos que você decida substituir os conjuntos de backup existentes quando criar um backup de banco de dados completo, a cadeia de logs existente permanecerá intacta. Com a cadeia de logs intacta, é possível restaurar o banco de dados a partir de qualquer backup de banco de dados completo do conjunto de mídias, seguido por todos os backups de logs subsequentes até o ponto de recuperação. O ponto de recuperação pode estar no fim do último backup de log ou em um ponto de recuperação específico em qualquer dos backups de log. Para obter mais informações, consulte [Backups de log de transações &#40;SQL Server&#41;](../relational-databases/backup-restore/transaction-log-backups-sql-server.md).  
  
 Para restaurar um banco de dados até o ponto de falha, a cadeia de logs deve estar intacta. Isto é, uma sequência ininterrupta de backups de log de transações deve se estender até o ponto de falha. Onde essa sequência de log deve começar depende do tipo de backup de dados que você está restaurando: banco de dados, parcial ou de arquivo. Para um backup de banco de dados ou backup parcial, a sequência de backups de log deve se estender do final de um banco de dados ou backup parcial. Para um conjunto de backups de arquivos, a sequência de backups de log deve se estender desde o início de um conjunto completo de backups de arquivos. Para obter mais informações, veja [Aplicar backups de log de transações &#40;SQL Server&#41;](../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md).  
  
### <a name="restore-log-backups"></a>Restaurar backups de log  
 A restauração de um backup de log rola para frente as alterações que foram registradas no log de transações para recriar o estado exato do banco de dados no momento em que a operação do backup de log começou. Ao restaurar um banco de dados, é necessário, também, restaurar os backups de log que foram criados após o backup completo do banco de dados restaurado ou, desde o início do primeiro backup de arquivos que você restaura. Normalmente, depois de restaurar o backup de dados ou diferencial mais recente, será necessário restaurar uma série de backups de log até alcançar o seu ponto de recuperação. Em seguida, o banco de dados é recuperado. Isso rola para trás todas as transações que estavam incompletas quando a recuperação começou e coloca o banco de dados online. Depois que o banco de dados for recuperado, não será possível restaurar mais nenhum backup. Para obter mais informações, consulte [Aplicar backups de log de transações &#40;SQL Server&#41;](../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md).  

## <a name="checkpoints-and-the-active-portion-of-the-log"></a>Pontos de verificação e a parte ativa do log  

Os pontos de verificação liberam para o disco páginas de dados sujas do cache do buffer do banco de dados atual. Isso minimiza a parte ativa do log que deve ser processada durante a recuperação completa de um banco de dados. Durante uma recuperação completa, são executados os seguintes tipos de ações:

* Os registros de log de modificações não liberados para disco antes de o sistema parar são rolados para frente.
* Todas as modificações associadas a transações incompletas, tais como transações para as quais não há registro de log COMMIT ou ROLLBACK, são revertidas.

### <a name="checkpoint-operation"></a>Operação de ponto de verificação

Um ponto de verificação executa os seguintes processos no banco de dados:

* Escreve um registro no arquivo de log, marcando o início do ponto de verificação.
* Armazena informações registradas para o ponto de verificação em uma cadeia de registros de log de ponto de verificação.  
 
    Uma informação registrada no ponto de verificação é o número de sequência de log (LSN) do primeiro registro de log que deve estar presente para o êxito de uma reversão de todo o banco de dados. Esse LSN é chamado de LSN de recuperação mínima (MinLSN). O MinLSN é o mínimo do: 

    * LSN do início do ponto de verificação.
    * LSN do início da transação ativa mais antiga.
    * LSN do início da transação de replicação mais antiga que ainda não foi entregue ao banco de dados de distribuição. 

    Os registros de ponto de verificação também contêm uma lista de todas as transações ativas que modificaram o banco de dados.

* Se o banco de dados usar o modelo de recuperação simples, ele marca para reutilização o espaço que precede o MinLSN. 
* Grava todo o log sujo e páginas de dados no disco.
* Grava um registro marcando o final do ponto de verificação no arquivo de log.
* Grava o LSN do início dessa cadeia na página de inicialização de banco de dados.

#### <a name="activities-that-cause-a-checkpoint"></a>Atividades que causam um ponto de verificação

Os pontos de verificação ocorrem nas seguintes situações:

* Uma instrução CHECKPOINT é executada explicitamente. Um ponto de verificação ocorre no banco de dados atual para a conexão.
* Uma operação de log mínimo é executada no banco de dados; por exemplo, uma operação de cópia em massa é executada em um banco de dados que está usando o modelo de recuperação bulk-logged. 
* Os arquivos de banco de dados foram adicionados ou removidos usando ALTER DATABASE.
* Uma instância do SQL Server é interrompida por uma instrução SHUTDOWN ou pela interrupção do serviço do SQL Server (MSSQLSERVER). Qualquer ação causa um ponto de verificação em cada banco de dados na instância do SQL Server.
* Uma instância do SQL Server gera periodicamente pontos de verificação automáticos em cada banco de dados para reduzir o tempo que a instância levaria para recuperar o banco de dados.
* É realizado um backup de banco de dados.
* É executada uma atividade que requer um desligamento de banco de dados. Por exemplo, AUTO_CLOSE está ON e a última conexão de usuário com o banco de dados está fechada ou é feita uma modificação de opção de banco de dados que requer o reinício do banco de dados.

### <a name="automatic-checkpoints"></a>Pontos de verificação automáticos

O mecanismo de banco de dados do SQL Server gera pontos de verificação automáticos. O intervalo entre pontos de verificação automáticos baseia-se na quantidade de espaço do log usado e o tempo decorrido desde o último ponto de verificação. O intervalo de tempo entre pontos de verificação automáticos pode ser muito variável e longo se forem feitas algumas modificações no banco de dados. Pontos de verificação automáticos também podem ocorrer com frequência se forem modificados muitos dados.

Use a opção de configuração de servidor **intervalo de recuperação** para calcular o intervalo entre pontos de verificação automáticos para todos os bancos de dados em uma instância do servidor. Essa opção especifica o tempo máximo que o Mecanismo do Banco de Dados deve usar para recuperar um banco de dados durante um reinício do sistema. O Mecanismo do Banco de Dados calcula quantos registros de log podem ser processados no **intervalo de recuperação** durante uma operação de recuperação. 

O intervalo entre pontos de verificação automáticos também depende do modelo de recuperação:

* Se o banco de dados estiver usando o modelo de recuperação em partes ou completa, será gerado um ponto de verificação automático sempre que o número de registros de log atingir o número de estimativas do Mecanismo do Banco de Dados que ele pode processar durante o tempo especificado na opção de intervalo de recuperação.
* Se o banco de dados estiver usando o modelo de recuperação simples, é gerado um ponto de verificação automático sempre que o número de registros de log atingir o menor destes dois valores: 

    * O log se torna 70% completo.
    * O número de registros de log atinge o número de estimativas do Mecanismo do Banco de Dados que ele pode processar durante o tempo especificado na opção de intervalo de recuperação.

Para obter informações sobre como definir o intervalo de recuperação, consulte [Configure the recovery interval Server Configuration Option](../database-engine/configure-windows/configure-the-recovery-interval-server-configuration-option.md).

> [!TIP]  
> A opção de configuração avançada -k do SQL Server permite que um administrador de banco de dados acelere o comportamento de E/S do ponto de verificação com base na taxa de transferência do subsistema de E/S de alguns tipos de pontos de verificação. A opção de configuração -k se aplica a pontos de verificação automáticos e a qualquer outro ponto de verificação sem limitação. 
 
Pontos de verificação automáticos truncarão a seção não utilizada do log de transações se o banco de dados estiver usando o modelo de recuperação simples. Contudo, se o banco de dados estiver usando os modelos de recuperação bulk-logged ou completa, o log não será truncado pelos pontos de verificação automáticos. Para obter mais informações, consulte [O log de transações](../relational-databases/logs/the-transaction-log-sql-server.md). 

A instrução CHECKPOINT agora fornece um argumento checkpoint_duration opcional que especifica o intervalo de tempo necessário, em segundos, para a conclusão dos pontos de verificação. Para obter mais informações, consulte [CHECKPOINT](../t-sql/language-elements/checkpoint-transact-sql.md).

### <a name="active-log"></a>log ativo

A seção do arquivo de log desde o MinLSN até o último registro de log gravado é chamada de parte ativa do log ou log ativo. Essa é a seção do log necessária para fazer uma recuperação completa do banco de dados. Nenhuma parte do log ativo pode ter sido truncada. Todos os registros de log devem ser truncados das partes do log antes do MinLSN.

A ilustração seguinte mostra uma versão simplificada de um log de término de uma transação com duas transações ativas. Os registros de ponto de verificação foram compactados em um único registro.

![active_log](../relational-databases/media/active-log.gif) 

LSN 148 é o último registro no log de transação. No momento em que o ponto de verificação gravado em LSN 147 foi processado, Tran 1 havia sido confirmada e Tran 2 era a única transação ativa. Isso torna o primeiro registro de log para Tran 2 o registro de log mais antigo para uma transação ativa no momento do último ponto de verificação. Isso torna LSN 142 o registro Iniciar transação para Tran 2, o MinLSN.

### <a name="long-running-transactions"></a>Transações de longa execução

O log ativo deve incluir todas as partes de todas as transações não confirmadas. Um aplicativo que inicia uma transação e não a confirma ou reverte-a impede que o Mecanismo de Banco de Dados avance o MinLSN. Isso pode causar dois tipos de problemas:

* Se o sistema for desligado após a transação realizar muitas modificações não confirmadas, a fase de recuperação do reinício subsequente poderá demorar muito mais do que o tempo especificado na opção **intervalo de recuperação** .
* O log pode ficar muito grande, pois não pode ser truncado além do MinLSN. Isso ocorre mesmo se o banco de dados estiver usando o modelo de recuperação simples, no qual o log de transações é geralmente truncado em cada ponto de verificação automático.

### <a name="replication-transactions"></a>Transações de replicação

O Log Reader Agent monitora o log de transações de cada banco de dados configurado para replicação transacional e copia as transações marcadas para replicação do log de transações no banco de dados de distribuição. O log ativo deve conter todas as transações marcadas para replicação, mas que ainda não foram enviadas ao banco de dados de distribuição. Se essas transações não forem replicadas de maneira oportuna, elas poderão impedir o truncamento do log. Para obter mais informações, consulte [Replicação transacional](../relational-databases/replication/transactional/transactional-replication.md).

## <a name="see-also"></a>Consulte também 
Recomendamos a leitura dos artigos e manuais a seguir para obter mais informações sobre o log de transações e as melhores práticas de gerenciamento do log de transações.  
  
[O log de transações &#40;SQL Server&#41;](../relational-databases/logs/the-transaction-log-sql-server.md)    
[Gerenciar o tamanho do arquivo de log de transações](../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md)   
[Backups de log de transações &#40;SQL Server&#41;](../relational-databases/backup-restore/transaction-log-backups-sql-server.md)   
[sys.dm_db_log_info &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md)  
[sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)    
[Noções básicas sobre registro em log e recuperação no SQL Server, por Paul Randal](http://technet.microsoft.com/magazine/2009.02.logging.aspx)    
[Gerenciamento de log de transações do SQL Server, por Tony Davis e Gail Shaw](http://www.simple-talk.com/books/sql-books/sql-server-transaction-log-management-by-tony-davis-and-gail-shaw/)  
  
  
