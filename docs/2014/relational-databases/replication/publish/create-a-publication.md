---
title: Criar uma publicação | Microsoft Docs
ms.custom: ''
ms.date: 06/30/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- publications [SQL Server replication], creating
- articles [SQL Server replication], defining
- adding articles
- articles [SQL Server replication], adding
ms.assetid: 52ee6de9-1d58-4cb9-8711-372bddbe7154
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 87fc7802ea79a73c452f515f72f553850f017bb6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "73882329"
---
# <a name="create-a-publication"></a>Create a Publication
  Este tópico descreve como criar uma publicação no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]ou RMO (Replication Management Objects).  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para criar uma publicação e definir artigos, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO (Replication Management Objects)](#RMOProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   Os nomes de publicação e de artigo não podem incluir nenhum dos seguintes caracteres: % , \* , [ , ] , | , : , " , ? , ', \,/, \< , >. Se os objetos do banco de dados incluírem algum desses caracteres e você desejar replicá-los, será necessário especificar um nome de artigo que seja diferente do nome do objeto na caixa de diálogo **Propriedades do Artigo – \<Artigo>** , disponível na página **Artigos** no assistente.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
 Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for preciso armazenar credenciais, use os serviços [criptográficos](https://go.microsoft.com/fwlink/?LinkId=34733) fornecidos pelo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework do Windows.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Crie publicações e defina artigos com o Assistente para Nova Publicação. Após a criação de uma publicação, exiba e modifique as propriedades da publicação na caixa de diálogo **Propriedades da Publicação – \<Publicação>** . Para obter informações sobre como criar uma publicação de um banco de dados Oracle, consulte [Criar uma publicação de um banco de dados Oracle](create-a-publication-from-an-oracle-database.md).  
  
#### <a name="to-create-a-publication-and-define-articles"></a>Para criar uma publicação e definir artigos  
  
1.  Conecte-se ao Publicador no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] e, em seguida, expanda o nó de servidor.  
  
2.  Expanda a pasta **Replicação** e clique com o botão direito do mouse na pasta **Publicações Locais** .  
  
3.  Clique em **Nova Publicação**.  
  
4.  Siga as páginas no Assistente para Nova Publicação para:  
  
    -   Especificar um Distribuidor se a distribuição não foi configurada no servidor. Para obter mais informações sobre a configuração de distribuição, consulte [Configure Publishing and Distribution](../configure-publishing-and-distribution.md) (Configurar publicação e distribuição).  
  
         Se especificar na página do **Distribuidor** que o servidor do Publicador atuará como o seu próprio Distribuidor (um Distribuidor local) e o servidor não estiver configurado como um Distribuidor, o Assistente para Nova Publicação configurará o servidor. Você especificará uma pasta de instantâneo padrão para o Distribuidor na página **Pasta de Instantâneos** . A pasta de instantâneo é simplesmente um diretório que você designou como um compartilhamento, agentes que leem essa pasta e gravam nela devem ter permissões suficientes para acessá-la. Para obter mais informações sobre como proteger a pasta adequadamente, consulte [Secure the Snapshot Folder](../security/secure-the-snapshot-folder.md) (Proteger a pasta de instantâneo).  
  
         Se você especificar que um outro servidor deverá atuar como um Distribuidor, você deverá inserir uma senha na página **Senha Administrativa** para conexões feitas do Publicador ao Distribuidor. Esta senha deve corresponder à senha especificada quando o Publicador foi habilitado no Distribuidor remoto.  
  
         Para obter mais informações, consulte [Configure Distribution](../configure-distribution.md).  
  
    -   Escolha um banco de dados de publicação.  
  
    -   Selecione um tipo de publicação. Para obter mais informações, consulte [Types of Replication](../types-of-replication.md) (Tipos de replicação).  
  
    -   Especifique os dados e os objetos de banco de dados para serem publicados; opcionalmente filtre as colunas de artigos de tabela e defina as propriedades dos artigos.  
  
    -   Opcionalmente filtre as linhas de artigos de tabela. Para obter mais informações, consulte [Filter Published Data](filter-published-data.md) (Filtrar dados publicados).  
  
    -   Defina a agenda do Snapshot Agent.  
  
    -   Especifique as credenciais sob as quais os agentes de replicação a seguir executam e fazem conexões:  
  
         \- Snapshot Agent para todas as publicações.  
  
         \- O Agente de Leitor de Log para todas as publicações transacionais.  
  
         \- O Queue Reader Agent para as publicações transacionais que permitem atualização de assinaturas.  
  
         Para obter mais informações, consulte [Replication Agent Security Model](../security/replication-agent-security-model.md) e [Replication Security Best Practices](../security/replication-security-best-practices.md).  
  
    -   Opcionalmente faça o script da publicação. Para obter mais informações, consulte [Scripting Replication](../scripting-replication.md).  
  
    -   Especifique um nome para a publicação.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
 Publicações podem ser criadas programaticamente usando procedimentos armazenados de replicação. Os procedimentos armazenados a serem usados dependerão do tipo de publicação a ser criada.  
  
#### <a name="to-create-a-snapshot-or-transactional-publication"></a>Para criar uma publicação de instantâneo ou transacional  
  
1.  No Publicador do banco de dados de publicação, execute [sp_replicationdboption &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql) para habilitar publicação do banco de dados atual usando replicação de instantâneo ou transacional.  
  
2.  Para uma publicação transacional, determine se um existe um trabalho do Log Reader Agent para o banco de dados de publicação. (Essa etapa não é requerida para publicações de instantâneo.)  
  
    -   Se já houver um trabalho do Log Reader Agent para o banco de dados de publicação, passe à etapa 3.  
  
    -   Se você não estiver seguro quanto à existência de um trabalho do Agente do Leitor de Log para um banco de dados publicado, execute [sp_helplogreader_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql) no Publicador do banco de dados de publicação.  
  
    -   Se o conjunto de resultados estiver vazio, crie um trabalho do Log Reader Agent. No Publicador, execute [sp_addlogreader_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql). Especifique as credenciais do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows com as quais o agente é executado em **\@job_name** e **\@password**. Se o agente pretender usar a Autenticação do SQL Server ao se conectar ao Publicador, você também precisará especificar um valor igual a **0** em **\@publisher_security_mode** e as informações de logon do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em **\@publisher_login** e **\@publisher_password**. Passe para a etapa 3.  
  
3.  No Publicador, execute [sp_addpublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql). Especifique um nome de publicação para ** \@publicação**e, para o ** \@parâmetro repl_freq** , especifique um valor de `snapshot` para uma publicação de instantâneo ou um valor `continuous` de para uma publicação transacional. Especifique quaisquer outras opções de publicação. Isso define a publicação.  
  
    > [!NOTE]  
    >  Os nomes de publicação não podem incluir nenhum dos caracteres a seguir:  
    >   
    >  % * [ ] | : " ? \ / \< >  
  
4.  No Publicador, execute [sp_addpublication_snapshot &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql). Especifique o nome da publicação usado na etapa 3 em **\@publication** e as credenciais do Windows com as quais o Agente de Instantâneo é executado em **\@snapshot_job_name** e **\@password**. Se o agente pretender usar a Autenticação do SQL Server ao se conectar ao Publicador, você também precisará especificar um valor igual a **0** em **\@publisher_security_mode** e as informações de logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em **\@publisher_login** e **\@publisher_password**. Isso cria um trabalho do Agente de Instantâneo para a publicação.  
  
    > [!IMPORTANT]  
    >  Quando um Publicador é configurado com um Distribuidor remoto, os valores fornecidos para todos os parâmetros, inclusive *job_login* e *job_password*, são enviados ao Distribuidor como texto sem-formatação. Você deve criptografar a conexão entre o Publicador e seu Distribuidor remoto antes de executar esse procedimento armazenado. Para obter mais informações, veja [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
5.  Adicione artigos à publicação. Para obter mais informações, consulte [Define an Article](define-an-article.md).  
  
6.  Inicie o trabalho do Agente de Instantâneo para gerar o instantâneo inicial para essa publicação. Para obter mais informações, consulte [Criar e aplicar o instantâneo inicial](../create-and-apply-the-initial-snapshot.md).  
  
#### <a name="to-create-a-merge-publication"></a>Para criar uma publicação de mesclagem  
  
1.  No Publicador, execute [sp_replicationdboption &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql) para habilitar a publicação do banco de dados atual usando a replicação de mesclagem.  
  
2.  No Publicador do banco de dados de publicação, execute [sp_addmergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql). Especifique o nome da publicação em **\@publication** e as outras opções de publicação. Isso define a publicação.  
  
    > [!NOTE]  
    >  Os nomes de publicação não podem incluir nenhum dos caracteres a seguir:  
    >   
    >  % * [ ] | : " ? \ / \< >  
  
3.  No Publicador, execute [sp_addpublication_snapshot &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql). Especifique o nome da publicação usado na etapa 2 em **\@publication** e as credenciais do Windows com as quais o Agente de Instantâneo é executado em **\@snapshot_job_name** e **\@password**. Se o agente pretender usar a Autenticação do SQL Server ao se conectar ao Publicador, você também precisará especificar um valor igual a **0** em **\@publisher_security_mode** e as informações de logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em **\@publisher_login** e **\@publisher_password**. Isso cria um trabalho do Agente de Instantâneo para a publicação.  
  
    > [!IMPORTANT]  
    >  Quando um Publicador é configurado com um Distribuidor remoto, os valores fornecidos para todos os parâmetros, inclusive *job_login* e *job_password*, são enviados ao Distribuidor como texto sem-formatação. Você deve criptografar a conexão entre o Publicador e seu Distribuidor remoto antes de executar esse procedimento armazenado. Para obter mais informações, veja [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
4.  Adicione artigos à publicação. Para obter mais informações, consulte [Define an Article](define-an-article.md).  
  
5.  Inicie o trabalho do Agente de Instantâneo para gerar o instantâneo inicial para essa publicação. Para obter mais informações, consulte [Criar e aplicar o instantâneo inicial](../create-and-apply-the-initial-snapshot.md).  
  
###  <a name="example-transact-sql"></a><a name="TsqlExample"></a> Exemplo (Transact-SQL)  
 Este exemplo cria uma publicação transacional. As variáveis de script são usadas para passar as credenciais do Windows necessárias para criar trabalhos do Agente de Instantâneo e do Agente de Leitor de Log.  
  
 [!code-sql[HowTo#sp_AddTranPub](../../../snippets/tsql/SQL15/replication/howto/tsql/createtranpub.sql#sp_addtranpub)]  
  
 Este exemplo cria uma publicação de mesclagem. As variáveis de script são usadas para passar as credenciais do Windows necessárias para criar o trabalho do Agente de Instantâneo.  
  
 [!code-sql[HowTo#sp_AddMergePub](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepub.sql#sp_addmergepub)]  
  
##  <a name="using-replication-management-objects-rmo"></a><a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
 Crie publicações de forma programada, usando o RMO (Replication Management Objects). As classes de RMO usadas para criar uma publicação dependem do tipo de publicação criada.  
  
#### <a name="to-create-a-snapshot-or-transactional-publication"></a>Para criar uma publicação de instantâneo ou transacional  
  
1.  Crie uma conexão com o Publicador usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> para o banco de dados de publicação; defina a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> para a instância de <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da etapa 1 e chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> . Se <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> retornar `false`, verifique se o banco de dados existe.  
  
3.  Se a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledTransPublishing%2A> for `false`, defina-a como `true`.  
  
4.  Para uma publicação transacional, verifique o valor da <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentExists%2A> propriedade. Se essa propriedade for `true`, um trabalho do Log Reader Agent já existirá para esse banco de dados. Se essa propriedade for `false`, faça o seguinte:  
  
    -   Defina os campos <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> e <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> ou <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.SecurePassword%2A> de <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentProcessSecurity%2A> para fornecer as credenciais da conta do Windows do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] na qual o Log Reader Agent é executado.  
  
        > [!NOTE]  
        >  Não é necessário definir <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentProcessSecurity%2A> quando a publicação é criada por um membro da função de servidor fixa `sysadmin`. Nesse caso, o agente representará a conta do SQL Server Agent. Para obter mais informações, consulte [Replication Agent Security Model](../security/replication-agent-security-model.md).  
  
    -   (Opcional) Defina os campos <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> e <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> ou <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> de <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentPublisherSecurity%2A> ao usar a Autenticação do SQL Server para conexão com o Publicador.  
  
    -   Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.CreateLogReaderAgent%2A> para criar o trabalho do Log Reader Agent para o banco de dados.  
  
5.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.TransPublication> e defina as propriedades a seguir para esse objeto:  
  
    -   O <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da Etapa 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
    -   Nome do banco de dados publicado para <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>.  
  
    -   Um nome para a publicação para <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>.  
  
    -   Um <xref:Microsoft.SqlServer.Replication.PublicationType> de ambos <xref:Microsoft.SqlServer.Replication.PublicationType.Transactional> ou <xref:Microsoft.SqlServer.Replication.PublicationType.Snapshot>.  
  
    -   Os campos <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> e <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> de <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> para fornecer as credenciais para a conta do Windows em que o Snapshot Agent é executado. Essa conta é também usada quando o Snapshot Agent faz conexões com o Distributor local e para conexões remotas quando se usa a Autenticação do Windows.  
  
        > [!NOTE]  
        >  Não é necessário definir <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> quando a publicação é criada por um membro da função de servidor fixa `sysadmin`. Nesse caso, o agente representará a conta do SQL Server Agent. Para obter mais informações, consulte [Replication Agent Security Model](../security/replication-agent-security-model.md).  
  
    -   (Opcional) Os campos <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> e <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> ou <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> de <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentPublisherSecurity%2A> ao usar a Autenticação do SQL Server para conexão com o Publicador.  
  
    -   (Opcional) Use o operador OR de lógica inclusiva (`|` no Visual C# e `Or` no Visual Basic) e o operador OR de lógica exclusiva (`^` no Visual C# e `Xor` no Visual Basic) para definir os valores <xref:Microsoft.SqlServer.Replication.PublicationAttributes> da propriedade <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A>.  
  
    -   (Opcional) O nome do Publicador para <xref:Microsoft.SqlServer.Replication.TransPublication.PublisherName%2A> quando o Publicador é não SQL Server.  
  
6.  Chame o método <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> para criar a publicação.  
  
    > [!IMPORTANT]  
    >  Quando um Publicador é configurado com um Distribuidor remoto, os valores fornecidos para todas as propriedades, inclusive <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A>, são enviados ao Distribuidor como texto sem-formatação. É necessário criptografar a conexão entre o Publicador e o respectivo Distribuidor remoto antes de chamar o método <xref:Microsoft.SqlServer.Replication.Publication.Create%2A>. Para obter mais informações, veja [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
7.  Chame o método <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> para criar o trabalho do Agente de Instantâneo para a publicação.  
  
#### <a name="to-create-a-merge-publication"></a>Para criar uma publicação de mesclagem  
  
1.  Crie uma conexão com o Publicador usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> para o banco de dados de publicação; defina a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> para a instância de <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da etapa 1 e chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> . Se <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> retornar `false`, verifique se o banco de dados existe.  
  
3.  Se <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledMergePublishing%2A> a propriedade `false`for, defina- `true`a como e <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A>chame.  
  
4.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.MergePublication> e defina as propriedades a seguir para esse objeto:  
  
    -   O <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da Etapa 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
    -   Nome do banco de dados publicado para <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>.  
  
    -   Um nome para a publicação para <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>.  
  
    -   Os campos <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> e <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> de <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> para fornecer as credenciais para a conta do Windows em que o Snapshot Agent é executado. Essa conta é também usada quando o Snapshot Agent faz conexões com o Distributor local e para conexões remotas quando se usa a Autenticação do Windows.  
  
        > [!NOTE]  
        >  Não é necessário definir <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> quando a publicação é criada por um membro da função de servidor fixa `sysadmin`. Para obter mais informações, consulte [Replication Agent Security Model](../security/replication-agent-security-model.md).  
  
    -   (Opcional) Use o operador OR de lógica inclusiva (`|` no Visual C# e `Or` no Visual Basic) e o operador OR de lógica exclusiva (`^` no Visual C# e `Xor` no Visual Basic) para definir os valores <xref:Microsoft.SqlServer.Replication.PublicationAttributes> da propriedade <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A>.  
  
5.  Chame o método <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> para criar a publicação.  
  
    > [!IMPORTANT]  
    >  Quando um Publicador é configurado com um Distribuidor remoto, os valores fornecidos para todas as propriedades, inclusive <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A>, são enviados ao Distribuidor como texto sem-formatação. É necessário criptografar a conexão entre o Publicador e o respectivo Distribuidor remoto antes de chamar o método <xref:Microsoft.SqlServer.Replication.Publication.Create%2A>. Para obter mais informações, veja [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
6.  Chame o método <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> para criar o trabalho do Agente de Instantâneo para a publicação.  
  
###  <a name="examples-rmo"></a><a name="PShellExample"></a> Exemplos (RMO)  
 Esse exemplo ativa o banco de dados AdventureWorks para publicação transacional; define um trabalho do Agente de Leitor de Log e cria a publicação AdvWorksProductTran. É preciso definir um artigo para essa publicação. As credenciais da conta do Windows necessárias para criar o trabalho do Log Reader Agent e o do Snapshot Agent são passadas em runtime. Para saber como usar RMO para definir artigos instantâneos e transacionais, consulte [Define an Article](define-an-article.md).  
  
 [!code-csharp[HowTo#rmo_CreateTranPub](../../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createtranpub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateTranPub](../../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createtranpub)]  
  
 Esse exemplo ativa o banco de dados AdventureWorks para publicação de mesclagem e cria a publicação AdvWorksSalesOrdersMerge. Artigos ainda precisam ser definidos para essa publicação. As credenciais da conta do Windows, necessárias para criar o trabalho do Agente de Instantâneo, são passadas em runtime. Para saber como usar RMO para definir artigos de mesclagem, consulte [Define an Article](define-an-article.md).  
  
 [!code-csharp[HowTo#rmo_CreateMergePub](../../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createmergepub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePub](../../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createmergepub)]  
  
## <a name="see-also"></a>Consulte Também  
 [Usar sqlcmd com variáveis de script](../../scripting/sqlcmd-use-with-scripting-variables.md)   
 [Publicar dados e objetos de banco de dados](publish-data-and-database-objects.md)   
 [Replication Management Objects Concepts](../concepts/replication-management-objects-concepts.md)   
 [Define an Article](define-an-article.md)   
 [Exibir e modificar as propriedades da publicação](view-and-modify-publication-properties.md)   
 [Configurar Distribuição](../configure-distribution.md)   
 [Proteger o Distribuidor](../security/secure-the-distributor.md)   
 [Proteger o Publicador](../security/secure-the-publisher.md)  
  
  
