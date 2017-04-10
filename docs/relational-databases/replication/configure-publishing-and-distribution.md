---
title: "Configurar a publica&#231;&#227;o e a distribui&#231;&#227;o | Microsoft Docs"
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
  - "replicação [SQL Server], distribuição"
  - "distribution configuration [SQL Server replication]"
  - "publicação [replicação do SQL Server], configurando"
ms.assetid: 3cfc8966-833e-42fa-80cb-09175d1feed7
caps.latest.revision: 42
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 42
---
# Configurar a publica&#231;&#227;o e a distribui&#231;&#227;o
  Este tópico descreve como configurar publicação e distribuição no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] ou RMO (Replication Management Objects).  
  

##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
 Para obter mais informações, consulte [Implantação segura e &#40;Replicação&#41;](../../relational-databases/replication/security/secure-deployment-replication.md).  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Configure a distribuição, usando o Assistente para Novas Publicações ou o Assistente para Configurar a Distribuição. Depois que o Distribuidor estiver configurado, exiba e modifique as propriedades na caixa de diálogo **Propriedades do Distribuidor – \<Distribuidor>**. Use o Assistente para Configurar Distribuição se você desejar configurar um Distribuidor para que os membros de funções de banco de dados fixas **db_owner** possam criar publicações ou para configurar um Distribuidor remoto que não é um Editor.  
  
#### Para configurar a distribuição  
  
1.  No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se ao servidor que será o Distribuidor (em muitos casos, o Editor e o Distribuidor são o mesmo servidor) e, então, expanda o nó do servidor.  
  
2.  Clique com o botão direito do mouse na pasta **Replicação** e clique em **Configurar Distribuição**.  
  
3.  Siga o Assistente para Configurar Distribuição para:  
  
    -   Selecionar um Distribuidor. Para usar um distribuidor local, selecionar **'\<ServerName>' atuará como seu próprio Distribuidor; o SQL Server criará um banco de dados de distribuição e um log**. Para usar um Distribuidor remoto, selecione **Use o seguinte servidor como Distribuidor**e, em seguida, selecione um servidor. O servidor já deve ser configurado como um Distribuidor e o Publicador deve ser habilitado a usar o Distribuidor. Para obter mais informações, consulte [Habilitar um Publicador Remoto em um Distribuidor &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/enable-a-remote-publisher-at-a-distributor-sql-server-management-studio.md).  
  
         Se você selecionar um Distribuidor remoto, você deverá inserir uma senha na página **Senha Administrativa** para conexões feitas do Publicador ao Distribuidor. Esta senha deve corresponder à senha especificada quando o Publicador foi habilitado no Distribuidor remoto.  
  
    -   Especifique uma pasta de instantâneo de raiz (para um Distribuidor local). A pasta de instantâneo é simplesmente um diretório que você designou como um compartilhamento, agentes que leem essa pasta e gravam nela devem ter permissões suficientes para acessá-la. Cada Publicador que usa esse Distribuidor cria uma pasta na pasta raiz, e cada publicação cria pastas na pasta Publicador em que armazenará arquivos de instantâneos. Para obter mais informações sobre como proteger a pasta adequadamente, consulte [Proteger a Pasta de Instantâneos](../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
    -   Especifique o banco de dados de distribuição (para um Distribuidor local). O banco de dados de distribuição armazena metadados e dados de histórico para todos os tipos de replicação e transações para replicação transacional.  
  
    -   Além disso, permite que outros Publicadores usem o Distribuidor. Se outros Publicadores estiverem habilitados para usar o Distribuidor, você deverá inserir uma senha na página **Senha do Distribuidor** para conexões feitas desses Publicadores para os Distribuidores.  
  
    -   Além disso, faça o script das definições de configuração. Para obter mais informações, consulte [Scripting Replication](../../relational-databases/replication/scripting-replication.md).  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 Publicação e distribuição de replicação podem ser configuradas de forma programada, usando-se procedimentos de replicação armazenados.  
  
#### Para configurar publicação usando um distribuidor local  
  
1.  Execute [sp_get_distributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-get-distributor-transact-sql.md) para determinar se o servidor já está configurado como um Distribuidor.  
  
    -   Se o valor **installed** no resultado definido for **0**, execute [sp_adddistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md) no Distribuidor no banco de dados mestre.  
  
    -   Se o valor **bd de distribuição instalado** no resultado definido for **0**, execute [sp_adddistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md) no Distribuidor no banco de dados mestre. Especifique o nome do banco de dados de distribuição para **@database**. Opcionalmente, você pode especificar o período máximo de retenção transacional para **@max_distretention** e o período de retenção de histórico para **@history_retention**. Se um banco de dados novo estiver sendo criado, especifique os parâmetros de propriedade de banco de dados desejados.  
  
2.  No Distribuidor, que também é o Editor, execute [sp_adddistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md), especificando o compartilhamento UNC que será usado como pasta padrão de instantâneo para **@working_directory**.  
  
3.  No Editor, execute [sp_replicationdboption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md). Especifique o banco de dados sendo publicado para **@dbname**, o tipo de replicação para **@optname**, e o valor **true** para **@value**.  
  
#### Para configurar publicação usando um distribuidor remoto  
  
1.  Execute [sp_get_distributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-get-distributor-transact-sql.md) para determinar se o servidor já está configurado como um Distribuidor.  
  
    -   Se o valor **installed** no resultado definido for **0**, execute [sp_adddistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md) no Distribuidor no banco de dados mestre. Especifique uma senha forte para **@password**. Essa senha para a conta **distributor_admin** será usada pelo Publicador ao se conectar ao Editor.  
  
    -   Se o valor **bd de distribuição instalado** no resultado definido for **0**, execute [sp_adddistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md) no Distribuidor no banco de dados mestre. Especifique o nome do banco de dados de distribuição para **@database**. Opcionalmente, você pode especificar o período máximo de retenção transacional para **@max_distretention** e o período de retenção de histórico para **@history_retention**. Se um banco de dados novo estiver sendo criado, especifique os parâmetros de propriedade de banco de dados desejados.  
  
2.  No Distribuidor, execute [sp_adddistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md), especificando o compartilhamento UNC que será usado como pasta padrão de instantâneo para **@working_directory**. Se o Distribuidor usar a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao se conectar ao Editor, você também deverá especificar um valor de **0** para **@security_mode** e as informações de logon do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para **@login** e **@password**.  
  
3.  No Editor do banco de dados mestre, execute [sp_adddistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md). Especifique a senha forte usada na etapa 1 para **@password**. Essa senha será usada pelo Publicador ao se conectar ao Distribuidor.  
  
4.  No Editor, execute [sp_replicationdboption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md). Especifique o banco de dados que está sendo publicado para **@dbname**, o tipo de replicação para **@optname**, e o valor de verdadeiro para **@value**.  
  
###  <a name="TsqlExample"></a> Exemplo (Transact-SQL)  
 O exemplo a seguir mostra como configurar publicação e distribuição programaticamente. Nesse exemplo, o nome do servidor que está sendo configurado como publicador e um distribuidor local são fornecidos usando variáveis de script. Publicação e distribuição de replicação podem ser configuradas de forma programada, usando-se procedimentos de replicação armazenados.  
  
 [!code-sql[HowTo#AddDistPub](../../relational-databases/replication/codesnippet/tsql/configure-publishing-and_1.sql)]  
  
##  <a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
  
#### Para configurar a publicação e a distribuição em um único servidor  
  
1.  Crie uma conexão com o servidor usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection>.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.ReplicationServer> classe. Passe o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da etapa 1.  
  
3.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.DistributionDatabase> classe.  
  
4.  Definir o <xref:Microsoft.SqlServer.Replication.DistributionDatabase.Name%2A> propriedade como o nome do banco de dados e defina o <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propriedade para o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da etapa 1.  
  
5.  Instale o distribuidor chamando o <xref:Microsoft.SqlServer.Replication.ReplicationServer.InstallDistributor%2A> método. Passar o <xref:Microsoft.SqlServer.Replication.DistributionDatabase> objeto da etapa 3.  
  
6.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.DistributionPublisher> classe.  
  
7.  Defina as seguintes propriedades de <xref:Microsoft.SqlServer.Replication.DistributionPublisher>:  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Name%2A> - nome do publicador.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> - o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da etapa 1.  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.DistributionDatabase%2A> -o nome do banco de dados criado na etapa 5.  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.WorkingDirectory%2A> -compartilhamento usado para acessar os arquivos de instantâneo.  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.PublisherSecurity%2A> -o modo de segurança usado ao conectar-se ao publicador. <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> é recomendado.  
  
8.  Chamar o <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Create%2A> método.  
  
#### Para configurar a publicação e a distribuição usando um Distribuidor remoto  
  
1.  Crie uma conexão com o servidor do Distribuidor remoto usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection>.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.ReplicationServer> classe. Passe o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da etapa 1.  
  
3.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.DistributionDatabase> classe.  
  
4.  Definir o <xref:Microsoft.SqlServer.Replication.DistributionDatabase.Name%2A> propriedade para o nome do banco de dados e o conjunto de <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propriedade para o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da etapa 1.  
  
5.  Instale o distribuidor chamando o <xref:Microsoft.SqlServer.Replication.ReplicationServer.InstallDistributor%2A> método. Especifique uma senha segura (usada pelo publicador ao conectar-se ao distribuidor remoto) e o <xref:Microsoft.SqlServer.Replication.DistributionDatabase> objeto da etapa 3. Para obter mais informações, consulte [Proteger o Distribuidor](../../relational-databases/replication/security/secure-the-distributor.md).  
  
    > **IMPORTANTE:** Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for preciso armazenar credenciais, use os serviços [criptográficos](http://go.microsoft.com/fwlink/?LinkId=34733) fornecidos pelo [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework do Windows.  
  
6.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.DistributionPublisher> classe.  
  
7.  Defina as seguintes propriedades de <xref:Microsoft.SqlServer.Replication.DistributionPublisher>:  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Name%2A> - nome do servidor do publicador local.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> - o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da etapa 1.  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.DistributionDatabase%2A> -o nome do banco de dados criado na etapa 5.  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.WorkingDirectory%2A> -compartilhamento usado para acessar os arquivos de instantâneo.  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.PublisherSecurity%2A> -o modo de segurança usado ao conectar-se ao publicador. <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> é recomendado.  
  
8.  Chamar o <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Create%2A> método.  
  
9. Crie uma conexão com o servidor do Editor local usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection>.  
  
10. Criar uma instância do <xref:Microsoft.SqlServer.Replication.ReplicationServer> classe. Passe o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da etapa 9.  
  
11. Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationServer.InstallDistributor%2A> método. Passe o nome do Distribuidor remoto e a senha para o Distribuidor remoto especificados na etapa 5.  
  
    > **IMPORTANTE:**  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for preciso armazenar credenciais, use os [serviços criptográficos](http://go.microsoft.com/fwlink/?LinkId=34733) fornecidos pelo Windows .NET Framework.  
  
###  <a name="PShellExample"></a> Exemplo (RMO)  
 Você pode configurar a replicação da publicação e da distribuição de forma programada usando o RMO (Replication Management Objects).  
  
 [!code-csharp[HowTo#rmo_AddDistPub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_adddistpub)]  
  
 [!code-vb[HowTo#rmo_vb_AddDistPub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_adddistpub)]  
  
## Consulte também  
 [View and Modify Distributor and Publisher Properties](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [Conceitos dos procedimentos armazenados do sistema de replicação](../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Configurar a distribuição](../../relational-databases/replication/configure-distribution.md)   
 [Conceitos de Replication Management Objects](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [Configurar a replicação para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/configure-replication-for-always-on-availability-groups-sql-server.md)  
  
  