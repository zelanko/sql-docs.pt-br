---
title: Criar um instantâneo para uma publicação de mesclagem com filtros parametrizados | Microsoft Docs
ms.custom: ''
ms.date: 06/30/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- parameterized filters [SQL Server replication], snapshots
- snapshots [SQL Server replication], parameterized filters and
- filters [SQL Server replication], parameterized
ms.assetid: 00dfb229-f1de-4d33-90b0-d7c99ab52dcb
caps.latest.revision: 43
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5de6e6d274ccaf030e900ce9448b2713091d9a79
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37179853"
---
# <a name="create-a-snapshot-for-a-merge-publication-with-parameterized-filters"></a>Criar um instantâneo para uma publicação de mesclagem com filtros com parâmetros
  Este tópico descreve como criar um instantâneo para uma publicação de mesclagem com filtros parametrizados no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]ou RMO (Replication Management Objects).  
  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Ao gerar um instantâneo para uma publicação de mesclagem usando filtros com parâmetros, você deve, primeiro, gerar um instantâneo padrão (esquema), que contenha todos os dados publicados e os metadados do Assinante para a assinatura. Para obter mais informações, consulte [Criar e aplicar o instantâneo inicial](create-and-apply-the-initial-snapshot.md). Após ter criado um instantâneo de esquema, você poderá gerar o instantâneo que contém a partição Assinante específica dos dados publicados.  
  
-   Se a filtragem para um ou mais artigos da publicação gerar partições não sobrepostas, exclusivas de cada assinatura, os metadados serão limpos sempre que o Agente de Mesclagem for executado. Isso significa que o instantâneo particionado irá expirar mais rapidamente. Ao usar essa opção, considere permitir que os Assinantes possam iniciar a geração e a entrega do instantâneo. Para obter mais informações sobre opções de filtragem, consulte a seção Setting "Setting 'partition options'" (Definindo opções de partição) de [Snapshots for Merge Publications with Parameterized Filters](snapshots-for-merge-publications-with-parameterized-filters.md) (Instantâneos para publicações de mesclagem com filtros parametrizados).  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Gerar instantâneos para partições na página **Partições de Dados** da caixa de diálogo **Propriedades da Publicação – \<Publicação>**. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md). É possível permitir que os Assinantes iniciem a geração de instantâneo e entreguem e/ou gerem instantâneos.  
  
 Antes de gerar instantâneos para uma ou mais partições, é preciso:  
  
1.  Criar uma publicação de mesclagem com o Assistente para Nova Publicação, e especificar um ou mais filtros de linha com parâmetros na página **Adicionar Filtro** do assistente. Para obter mais informações, consulte [Definir e modificar um filtro de linha com parâmetros para um artigo de mesclagem](publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md).  
  
2.  Gerar um instantâneo de esquema para a publicação. Por padrão, o instantâneo de esquema é gerado quando o Assistente para Nova Publicação é encerrado. Nesse momento é igualmente possível gerar um instantâneo de esquema no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
#### <a name="to-generate-a-schema-snapshot"></a>Para gerar um instantâneo de esquema  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações** .  
  
3.  Clique com o botão direito do mouse na publicação para a qual você quer criar um instantâneo e, então, clique em **Exibir Status do Snapshot Agent**.  
  
4.  Na caixa de diálogo **Exibir Status do Snapshot Agent – \<Publicação>**, clique em **Iniciar**.  
  
     Quando Snapshot Agent terminar de gerar o instantâneo, uma mensagem será exibida, tal como "[100%] Um instantâneo de 17 artigo(s) foi gerado."  
  
#### <a name="to-allow-subscribers-to-initiate-snapshot-generation-and-delivery"></a>Para permitir que os Assinantes iniciem a geração e entrega de instantâneo  
  
1.  Na página **Partições de Dados** da caixa de diálogo **Propriedades da publicação – \<Publicação>**, selecione **Definir automaticamente uma partição e gerar um instantâneo, se necessário, quando um novo Assinante tentar sincronizar**.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
#### <a name="to-generate-and-refresh-snapshots"></a>Para gerar e atualizar instantâneos  
  
1.  Na página **Partições de Dados** da caixa de diálogo **Propriedades da Publicação – \<Publication>**, clique em **Adicionar**.  
  
2.  Digite um valor para **HOST_NAME()** e/ou um valor para **SUSER_SNAME()** , associado à partição para a qual será criado um instantâneo.  
  
3.  Especifique, opcionalmente, um cronograma para atualizar instantâneos:  
  
    1.  Selecione **Agendar o Snapshot Agent para que esta partição seja executada no(s) seguinte(s) horário(s):**  
  
    2.  Aceite o cronograma padrão para atualizar instantâneos ou clique em **Alterar** para especificar um cronograma diferente.  
  
4.  Clique em **OK**, que retorna à caixa de diálogo **Propriedades da Publicação – \<Publicação>**.  
  
5.  Selecione a partição na grade de propriedades e, depois, clique em **Gerar os instantâneos selecionados agora**.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 Ao usar os procedimentos armazenados e o Agente de Instantâneo, será possível realizar o seguinte:  
  
-   Permita que os Assinantes solicitem geração e aplicação de instantâneos na primeira vez que eles sincronizarem.  
  
-   Gere previamente instantâneos para cada partição.  
  
-   Gerar manualmente um instantâneo para cada Assinante.  
  
    > [!IMPORTANT]  
    >  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
#### <a name="to-create-a-publication-that-allows-subscribers-to-initiate-snapshot-generation-and-delivery"></a>Para criar uma publicação que permita que os Assinantes inicializem geração e entrega de instantâneo  
  
1.  No Publicador do banco de dados de publicação, execute [sp_addmergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql). Especifique os seguintes parâmetros:  
  
    -   O nome da publicação para **@publication**.  
  
    -   Um valor de `true` para **@allow_subscriber_initiated_snapshot**, que permite que os assinantes a iniciarem o processo de instantâneo.  
  
    -   (Opcional) O número de processos de instantâneo dinâmico que pode executar simultaneamente para **@max_concurrent_dynamic_snapshots**. Se o número máximo de processos estiver em execução e o Assinante tentar gerar um instantâneo, o processo será colocado em uma fila. Por padrão não há nenhum limite para o número de processos simultâneos.  
  
2.  No Publicador, execute [sp_addpublication_snapshot &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql). Especifique o nome da publicação usado na etapa 1 para **@publication** e o [!INCLUDE[msCoName](../../includes/msconame-md.md)] credenciais do Windows sob as quais o [Replication Snapshot Agent](agents/replication-snapshot-agent.md) autenticação ao conectar-se para o Publisher, você também deve especificar um valor de **0** para **@publisher_security_mode** e o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] informações de logon para **@publisher_login** e **@publisher_password**. Isso cria um trabalho do Agente de Instantâneo para a publicação. Para obter mais informações sobre como gerar um instantâneo inicial e definir uma agenda personalizada para o Snapshot Agent, consulte [Criar e aplicar o instantâneo inicial](create-and-apply-the-initial-snapshot.md).  
  
    > [!IMPORTANT]  
    >  Quando um Publicador é configurado com um Distribuidor remoto, os valores fornecidos para todos os parâmetros, inclusive *job_login* e *job_password*, são enviados ao Distribuidor como texto sem-formatação. Você deve criptografar a conexão entre o Publicador e seu Distribuidor remoto antes de executar esse procedimento armazenado. Para obter mais informações, veja [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
3.  Execute [sp_addmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) para adicionar artigos à publicação. Esse procedimento armazenado deve ser executado uma vez para cada artigo na publicação. Ao usar filtros com parâmetros, você deve especificar um filtro de linha com parâmetros para um ou mais artigos que usam o parâmetro **@subset_filterclause** . Para obter mais informações, consulte [Define and Modify a Parameterized Row Filter for a Merge Article](publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md).  
  
4.  Se outros artigos serão filtrados com base no filtro de linha parametrizado, execute [sp_addmergefilter &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql) para definir as relações de junção ou de registro lógico entre artigos. Esse procedimento armazenado deve ser executado uma vez para cada artigo sendo definido. Para obter mais informações, consulte [Define and Modify a Join Filter Between Merge Articles](publish/define-and-modify-a-join-filter-between-merge-articles.md).  
  
5.  Quando o Merge Agent solicita que o instantâneo inicialize o Assinante, o instantâneo para a solicitação de partição de assinatura é gerado automaticamente.  
  
#### <a name="to-create-a-publication-and-pre-generate-or-automatically-refresh-snapshots"></a>Para criar uma publicação e pré-gerar ou atualizar automaticamente instantâneos  
  
1.  Execute [sp_addmergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql) para criar a publicação. Para obter mais informações, consulte [Create a Publication](publish/create-a-publication.md).  
  
2.  No Publicador, execute [sp_addpublication_snapshot &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql). Especifique o nome da publicação usado na etapa 1 para **@publication** e as credenciais do Windows no qual o Snapshot Agent executa para **@job_login** e **@password**. Se o agente usar a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando se conectar ao Publicador, você também deverá especificar um valor de **0** para **@publisher_security_mode** e as credenciais do Windows [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para **@publisher_login** e **@publisher_password**. Isso cria um trabalho do Agente de Instantâneo para a publicação. Para obter mais informações sobre como gerar um instantâneo inicial e definir uma agenda personalizada para o Snapshot Agent, consulte [Criar e aplicar o instantâneo inicial](create-and-apply-the-initial-snapshot.md).  
  
    > [!IMPORTANT]  
    >  Quando um Publicador é configurado com um Distribuidor remoto, os valores fornecidos para todos os parâmetros, inclusive *job_login* e *job_password*, são enviados ao Distribuidor como texto sem-formatação. Você deve criptografar a conexão entre o Publicador e seu Distribuidor remoto antes de executar esse procedimento armazenado. Para obter mais informações, veja [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
3.  Execute [sp_addmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) para adicionar artigos à publicação. Esse procedimento armazenado deve ser executado uma vez para cada artigo na publicação. Ao usar filtros com parâmetros, você deve especificar um filtro de linha com parâmetros para um artigo usando o parâmetro **@subset_filterclause** . Para obter mais informações, consulte [Definir e modificar um filtro de linha com parâmetros para um artigo de mesclagem](publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md).  
  
4.  Se outros artigos serão filtrados com base no filtro de linha parametrizado, execute [sp_addmergefilter &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql) para definir as relações de junção ou de registro lógico entre artigos. Esse procedimento armazenado deve ser executado uma vez para cada artigo sendo definido. Para obter mais informações, consulte [Define and Modify a Join Filter Between Merge Articles](publish/define-and-modify-a-join-filter-between-merge-articles.md).  
  
5.  No Publicador do banco de dados de publicação, execute [sp_helpmergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql), especificando o valor de **@publication** da etapa 1. Observe o valor **snapshot_jobid** no conjunto de resultados.  
  
6.  Converta o valor do **snapshot_jobid** obtido na etapa 5 para **uniqueidentifier**.  
  
7.  No publicador do banco de dados **msdb**, execute [sp_start_job &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-start-job-transact-sql), especificando o valor convertido obtido na etapa 6 para **@job_id**.  
  
8.  No Publicador do banco de dados de publicação, execute [sp_addmergepartition &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql). Especifique o nome da publicação da etapa 1 para **@publication** e o valor usado para definir a partição de **@suser_sname** se [SUSER_SNAME &#40;Transact-SQL&#41;](/sql/t-sql/functions/suser-sname-transact-sql) for usada na cláusula de filtro ou de **@host_name** se [HOST_NAME &#40;Transact-SQL&#41;](/sql/t-sql/functions/host-name-transact-sql) for usado na cláusula de filtro.  
  
9. No publicador do banco de dados de publicação, execute [sp_adddynamicsnapshot_job &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-adddynamicsnapshot-job-transact-sql). Especifique o nome da publicação da etapa 1 para **@publication**, o valor **@suser_sname** ou **@host_name** da etapa 8, e uma agenda para o trabalho. Isso irá criar o trabalho que gera o instantâneo com parâmetros para a partição especificada. Para obter mais informações, consulte [Specify Synchronization Schedules](specify-synchronization-schedules.md).  
  
    > [!NOTE]  
    >  Esse trabalho executa, usando a mesma conta Windows do trabalho de instantâneo inicial definido na etapa 2. Para remover o trabalho de instantâneo parametrizado e sua partição de dados relacionada, execute [sp_dropdynamicsnapshot_job &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropdynamicsnapshot-job-transact-sql).  
  
10. No Publicador do banco de dados de publicação, execute [sp_helpmergepartition &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpmergepartition-transact-sql), especificando o valor de **@publication** da etapa 1 e o valor de **@suser_sname** ou **@host_name** da etapa 8. Observe o valor **dynamic_snapshot_jobid** no conjunto de resultados.  
  
11. No Distribuidor no banco de dados **msdb**, execute [sp_start_job &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-start-job-transact-sql), especificando o valor obtido na etapa 9 para **@job_id**. Isso inicia o trabalho de instantâneo com parâmetros para a partição.  
  
12. Repita as etapas de 8 a11 para gerar um instantâneo particionado para cada assinatura.  
  
#### <a name="to-create-a-publication-and-manually-create-snapshots-for-each-partition"></a>Para criar uma publicação e criar manualmente instantâneos para cada partição  
  
1.  Execute [sp_addmergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql) para criar a publicação. Para obter mais informações, consulte [Create a Publication](publish/create-a-publication.md).  
  
2.  No Publicador, execute [sp_addpublication_snapshot &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql). Especifique o nome da publicação usado na etapa 1 para **@publication** e as credenciais do Windows no qual o Snapshot Agent executa para **@job_login** e **@password**. Se o agente usar a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando se conectar ao Publicador, você também deverá especificar um valor de **0** para **@publisher_security_mode** e as credenciais do Windows [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para **@publisher_login** e **@publisher_password**. Isso cria um trabalho do Agente de Instantâneo para a publicação. Para obter mais informações sobre como gerar um instantâneo inicial e definir uma agenda personalizada para o Snapshot Agent, consulte [Criar e aplicar o instantâneo inicial](create-and-apply-the-initial-snapshot.md).  
  
    > [!IMPORTANT]  
    >  Quando um Publicador é configurado com um Distribuidor remoto, os valores fornecidos para todos os parâmetros, inclusive *job_login* e *job_password*, são enviados ao Distribuidor como texto sem-formatação. Você deve criptografar a conexão entre o Publicador e seu Distribuidor remoto antes de executar esse procedimento armazenado. Para obter mais informações, veja [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
3.  Execute [sp_addmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) para adicionar artigos à publicação. Esse procedimento armazenado deve ser executado uma vez para cada artigo na publicação. Ao usar filtros com parâmetros, você deve especificar um filtro de linha com parâmetros para pelo menos um artigo usando o parâmetro **@subset_filterclause** . Para obter mais informações, consulte [Definir e modificar um filtro de linha com parâmetros para um artigo de mesclagem](publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md).  
  
4.  Se outros artigos serão filtrados com base no filtro de linha parametrizado, execute [sp_addmergefilter &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql) para definir as relações de junção ou de registro lógico entre artigos. Esse procedimento armazenado deve ser executado uma vez para cada artigo sendo definido. Para obter mais informações, consulte [Define and Modify a Join Filter Between Merge Articles](publish/define-and-modify-a-join-filter-between-merge-articles.md).  
  
5.  Inicie o trabalho de instantâneo ou execute o Replication Snapshot Agent no prompt de comando para gerar o esquema de instantâneo padrão e outros arquivos. Para obter mais informações, consulte [Create and Apply the Initial Snapshot](create-and-apply-the-initial-snapshot.md).  
  
6.  Execute o Replication Snapshot Agent novamente no prompt de comando para gerar arquivos (.bcp) para cópia em massa, especificando o local do instantâneo particionado para **-DynamicSnapshotLocation** e uma ou ambas as seguintes propriedades que definam a partição:  
  
    -   **-DynamicFilterHostName** – o valor se [HOST_NAME &#40;Transact-SQL&#41;](/sql/t-sql/functions/host-name-transact-sql) for usado.  
  
    -   **-DynamicFilterLogin** – o valor se [SUSER_SNAME &#40;Transact-SQL&#41;](/sql/t-sql/functions/suser-sname-transact-sql) for usado.  
  
7.  Repita a etapa 6 para gerar um instantâneo particionado para cada assinatura.  
  
8.  Execute o Merge Agent para cada assinatura para aplicar o instantâneo inicial particionado nos Assinantes, especificando as propriedades a seguir:  
  
    -   **-Hostname** - o valor usado para definir a partição, se o valor atual de HOST_NAME estiver sendo substituído.  
  
    -   **- DynamicSnapshotLocation** - o local do instantâneo dinâmico para esta partição.  
  
> [!NOTE]  
>  Para obter mais informações sobre como programar agentes de replicação, consulte [Replication Agent Executables Concepts](concepts/replication-agent-executables-concepts.md) (Conceitos dos executáveis do agente de replicação).  
  
###  <a name="TsqlExample"></a> Exemplos (Transact-SQL)  
 Esse exemplo cria uma publicação de mesclagem com filtros com parâmetros onde Assinantes inicia o processo de geração de instantâneo. Os valores para **@job_login** e **@job_password** são passados no uso de valores de script.  
  
 [!code-sql[HowTo#sp_MergeDynamicPub1](../../snippets/tsql/SQL15/replication/howto/tsql/createmergepubdynamic1.sql#sp_mergedynamicpub1)]  
  
 Esse exemplo cria uma publicação usando um filtro com parâmetros, onde cada Assinante tem sua partição definida ao executar [sp_addmergepartition](/sql/relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql) e o trabalho de instantâneo filtrado criado pela execução [sp_adddynamicsnapshot_job](/sql/relational-databases/system-stored-procedures/sp-adddynamicsnapshot-job-transact-sql) passando as informações de particionamento. Os valores para **@job_login** e **@job_password** são passados no uso de valores de script.  
  
 [!code-sql[HowTo#sp_MergeDynamicPubPlusPartition](../../snippets/tsql/SQL15/replication/howto/tsql/createmergepubdynamic2.sql#sp_mergedynamicpubpluspartition)]  
  
 Esse exemplo cria uma publicação usando um filtro com parâmetros, onde cada Assinante deve ter sua própria partição de dados e trabalho de instantâneo criado pelo fornecimento das informações de particionamento. Um Assinante fornece informações de particionamento, usando parâmetros de linha de comando ao executar, manualmente, os agentes de replicação. Esse exemplo assume que também foi criada uma assinatura para a publicação.  
  
 [!code-sql[HowTo#sp_MergeDynamicPubPartitionManual](../../snippets/tsql/SQL15/replication/howto/tsql/createmergepubdynamic3.sql#sp_mergedynamicpubpartitionmanual)]  
  
 
```
REM Line breaks are added to improve readability.   
REM In a batch file, commands must be made in a single line.  
REM Run the Snapshot agent from the command line to generate the standard snapshot   
REM schema and other files.   
SET DistPub=%computername%  
SET PubDB=AdventureWorks2012   
SET PubName=AdvWorksSalesPersonMerge  
  
"C:\Program Files\Microsoft SQL Server\120\COM\SNAPSHOT.EXE" -Publication %PubName%    
-Publisher %DistPub% -Distributor  %DistPub%  -PublisherDB %PubDB%  -ReplicationType 2    
-OutputVerboseLevel 1  -DistributorSecurityMode 1  
  
PAUSE  
```

```
REM Run the Snapshot agent from the command line, this time to generate   
REM the bulk copy (.bcp) data for each Subscriber partition.    
SET DistPub=%computername%  
SET PubDB=AdventureWorks2012   
SET PubName=AdvWorksSalesPersonMerge  
SET SnapshotDir=\\%DistPub%\repldata\unc\fernando  
  
MD %SnapshotDir%  
  
"C:\Program Files\Microsoft SQL Server\120\COM\SNAPSHOT.EXE" -Publication %PubName%    
-Publisher %DistPub%  -Distributor  %DistPub%  -PublisherDB %PubDB%  -ReplicationType 2    
-OutputVerboseLevel 1  -DistributorSecurityMode 1  -DynamicFilterHostName "adventure-works\Fernando"    
-DynamicSnapshotLocation %SnapshotDir%  
  
PAUSE  
```

```
REM Run the Merge Agent for each subscription to apply the partitioned   
REM snapshot for each Subscriber.    
SET Publisher = %computername%  
SET Subscriber = %computername%  
SET PubDB = AdventureWorks2012   
SET SubDB = AdventureWorks2012Replica   
SET PubName = AdvWorksSalesPersonMerge   
SET SnapshotDir=\\%DistPub%\repldata\unc\fernando  
  
"C:\Program Files\Microsoft SQL Server\120\COM\REPLMERG.EXE" -Publisher  %Publisher%    
-Subscriber  %Subscriber%  -Distributor %Publisher%  -PublisherDB %PubDB%    
-SubscriberDB %SubDB% -Publication %PubName%  -PublisherSecurityMode 1  -OutputVerboseLevel 3    
-Output -SubscriberSecurityMode 1  -SubscriptionType 3 -DistributorSecurityMode 1    
-Hostname "adventure-works\Fernando"  -DynamicSnapshotLocation %SnapshotDir%  
  
PAUSE
```
  
  
##  <a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
 Você pode usar RMO (Replication Management Objects) para gerar instantâneos particionados programaticamente dos seguintes modos:  
  
-   Permita que os Assinantes solicitem geração e aplicação de instantâneos na primeira vez que eles sincronizarem.  
  
-   Gere previamente instantâneos para cada partição.  
  
-   Gere manualmente um instantâneo para cada Assinante executando o Snapshot Agent.  
  
> [!NOTE]  
>  Quando a filtragem de um artigo gerar partições não sobrepostas, exclusivas de cada assinatura (especificando um valor de <xref:Microsoft.SqlServer.Replication.PartitionOptions.NonOverlappingSingleSubscription> para <xref:Microsoft.SqlServer.Replication.MergeArticle.PartitionOption%2A> ao criar um artigo de mesclagem), metadados são limpos sempre que o Merge Agent for executado. Isso significa que o instantâneo particionado irá expirar mais rapidamente. Ao usar essa opção, considere permitir que os Assinantes solicitem geração do instantâneo. Para obter mais informações, consulte a seção "Usando as opções de filtragem” apropriadas no tópico [Parameterized Row Filters](merge/parameterized-filters-parameterized-row-filters.md).  
  
> [!IMPORTANT]  
>  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for preciso armazenar credenciais, use os serviços [criptográficos](http://go.microsoft.com/fwlink/?LinkId=34733) fornecidos pelo [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework do Windows.  
  
#### <a name="to-create-a-publication-that-allows-subscribers-to-initiate-snapshot-generation-and-delivery"></a>Para criar uma publicação que permita que os Assinantes inicializem geração e entrega de instantâneo  
  
1.  Crie uma conexão com o Publicador usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> para o banco de dados de publicação; defina a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> para a instância de <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da etapa 1 e chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> . Se <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> retornar `false`, confirme a existência do banco de dados.  
  
3.  Se <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledMergePublishing%2A> é de propriedade `false`, defina-o como `true` e chame <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A>.  
  
4.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.MergePublication> e defina as propriedades a seguir para esse objeto:  
  
    -   O <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da Etapa 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
    -   Nome do banco de dados publicado para <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>.  
  
    -   Um nome para a publicação para <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>.  
  
    -   O número máximo de trabalhos de instantâneo dinâmicos a serem executados para <xref:Microsoft.SqlServer.Replication.MergePublication.MaxConcurrentDynamicSnapshots%2A>. Uma vez que solicitações de instantâneo iniciado pelo Assinante podem ocorrer a qualquer momento, essa propriedade limita o número de trabalhos do Snapshot Agent que podem ser executados simultaneamente quando vários Assinantes solicitam seu instantâneo particionado ao mesmo tempo. Quando o número máximo de trabalhos estiver sendo executado, solicitações de instantâneos particionados adicionais são enfileiradas até que um dos trabalhos que está sendo executado seja concluído.  
  
    -   Use o OR lógico bit a bit (`|` no Visual c# e `Or` no Visual Basic) para adicionar o valor <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowSubscriberInitiatedSnapshot> para <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A>.  
  
    -   Os campos <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> e <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> de <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> para fornecer as credenciais para a conta do Windows [!INCLUDE[msCoName](../../includes/msconame-md.md)] em que o Snapshot Agent é executado.  
  
        > [!NOTE]  
        >  Recomenda-se definir <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> quando a publicação é criada por um membro da função de servidor fixa `sysadmin`. Para obter mais informações, consulte [Replication Agent Security Model](security/replication-agent-security-model.md).  
  
5.  Chame o método <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> para criar a publicação.  
  
    > [!IMPORTANT]  
    >  Quando um Publicador é configurado com um Distribuidor remoto, os valores fornecidos para todas as propriedades, inclusive <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A>, são enviados ao Distribuidor como texto sem-formatação. É necessário criptografar a conexão entre o Publicador e o respectivo Distribuidor remoto antes de chamar o método <xref:Microsoft.SqlServer.Replication.Publication.Create%2A>. Para obter mais informações, veja [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
6.  Use a propriedade <xref:Microsoft.SqlServer.Replication.MergeArticle> para adicionar artigos à publicação. Especifique a propriedade <xref:Microsoft.SqlServer.Replication.MergeArticle.FilterClause%2A> para pelo menos um artigo que defina o filtro com parâmetros. (Opcional) Crie objetos <xref:Microsoft.SqlServer.Replication.MergeJoinFilter> que definam filtros de junção entre artigos. Para obter mais informações, consulte [Define an Article](publish/define-an-article.md).  
  
7.  Se o valor de <xref:Microsoft.SqlServer.Replication.Publication.SnapshotAgentExists%2A> está `false`, chame <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> para criar o trabalho inicial do Snapshot Agent para essa publicação.  
  
8.  Chame o método <xref:Microsoft.SqlServer.Replication.Publication.StartSnapshotGenerationAgentJob%2A> do objeto <xref:Microsoft.SqlServer.Replication.MergePublication> criado na etapa 4. Isso inicia o trabalho do agente que gera o instantâneo inicial. Para obter mais informações sobre como gerar um instantâneo inicial e definir uma agenda personalizada para o Snapshot Agent, consulte [Criar e aplicar o instantâneo inicial](create-and-apply-the-initial-snapshot.md).  
  
9. (Opcional) Procure um valor de `true` para a propriedade <xref:Microsoft.SqlServer.Replication.MergePublication.SnapshotAvailable%2A> a fim de determinar quando o instantâneo inicial está pronto para ser usado.  
  
10. Quando o Merge Agent para um Assinante for conectado pela primeira vez, um instantâneo particionado é gerado automaticamente.  
  
#### <a name="to-create-a-publication-and-pregenerate-or-automatically-refresh-snapshots"></a>Para criar uma publicação e gerar previamente ou atualizar automaticamente instantâneos  
  
1.  Use uma instância da classe <xref:Microsoft.SqlServer.Replication.MergePublication> para definir uma publicação de mesclagem. Para obter mais informações, consulte [Create a Publication](publish/create-a-publication.md).  
  
2.  Use a propriedade <xref:Microsoft.SqlServer.Replication.MergeArticle> para adicionar artigos à publicação. Especifique a propriedade <xref:Microsoft.SqlServer.Replication.MergeArticle.FilterClause%2A> para pelo menos um artigo que defina o filtro com parâmetros e crie quaisquer objetos <xref:Microsoft.SqlServer.Replication.MergeJoinFilter> que definam filtros de junção entre artigos. Para obter mais informações, consulte [Define an Article](publish/define-an-article.md).  
  
3.  Se o valor de <xref:Microsoft.SqlServer.Replication.Publication.SnapshotAgentExists%2A> está `false`, chame <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> para criar o trabalho do snapshot agent para essa publicação.  
  
4.  Chame o método <xref:Microsoft.SqlServer.Replication.Publication.StartSnapshotGenerationAgentJob%2A> do objeto <xref:Microsoft.SqlServer.Replication.MergePublication> criado na etapa 1. Esse método inicia o trabalho do agente que gera o instantâneo inicial. Para obter mais informações sobre como gerar um instantâneo inicial e definir uma agenda personalizada para o Snapshot Agent, consulte [Criar e aplicar o instantâneo inicial](create-and-apply-the-initial-snapshot.md).  
  
5.  Procure um valor de `true` para o <xref:Microsoft.SqlServer.Replication.MergePublication.SnapshotAvailable%2A> propriedade para determinar quando o instantâneo inicial está pronto para uso.  
  
6.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.MergePartition> e defina os critérios de filtragem com parâmetros para o Assinante, usando uma ou mais das seguintes propriedades:  
  
    -   Se a partição do Assinante for definida pelo resultado de [SUSER_SNAME &#40;Transact-SQL&#41;](/sql/t-sql/functions/suser-sname-transact-sql), use <xref:Microsoft.SqlServer.Replication.MergePartition.DynamicFilterLogin%2A>.  
  
    -   Se a partição do Assinante for definida pelo resultado de [HOST_NAME &#40;Transact-SQL&#41;](/sql/t-sql/functions/host-name-transact-sql) ou uma sobrecarga dessa função, use <xref:Microsoft.SqlServer.Replication.MergePartition.DynamicFilterHostName%2A>.  
  
7.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.MergeDynamicSnapshotJob> e defina a mesma propriedade que a da etapa 6.  
  
8.  Use a classe <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule> para definir uma agenda para gerar o instantâneo filtrado para a partição de Assinante.  
  
9. Usando a instância de <xref:Microsoft.SqlServer.Replication.MergePublication> da etapa 1, chame <xref:Microsoft.SqlServer.Replication.MergePublication.AddMergePartition%2A>. Passe o objeto <xref:Microsoft.SqlServer.Replication.MergePartition> da etapa 6.  
  
10. Usando a instância de <xref:Microsoft.SqlServer.Replication.MergePublication> da etapa 1, chame o método <xref:Microsoft.SqlServer.Replication.MergePublication.AddMergeDynamicSnapshotJob%2A> . Passe o objeto <xref:Microsoft.SqlServer.Replication.MergeDynamicSnapshotJob> da etapa 7 e o objeto <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule> da etapa 8.  
  
11. Chame <xref:Microsoft.SqlServer.Replication.MergePublication.EnumMergeDynamicSnapshotJobs%2A>e localize o objeto <xref:Microsoft.SqlServer.Replication.MergeDynamicSnapshotJob> para o trabalho de instantâneo particionado recém-adicionado à matriz retornada.  
  
12. Adquira a propriedade <xref:Microsoft.SqlServer.Replication.MergeDynamicSnapshotJob.Name%2A> para o trabalho.  
  
13. Crie uma conexão com o Distribuidor usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
14. Crie uma instância da classe <xref:Microsoft.SqlServer.Management.Smo.Server> do SQL Server Management Objetcs (SMO), passando o objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da etapa 13.  
  
15. Crie uma instância da classe <xref:Microsoft.SqlServer.Management.Smo.Agent.Job> passando a propriedade <xref:Microsoft.SqlServer.Management.Smo.Server.JobServer%2A> do objeto <xref:Microsoft.SqlServer.Management.Smo.Server> da etapa 14 e o nome do trabalho da etapa 12.  
  
16. Chame o método <xref:Microsoft.SqlServer.Management.Smo.Agent.Job.Start%2A> para iniciar o trabalho de instantâneo particionado.  
  
17. Repita as etapas 6-16 para cada Assinante.  
  
#### <a name="to-create-a-publication-and-manually-create-snapshots-for-each-partition"></a>Para criar uma publicação e criar manualmente instantâneos para cada partição  
  
1.  Use uma instância da classe <xref:Microsoft.SqlServer.Replication.MergePublication> para definir uma publicação de mesclagem. Para obter mais informações, consulte [Create a Publication](publish/create-a-publication.md).  
  
2.  Use a propriedade <xref:Microsoft.SqlServer.Replication.MergeArticle> para adicionar artigos para a publicação. Especifique a propriedade <xref:Microsoft.SqlServer.Replication.MergeArticle.FilterClause%2A> para pelo menos um artigo que defina o filtro com parâmetros e crie quaisquer objetos <xref:Microsoft.SqlServer.Replication.MergeJoinFilter> que definam filtros de junção entre artigos. Para obter mais informações, consulte [Define an Article](publish/define-an-article.md).  
  
3.  Gere o instantâneo inicial. Para obter mais informações, consulte [Create and Apply the Initial Snapshot](create-and-apply-the-initial-snapshot.md).  
  
4.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent> e defina as seguintes propriedades necessárias:  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publisher%2A> - nome do Publicador  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherDatabase%2A> - nome do banco de dados de publicação  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publication%2A> - nome da publicação  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Distributor%2A> - nome do Distribuidor  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherSecurityMode%2A> - um valor de <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> para Autenticação integrada do Windows usada ou um valor de <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> para usar o Autenticação do SQL Server.  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorSecurityMode%2A> - um valor de <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> para Autenticação integrada do Windows usada ou um valor de <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> para usar o Autenticação do SQL Server.  
  
5.  Defina um valor de <xref:Microsoft.SqlServer.Replication.ReplicationType.Merge> para <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.ReplicationType%2A>.  
  
6.  Defina uma ou mais das seguintes propriedades a fim de definir os parâmetros de particionamento:  
  
    -   Se a partição do Assinante for definida pelo resultado de [SUSER_SNAME &#40;Transact-SQL&#41;](/sql/t-sql/functions/suser-sname-transact-sql), use <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DynamicFilterLogin%2A>.  
  
    -   Se a partição do Assinante for definida pelo resultado de [HOST_NAME &#40;Transact-SQL&#41;](/sql/t-sql/functions/host-name-transact-sql) ou uma sobrecarga dessa função, use <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DynamicFilterHostName%2A>.  
  
7.  Chame o método <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.GenerateSnapshot%2A> .  
  
8.  Repita as etapas 4-7 para cada Assinante.  
  
###  <a name="PShellExample"></a> Exemplos (RMO)  
 Esse exemplo cria uma publicação de mesclagem que permite aos Assinantes solicitar geração de instantâneo.  
  
 [!code-csharp[HowTo#rmo_CreateMergePub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createmergepub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createmergepub)]  
  
 Esse exemplo cria a partição de Assinante e o instantâneo filtrado manualmente para uma publicação de mesclagem com filtros de linha com parâmetros.  
  
 [!code-csharp[HowTo#rmo_CreateMergePartition](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createmergepartition)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePartition](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createmergepartition)]  
  
 Esse exemplo inicia manualmente o Agente de Instantâneo para gerar o instantâneo de dados filtrado para um Assinante para uma publicação de mesclagem com filtros de linha com parâmetros.  
  
 [!code-csharp[HowTo#rmo_GenerateFilteredSnapshot](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_generatefilteredsnapshot)]  
  
 [!code-vb[HowTo#rmo_vb_GenerateFilteredSnapshot](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_generatefilteredsnapshot)]  
  
## <a name="see-also"></a>Consulte também  
 [Parameterized Row Filters](merge/parameterized-filters-parameterized-row-filters.md)   
 [Replication System Stored Procedures Concepts](concepts/replication-system-stored-procedures-concepts.md)   
 [Instantâneos para publicações de mesclagem com filtros parametrizados](snapshots-for-merge-publications-with-parameterized-filters.md)   
 [Replication Security Best Practices](security/replication-security-best-practices.md)  
  
  
