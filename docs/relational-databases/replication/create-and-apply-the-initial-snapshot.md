---
title: "Criar e aplicar o instant&#226;neo inicial | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "instantâneos [replicação do SQL Server], criando"
  - "replicação de instantâneo [SQL Server], instantâneos iniciais"
ms.assetid: 742727a1-5189-44ec-b3ae-6fd7aa1f5347
caps.latest.revision: 44
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 44
---
# Criar e aplicar o instant&#226;neo inicial
  Este tópico descreve como criar e aplicar o instantâneo inicial no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../includes/tsql-md.md)] ou o RMO (Replication Management Objects). Publicações de mesclagem que usam filtros com parâmetros exigem um instantâneo de duas partes. Para obter mais informações, consulte [Create a Snapshot for a Merge Publication with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
 **Neste tópico**  
  
-   **Para criar e aplicar o instantâneo inicial, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO (Replication Management Objects)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Por padrão, se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent está sendo executado, um instantâneo é gerado imediatamente pelo Agente de Instantâneo depois que a publicação seja criada com o Assistente para Nova Publicação. Por padrão, isso é então aplicado pelo Distribution Agent (para replicações transacionais e instantâneas) ou o Merge Agent (para assinaturas de mesclagem) para todas as assinaturas. Um instantâneo também pode ser gerado usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e o Replication Monitor. Para obter informações sobre como iniciar o Monitor de replicação, consulte [Iniciar o Replication Monitor](../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
#### Para criar um instantâneo no Management Studio  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações Locais** .  
  
3.  Clique com botão direito a publicação para o qual você deseja criar um instantâneo e, em seguida, clique em **Exibir o Status do Snapshot Agent**.  
  
4.  No **Exibir Status do Snapshot Agent - \< publicação>** caixa de diálogo, clique em **Iniciar**.  
  
 Quando Snapshot Agent terminar de gerar o instantâneo, uma mensagem será exibida, tal como "[100%] Um instantâneo de 17 artigo(s) foi gerado."  
  
#### Para criar um instantâneo no Replication Monitor  
  
1.  No Replication Monitor, expanda um Grupo do publicador no painel esquerdo e, depois, expanda um Publicador.  
  
2.  Clique com botão direito a publicação para o qual você deseja gerar um instantâneo e, em seguida, clique em **Gerar instantâneo**.  
  
3.  Para exibir o status do Snapshot Agent, clique na guia **Agentes** . Para obter mais informações, clique com botão direito na grade, o agente de instantâneo e, em seguida, clique em **Exibir detalhes**.  
  
#### Para aplicar um instantâneo  
  
1.  Depois que um instantâneo for gerado, ele é aplicado pela sincronização da assinatura com o Distribution Agent ou Merge Agent:  
  
    -   Se o agente é definido para ser executado continuamente (o padrão para replicação transacional), o instantâneo é automaticamente aplicado após ser gerado.  
  
    -   Se o agente tiver execução agendada, o instantâneo será aplicado na próxima execução agendada do agente.  
  
    -   Se o agente tiver execução sob demanda, o instantâneo será aplicado na próxima vez que você executar o agente.  
  
     Para obter mais informações sobre assinaturas de sincronização, consulte [sincronizar uma assinatura Push](../../relational-databases/replication/synchronize-a-push-subscription.md) e [sincronizar uma assinatura Pull](../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 Instantâneos iniciais podem ser criados de forma programada criando e executando um trabalho do Agente de Instantâneo ou executando o arquivo executável do Agente de Instantâneo de um arquivo em lote. Depois da geração de um instantâneo inicial, ele é transferido para e aplicado no Assinante quando a assinatura é sincronizada pela primeira vez. Se o Agente de Instantâneo for executado de um prompt de comando ou um arquivo em lote, será preciso executar novamente o agente sempre que o instantâneo existente se tornar inválido.  
  
> [!IMPORTANT]  
>  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
#### Para criar e executar um trabalho do Snapshot Agent a fim de gerar o instantâneo inicial  
  
1.  Crie uma publicação de instantâneo, transacional ou de mesclagem. Para obter mais informações, consulte [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md).  
  
2.  Executar [sp_addpublication_snapshot & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md). Especifique **@publication** e os seguintes parâmetros:  
  
    -   **@Job_login, que especifica** as credenciais de autenticação do Windows na qual o Snapshot Agent é executado no distribuidor.  
  
    -   **O @job_password**, que é a senha para as credenciais fornecidas do Windows.  
  
    -   (Opcional) Um valor de **0** para **@publisher_security_mode** se o agente usar autenticação do SQL Server ao conectar-se ao publicador. Nesse caso, você também deve especificar as informações de logon de autenticação do SQL Server para **@publisher_login** e **@publisher_password**.  
  
    -   (Opcional) Uma agenda de sincronização para o trabalho do Snapshot Agent. Para obter mais informações, consulte [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md).  
  
    > [!IMPORTANT]  
    >  Ao configurar um editor com um distribuidor remoto, os valores fornecidos para todos os parâmetros, incluindo *job_login* e *job_password*, são enviados ao distribuidor como texto sem formatação. Você deve criptografar a conexão entre o Publicador e seu Distribuidor remoto antes de executar esse procedimento armazenado. Para obter mais informações, consulte [Habilitar conexões criptografadas para o mecanismo de banco de dados e 40; SQL Server Configuration Manager & 41;](../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
3.  Adicione artigos à publicação. Para obter mais informações, consulte [Define an Article](../../relational-databases/replication/publish/define-an-article.md).  
  
4.  No publicador do banco de dados de publicação, execute [sp_startpublication_snapshot & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-startpublication-snapshot-transact-sql.md), especificando o valor de **@publication** da etapa 1.  
  
#### Para executar o Snapshot Agent para gerar o instantâneo inicial.  
  
1.  Crie uma publicação de instantâneo, transacional ou de mesclagem. Para obter mais informações, consulte [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md).  
  
2.  Adicione artigos à publicação. Para obter mais informações, consulte [Define an Article](../../relational-databases/replication/publish/define-an-article.md).  
  
3.  No prompt de comando ou em um arquivo em lotes, inicie o [Replication Snapshot Agent](../../relational-databases/replication/agents/replication-snapshot-agent.md) executando **snapshot.exe**, especificando os seguintes argumentos de linha de comando:  
  
    -   **-Publication**  
  
    -   **-Publisher**  
  
    -   **-Distributor**  
  
    -   **-PublisherDB**  
  
    -   **-ReplicationType**  
  
     Se você estiver usando Autenticação do SQL Server, deve-se também especificar os seguintes argumentos:  
  
    -   **-DistributorLogin**  
  
    -   **-DistributorPassword**  
  
    -   **-DistributorSecurityMode** = **0**  
  
    -   **-PublisherLogin**  
  
    -   **-PublisherPassword**  
  
    -   **-PublisherSecurityMode** = **0**  
  
###  <a name="TsqlExample"></a> Exemplos (Transact-SQL)  
 Este exemplo mostra como criar uma publicação transacional e adicionar um trabalho do Snapshot Agent para a nova publicação (usando **sqlcmd** variáveis de script). O exemplo também inicia o trabalho.  
  
 [!code-sql[HowTo#sp_trangenerate_snapshot](../../relational-databases/replication/codesnippet/tsql/create-and-apply-the-ini_1.sql)]  
  
 Este exemplo cria uma publicação de mesclagem e adiciona um trabalho do agente de instantâneo (usando **sqlcmd** variáveis) para a publicação. Esse exemplo também inicia o trabalho.  
  
 [!code-sql[HowTo#sp_mergegenerate_snapshot](../../relational-databases/replication/codesnippet/tsql/create-and-apply-the-ini_2.sql)]  
  
 Os seguintes argumentos de linha de comando iniciam o Snapshot Agent para gerar o instantâneo para uma publicação de mesclagem.  
  
> [!NOTE]  
>  Quebras de linhas foram adicionadas para melhorar a legibilidade. Em um arquivo em lotes, devem ser feitos comandos em uma única linha.  
  
```  
  
REM -- Declare variables  
SET Publisher=%InstanceName%  
SET PublicationDB=AdventureWorks2012   
SET Publication=AdvWorksSalesOrdersMerge   
  
REM --Start the Snapshot Agent to generate the snapshot for AdvWorksSalesOrdersMerge.  
"C:\Program Files\Microsoft SQL Server\120\COM\SNAPSHOT.EXE" -Publication %Publication%   
-Publisher %Publisher% -Distributor %Publisher% -PublisherDB %PublicationDB%   
-ReplicationType 2 -OutputVerboseLevel 1 -DistributorSecurityMode 1  
  
```  
  
##  <a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
 O Agente de Instantâneo gera instantâneos depois da criação da publicação. É possível gerar esses instantâneos de forma programada usando o RMO (Replication Management Objects) e o acesso de código direto para as funcionalidades do agente de replicação. Os objetos usados dependem do tipo de replicação. O Snapshot Agent pode ser iniciado usando o objeto <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent> ou usando de forma assíncrona o trabalho do agente. Depois da geração do instantâneo inicial, ele é transferido para o Assinante, onde é aplicado quando a assinatura é sincronizada pela primeira vez. Será necessário executar novamente o agente sempre que o instantâneo existente não mais contiver dados válidos e atualizados. Para obter mais informações, consulte [Manter publicações](../../relational-databases/replication/publish/maintain-publications.md).  
  
> [!IMPORTANT]  
>  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for preciso armazenar credenciais, use os serviços [criptográficos](http://go.microsoft.com/fwlink/?LinkId=34733) fornecidos pelo [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework do Windows.  
  
#### Para gerar o instantâneo inicial de uma publicação de instantâneo ou transacional por meio da iniciação do trabalho do Snapshot Agent (assíncrono)  
  
1.  Criar uma conexão com o publicador usando o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.TransPublication> classe. Definir o <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> e <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> Propriedades para a publicação e defina o <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propriedade para a conexão criada na etapa 1.  
  
3.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para carregar as propriedades remanescentes do objeto. Se esse método retornar **false**, as propriedades de publicação na etapa 2 foram definidas incorretamente ou a publicação não existe.  
  
4.  Se o valor de <xref:Microsoft.SqlServer.Replication.Publication.SnapshotAgentExists%2A> é **false**, chame <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> para criar o trabalho do agente de instantâneo desta publicação.  
  
5.  Chamar o <xref:Microsoft.SqlServer.Replication.Publication.StartSnapshotGenerationAgentJob%2A> método para iniciar o trabalho de agente que gera o instantâneo desta publicação.  
  
6.  (Opcional) Quando o valor de <xref:Microsoft.SqlServer.Replication.TransPublication.SnapshotAvailable%2A> é **true**, o instantâneo está disponível para assinantes.  
  
#### Para gerar o instantâneo inicial de uma publicação de instantâneo ou transacional por meio da execução do Snapshot Agent (síncrono)  
  
1.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent> e defina as seguintes propriedades necessárias:  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publisher%2A> - nome do publicador  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherDatabase%2A> - nome do banco de dados de publicação  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publication%2A> - nome da publicação  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Distributor%2A> - nome do distribuidor  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherSecurityMode%2A> -um valor de <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> para usar a autenticação do Windows ao se conectar ao publicador ou um valor de <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> e valores para <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherLogin%2A> e <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherPassword%2A> usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação ao conectar-se ao publicador. A Autenticação do Windows é recomendável.  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorSecurityMode%2A> -um valor de <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> para usar a autenticação do Windows ao se conectar ao distribuidor ou um valor de <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> e valores para <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorLogin%2A> e <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorPassword%2A> usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação ao conectar-se ao distribuidor. A Autenticação do Windows é recomendável.  
  
2.  Definir um valor de <xref:Microsoft.SqlServer.Replication.ReplicationType.Transactional> ou <xref:Microsoft.SqlServer.Replication.ReplicationType.Snapshot> para <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.ReplicationType%2A>.  
  
3.  Chame o método <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.GenerateSnapshot%2A> .  
  
#### Para gerar o instantâneo inicial para uma publicação de mesclagem iniciando o trabalho do Snapshot Agent (assíncrono)  
  
1.  Criar uma conexão com o publicador usando o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.MergePublication> classe. Definir o <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> e <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> Propriedades para a publicação e defina o <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propriedade para a conexão criada na etapa 1.  
  
3.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para carregar as propriedades remanescentes do objeto. Se esse método retornar **false**, as propriedades de publicação na etapa 2 foram definidas incorretamente ou a publicação não existe.  
  
4.  Se o valor de <xref:Microsoft.SqlServer.Replication.Publication.SnapshotAgentExists%2A> é **false**, chame <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> para criar o trabalho do agente de instantâneo desta publicação.  
  
5.  Chamar o <xref:Microsoft.SqlServer.Replication.Publication.StartSnapshotGenerationAgentJob%2A> método para iniciar o trabalho de agente que gera o instantâneo desta publicação.  
  
6.  (Opcional) Quando o valor de <xref:Microsoft.SqlServer.Replication.MergePublication.SnapshotAvailable%2A> é **true**, o instantâneo está disponível para assinantes.  
  
#### Para gerar o instantâneo inicial de uma publicação de mesclagem pela execução do Snapshot Agent (síncrono)  
  
1.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent> e defina as seguintes propriedades necessárias:  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publisher%2A> - nome do publicador  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherDatabase%2A> - nome do banco de dados de publicação  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publication%2A> - nome da publicação  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Distributor%2A> - nome do distribuidor  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherSecurityMode%2A> -um valor de <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> para usar a autenticação do Windows ao se conectar ao publicador ou um valor de <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> e valores para <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherLogin%2A> e <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherPassword%2A> usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação ao conectar-se ao publicador. A Autenticação do Windows é recomendável.  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorSecurityMode%2A> -um valor de <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> para usar a autenticação do Windows ao se conectar ao distribuidor ou um valor de <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> e valores para <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorLogin%2A> e <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorPassword%2A> usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação ao conectar-se ao distribuidor. A Autenticação do Windows é recomendável.  
  
2.  Definir um valor de <xref:Microsoft.SqlServer.Replication.ReplicationType.Merge> para <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.ReplicationType%2A>.  
  
3.  Chame o método <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.GenerateSnapshot%2A> .  
  
###  <a name="PShellExample"></a> Exemplos (RMO)  
 Esse exemplo executa o Agente de Instantâneo sincronicamente para gerar o instantâneo inicial para uma publicação transacional.  
  
 [!code-csharp[HowTo#rmo_GenerateSnapshot](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_generatesnapshot)]  
  
 [!code-vb[HowTo#rmo_vb_GenerateSnapshot](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_generatesnapshot)]  
  
 Esse exemplo inicia de forma assíncrona o trabalho do agente sincronicamente para gerar o instantâneo inicial para uma publicação transacional.  
  
 [!code-csharp[HowTo#rmo_GenerateSnapshot_WithJob](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_generatesnapshot_withjob)]  
  
 [!code-vb[HowTo#rmo_vb_GenerateSnapshot_WithJob](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_generatesnapshot_withjob)]  
  
## Consulte também  
 [Crie uma publicação](../../relational-databases/replication/publish/create-a-publication.md)   
 [Criar uma assinatura pull](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md)   
 [Criar e aplicar o instantâneo](../../relational-databases/replication/create-and-apply-the-snapshot.md)   
 [Inicializar uma assinatura com um instantâneo](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Conceitos de Replication Management Objects](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [Práticas recomendadas em relação à segurança de replicação](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Conceitos dos procedimentos armazenados do sistema de replicação](../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Usar sqlcmd com variáveis de script](../../relational-databases/scripting/use-sqlcmd-with-scripting-variables.md)  
  
  