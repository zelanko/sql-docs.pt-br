---
title: "Criar uma assinatura push | Microsoft Docs"
ms.custom: ""
ms.date: "08/25/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "push subscriptions [SQL Server replication], creating"
  - "merge replication subscribing [SQL Server replication], push subscriptions"
  - "subscriptions [SQL Server replication], push"
  - "snapshot replication [SQL Server], subscribing"
  - "replicação transacional, assinatura"
ms.assetid: adfbbc61-58d1-4330-9ad6-b14ab1142e2b
caps.latest.revision: 41
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 41
---
# Criar uma assinatura push
  Este tópico descreve como criar uma inscrição de envio em [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)], ou objetos de gerenciamento de replicação (RMO). Para obter informações sobre como criar uma inscrição de envio para um não[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinante, consulte [criar uma assinatura para um assinante não-SQL Server](../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md).  
  
 
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Crie uma assinatura push no Publicador ou Assinante, usando o Assistente para Novas Assinaturas. Siga as páginas no assistente para:  
  
-   Especificar o Publicador e a publicação.  
  
-   Selecione onde os agentes de replicação executarão. Para uma inscrição de envio, selecione **Executar todos os agentes no distribuidor (assinaturas push)** sobre o **local do Distribution Agent** página ou **local do Merge Agent** página, dependendo do tipo de publicação.  
  
-   Especifique Assinantes e bancos de dados de assinatura.  
  
-   Especifique os logons e senhas usadas para conexões feitas por agentes de replicação:  
  
    -   Para assinaturas para instantâneos e publicações transacionais, especifique as credenciais na página **Segurança do Distribution Agent** .  
  
    -   Para assinaturas para publicações de mesclagem, especifique as credenciais na página **Segurança do Merge Agent** .  
  
     Para obter informações sobre as permissões necessárias para cada agente, consulte [modelo de segurança do agente de replicação](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
-   Especifique uma agenda de sincronização e quando o Assinante deve ser inicializado.  
  
-   Especifique opções adicionais para publicações de mesclagem: tipo de assinatura e valores para filtragem com parâmetros.  
  
-   Especifique opções adicionais para publicações transacionais que permitem assinaturas de atualização: se os Assinantes devem confirmar alterações no Publicador imediatamente ou gravá-las em uma fila; credenciais usadas do Assinante para o Publicador.  
  
-   Opcionalmente, faça o script da assinatura.  
  
#### Para criar uma assinatura push do Publicador  
  
1.  Conecte-se ao Publicador no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e, depois, expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações Locais** .  
  
3.  Clique com botão direito a publicação para o qual você deseja criar uma ou mais assinaturas e, em seguida, clique em **novas assinaturas**.  
  
4.  Complete as páginas no Assistente para Novas Assinaturas.  
  
#### Para criar uma assinatura push do Assinante  
  
1.  Conecte-se ao Assinante no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** .  
  
3.  Clique com botão direito do **assinaturas locais** pasta e clique **novas assinaturas**.  
  
4.  No **publicação** página do Assistente para nova assinatura, selecione **\< encontrar Editor SQL Server>** ou **\< encontrar editor Oracle>** do **Publisher** lista suspensa.  
  
5.  Conecte-se ao Publicador na caixa de diálogo **Conectar ao Servidor** .  
  
6.  Selecione uma publicação na página **Publicação** .  
  
7.  Complete as páginas no Assistente para Novas Assinaturas.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 As assinaturas push podem ser criadas de forma programada, usando procedimentos armazenados de replicação. Os procedimentos armazenados usados dependem do tipo de publicação ao qual a assinatura pertence.  
  
> **IMPORTANTE:** Quando possível, solicite aos usuários que insiram as credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
#### Para criar uma assinatura push em um instantâneo ou publicação transacional  
  
1.  O publicador do banco de dados de publicação, verifique se a publicação oferece suporte a assinaturas push executando [sp_helppublication](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md).  
  
    -   Se o valor de **allow_push** é **1**, há suporte para assinaturas push.  
  
    -   Se o valor de **allow_push** é **0**, execute [sp_changepublication](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md), especificando **allow_push** para **@property** e **true** para **@value**.  
  
2.  No publicador do banco de dados de publicação, execute [sp_addsubscription](https://msdn.microsoft.com/library/ms181702.aspx). Especifique **@publication**, **@subscriber** e **@destination_db**. Especifique um valor de **push** para **@subscription_type**. Para obter informações sobre como atualizar assinaturas, consulte [criar uma assinatura atualizável em uma publicação transacional](https://msdn.microsoft.com/library/ms152769.aspx).  
  
3.  No publicador do banco de dados de publicação, execute [sp_addpushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md). Especifique o seguinte:  
  
    -   O **@subscriber**, **@subscriber_db**, e **@publication** parâmetros.  
  
    -   O [!INCLUDE[msCoName](../../includes/msconame-md.md)] credenciais do Windows sob a qual o agente de distribuição no distribuidor executa **@job_login** e **@job_password**.  
  
        > **Observação:** conexões feitas usando a autenticação integrada do Windows sempre usam as credenciais do Windows especificadas por **@job_login** e **@job_password**. O Distribution Agent sempre faz a conexão local com o Distribuidor usando a Autenticação Integrada do Windows. Por padrão, o agente se conecta ao Assinante usando a Autenticação Integrada do Windows.  
  
    -   (Opcional) Um valor de **0** para **@subscriber_security_mode** e [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] informações de logon para **@subscriber_login** e **@subscriber_password**. Especifique esses parâmetros se for necessário usar a Autenticação do SQL Server para conexão com o Assinante.  
  
    -   Agenda para o trabalho do Distribution Agent para essa assinatura. Para obter mais informações, consulte [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md).  
  
    > **IMPORTANTE:** Ao criar uma inscrição de envio em um publicador com um distribuidor remoto, os valores fornecidos para todos os parâmetros, inclusive *job_login* e *job_password*, são enviados ao distribuidor como texto sem formatação. Você deve criptografar a conexão entre o Publicador e seu Distribuidor remoto antes de executar esse procedimento armazenado. Para obter mais informações, veja [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
#### Para criar uma assinatura push para publicação de mesclagem  
  
1.  O publicador do banco de dados de publicação, verifique se a publicação oferece suporte a assinaturas push executando [sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md).  
  
    -   Se o valor de **allow_push** é **1**, a publicação oferece suporte a assinaturas push.  
  
    -   Se o valor de **allow_push** não é **1**, execute [sp_changemergepublication](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md), especificando **allow_push** para **@property** e **true** para **@value**.  
  
2.  No publicador do banco de dados de publicação, execute [sp_addmergesubscription](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md), especificando os seguintes parâmetros:  
  
    -   **@publication**. Esse é o nome da publicação.  
  
    -   **@subscriber_type**. Para uma assinatura de cliente, especifique **local** e, para uma assinatura de servidor, especifique **global**.  
  
    -   **@subscription_priority**. Para uma assinatura de servidor, especifique uma prioridade para a assinatura (**0,00** para **99,99**).  
  
         Para obter mais informações, consulte [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
3.  No publicador do banco de dados de publicação, execute [sp_addmergepushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md). Especifique o seguinte:  
  
    -   O **@subscriber**, **@subscriber_db**, e **@publication** parâmetros.  
  
    -   As credenciais do Windows sob a qual o Merge Agent no distribuidor executa **@job_login** e **@job_password**.  
  
        > **Observação:**  conexões feitas usando a autenticação integrada do Windows sempre usam as credenciais do Windows especificadas por **@job_login** e **@job_password**. O Merge Agent sempre faz a conexão local com o Distribuidor usando a Autenticação Integrada do Windows. Por padrão, o agente se conecta ao Assinante usando a Autenticação Integrada do Windows.  
  
    -   (Opcional) Um valor de **0** para **@subscriber_security_mode** e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] informações de logon para **@subscriber_login** e **@subscriber_password**. Especifique esses parâmetros se for necessário usar a Autenticação do SQL Server para conexão com o Assinante.  
  
    -   (Opcional) Um valor de **0** para **@publisher_security_mode** e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] informações de logon para **@publisher_login** e **@publisher_password**. Especifique esses valores se for necessário usar a Autenticação do SQL Server para conexão com o Publicador.  
  
    -   Agenda para o trabalho do Merge Agent para essa assinatura. Para obter mais informações, consulte [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md).  
  
    > **IMPORTANTE:** Ao criar uma inscrição de envio em um publicador com um distribuidor remoto, os valores fornecidos para todos os parâmetros, inclusive *job_login* e *job_password*, são enviados ao distribuidor como texto sem formatação. Você deve criptografar a conexão entre o Publicador e seu Distribuidor remoto antes de executar esse procedimento armazenado. Para obter mais informações, veja [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
###  <a name="TsqlExample"></a> Exemplos (Transact-SQL)  
 O exemplo a seguir cria uma nova assinatura push para uma publicação transacional. Os valores de logon e senha são fornecidos em tempo de execução, usando as variáveis de script **sqlcmd** .  
  
 [!code-sql[HowTo#sp_addtranpushsubscription_agent](../../relational-databases/replication/codesnippet/tsql/create-a-push-subscription_1.sql)]  
  
 O exemplo a seguir cria uma nova assinatura push para uma publicação de mesclagem. Os valores de logon e senha são fornecidos em tempo de execução, usando as variáveis de script **sqlcmd** .  
  
 [!code-sql[HowTo#sp_addmergepushsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/create-a-push-subscription_2.sql)]  
  
##  <a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
 Crie assinaturas push de forma programada, usando RMO (Replication Management Objects). As classes RMO usadas para criar uma assinatura push dependem do tipo de publicação no qual a assinatura é criada.  
  
> **IMPORTANTE:** Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for preciso armazenar credenciais, use os serviços [criptográficos](http://go.microsoft.com/fwlink/?LinkId=34733) fornecidos pelo [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework do Windows.  
  
#### Para criar uma assinatura push em um instantâneo ou publicação transacional  
  
1.  Criar uma conexão com o publicador usando o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.TransPublication> classe usando a conexão do publicador da etapa 1. Especifique <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>, <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>, e <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método. Se esse método retornar **false**, as propriedades especificadas na etapa 2 foram definidas incorretamente ou a publicação não existe no servidor.  
  
4.  Executar um e lógico bit a bit (**&** no Visual c# e **e** no Visual Basic) entre a <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> propriedade e <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPush>. Se o resultado for <xref:Microsoft.SqlServer.Replication.PublicationAttributes.None>, defina <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> ao resultado de um OR lógico bit a bit (**|** no Visual c# e **ou** no Visual Basic) entre <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> e <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPush>. Em seguida, chame <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> para permitir inscrições de envio.  
  
5.  Se o banco de dados de assinatura não existir, crie-o usando o <xref:Microsoft.SqlServer.Management.Smo.Database> classe. Para obter mais informações, consulte [criação, alteração e remoção de bancos de dados](../../relational-databases/server-management-objects-smo/tasks/creating-altering-and-removing-databases.md).  
  
6.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.TransSubscription> classe.  
  
7.  Defina as seguintes propriedades de assinatura:  
  
    -   O <xref:Microsoft.SqlServer.Management.Common.ServerConnection> para o publicador criado na etapa 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
    -   Nome do banco de dados de assinatura para <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>.  
  
    -   Nome do assinante para <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>.  
  
    -   Nome do banco de dados de publicação para <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>.  
  
    -   Nome da publicação para <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>.  
  
    -   O <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> e <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> ou <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.SecurePassword%2A> campos de <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A> para fornecer as credenciais para o [!INCLUDE[msCoName](../../includes/msconame-md.md)] conta do Windows sob a qual o Distribution Agent é executado no distribuidor. Essa conta é usada para fazer conexões locais com o Distribuidor e para fazer conexões remotas que usam a Autenticação do Windows.  
  
        > **Observação:** configuração <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A> não é necessária quando a assinatura é criada por um membro do **sysadmin** função de servidor fixa, no entanto, é recomendável. Nesse caso, o agente representará a conta do SQL Server Agent. Para obter mais informações, consulte [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
    -   (Opcional) Um valor de **true** (o padrão) para <xref:Microsoft.SqlServer.Replication.Subscription.CreateSyncAgentByDefault%2A> para criar um trabalho de agente que é usado para sincronizar a assinatura. Se você especificar **false**, a assinatura só poderá ser sincronizada programaticamente.  
  
    -   (Opcional) Definir o <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> e <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> ou <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> campos de <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> ao usar a autenticação do SQL Server para conectar-se ao assinante.  
  
8.  Chamar o <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> método.  
  
    > **IMPORTANTE!!**Ao criar uma inscrição de envio em um publicador com um distribuidor remoto, os valores fornecidos para todas as propriedades, inclusive <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>, são enviados ao distribuidor como texto sem formatação. Você deve criptografar a conexão entre o publicador e seu distribuidor remoto antes de chamar o <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> método. Para obter mais informações, veja [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
#### Para criar uma assinatura push para publicação de mesclagem  
  
1.  Criar uma conexão com o publicador usando o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.MergePublication> classe usando a conexão do publicador da etapa 1. Especifique <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>, <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>, e <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método. Se esse método retornar **false**, as propriedades especificadas na etapa 2 foram definidas incorretamente ou a publicação não existe no servidor.  
  
4.  Executar um e lógico bit a bit (**&** no Visual c# e **e** no Visual Basic) entre a <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> propriedade e <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPush>. Se o resultado for <xref:Microsoft.SqlServer.Replication.PublicationAttributes.None>, defina <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> ao resultado de um OR lógico bit a bit (**|** no Visual c# e **ou** no Visual Basic) entre <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> e <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPush>. Em seguida, chame <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> para permitir inscrições de envio.  
  
5.  Se o banco de dados de assinatura não existir, crie-o usando o <xref:Microsoft.SqlServer.Management.Smo.Database> classe. Para obter mais informações, consulte [criação, alteração e remoção de bancos de dados](../../relational-databases/server-management-objects-smo/tasks/creating-altering-and-removing-databases.md).  
  
6.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.MergeSubscription> classe.  
  
7.  Defina as seguintes propriedades de assinatura:  
  
    -   O <xref:Microsoft.SqlServer.Management.Common.ServerConnection> para o publicador criado na etapa 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
    -   Nome do banco de dados de assinatura para <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>.  
  
    -   Nome do assinante para <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>.  
  
    -   Nome do banco de dados de publicação para <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>.  
  
    -   Nome da publicação para <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>.  
  
    -   O <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> e <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> ou <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.SecurePassword%2A> campos de <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A> para fornecer as credenciais para o [!INCLUDE[msCoName](../../includes/msconame-md.md)] conta do Windows na qual o Merge Agent é executado no distribuidor. Essa conta é usada para fazer conexões locais com o Distribuidor e para fazer conexões remotas que usam a Autenticação do Windows.  
  
        > **Observação:** configuração <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A> não é necessária quando a assinatura é criada por um membro do **sysadmin** função de servidor fixa, no entanto, é recomendável. Nesse caso, o agente representará a conta do SQL Server Agent. Para obter mais informações, consulte [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
    -   (Opcional) Um valor de **true** (o padrão) para <xref:Microsoft.SqlServer.Replication.Subscription.CreateSyncAgentByDefault%2A> para criar um trabalho de agente que é usado para sincronizar a assinatura. Se você especificar **false**, a assinatura só poderá ser sincronizada programaticamente.  
  
    -   (Opcional) Definir o <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> e <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> ou <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> campos de <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> ao usar a autenticação do SQL Server para conectar-se ao assinante.  
  
    -   (Opcional) Definir o <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> e <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> ou <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> campos de <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherSecurity%2A> ao usar a autenticação do SQL Server para se conectar ao Editor.  
  
8.  Chamar o <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> método.  
  
    > **IMPORTANTE:**  Ao criar uma inscrição de envio em um publicador com um distribuidor remoto, os valores fornecidos para todas as propriedades, inclusive <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>, são enviados ao distribuidor como texto sem formatação. Você deve criptografar a conexão entre o publicador e seu distribuidor remoto antes de chamar o <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> método. Para obter mais informações, veja [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
###  <a name="PShellExample"></a> Exemplos (RMO)  
 Esse exemplo cria uma nova assinatura push para uma publicação transacional. As credenciais da conta do Windows usadas para executar o trabalho do Distribution Agent são passadas em tempo de execução.  
  
 [!code-csharp[HowTo#rmo_CreateTranPushSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createtranpushsub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateTranPushSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createtranpushsub)]  
  
 Esse exemplo cria uma nova assinatura push para uma publicação de mesclagem. As credenciais da conta do Windows usadas para executar o trabalho do Agente de Mesclagem são passadas em tempo de execução.  
  
 [!code-csharp[HowTo#rmo_CreateMergePushSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergepushsub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePushSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergepushsub)]  
  
## Consulte também  
 [Exibir e modificar propriedades de assinatura push](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [Práticas recomendadas em relação à segurança de replicação](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Crie uma publicação](../../relational-databases/replication/publish/create-a-publication.md)   
 [Conceitos de Replication Management Objects](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [Sincronizar uma assinatura push](../../relational-databases/replication/synchronize-a-push-subscription.md)   
 [Assinar publicações](../../relational-databases/replication/subscribe-to-publications.md)   
 [Usar sqlcmd com variáveis de script](../../relational-databases/scripting/use-sqlcmd-with-scripting-variables.md)  
  
  