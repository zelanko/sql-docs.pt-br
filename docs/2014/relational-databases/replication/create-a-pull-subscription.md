---
title: Criar uma assinatura pull | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- pull subscriptions [SQL Server replication], creating
- merge replication subscribing [SQL Server replication], pull subscriptions
- subscriptions [SQL Server replication], pull
- snapshot replication [SQL Server], subscribing
- transactional replication, subscribing
ms.assetid: 41d1886d-59c9-41fc-9bd6-a59b40e0af6e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f8868957d7c479de3a51a599deed42c34d6676eb
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52753488"
---
# <a name="create-a-pull-subscription"></a>Create a Pull Subscription
  Este tópico descreve como criar uma assinatura pull no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]ou RMO (Replication Management Objects).  
  
 A configuração de uma assinatura pull para a replicação de P2P é possível por script, mas não está disponível por meio do assistente.  
  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Crie uma assinatura pull no Publicador ou Assinante, usando o Assistente para Novas Assinaturas. Siga as páginas no assistente para:  
  
-   Especificar o Publicador e a publicação.  
  
-   Selecione onde os agentes de replicação executarão. Para uma assinatura pull, selecione **Executar cada agente como seu assinante (assinaturas pull)** na página **Local do Distribution Agent** ou na página **Local do Merge Agent** , dependendo do tipo de publicação.  
  
-   Especifique Assinantes e bancos de dados de assinatura.  
  
-   Especifique os logons e senhas usadas para conexões feitas por agentes de replicação:  
  
    -   Para assinaturas para instantâneos e publicações transacionais, especifique as credenciais na página **Segurança do Distribution Agent** .  
  
    -   Para assinaturas para publicações de mesclagem, especifique as credenciais na página **Segurança do Merge Agent** .  
  
     Para obter informações sobre as permissões exigidas por cada agente, consulte [Replication Agent Security Model](security/replication-agent-security-model.md).  
  
-   Especifique uma agenda de sincronização e quando o Assinante deve ser inicializado.  
  
-   Especifique opções adicionais para as publicações de mesclagem: tipo da assinatura; valores para filtragem com parâmetros e as informações para sincronização através de HTTPS se a publicação estiver habilitada para sincronização da Web.  
  
-   Especifique opções adicionais para publicações transacionais que permitem assinaturas de atualização: se os Assinantes devem confirmar alterações no Publicador imediatamente ou gravá-las em uma fila; credenciais usadas do Assinante para o Publicador.  
  
-   Opcionalmente, faça o script da assinatura.  
  
#### <a name="to-create-a-pull-subscription-from-the-publisher"></a>Para criar uma assinatura pull do Publicador  
  
1.  Conecte-se ao Publicador no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e, depois, expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações Locais** .  
  
3.  Clique com o botão direito do mouse na publicação na qual você deseja criar uma ou mais assinaturas e clique em **Novas Assinaturas**.  
  
4.  Complete as páginas no Assistente para Novas Assinaturas.  
  
#### <a name="to-create-a-pull-subscription-from-the-subscriber"></a>Para criar uma assinatura pull do Assinante  
  
1.  Conecte-se ao Assinante no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** .  
  
3.  Clique com o botão direito do mouse na pasta **Assinaturas Locais** e depois clique em **Novas Assinaturas**.  
  
4.  Na página **Publicação** do Assistente para Nova Assinatura, selecione **\<Encontrar publicador do SQL Server>** ou **\<Encontrar publicador do Oracle>** na lista suspensa **Publicador**.  
  
5.  Conecte-se ao Publicador na caixa de diálogo **Conectar ao Servidor** .  
  
6.  Selecione uma publicação na página **Publicação** .  
  
7.  Complete as páginas no Assistente para Novas Assinaturas.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 As assinaturas pull podem ser criadas de forma programada, usando os procedimentos de replicação armazenados. Os procedimentos armazenados usados dependem do tipo de publicação ao qual a assinatura pertence.  
  
#### <a name="to-create-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>Para criar uma assinatura pull em um instantâneo ou em uma publicação transacional  
  
1.  No Publicador, verifique se a publicação dá suporte a assinaturas pull executando [sp_helppublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql).  
  
    -   Se o valor de **allow_pull** no conjunto de resultados for **1**, a publicação terá suporte para as assinaturas pull.  
  
    -   Se o valor de **allow_pull** é **0**, execute [sp_changepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql), especificando **allow_pull**para **@property** e `true` para **@value**.  
  
2.  No Assinante, execute [sp_addpullsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql). Especifique **@publisher** e **@publication**. Para obter mais informações sobre assinaturas de atualização, consulte [Criar uma assinatura atualizável em uma publicação transacional](publish/create-an-updatable-subscription-to-a-transactional-publication.md)  
  
3.  No Assinante, execute [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql). Especifique o seguinte:  
  
    -   Os parâmetros **@publisher**, **@publisher_db**, e **@publication** .  
  
    -   Os parâmetros [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows sob as quais o Distribution Agent do Assinante é executado para **@job_login** e **@job_password**.  
  
        > [!NOTE]  
        >  As conexões realizadas com Autenticação Integrada do Windows sempre usam as credenciais do Windows especificadas por **@job_login** e **@job_password**. O Distribution Agent sempre faz a conexão local ao Assinante usando a Autenticação Integrada do Windows. Por padrão, o agente conecta-se ao Distribuidor usando a Autenticação Integrada do Windows.  
  
    -   (Opcional) Um valor de **0** para **@distributor_security_mode** e o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] informações de logon para **@distributor_login** e **@distributor_password**, se você precisar usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação ao conectar-se ao distribuidor.  
  
    -   Agenda para o trabalho do Distribution Agent para essa assinatura. Para obter mais informações, consulte [Specify Synchronization Schedules](specify-synchronization-schedules.md).  
  
4.  No Publicador, execute [sp_addsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql) para registrar a assinatura pull. Especifique **@publication**, o **@subscriber**, e **@destination_db**. Especifique um valor de **pull** para **@subscription_type**.  
  
#### <a name="to-create-a-pull-subscription-to-a-merge-publication"></a>Para criar uma assinatura pull para a publicação de mesclagem  
  
1.  No Publicador, verifique se a publicação dá suporte a assinaturas pull executando [sp_helpmergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql).  
  
    -   Se o valor de **allow_pull** no conjunto de resultados for **1**, a publicação terá suporte para as assinaturas pull.  
  
    -   Se o valor de **allow_pull** é **0**, execute [sp_changemergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql), especificando **allow_pull** para **@property** e `true` para **@value**.  
  
2.  No Assinante, execute [sp_addmergepullsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql). Especifique **@publisher**, **@publisher_db**, **@publication**e os parâmetros a seguir:  
  
    -   **@subscriber_type** – especifique **local** para uma assinatura de cliente e **global** para uma assinatura de servidor.  
  
    -   **@subscription_priority** – especifique uma prioridade para a assinatura (**0.00** a **99.99**). Isso só é necessário para uma assinatura de servidor.  
  
         Para obter mais informações, consulte [Advanced Merge Replication Conflict Detection and Resolution](merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
3.  No Assinante, execute [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql). Especifique os seguintes parâmetros:  
  
    -   **@publisher**, **@publisher_db**, e **@publication**.  
  
    -   As credenciais do Windows sob as quais o Merge Agent no Assinante é executado para **@job_login** e **@job_password**.  
  
        > [!NOTE]  
        >  As conexões realizadas com Autenticação Integrada do Windows sempre usam as credenciais do Windows especificadas por **@job_login** e **@job_password**. O Merge Agent sempre faz a conexão local ao Assinante usando a Autenticação Integrada do Windows. Por padrão, o agente se conecta ao Distribuidor e ao Publicador usando a Autenticação Integrada do Windows.  
  
    -   (Opcional) Um valor de **0** para **@distributor_security_mode** e as informações de logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para **@distributor_login** e **@distributor_password**, se for necessário usar a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao se conectar ao Distribuidor.  
  
    -   (Opcional) Um valor de **0** para **@publisher_security_mode** e as informações de logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para **@publisher_login** e **@publisher_password**, se for necessário usar a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao conectar-se ao Publicador.  
  
    -   Agenda para o trabalho do Merge Agent para essa assinatura. Para obter mais informações, consulte [Criar uma assinatura atualizável em uma publicação transacional](publish/create-an-updatable-subscription-to-a-transactional-publication.md)  
  
4.  No Publicador, execute [sp_addmergesubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql). Especifique **@publication**, **@subscriber**, **@subscriber_db**, e o valor **pull** para **@subscription_type**. Isso registra a assinatura pull.  
  
###  <a name="TsqlExample"></a> Exemplos (Transact-SQL)  
 O exemplo a seguir cria uma nova assinatura pull para uma publicação transacional. O primeiro lote é executado no Assinante, e o segundo lote é executado no Publicador. Os valores para o logon e senha são fornecidos no tempo de execução usando as variáveis sqlcmd scripting.  
  
 [!code-sql[HowTo#sp_addtranpullsubscriptionagent](../../snippets/tsql/SQL15/replication/howto/tsql/createtranpullsub.sql#sp_addtranpullsubscriptionagent)]  
  
 [!code-sql[HowTo#sp_addtranpullsubscription](../../snippets/tsql/SQL15/replication/howto/tsql/createtranpullsub.sql#sp_addtranpullsubscription)]  
  
 O exemplo a seguir cria uma nova assinatura pull para uma publicação de mesclagem. O primeiro lote é executado no Assinante, e o segundo lote é executado no Publicador. Os valores de logon e senha são fornecidos em tempo de execução através das variáveis de script **sqlcmd** .  
  
 [!code-sql[HowTo#sp_addmergepullsubscriptionagent](../../snippets/tsql/SQL15/replication/howto/tsql/createmergepullsub.sql#sp_addmergepullsubscriptionagent)]  
  
 [!code-sql[HowTo#sp_addmergepullsubscription](../../snippets/tsql/SQL15/replication/howto/tsql/createmergepullsub.sql#sp_addmergepullsubscription)]  
  
##  <a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
 As classes RMO usadas para criar uma assinatura pull dependem do tipo de publicação ao qual a assinatura pertence.  
  
#### <a name="to-create-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>Para criar uma assinatura pull em um instantâneo ou em uma publicação transacional  
  
1.  Crie conexões para o Assinante e Publicador, usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.TransPublication> usando a conexão com o Publicador da etapa 1. Especifique <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>, <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> e <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A>. Se esse método retornar `false`, as propriedades especificadas na etapa 2 estarão incorretas ou a publicação não existe no servidor.  
  
4.  Realize uma lógica AND de bit a bit (`&` no Visual C# e `And` no Visual Basic) entre a propriedade <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> e <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPull>. Se o resultado for <xref:Microsoft.SqlServer.Replication.PublicationAttributes.None>, defina <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> para o resultado de uma lógica bit a bit OR (`|` em Visual C# e `Or` em Visual Basic) entre <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> e <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPull>. Em seguida, chame <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> para habilitar assinaturas pull.  
  
5.  Se não houver banco de dados de assinatura, crie-o usando a classe <xref:Microsoft.SqlServer.Management.Smo.Database> . Para obter mais informações, consulte [Creating, Altering, and Removing Databases](../server-management-objects-smo/tasks/creating-altering-and-removing-databases.md) (Criando, alterando e removendo bancos de dados).  
  
6.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.TransPullSubscription> .  
  
7.  Defina as seguintes propriedades de assinatura:  
  
    -   O <xref:Microsoft.SqlServer.Management.Common.ServerConnection> para o Assinante criado na etapa 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
    -   Nome do banco de dados de assinatura para <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>.  
  
    -   Nome do Publicador para <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>.  
  
    -   Nome do banco de dados de publicação para <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>.  
  
    -   Nome da publicação para <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>.  
  
    -   Os campos <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> e <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> ou <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.SecurePassword%2A> de <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A> para fornecer as credenciais para a conta do Windows [!INCLUDE[msCoName](../../includes/msconame-md.md)] em que o Distribution Agent é executado no Assinante. Essa conta é usada para fazer conexões locais com o Assinante e para fazer conexões remotas que usam a Autenticação do Windows.  
  
        > [!NOTE]  
        >  Não é necessário definir <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A> quando a assinatura for criada por um membro da função de servidor fixa `sysadmin`; no entanto, é recomendado. Nesse caso, o agente representará a conta do SQL Server Agent. Para obter mais informações, consulte [Replication Agent Security Model](security/replication-agent-security-model.md).  
  
    -   (Opcional) Um valor de `true` para <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> para criar um trabalho de agente que seja usado para sincronizar a assinatura. Se você especificar `false` (o padrão), a assinatura pode ser sincronizada apenas de forma programada e é preciso especificar propriedades adicionais para <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent> ao acessar esse objeto da propriedade <xref:Microsoft.SqlServer.Replication.TransPullSubscription.SynchronizationAgent%2A>. Para obter mais informações, consulte [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md).  
  
        > [!NOTE]  
        >  O SQL Server Agent não está disponível em todas as edições do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md). Quando você especifica um valor de `true` para Assinantes do Express, o trabalho de agente não é criado. Porém, importantes metadados relacionados a assinatura são armazenados no Assinante.  
  
    -   (Opcional) Defina os campos <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> e <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> ou <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> de <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> ao usar a Autenticação do SQL Server para conexão com o Distribuidor.  
  
8.  Chame o método <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A> .  
  
9. Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.TransPublication> da etapa 2, chame o método <xref:Microsoft.SqlServer.Replication.TransPublication.MakePullSubscriptionWellKnown%2A> para registrar a assinatura pull com o Publicador. Se esse registro já existir, haverá uma exceção.  
  
#### <a name="to-create-a-pull-subscription-to-a-merge-publication"></a>Para criar uma assinatura pull para a publicação de mesclagem  
  
1.  Crie conexões para o Assinante e o Publicador usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.MergePublication> usando a conexão com o Publicador da etapa 1. Especifique <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>, <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>, e <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A>. Se esse método retornar `false`, as propriedades especificadas na etapa 2 estarão incorretas ou a publicação não existe no servidor.  
  
4.  Realize uma lógica AND de bit a bit (`&` no Visual C# e `And` no Visual Basic) entre a propriedade <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> e <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPull>. Se o resultado for <xref:Microsoft.SqlServer.Replication.PublicationAttributes.None>, defina <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> para o resultado de uma lógica bit a bit OR (`|` em Visual C# e `Or` em Visual Basic) entre <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> e <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPull>. Em seguida, chame <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> para habilitar assinaturas pull.  
  
5.  Se não houver banco de dados de assinatura, crie-o usando a classe <xref:Microsoft.SqlServer.Management.Smo.Database> . Para obter mais informações, consulte [Creating, Altering, and Removing Databases](../server-management-objects-smo/tasks/creating-altering-and-removing-databases.md) (Criando, alterando e removendo bancos de dados).  
  
6.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.MergePullSubscription> .  
  
7.  Defina as seguintes propriedades de assinatura:  
  
    -   O <xref:Microsoft.SqlServer.Management.Common.ServerConnection> para o Assinante criado na etapa 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
    -   Nome do banco de dados de assinatura para <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>.  
  
    -   Nome do Publicador para <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>.  
  
    -   Nome do banco de dados de publicação para <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>.  
  
    -   Nome da publicação para <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>.  
  
    -   Os campos <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> e <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> ou <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.SecurePassword%2A> de <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A> para fornecer as credenciais para a conta do Windows [!INCLUDE[msCoName](../../includes/msconame-md.md)] na qual o Merge Agent é executado no Assinante. Essa conta é usada para fazer conexões locais com o Assinante e para fazer conexões remotas que usam a Autenticação do Windows.  
  
        > [!NOTE]  
        >  Não é necessário definir <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A> quando a assinatura for criada por um membro da função de servidor fixa `sysadmin`; no entanto, é recomendado. Nesse caso, o agente representará a conta do SQL Server Agent. Para obter mais informações, consulte [Replication Agent Security Model](security/replication-agent-security-model.md).  
  
    -   (Opcional) Um valor de `true` para <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> para criar um trabalho de agente que seja usado para sincronizar a assinatura. Se você especificar `false` (o padrão), a assinatura pode ser sincronizada apenas de forma programada e é preciso especificar propriedades adicionais para <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent> ao acessar esse objeto da propriedade <xref:Microsoft.SqlServer.Replication.MergePullSubscription.SynchronizationAgent%2A>. Para obter mais informações, consulte [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md).  
  
    -   (Opcional) Defina os campos <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> e <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> ou <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> de <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> ao usar a Autenticação do SQL Server para conexão com o Distribuidor.  
  
    -   (Opcional) Defina os campos <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> e <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> ou <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> de <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherSecurity%2A> ao usar a Autenticação do SQL Server para conexão com o Publicador.  
  
8.  Chame o método <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A>.  
  
9. Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.MergePublication> da etapa 2, chame o método <xref:Microsoft.SqlServer.Replication.MergePublication.MakePullSubscriptionWellKnown%2A> para registrar a assinatura pull com o Publicador. Se esse registro já existir, haverá uma exceção.  
  
###  <a name="PShellExample"></a> Exemplo (RMO)  
 Esse exemplo cria uma assinatura pull para uma publicação transacional. As credenciais da conta do Windows [!INCLUDE[msCoName](../../includes/msconame-md.md)] usadas para criar o trabalho do Distribution Agent são passadas em tempo de execução.  
  
 [!code-csharp[HowTo#rmo_CreateTranPullSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createtranpullsub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateTranPullSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createtranpullsub)]  
  
 Esse exemplo cria uma assinatura pull para uma publicação de mesclagem. As credenciais da conta do Windows usadas para criar o trabalho do Agente de Mesclagem são passadas em tempo de execução.  
  
 [!code-csharp[HowTo#rmo_CreateMergePullSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createmergepullsub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePullSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createmergepullsub)]  
  
 Esse exemplo cria uma assinatura pull para uma publicação de mesclagem, sem criar um trabalho de agente associado e metadados de assinatura em [MSsubscription_properties](/sql/relational-databases/system-tables/mssubscription-properties-transact-sql). As credenciais da conta do Windows usadas para criar o trabalho do Agente de Mesclagem são passadas em tempo de execução.  
  
 [!code-csharp[HowTo#rmo_CreateMergePullSub_NoJob](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createmergepullsub_nojob)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePullSub_NoJob](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createmergepullsub_nojob)]  
  
 Esse exemplo cria uma assinatura pull para uma publicação de mesclagem que pode ser sincronizada pela Internet usando-se sincronização da Web. As credenciais da conta do Windows usadas para criar o trabalho do Agente de Mesclagem são passadas em tempo de execução. Para obter mais informações, consulte [Configure Web Synchronization](configure-web-synchronization.md).  
  
 [!code-csharp[HowTo#rmo_CreateMergePullSub_WebSync](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createmergepullsub_websync)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePullSub_WebSync](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createmergepullsub_websync)]  
  
## <a name="see-also"></a>Consulte também  
 [Replication Management Objects Concepts](concepts/replication-management-objects-concepts.md)   
 [Exibir e modificar propriedades de assinatura pull](view-and-modify-pull-subscription-properties.md)   
 [Configure Web Synchronization](configure-web-synchronization.md)   
 [Subscribe to Publications](subscribe-to-publications.md)   
 [Replication Security Best Practices](security/replication-security-best-practices.md)  
  
  
