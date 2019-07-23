---
title: Opção SORT_IN_TEMPDB para índices | Microsoft Docs
ms.custom: ''
ms.date: 04/24/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- SORT_IN_TEMPDB option
- disk space [SQL Server], indexes
- space [SQL Server], indexes
- tempdb database [SQL Server], indexes
- indexes [SQL Server], tempdb database
- index creation [SQL Server], tempdb database
ms.assetid: 754a003f-fe51-4d10-975a-f6b8c04ebd35
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 03dbb54a41ef319b7a44185cee00d5de7d46b126
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67909539"
---
# <a name="sortintempdb-option-for-indexes"></a>Opção SORT_IN_TEMPDB para índices
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Quando você cria ou recria um índice, definindo a opção SORT_IN_TEMPDB como ON, você pode direcionar [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] para usar **tempdb** para armazenar os resultados intermediários de classificação utilizados para criar o índice. Embora essa opção aumente a quantidade de espaço temporário em disco usada para criar um índice, a opção pode reduzir o tempo necessário à criação ou recriação de um índice quando **tempdb** estiver em um conjunto de discos diferente do banco de dados do usuário. Para obter mais informações sobre **tempdb**, veja [Configurar a opção index create memory de configuração de servidor](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md).  
  
## <a name="phases-of-index-building"></a>Fases da criação do índice  
 Conforme [!INCLUDE[ssDE](../../includes/ssde-md.md)] constrói um índice, ele passa pelas fases seguintes:  
  
-   O [!INCLUDE[ssDE](../../includes/ssde-md.md)] primeiro verifica as páginas de dados da tabela base para recuperar valores chave e constrói uma linha de folha de índice para cada linha de dados. Quando os buffers internos de classificação estiverem preenchidos com entradas de índice de folha, as entradas serão classificadas e serão gravadas no disco como uma execução de classificação intermediária. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] , em seguida, retoma a verificação da página de dados até que os buffers de classificação sejam preenchidos novamente. Esse padrão de verificação de várias páginas de dados, seguido pela classificação e gravação de uma execução de classificação, continua até a conclusão do processamento de todas as linhas da tabela base.  
  
     Em um índice clusterizado, as linhas de folha do índice são as linhas de dados da tabela; portanto, a execução intermediária de classificação contém todas as linhas de dados. Em um índice não clusterizado, as linhas de folha podem conter colunas não chave, mas são geralmente menores do que um índice clusterizado. Se as chaves do índice forem grandes, ou se houver várias colunas não chave incluídas no índice, uma execução de classificação não clusterizado poderá ser grande. Para obter mais informações sobre como incluir colunas não chave, veja [Criar índices com colunas incluídas](../../relational-databases/indexes/create-indexes-with-included-columns.md).  
  
-   O [!INCLUDE[ssDE](../../includes/ssde-md.md)] mescla as execuções classificadas de linhas de folha de índice em um único fluxo classificado. O componente de mescla de classificação do [!INCLUDE[ssDE](../../includes/ssde-md.md)] inicia com a primeira página de cada execução de classificação, encontra a menor chave em todas as páginas, e transmite aquela linha de folha ao componente de criação do índice. A próxima chave menor é processada, depois a próxima, e assim por diante. Quando a última linha de índice de folha é extraída de uma página de execução de classificação, o processo alterna para próxima página daquela execução de classificação. Quando forem processadas todas as páginas em uma extensão de execução de classificação, a extensão será liberada. Conforme cada linha de índice de folha é transmitida ao componente de criação de índice, é incluída em uma página de índice de folha no buffer. Cada página de folha é gravada conforme é preenchida. Conforme as páginas de folha são gravadas, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] também constrói os níveis superiores do índice. Cada página de índice de nível superior é gravada conforme é preenchida.  
  
## <a name="sortintempdb-option"></a>opção SORT_IN_TEMPDB  
 Quando SORT_IN_TEMPDB é definido como OFF, o padrão, as execuções da classificação são armazenadas no grupo de arquivos de destino. Durante a primeira fase de criação do índice, as leituras alternadas das páginas da tabela base e gravação das execuções de classificação movem os cabeçalhos de leitura/gravação de disco de uma área do disco para outra. Os cabeçalhos estão na área da página de dados conforme as páginas de dados são verificadas. Eles se mudam para uma área de espaço livre quando os buffers de classificação forem preenchidos e a execução atual de classificação estiver gravada no disco e, em seguida, voltam para a área da página de dados conforme retoma a verificação da página da tabela. O movimento do cabeçalho de leitura/gravação é maior na segunda fase. Neste momento, o processo de classificação está normalmente alternando leituras de cada área de execução de classificação. Ambas as execuções de classificação e as novas páginas de índice são criadas no grupo de arquivos de destino. Isto significa que ao mesmo tempo em que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] está propagando leituras entre as execuções de classificação, ele precisa ir periodicamente até as extensões do índice para gravar novas páginas de índice conforme forem preenchidas.  
  
 Se a opção SORT_IN_TEMPDB for definida como ON e **tempdb** estiver em um conjunto separado de discos do grupo de arquivos de destino, durante a primeira fase, as leituras das páginas de dados ocorrerão em um disco diferente da gravação na área de trabalho de classificação em **tempdb**. Isto significa que as leituras de disco das chaves de dados geralmente continuam mais em série pelo disco, e a gravação no disco **tempdb** também é geralmente em série, conforme a gravação faz para criar o índice final. Mesmo se outros usuários estiverem usando o banco de dados e acessando endereços de disco separados, o padrão geral de leituras e gravações é mais eficiente quando SORT_IN_TEMPDB é especificado, do que quando não é.  
  
 A opção SORT_IN_TEMPDB pode melhorar a proximidade de extensões de índice, especialmente se a operação CREATE INDEX não estiver sendo processada em paralelo. As extensões da área de trabalho de classificação são liberadas um tanto aleatoriamente com respeito à localização no banco de dados. Se as áreas de trabalho de classificação estiverem no grupo de arquivos de destino, conforme as extensões de trabalho de classificação são liberadas, elas podem ser adquiridas pelas solicitações de extensões para manterem a estrutura do índice conforme ele for construído. Isto pode distribuir aleatoriamente as localizações das extensões de índice até certo ponto. Se as extensões de classificação forem mantidas separadamente em **tempdb**, a sequência de liberação não afetará a localização das extensões do índice. Além disso, quando as execuções intermediárias de classificação são armazenadas em **tempdb** em vez do grupo de arquivos de destino, existe mais espaço disponível no grupo de arquivos de destino. Isto aumenta as chances de as extensões de índice ser contíguas.  
  
 A opção SORT_IN_TEMPDB afeta somente a instrução atual. Nenhum metadado registra se o índice foi ou não classificado em **tempdb**. Por exemplo, se você criar um índice não clusterizado usando a opção SORT_IN_TEMPDB, e mais tarde criar um índice clusterizado sem especificar a opção, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] não usará a opção quando recriar o índice não clusterizado.  
  
> [!NOTE]  
>  Se a operação de classificação não for necessária, ou se a classificação puder ser executada na memória, a opção SORT_IN_TEMPDB será ignorada.  
  
## <a name="disk-space-requirements"></a>Requisitos de espaço em disco  
 Quando você definir a opção SORT_IN_TEMPDB como ON, você deverá ter espaço livre em disco suficiente disponível em **tempdb** para manter as execuções de classificação intermediárias e espaço livre em disco suficiente no grupo de arquivos de destino para manter o novo índice. A instrução CREATE INDEX falha se houver espaço livre insuficiente e se por alguma razão os bancos de dados não puderem crescer automaticamente para adquirir mais espaço, considerando que nenhum espaço no disco ou se o crescimento automático estiver definido como off.  
  
 Se SORT_IN_TEMPDB for definido como OFF, o espaço livre em disco disponível no grupo de arquivos de destino deve ser praticamente do tamanho do índice final. Durante a primeira fase, as execuções de classificação são criadas e requerem praticamente a mesma quantidade de espaço do índice final. Durante a segunda fase, cada extensão de execução de classificação é liberada depois de ser processada. Isto significa que as extensões de execução de classificação são liberadas aproximadamente a mesma taxa de aquisição das extensões para manter as páginas do índice final; portanto, os requisitos de espaço geral não excedem muito o tamanho do índice final. Um efeito colateral disto é que se a quantidade de espaço livre for muito perto do tamanho do índice final, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] geralmente vai reutilizar as extensões de execução de classificação muito depressa depois que forem liberadas. Como as extensões de execução de classificação são liberadas de forma um pouco aleatória, isto reduz a continuidade das extensões do índice neste cenário. Se SORT_IN_TEMPDB for definido como OFF, a continuidade das extensões do índice é melhorada se houver espaço livre suficiente disponível no grupo de arquivos de destino, que as extensões do índice podem ser alocadas de um pool contíguo, em vez das extensões de corrida de classificação recentemente desalocadas.  
  
Quando você criar um índice não clusterizado, você deve ter disponível, como espaço livre:  
  
-   Se SORT_IN_TEMPDB for definido como ON, deve haver espaço livre suficiente em **tempdb** para armazenar as execuções de classificação, e espaço livre suficiente no grupo de arquivos de destino para armazenar a estrutura final do índice. As execuções de classificação contêm as linhas de folha do índice.  
  
-   Se SORT_IN_TEMPDB for definido como OFF, o espaço livre no grupo de arquivos de destino deve ser grande o suficiente para armazenar a estrutura final do índice. A continuidade da extensão do índice pode ser melhorada se houver mais espaço livre disponível.  
  
Quando você criar um índice clusterizado em uma tabela que não tem índices não clusterizado, você deverá ter disponível como espaço livre:  
  
-   Se SORT_IN_TEMPDB for definido como ON, deverá haver espaço livre suficiente em **tempdb** para armazenar as execuções de classificação. Isso inclui as linhas de dados da tabela. Deve haver espaço livre suficiente no grupo de arquivos de destino para armazenar a estrutura final do índice. Isso inclui as linhas de dados da tabela e o índice árvore B. Você pode precisar ajustar a estimativa de fatores, como ter um tamanho grande de chave ou um fator de preenchimento com um valor baixo.  
  
-   Se SORT_IN_TEMPDB for definido como OFF, o espaço livre no grupo de arquivos de destino deverá ser grande o suficiente para armazenar a tabela final. Isso inclui a estrutura do índice. A continuidade da tabela e da extensão do índice poderá ser melhorada se houver mais espaço livre disponível.  
  
Quando você criar um índice clusterizado em uma tabela que tem índices não clusterizado, você deverá ter disponível como espaço livre:  
  
-   Se SORT_IN_TEMPDB for definido como ON, deve haver espaço livre suficiente em **tempdb** para armazenar a coleção de execuções de classificação para o maior índice, normalmente o índice clusterizado, e espaço livre suficiente no grupo de arquivos de destino para armazenar as estruturas finais de todos os índices. Isso inclui o índice clusterizado que contém as linhas de dados da tabela.  
  
-   Se SORT_IN_TEMPDB for definido como OFF, o espaço livre no grupo de arquivos de destino deverá ser grande o suficiente para armazenar a tabela final. Isso inclui as estruturas de todos os índices. A continuidade da tabela e da extensão do índice poderá ser melhorada se houver mais espaço livre disponível.  
  
## <a name="related-tasks"></a>Related Tasks  
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  
  
 [Reorganizar e recriar índices](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)  
  
 [Configurar a opção index create memory de configuração de servidor](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md)  
  
 [Requisitos de espaço em disco para operações de índice DDL](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md)  
  
  
