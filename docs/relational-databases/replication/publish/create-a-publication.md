---
title: "Crie uma publica&#231;&#227;o | Microsoft Docs"
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
  - "publicações [replicação do SQL Server], criando"
  - "artigos [replicação do SQL Server], definindo"
  - "adicionando artigos"
  - "artigos [replicação do SQL Server], adicionando"
ms.assetid: 52ee6de9-1d58-4cb9-8711-372bddbe7154
caps.latest.revision: 44
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 44
---
# Crie uma publica&#231;&#227;o
  Este tópico descreve como criar uma publicação no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou RMO (Replication Management Objects).  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para criar uma publicação e definir artigos, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO (Replication Management Objects)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Nomes de publicação e do artigo não podem incluir nenhum dos seguintes caracteres: %, \* , [,], |,:, ",? , ' , \ , / , \< , >. Se os objetos no banco de dados incluem qualquer um desses caracteres e para replicá-los, você deve especificar um nome de artigo é diferente do nome do objeto no **Propriedades do artigo - \< artigo>** caixa de diálogo, que está disponível na **artigos** página do assistente.  
  
###  <a name="Security"></a> Segurança  
 Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for preciso armazenar credenciais, use os serviços [criptográficos](http://go.microsoft.com/fwlink/?LinkId=34733) fornecidos pelo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework do Windows.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Crie publicações e defina artigos com o Assistente para Nova Publicação. Depois que uma publicação é criada, exibir e modificar propriedades de publicação na **Propriedades de publicação - \< publicação>** caixa de diálogo. Para obter informações sobre como criar uma publicação de um banco de dados Oracle, consulte [criar uma publicação de um banco de dados Oracle](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md).  
  
#### Para criar uma publicação e definir artigos  
  
1.  Conecte-se ao Publicador no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]e, depois, expanda o nó do servidor.  
  
2.  Expanda o **replicação** pasta e, em seguida, clique com botão direito do **publicações locais** pasta.  
  
3.  Clique em **Nova Publicação**.  
  
4.  Siga as páginas no Assistente para Nova Publicação para:  
  
    -   Especificar um Distribuidor se a distribuição não foi configurada no servidor. Para obter mais informações sobre a configuração de distribuição, consulte [Configurar publicação e distribuição](../../../relational-databases/replication/configure-publishing-and-distribution.md).  
  
         Se você especificar o **distribuidor** página que o servidor do publicador atuará como seu próprio distribuidor (um distribuidor local) e o servidor não está configurado como um distribuidor, o Assistente para nova publicação configurará o servidor. Você especificará uma pasta de instantâneo padrão para o Distribuidor na página **Pasta de Instantâneos** . A pasta de instantâneo é simplesmente um diretório que você designou como um compartilhamento, agentes que leem essa pasta e gravam nela devem ter permissões suficientes para acessá-la. Para obter mais informações sobre como proteger a pasta adequadamente, consulte [proteger a pasta de instantâneo](../../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
         Se você especificar que um outro servidor deverá atuar como um Distribuidor, você deverá inserir uma senha na página **Senha Administrativa** para conexões feitas do Publicador ao Distribuidor. Esta senha deve corresponder à senha especificada quando o Publicador foi habilitado no Distribuidor remoto.  
  
         Para obter mais informações, consulte [Configurar distribuição](../../../relational-databases/replication/configure-distribution.md).  
  
    -   Escolha um banco de dados de publicação.  
  
    -   Selecione um tipo de publicação. Para obter mais informações, consulte [tipos de replicação](../../../relational-databases/replication/types-of-replication.md).  
  
    -   Especifique os dados e os objetos de banco de dados para serem publicados; opcionalmente filtre as colunas de artigos de tabela e defina as propriedades dos artigos.  
  
    -   Opcionalmente filtre as linhas de artigos de tabela. Para obter mais informações, consulte [Filtrar dados publicados](../../../relational-databases/replication/publish/filter-published-data.md).  
  
    -   Defina a agenda do Snapshot Agent.  
  
    -   Especifique as credenciais sob as quais os agentes de replicação a seguir executam e fazem conexões:  
  
         \- Agente de instantâneo para todas as publicações.  
  
         \- O Log Reader Agent para todas as publicações transacionais.  
  
         \- Queue Reader Agent para publicações transacionais que permitem assinaturas de atualização.  
  
         Para obter mais informações, consulte [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md) e [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md).  
  
    -   Opcionalmente faça o script da publicação. Para obter mais informações, consulte [Scripting Replication](../../../relational-databases/replication/scripting-replication.md).  
  
    -   Especifique um nome para a publicação.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 Publicações podem ser criadas programaticamente usando procedimentos armazenados de replicação. Os procedimentos armazenados a serem usados dependerão do tipo de publicação a ser criada.  
  
#### Para criar uma publicação de instantâneo ou transacional  
  
1.  No publicador do banco de dados de publicação, execute [sp_replicationdboption & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) Para habilitar a publicação do banco de dados atual usando replicação de instantâneo ou transacional.  
  
2.  Para uma publicação transacional, determine se um existe um trabalho do Log Reader Agent para o banco de dados de publicação. (Essa etapa não é requerida para publicações de instantâneo.)  
  
    -   Se já houver um trabalho do Log Reader Agent para o banco de dados de publicação, passe à etapa 3.  
  
    -   Se você não tiver certeza se um trabalho do Log Reader Agent existe para um banco de dados publicado, execute [sp_helplogreader_agent & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md) o publicador do banco de dados de publicação.  
  
    -   Se o conjunto de resultados estiver vazio, crie um trabalho do Log Reader Agent. No publicador, execute [sp_addlogreader_agent & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md). Especifique o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] credenciais do Windows sob a qual o agente executa **@job_name** e **@password**. Se o agente usar autenticação do SQL Server ao se conectar ao Editor, você também deve especificar um valor de **0** para **@publisher_security_mode** e [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] informações de logon para **@publisher_login** e **@publisher_password**. Passe para a etapa 3.  
  
3.  No publicador, execute [sp_addpublication & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md). Especifique um nome de publicação para **@publication**, e, para o **@repl_freq** parâmetro, especifique um valor de **instantâneo** para uma publicação de instantâneo ou um valor de **contínua** para uma publicação transacional. Especifique quaisquer outras opções de publicação. Isso define a publicação.  
  
    > [!NOTE]  
    >  Os nomes de publicação não podem incluir nenhum dos caracteres a seguir:  
    >   
    >  % * [ ] | : " ? \ / \< >  
  
4.  No publicador, execute [sp_addpublication_snapshot & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md). Especifique o nome da publicação usado na etapa 3 para **@publication** e as credenciais do Windows na qual o Snapshot Agent é executado para **@snapshot_job_name** e **@password**. Se o agente usar autenticação do SQL Server ao se conectar ao Editor, você também deve especificar um valor de **0** para **@publisher_security_mode** e o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] informações de logon para **@publisher_login** e **@publisher_password**. Isso cria um trabalho do Agente de Instantâneo para a publicação.  
  
    > [!IMPORTANT]  
    >  Ao configurar um editor com um distribuidor remoto, os valores fornecidos para todos os parâmetros, incluindo *job_login* e *job_password*, são enviados ao distribuidor como texto sem formatação. Você deve criptografar a conexão entre o Publicador e seu Distribuidor remoto antes de executar esse procedimento armazenado. Para obter mais informações, consulte [Habilitar conexões criptografadas para o mecanismo de banco de dados e 40; SQL Server Configuration Manager & 41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
5.  Adicione artigos à publicação. Para obter mais informações, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
6.  Inicie o trabalho do Agente de Instantâneo para gerar o instantâneo inicial para essa publicação. Para obter mais informações, consulte [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
#### Para criar uma publicação de mesclagem  
  
1.  No publicador, execute [sp_replicationdboption & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) Para habilitar a publicação do banco de dados atual usando replicação de mesclagem.  
  
2.  No publicador do banco de dados de publicação, execute [sp_addmergepublication & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). Especifique o nome da publicação para **@publication** e quaisquer outras opções de publicação. Isso define a publicação.  
  
    > [!NOTE]  
    >  Os nomes de publicação não podem incluir nenhum dos caracteres a seguir:  
    >   
    >  % * [ ] | : " ? \ / \< >  
  
3.  No publicador, execute [sp_addpublication_snapshot & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md). Especifique o nome da publicação usado na etapa 2 para **@publication** e as credenciais do Windows na qual o Snapshot Agent é executado para **@snapshot_job_name** e **@password**. Se o agente usar autenticação do SQL Server ao se conectar ao Editor, você também deve especificar um valor de **0** para **@publisher_security_mode** e o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] informações de logon para **@publisher_login** e **@publisher_password**. Isso cria um trabalho do Agente de Instantâneo para a publicação.  
  
    > [!IMPORTANT]  
    >  Ao configurar um editor com um distribuidor remoto, os valores fornecidos para todos os parâmetros, incluindo *job_login* e *job_password*, são enviados ao distribuidor como texto sem formatação. Você deve criptografar a conexão entre o Publicador e seu Distribuidor remoto antes de executar esse procedimento armazenado. Para obter mais informações, consulte [Habilitar conexões criptografadas para o mecanismo de banco de dados e 40; SQL Server Configuration Manager & 41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
4.  Adicione artigos à publicação. Para obter mais informações, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
5.  Inicie o trabalho do Agente de Instantâneo para gerar o instantâneo inicial para essa publicação. Para obter mais informações, consulte [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
###  <a name="TsqlExample"></a> Exemplo (Transact-SQL)  
 Este exemplo cria uma publicação transacional. As variáveis de script são usadas para passar as credenciais do Windows necessárias para criar trabalhos do Agente de Instantâneo e do Agente de Leitor de Log.  
  
 [!code-sql[HowTo#sp_AddTranPub](../../../relational-databases/replication/codesnippet/tsql/create-a-publication_1.sql)]  
  
 Este exemplo cria uma publicação de mesclagem. As variáveis de script são usadas para passar as credenciais do Windows necessárias para criar o trabalho do Agente de Instantâneo.  
  
 [!code-sql[HowTo#sp_AddMergePub](../../../relational-databases/replication/codesnippet/tsql/create-a-publication_2.sql)]  
  
##  <a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
 Crie publicações de forma programada, usando o RMO (Replication Management Objects). As classes de RMO usadas para criar uma publicação dependem do tipo de publicação criada.  
  
#### Para criar uma publicação de instantâneo ou transacional  
  
1.  Criar uma conexão com o publicador usando o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> de classe para o banco de dados de publicação, defina o <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propriedade para a instância do <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da etapa 1 e chame o <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método. Se <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> retorna **false**, verifique se existe o banco de dados.  
  
3.  Se o <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledTransPublishing%2A> é de propriedade **false**, defina-o como **true**.  
  
4.  Para uma publicação transacional, verifique o valor de <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentExists%2A> propriedade. Se essa propriedade for **true**, um trabalho do Log Reader Agent já existirá para esse banco de dados. Se essa propriedade for **false**, faça o seguinte:  
  
    -   Definir o <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> e <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> ou <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.SecurePassword%2A> campos de <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentProcessSecurity%2A> para fornecer as credenciais para o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] da conta do Windows na qual o Log Reader Agent é executado.  
  
        > [!NOTE]  
        >  Definindo <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentProcessSecurity%2A> não é necessário quando a publicação é criada por um membro do **sysadmin** função de servidor fixa. Nesse caso, o agente representará a conta do SQL Server Agent. Para obter mais informações, consulte [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
    -   (Opcional) Definir o <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> e <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> ou <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> campos de <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentPublisherSecurity%2A> ao usar a autenticação do SQL Server para se conectar ao Editor.  
  
    -   Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.CreateLogReaderAgent%2A> método para criar o trabalho do Log Reader Agent para o banco de dados.  
  
5.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.TransPublication> de classe e defina as seguintes propriedades para esse objeto:  
  
    -   O <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da etapa 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
    -   O nome do banco de dados publicado <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>.  
  
    -   Um nome para a publicação de <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>.  
  
    -   Um <xref:Microsoft.SqlServer.Replication.PublicationType> do <xref:Microsoft.SqlServer.Replication.PublicationType.Transactional> ou <xref:Microsoft.SqlServer.Replication.PublicationType.Snapshot>.  
  
    -   O <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> e <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> campos de <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> para fornecer as credenciais da conta do Windows sob a qual o Snapshot Agent é executado. Essa conta é também usada quando o Snapshot Agent faz conexões com o Distributor local e para conexões remotas quando se usa a Autenticação do Windows.  
  
        > [!NOTE]  
        >  Definindo <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> não é necessário quando a publicação é criada por um membro do **sysadmin** função de servidor fixa. Nesse caso, o agente representará a conta do SQL Server Agent. Para obter mais informações, consulte [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
    -   (Opcional) O <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> e <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> ou <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> campos de <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentPublisherSecurity%2A> ao usar a autenticação do SQL Server para se conectar ao Editor.  
  
    -   (Opcional) Use o operador OR lógica inclusiva (**|** no Visual c# e **ou** no Visual Basic) e o operador OR lógica exclusiva (**^** no Visual c# e **Xor** no Visual Basic) para definir o <xref:Microsoft.SqlServer.Replication.PublicationAttributes> valores para o <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> propriedade.  
  
    -   (Opcional) O nome do publicador para <xref:Microsoft.SqlServer.Replication.TransPublication.PublisherName%2A> quando o publicador é um publicador não SQL Server.  
  
6.  Chamar o <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> método para criar a publicação.  
  
    > [!IMPORTANT]  
    >  Ao configurar um editor com um distribuidor remoto, os valores fornecidos para todas as propriedades, incluindo <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A>, são enviados ao distribuidor como texto sem formatação. Você deve criptografar a conexão entre o publicador e seu distribuidor remoto antes de chamar o <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> método. Para obter mais informações, consulte [Habilitar conexões criptografadas para o mecanismo de banco de dados e 40; SQL Server Configuration Manager & 41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
7.  Chamar o <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> método para criar o trabalho do Snapshot Agent para a publicação.  
  
#### Para criar uma publicação de mesclagem  
  
1.  Criar uma conexão com o publicador usando o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> de classe para o banco de dados de publicação, defina o <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propriedade para a instância do <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da etapa 1 e chame o <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método. Se <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> retorna **false**, verifique se existe o banco de dados.  
  
3.  Se <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledMergePublishing%2A> é de propriedade **false**, defina-o como **true**, e chamar <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A>.  
  
4.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.MergePublication> de classe e defina as seguintes propriedades para esse objeto:  
  
    -   O <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da etapa 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
    -   O nome do banco de dados publicado <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>.  
  
    -   Um nome para a publicação de <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>.  
  
    -   O <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> e <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> campos de <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> para fornecer as credenciais da conta do Windows sob a qual o Snapshot Agent é executado. Essa conta é também usada quando o Snapshot Agent faz conexões com o Distributor local e para conexões remotas quando se usa a Autenticação do Windows.  
  
        > [!NOTE]  
        >  Definindo <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> não é necessário quando a publicação é criada por um membro do **sysadmin** função de servidor fixa. Para obter mais informações, consulte [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
    -   (Opcional) Use o operador OR lógica inclusiva (**|** no Visual c# e **ou** no Visual Basic) e o operador OR lógica exclusiva (**^** no Visual c# e **Xor** no Visual Basic) para definir o <xref:Microsoft.SqlServer.Replication.PublicationAttributes> valores para o <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> propriedade.  
  
5.  Chamar o <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> método para criar a publicação.  
  
    > [!IMPORTANT]  
    >  Ao configurar um editor com um distribuidor remoto, os valores fornecidos para todas as propriedades, incluindo <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A>, são enviados ao distribuidor como texto sem formatação. Você deve criptografar a conexão entre o publicador e seu distribuidor remoto antes de chamar o <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> método. Para obter mais informações, consulte [Habilitar conexões criptografadas para o mecanismo de banco de dados e 40; SQL Server Configuration Manager & 41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
6.  Chamar o <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> método para criar o trabalho do Snapshot Agent para a publicação.  
  
###  <a name="PShellExample"></a> Exemplos (RMO)  
 Esse exemplo ativa o banco de dados AdventureWorks para publicação transacional; define um trabalho do Agente de Leitor de Log e cria a publicação AdvWorksProductTran. É preciso definir um artigo para essa publicação. As credenciais da conta do Windows necessárias para criar o trabalho do Log Reader Agent e o do Snapshot Agent são passadas em tempo de execução. Para saber como usar RMO para definir artigos instantâneos e transacionais, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
 [!code-csharp[HowTo#rmo_CreateTranPub](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createtranpub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateTranPub](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createtranpub)]  
  
 Esse exemplo ativa o banco de dados AdventureWorks para publicação de mesclagem e cria a publicação AdvWorksSalesOrdersMerge. Artigos ainda precisam ser definidos para essa publicação. As credenciais da conta do Windows, necessárias para criar o trabalho do Agente de Instantâneo, são passadas em tempo de execução. Para saber como usar RMO para definir artigos de mesclagem, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
 [!code-csharp[HowTo#rmo_CreateMergePub](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergepub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePub](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergepub)]  
  
## Consulte também  
 [Usar sqlcmd com variáveis de script](../../../relational-databases/scripting/use-sqlcmd-with-scripting-variables.md)   
 [Publicar dados e objetos de banco de dados](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Conceitos de Replication Management Objects](../../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [Defina um Artigo](../../../relational-databases/replication/publish/define-an-article.md)   
 [Visualizar e modificar as propriedades da publicação](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Configurar a distribuição](../../../relational-databases/replication/configure-distribution.md)   
 [Proteger o distribuidor](../../../relational-databases/replication/security/secure-the-distributor.md)   
 [Proteger o Publicador](../../../relational-databases/replication/security/secure-the-publisher.md)  
  
  