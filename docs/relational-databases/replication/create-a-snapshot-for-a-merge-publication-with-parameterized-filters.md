---
title: "Criar um instant&#226;neo para uma publica&#231;&#227;o de mesclagem com filtros com par&#226;metros | Microsoft Docs"
ms.custom: ""
ms.date: "05/03/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "filtros parametrizados [replicação do SQL Server], instantâneos"
  - "instantâneos [replicação do SQL Server], filtros parametrizados"
  - "filtros [replicação do SQL Server], parametrizados"
ms.assetid: 00dfb229-f1de-4d33-90b0-d7c99ab52dcb
caps.latest.revision: 45
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 45
---
# Criar um instant&#226;neo para uma publica&#231;&#227;o de mesclagem com filtros com par&#226;metros
  Este tópico descreve como criar um instantâneo para uma publicação de mesclagem com filtros parametrizados no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] ou RMO (Replication Management Objects).  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Recomendações](#Recommendations)  
  
-   **Para criar um instantâneo para uma publicação de mesclagem com filtros com parâmetros, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO (Replication Management Objects)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Ao gerar um instantâneo para uma publicação de mesclagem usando filtros com parâmetros, você deve, primeiro, gerar um instantâneo padrão (esquema), que contenha todos os dados publicados e os metadados do Assinante para a assinatura. Para obter mais informações, consulte [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md). Após ter criado um instantâneo de esquema, você poderá gerar o instantâneo que contém a partição Assinante específica dos dados publicados.  
  
-   Se a filtragem para um ou mais artigos da publicação gerar partições não sobrepostas, exclusivas de cada assinatura, os metadados serão limpos sempre que o Agente de Mesclagem for executado. Isso significa que o instantâneo particionado irá expirar mais rapidamente. Ao usar essa opção, considere permitir que os Assinantes possam iniciar a geração e a entrega do instantâneo. Para obter mais informações sobre opções de filtragem, consulte a seção "Definindo opções de partição" [instantâneos para publicações de mesclagem com filtros parametrizados](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md).  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Gerar instantâneos para partições no **partições de dados** página o **Propriedades de publicação - \< publicação>** caixa de diálogo. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md). É possível permitir que os Assinantes iniciem a geração de instantâneo e entreguem e/ou gerem instantâneos.  
  
 Antes de gerar instantâneos para uma ou mais partições, é preciso:  
  
1.  Criar uma publicação de mesclagem com o Assistente para Nova Publicação, e especificar um ou mais filtros de linha com parâmetros na página **Adicionar Filtro** do assistente. Para obter mais informações, consulte [Define and Modify a Parameterized Row Filter for a Merge Article](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md).  
  
2.  Gerar um instantâneo de esquema para a publicação. Por padrão, o instantâneo de esquema é gerado quando o Assistente para Nova Publicação é encerrado. Nesse momento é igualmente possível gerar um instantâneo de esquema no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
#### Para gerar um instantâneo de esquema  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações** .  
  
3.  Clique com botão direito a publicação para o qual você deseja criar um instantâneo e, em seguida, clique em **Exibir o Status do Snapshot Agent**.  
  
4.  No **Exibir Status do Snapshot Agent - \< publicação>** caixa de diálogo, clique em **Iniciar**.  
  
     Quando Snapshot Agent terminar de gerar o instantâneo, uma mensagem será exibida, tal como "[100%] Um instantâneo de 17 artigo(s) foi gerado."  
  
#### Para permitir que os Assinantes iniciem a geração e entrega de instantâneo  
  
1.  Sobre o **partições de dados** página do **Propriedades de publicação - \< publicação>** caixa de diálogo, selecione **definir uma partição e gerar um instantâneo, se necessário, quando um novo assinante tenta sincronizar automaticamente**.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
#### Para gerar e atualizar instantâneos  
  
1.  No **partições de dados** página o **Propriedades de publicação - \< publicação>** caixa de diálogo, clique em **Adicionar**.  
  
2.  Insira um valor para o **HOST_NAME ()** e/ou **suser_sname ()** valor associado à partição para a qual você deseja criar um instantâneo.  
  
3.  Especifique, opcionalmente, um cronograma para atualizar instantâneos:  
  
    1.  Selecione **agendamento do agente de instantâneo desta partição ser executada às vezes a seguir**  
  
    2.  Aceite o cronograma padrão para atualizar instantâneos ou clique em **Alterar** para especificar um cronograma diferente.  
  
4.  Clique em **OK**, que retorna ao **Propriedades de publicação - \< publicação>** caixa de diálogo.  
  
5.  Selecione a partição na grade de propriedades e, depois, clique em **Gerar os instantâneos selecionados agora**.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 Ao usar os procedimentos armazenados e o Agente de Instantâneo, será possível realizar o seguinte:  
  
-   Permita que os Assinantes solicitem geração e aplicação de instantâneos na primeira vez que eles sincronizarem.  
  
-   Gere previamente instantâneos para cada partição.  
  
-   Gerar manualmente um instantâneo para cada Assinante.  
  
    > [!IMPORTANT]  
    >  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
#### Para criar uma publicação que permita que os Assinantes inicializem geração e entrega de instantâneo  
  
1.  No publicador do banco de dados de publicação, execute [sp_addmergepublication & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). Especifique os seguintes parâmetros:  
  
    -   O nome da publicação para **@publication**.  
  
    -   Um valor de **true** para **@allow_subscriber_initiated_snapshot**, que permite que os assinantes iniciar o processo de instantâneo.  
  
    -   (Opcional) O número de processos de instantâneo dinâmico que podem ser executados simultaneamente para **@max_concurrent_dynamic_snapshots**. Se o número máximo de processos estiver em execução e o Assinante tentar gerar um instantâneo, o processo será colocado em uma fila. Por padrão não há nenhum limite para o número de processos simultâneos.  
  
2.  No publicador, execute [sp_addpublication_snapshot & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md). Especifique o nome da publicação usado na etapa 1 para **@publication** e [!INCLUDE[msCoName](../../includes/msconame-md.md)] as credenciais do Windows sob a qual o [Replication Snapshot Agent](../../relational-databases/replication/agents/replication-snapshot-agent.md) é executado para **@job_login** e **@password**. Se o agente usará [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação ao conectar-se ao publicador, você deve especificar um valor de **0** para **@publisher_security_mode** e [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] informações de logon para **@publisher_login** e **@publisher_password**. Isso cria um trabalho do Agente de Instantâneo para a publicação. Para obter mais informações sobre como gerar um instantâneo inicial e definir uma agenda personalizada para o Snapshot Agent, consulte [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
    > [!IMPORTANT]  
    >  Ao configurar um editor com um distribuidor remoto, os valores fornecidos para todos os parâmetros, incluindo *job_login* e *job_password*, são enviados ao distribuidor como texto sem formatação. Você deve criptografar a conexão entre o Publicador e seu Distribuidor remoto antes de executar esse procedimento armazenado. Para obter mais informações, consulte [Habilitar conexões criptografadas para o mecanismo de banco de dados e 40; SQL Server Configuration Manager & 41;](../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
3.  Executar [sp_addmergearticle & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) Para adicionar artigos à publicação. Esse procedimento armazenado deve ser executado uma vez para cada artigo na publicação. Ao usar filtros com parâmetros, você deve especificar um filtro de linha com parâmetros para um ou mais artigos usando o **@subset_filterclause** parâmetro. Para obter mais informações, consulte [Define and Modify a Parameterized Row Filter for a Merge Article](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md).  
  
4.  Se outros artigos serão filtrados com base no filtro de linha com parâmetros, execute [sp_addmergefilter & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md) Para definir a associação ou relações de registro lógico entre artigos. Esse procedimento armazenado deve ser executado uma vez para cada artigo sendo definido. Para obter mais informações, consulte [Define and Modify a Join Filter Between Merge Articles](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md).  
  
5.  Quando o Merge Agent solicita que o instantâneo inicialize o Assinante, o instantâneo para a solicitação de partição de assinatura é gerado automaticamente.  
  
#### Para criar uma publicação e pré-gerar ou atualizar automaticamente instantâneos  
  
1.  Executar [sp_addmergepublication & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) para criar a publicação. Para obter mais informações, consulte [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md).  
  
2.  No publicador, execute [sp_addpublication_snapshot & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md). Especifique o nome da publicação usado na etapa 1 para **@publication** e as credenciais do Windows na qual o Snapshot Agent é executado para **@job_login** e **@password**. Se o agente usará [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação ao conectar-se ao publicador, você deve especificar um valor de **0** para **@publisher_security_mode** e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] informações de logon para **@publisher_login** e **@publisher_password**. Isso cria um trabalho do Agente de Instantâneo para a publicação. Para obter mais informações sobre como gerar um instantâneo inicial e definir uma agenda personalizada para o Snapshot Agent, consulte [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
    > [!IMPORTANT]  
    >  Ao configurar um editor com um distribuidor remoto, os valores fornecidos para todos os parâmetros, incluindo *job_login* e *job_password*, são enviados ao distribuidor como texto sem formatação. Você deve criptografar a conexão entre o Publicador e seu Distribuidor remoto antes de executar esse procedimento armazenado. Para obter mais informações, consulte [Habilitar conexões criptografadas para o mecanismo de banco de dados e 40; SQL Server Configuration Manager & 41;](../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
3.  Executar [sp_addmergearticle & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) Para adicionar artigos à publicação. Esse procedimento armazenado deve ser executado uma vez para cada artigo na publicação. Ao usar filtros com parâmetros, você deve especificar um filtro de linha com parâmetros para um artigo usando o **@subset_filterclause** parâmetro. Para obter mais informações, consulte [Define and Modify a Parameterized Row Filter for a Merge Article](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md).  
  
4.  Se outros artigos serão filtrados com base no filtro de linha com parâmetros, execute [sp_addmergefilter & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md) Para definir a associação ou relações de registro lógico entre artigos. Esse procedimento armazenado deve ser executado uma vez para cada artigo sendo definido. Para obter mais informações, consulte [Define and Modify a Join Filter Between Merge Articles](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md).  
  
5.  No publicador do banco de dados de publicação, execute [sp_helpmergepublication & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md), especificando o valor de **@publication** da etapa 1. Observe o valor da **snapshot_jobid** no conjunto de resultados.  
  
6.  Converter o valor da **snapshot_jobid** obtido na etapa 5 para **uniqueidentifier**.  
  
7.  No publicador do **msdb** de banco de dados, execute [sp_start_job & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md), especificando o valor convertido obtido na etapa 6 para **@job_id**.  
  
8.  No publicador do banco de dados de publicação, execute [sp_addmergepartition & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql.md). Especifique o nome da publicação da etapa 1 para **@publication** e o valor usado para definir a partição de **@suser_sname** se [SUSER_SNAME & #40. O Transact-SQL e 41;](../../t-sql/functions/suser-sname-transact-sql.md) é usada na cláusula de filtro ou de **@host_name** se [HOST_NAME & #40. O Transact-SQL e 41;](../../t-sql/functions/host-name-transact-sql.md) é usada na cláusula de filtro.  
  
9. No publicador do banco de dados de publicação, execute [sp_adddynamicsnapshot_job & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-adddynamicsnapshot-job-transact-sql.md). Especifique o nome da publicação da etapa 1 para **@publication**, o valor de **@suser_sname** ou **@host_name** na etapa 8 e uma agenda para o trabalho. Isso irá criar o trabalho que gera o instantâneo com parâmetros para a partição especificada. Para obter mais informações, consulte [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md).  
  
    > [!NOTE]  
    >  Esse trabalho executa, usando a mesma conta Windows do trabalho de instantâneo inicial definido na etapa 2. Para remover o trabalho de instantâneo com parâmetros e sua partição de dados relacionados, execute [sp_dropdynamicsnapshot_job & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-dropdynamicsnapshot-job-transact-sql.md).  
  
10. No publicador do banco de dados de publicação, execute [sp_helpmergepartition & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-helpmergepartition-transact-sql.md), especificando o valor de **@publication** da etapa 1 e o valor de **@suser_sname** ou **@host_name** da etapa 8. Observe o valor da **dynamic_snapshot_jobid** no conjunto de resultados.  
  
11. No distribuidor a **msdb** de banco de dados, execute [sp_start_job & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md), especificando o valor obtido na etapa 9 para **@job_id**. Isso inicia o trabalho de instantâneo com parâmetros para a partição.  
  
12. Repita as etapas de 8 a11 para gerar um instantâneo particionado para cada assinatura.  
  
#### Para criar uma publicação e criar manualmente instantâneos para cada partição  
  
1.  Executar [sp_addmergepublication & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) para criar a publicação. Para obter mais informações, consulte [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md).  
  
2.  No publicador, execute [sp_addpublication_snapshot & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md). Especifique o nome da publicação usado na etapa 1 para **@publication** e as credenciais do Windows na qual o Snapshot Agent é executado para **@job_login** e **@password**. Se o agente usará [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação ao conectar-se ao publicador, você deve especificar um valor de **0** para **@publisher_security_mode** e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] informações de logon para **@publisher_login** e **@publisher_password**. Isso cria um trabalho do Agente de Instantâneo para a publicação. Para obter mais informações sobre como gerar um instantâneo inicial e definir uma agenda personalizada para o Snapshot Agent, consulte [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
    > [!IMPORTANT]  
    >  Ao configurar um editor com um distribuidor remoto, os valores fornecidos para todos os parâmetros, incluindo *job_login* e *job_password*, são enviados ao distribuidor como texto sem formatação. Você deve criptografar a conexão entre o Publicador e seu Distribuidor remoto antes de executar esse procedimento armazenado. Para obter mais informações, consulte [Habilitar conexões criptografadas para o mecanismo de banco de dados e 40; SQL Server Configuration Manager & 41;](../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
3.  Executar [sp_addmergearticle & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) Para adicionar artigos à publicação. Esse procedimento armazenado deve ser executado uma vez para cada artigo na publicação. Ao usar filtros com parâmetros, você deve especificar um filtro de linha com parâmetros para pelo menos um artigo usando o **@subset_filterclause** parâmetro. Para obter mais informações, consulte [Define and Modify a Parameterized Row Filter for a Merge Article](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md).  
  
4.  Se outros artigos serão filtrados com base no filtro de linha com parâmetros, execute [sp_addmergefilter & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md) Para definir a associação ou relações de registro lógico entre artigos. Esse procedimento armazenado deve ser executado uma vez para cada artigo sendo definido. Para obter mais informações, consulte [Define and Modify a Join Filter Between Merge Articles](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md).  
  
5.  Inicie o trabalho de instantâneo ou execute o Replication Snapshot Agent no prompt de comando para gerar o esquema de instantâneo padrão e outros arquivos. Para obter mais informações, consulte [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
6.  Execute o Replication Snapshot Agent novamente no prompt de comando para gerar arquivos de cópia (. BCP) em massa, especificando o local do instantâneo particionado para **- DynamicSnapshotLocation** e uma ou ambas as propriedades a seguir que define a partição:  
  
    -   **-DynamicFilterHostName** -o valor se [HOST_NAME & #40. O Transact-SQL e 41;](../../t-sql/functions/host-name-transact-sql.md) é usado.  
  
    -   **-DynamicFilterLogin** -o valor se [SUSER_SNAME & #40. O Transact-SQL e 41;](../../t-sql/functions/suser-sname-transact-sql.md) é usado.  
  
7.  Repita a etapa 6 para gerar um instantâneo particionado para cada assinatura.  
  
8.  Execute o Merge Agent para cada assinatura para aplicar o instantâneo inicial particionado nos Assinantes, especificando as propriedades a seguir:  
  
    -   **-Hostname** -o valor usado para definir a partição se o valor real do HOST_NAME está sendo substituído.  
  
    -   **-DynamicSnapshotLocation** -o local do instantâneo dinâmico para essa partição.  
  
> [!NOTE]  
>  Para obter mais informações sobre como programar agentes de replicação, consulte [conceitos dos executáveis do agente de replicação](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
###  <a name="TsqlExample"></a> Exemplos (Transact-SQL)  
 Esse exemplo cria uma publicação de mesclagem com filtros com parâmetros onde Assinantes inicia o processo de geração de instantâneo. Valores de **@job_login** e **@job_password** são passados usando variáveis de script.  
  
 [!code-sql[HowTo#sp_MergeDynamicPub1](../../relational-databases/replication/codesnippet/tsql/create-a-snapshot-for-a-_1.sql)]  
  
 Este exemplo cria uma publicação usando um filtro parametrizado onde cada assinante tem sua partição definida pela execução [sp_addmergepartition](../../relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql.md) e o trabalho de instantâneo filtrado criado executando [sp_adddynamicsnapshot_job](../../relational-databases/system-stored-procedures/sp-adddynamicsnapshot-job-transact-sql.md) passando as informações de particionamento. Valores de **@job_login** e **@job_password** são passados usando variáveis de script.  
  
 [!code-sql[HowTo#sp_MergeDynamicPubPlusPartition](../../relational-databases/replication/codesnippet/tsql/create-a-snapshot-for-a-_2.sql)]  
  
 Esse exemplo cria uma publicação usando um filtro com parâmetros, onde cada Assinante deve ter sua própria partição de dados e trabalho de instantâneo criado pelo fornecimento das informações de particionamento. Um Assinante fornece informações de particionamento, usando parâmetros de linha de comando ao executar, manualmente, os agentes de replicação. Esse exemplo assume que também foi criada uma assinatura para a publicação.  
  
 [!code-sql[HowTo#sp_MergeDynamicPubPartitionManual](../../relational-databases/replication/codesnippet/tsql/create-a-snapshot-for-a-_3.sql)]  
  
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
>  Quando a filtragem para um artigo gera partições não sobrepostas que são exclusivas para cada assinatura (especificando um valor de F:Microsoft.SqlServer.Replication.PartitionOptions.NonOverlappingSingleSubscription para P:Microsoft.SqlServer.Replication.MergeArticle.PartitionOption durante a criação de um artigo de mesclagem), os metadados são limpos sempre que o agente de mesclagem é executado. Isso significa que o instantâneo particionado irá expirar mais rapidamente. Ao usar essa opção, considere permitir que os Assinantes solicitem geração do instantâneo. Para obter mais informações, consulte a seção "Usando as opções de filtragem” apropriadas no tópico [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
> [!IMPORTANT]  
>  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for preciso armazenar credenciais, use os serviços [criptográficos](http://go.microsoft.com/fwlink/?LinkId=34733) fornecidos pelo [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework do Windows.  
  
#### Para criar uma publicação que permita que os Assinantes inicializem geração e entrega de instantâneo  
  
1.  Criar uma conexão com o publicador usando o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> de classe para o banco de dados de publicação, defina o <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propriedade para a instância do <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da etapa 1 e chame o <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método. Se <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> retorna **false**, confirme se o banco de dados existe.  
  
3.  Se <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledMergePublishing%2A> é de propriedade **false**, defina-o como **true** e chamar <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A>.  
  
4.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.MergePublication> de classe e defina as seguintes propriedades para esse objeto:  
  
    -   O <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da etapa 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
    -   O nome do banco de dados publicado <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>.  
  
    -   Um nome para a publicação de <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>.  
  
    -   O número máximo de trabalhos de instantâneo dinâmico para executar para <xref:Microsoft.SqlServer.Replication.MergePublication.MaxConcurrentDynamicSnapshots%2A>. Uma vez que solicitações de instantâneo iniciado pelo Assinante podem ocorrer a qualquer momento, essa propriedade limita o número de trabalhos do Snapshot Agent que podem ser executados simultaneamente quando vários Assinantes solicitam seu instantâneo particionado ao mesmo tempo. Quando o número máximo de trabalhos estiver sendo executado, solicitações de instantâneos particionados adicionais são enfileiradas até que um dos trabalhos que está sendo executado seja concluído.  
  
    -   Usar a lógica OR bit a bit (**|** no Visual c# e **ou** no Visual Basic) para adicionar o valor <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowSubscriberInitiatedSnapshot> para <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A>.  
  
    -   O <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> e <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> campos de <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> para fornecer as credenciais para o [!INCLUDE[msCoName](../../includes/msconame-md.md)] da conta do Windows na qual o trabalho do Snapshot Agent é executado.  
  
        > [!NOTE]  
        >  Definindo <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> é recomendada quando a publicação é criada por um membro do **sysadmin** função de servidor fixa. Para obter mais informações, consulte [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
5.  Chamar o <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> método para criar a publicação.  
  
    > [!IMPORTANT]  
    >  Ao configurar um editor com um distribuidor remoto, os valores fornecidos para todas as propriedades, incluindo <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A>, são enviados ao distribuidor como texto sem formatação. Você deve criptografar a conexão entre o publicador e seu distribuidor remoto antes de chamar o <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> método. Para obter mais informações, consulte [Habilitar conexões criptografadas para o mecanismo de banco de dados e 40; SQL Server Configuration Manager & 41;](../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
6.  Use o <xref:Microsoft.SqlServer.Replication.MergeArticle> propriedade para adicionar artigos à publicação. Especifique o <xref:Microsoft.SqlServer.Replication.MergeArticle.FilterClause%2A> propriedade para pelo menos um artigo que define o filtro parametrizado. (Opcional) Criar <xref:Microsoft.SqlServer.Replication.MergeJoinFilter> objetos definirem filtros de junção entre artigos. Para obter mais informações, consulte [Define an Article](../../relational-databases/replication/publish/define-an-article.md).  
  
7.  Se o valor de <xref:Microsoft.SqlServer.Replication.Publication.SnapshotAgentExists%2A> é **false**, chame <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> para criar o trabalho do agente de instantâneo inicial para esta publicação.  
  
8.  Chamar o <xref:Microsoft.SqlServer.Replication.Publication.StartSnapshotGenerationAgentJob%2A> método o <xref:Microsoft.SqlServer.Replication.MergePublication> objeto criado na etapa 4. Isso inicia o trabalho do agente que gera o instantâneo inicial. Para obter mais informações sobre como gerar um instantâneo inicial e definir uma agenda personalizada para o Snapshot Agent, consulte [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
9. (Opcional) Verificar se há um valor de **true** para o <xref:Microsoft.SqlServer.Replication.MergePublication.SnapshotAvailable%2A> propriedade para determinar quando o instantâneo inicial está pronto para uso.  
  
10. Quando o Merge Agent para um Assinante for conectado pela primeira vez, um instantâneo particionado é gerado automaticamente.  
  
#### Para criar uma publicação e gerar previamente ou atualizar automaticamente instantâneos  
  
1.  Usar uma instância de <xref:Microsoft.SqlServer.Replication.MergePublication> classe para definir uma publicação de mesclagem. Para obter mais informações, consulte [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md).  
  
2.  Use o <xref:Microsoft.SqlServer.Replication.MergeArticle> propriedade para adicionar artigos à publicação. Especifique o <xref:Microsoft.SqlServer.Replication.MergeArticle.FilterClause%2A> propriedade para pelo menos um artigo que define o filtro com parâmetros e crie quaisquer <xref:Microsoft.SqlServer.Replication.MergeJoinFilter> objetos definirem filtros de junção entre artigos. Para obter mais informações, consulte [Define an Article](../../relational-databases/replication/publish/define-an-article.md).  
  
3.  Se o valor de <xref:Microsoft.SqlServer.Replication.Publication.SnapshotAgentExists%2A> é **false**, chame <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> para criar o trabalho do agente de instantâneo desta publicação.  
  
4.  Chamar o <xref:Microsoft.SqlServer.Replication.Publication.StartSnapshotGenerationAgentJob%2A> método o <xref:Microsoft.SqlServer.Replication.MergePublication> objeto criado na etapa 1. Esse método inicia o trabalho do agente que gera o instantâneo inicial. Para obter mais informações sobre como gerar um instantâneo inicial e definir uma agenda personalizada para o Snapshot Agent, consulte [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
5.  Verificar se há um valor de **true** para o <xref:Microsoft.SqlServer.Replication.MergePublication.SnapshotAvailable%2A> propriedade para determinar quando o instantâneo inicial está pronto para uso.  
  
6.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.MergePartition> classe e definir os critérios de filtragem com parâmetros para o assinante usando uma ou ambas as seguintes propriedades:  
  
    -   Se a partição do assinante é definida pelo resultado de [SUSER_SNAME & #40. O Transact-SQL e 41;](../../t-sql/functions/suser-sname-transact-sql.md), use <xref:Microsoft.SqlServer.Replication.MergePartition.DynamicFilterLogin%2A>.  
  
    -   Se a partição do assinante é definida pelo resultado de [HOST_NAME & #40. O Transact-SQL e 41;](../../t-sql/functions/host-name-transact-sql.md) ou uma sobrecarga dessa função, use <xref:Microsoft.SqlServer.Replication.MergePartition.DynamicFilterHostName%2A>.  
  
7.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.MergeDynamicSnapshotJob> classe e definir a mesma propriedade da etapa 6.  
  
8.  Use o <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule> classe para definir uma agenda para gerar o instantâneo filtrado para a partição do assinante.  
  
9. Usando a instância do <xref:Microsoft.SqlServer.Replication.MergePublication> da etapa 1, chame <xref:Microsoft.SqlServer.Replication.MergePublication.AddMergePartition%2A>. Passar o <xref:Microsoft.SqlServer.Replication.MergePartition> objeto da etapa 6.  
  
10. Usando a instância do <xref:Microsoft.SqlServer.Replication.MergePublication> da etapa 1, chame o <xref:Microsoft.SqlServer.Replication.MergePublication.AddMergeDynamicSnapshotJob%2A> método. Passar o <xref:Microsoft.SqlServer.Replication.MergeDynamicSnapshotJob> objeto obtido na etapa 7 e o <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule> objeto da etapa 8.  
  
11. Chamar <xref:Microsoft.SqlServer.Replication.MergePublication.EnumMergeDynamicSnapshotJobs%2A>, e localize o <xref:Microsoft.SqlServer.Replication.MergeDynamicSnapshotJob> objeto para o trabalho de instantâneo particionado recém-adicionado na matriz retornada.  
  
12. Obter o <xref:Microsoft.SqlServer.Replication.MergeDynamicSnapshotJob.Name%2A> propriedade para o trabalho.  
  
13. Criar uma conexão com o distribuidor usando a <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
14. Criar uma instância do SQL Server Management Objects (SMO) <xref:Microsoft.SqlServer.Management.Smo.Server> classe, passando o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> objeto da etapa 13.  
  
15. Criar uma instância do <xref:Microsoft.SqlServer.Management.Smo.Agent.Job> classe, passando o <xref:Microsoft.SqlServer.Management.Smo.Server.JobServer%2A> propriedade o <xref:Microsoft.SqlServer.Management.Smo.Server> objeto da etapa 14 e o nome do trabalho na etapa 12.  
  
16. Chamar o <xref:Microsoft.SqlServer.Management.Smo.Agent.Job.Start%2A> método para iniciar o trabalho de instantâneo particionado.  
  
17. Repita as etapas 6-16 para cada Assinante.  
  
#### Para criar uma publicação e criar manualmente instantâneos para cada partição  
  
1.  Usar uma instância de <xref:Microsoft.SqlServer.Replication.MergePublication> classe para definir uma publicação de mesclagem. Para obter mais informações, consulte [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md).  
  
2.  Use o <xref:Microsoft.SqlServer.Replication.MergeArticle> propriedade para adicionar artigos na publicação, especifique o <xref:Microsoft.SqlServer.Replication.MergeArticle.FilterClause%2A> propriedade para pelo menos um artigo que define o filtro com parâmetros e crie quaisquer <xref:Microsoft.SqlServer.Replication.MergeJoinFilter> objetos definirem filtros de junção entre artigos. Para obter mais informações, consulte [Define an Article](../../relational-databases/replication/publish/define-an-article.md).  
  
3.  Gere o instantâneo inicial. Para obter mais informações, consulte [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
4.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent> e defina as seguintes propriedades necessárias:  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publisher%2A> - nome do publicador  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherDatabase%2A> - nome do banco de dados de publicação  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publication%2A> - nome da publicação  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Distributor%2A> - nome do distribuidor  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherSecurityMode%2A> -um valor de <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> usado autenticação integrada do Windows ou um valor de <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> para usar a autenticação do SQL Server.  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorSecurityMode%2A> -um valor de <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> usado autenticação integrada do Windows ou um valor de <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> para usar a autenticação do SQL Server.  
  
5.  Definir um valor de <xref:Microsoft.SqlServer.Replication.ReplicationType.Merge> para <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.ReplicationType%2A>.  
  
6.  Defina uma ou mais das seguintes propriedades a fim de definir os parâmetros de particionamento:  
  
    -   Se a partição do assinante é definida pelo resultado de [SUSER_SNAME & #40. O Transact-SQL e 41;](../../t-sql/functions/suser-sname-transact-sql.md), use <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DynamicFilterLogin%2A>.  
  
    -   Se a partição do assinante é definida pelo resultado de [HOST_NAME & #40. O Transact-SQL e 41;](../../t-sql/functions/host-name-transact-sql.md) ou uma sobrecarga dessa função, use <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DynamicFilterHostName%2A>.  
  
7.  Chame o método <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.GenerateSnapshot%2A> .  
  
8.  Repita as etapas 4-7 para cada Assinante.  
  
###  <a name="PShellExample"></a> Exemplos (RMO)  
 Esse exemplo cria uma publicação de mesclagem que permite aos Assinantes solicitar geração de instantâneo.  
  
 [!code-csharp[HowTo#rmo_CreateMergePub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergepub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergepub)]  
  
 Esse exemplo cria a partição de Assinante e o instantâneo filtrado manualmente para uma publicação de mesclagem com filtros de linha com parâmetros.  
  
 [!code-csharp[HowTo#rmo_CreateMergePartition](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergepartition)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePartition](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergepartition)]  
  
 Esse exemplo inicia manualmente o Agente de Instantâneo para gerar o instantâneo de dados filtrado para um Assinante para uma publicação de mesclagem com filtros de linha com parâmetros.  
  
 [!code-csharp[HowTo#rmo_GenerateFilteredSnapshot](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_generatefilteredsnapshot)]  
  
 [!code-vb[HowTo#rmo_vb_GenerateFilteredSnapshot](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_generatefilteredsnapshot)]  
  
## Consulte também  
 [Filtros de linha com parâmetros](../../relational-databases/replication/merge/parameterized-row-filters.md)   
 [Conceitos dos procedimentos armazenados do sistema de replicação](../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Instantâneos para publicações de mesclagem com filtros com parâmetros](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)   
 [Práticas recomendadas em relação à segurança de replicação](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  