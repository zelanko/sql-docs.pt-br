---
title: "Configurar publicação e distribuição | Microsoft Docs"
ms.custom: 
ms.date: 08/25/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- replication [SQL Server], distribution
- distribution configuration [SQL Server replication]
- publishing [SQL Server replication], configuring
ms.assetid: 3cfc8966-833e-42fa-80cb-09175d1feed7
caps.latest.revision: 42
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: bd4ea4d94bb9986127e4d5ffd2b8801f73528b93
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="configure-publishing-and-distribution"></a>Configurar a publicação e a distribuição
  Este tópico descreve como configurar publicação e distribuição no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]ou RMO (Replication Management Objects).  
  

##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
 Para obter mais informações, consulte [Implantação segura e &#40;Replicação&#41;](../../relational-databases/replication/security/secure-deployment-replication.md).  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Configure a distribuição, usando o Assistente para Novas Publicações ou o Assistente para Configurar a Distribuição. Depois que o Distribuidor estiver configurado, exiba e modifique as propriedades na caixa de diálogo **Propriedades do Distribuidor – \<Distribuidor>**. Use o Assistente para Configurar Distribuição se você desejar configurar um Distribuidor para que os membros de funções de banco de dados fixas **db_owner** possam criar publicações ou para configurar um Distribuidor remoto que não é um Publicador.  
  
#### <a name="to-configure-distribution"></a>Para configurar a distribuição  
  
1.  No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se ao servidor que será o Distribuidor (em muitos casos, o Publicador e o Distribuidor são o mesmo servidor) e, então, expanda o nó do servidor.  
  
2.  Clique com o botão direito na pasta **Replicação** e clique em **Configurar Distribuição**.  
  
3.  Siga o Assistente para Configurar Distribuição para:  
  
    -   Selecionar um Distribuidor. Para usar um Distribuidor local, selecione **'\<ServerName>' atuará como seu próprio Distribuidor; o SQL Server criará um banco de dados de distribuição e um log**. Para usar um Distribuidor remoto, selecione **Use o seguinte servidor como Distribuidor**e, em seguida, selecione um servidor. O servidor já deve ser configurado como um Distribuidor e o Publicador deve ser habilitado a usar o Distribuidor. Para obter mais informações, consulte [Habilitar um Publicador Remoto em um Distribuidor &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/enable-a-remote-publisher-at-a-distributor-sql-server-management-studio.md).  
  
         Se você selecionar um Distribuidor remoto, você deverá inserir uma senha na página **Senha Administrativa** para conexões feitas do Publicador ao Distribuidor. Esta senha deve corresponder à senha especificada quando o Publicador foi habilitado no Distribuidor remoto.  
  
    -   Especifique uma pasta de instantâneo de raiz (para um Distribuidor local). A pasta de instantâneo é simplesmente um diretório que você designou como um compartilhamento, agentes que leem essa pasta e gravam nela devem ter permissões suficientes para acessá-la. Cada Publicador que usa esse Distribuidor cria uma pasta na pasta raiz, e cada publicação cria pastas na pasta Publicador em que armazenará arquivos de instantâneos. Para obter mais informações sobre como proteger a pasta adequadamente, consulte [Proteger a Pasta de Instantâneos](../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
    -   Especifique o banco de dados de distribuição (para um Distribuidor local). O banco de dados de distribuição armazena metadados e dados de histórico para todos os tipos de replicação e transações para replicação transacional.  
  
    -   Além disso, permite que outros Publicadores usem o Distribuidor. Se outros Publicadores estiverem habilitados para usar o Distribuidor, você deverá inserir uma senha na página **Senha do Distribuidor** para conexões feitas desses Publicadores para os Distribuidores.  
  
    -   Além disso, faça o script das definições de configuração. Para obter mais informações, consulte [Scripting Replication](../../relational-databases/replication/scripting-replication.md).  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 Publicação e distribuição de replicação podem ser configuradas de forma programada, usando-se procedimentos de replicação armazenados.  
  
#### <a name="to-configure-publishing-using-a-local-distributor"></a>Para configurar publicação usando um distribuidor local  
  
1.  Execute [sp_get_distributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-get-distributor-transact-sql.md) para determinar se o servidor já está configurado como um Distribuidor.  
  
    -   Se o valor **installed** no resultado definido for **0**, execute [sp_adddistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md) no Distribuidor no banco de dados mestre.  
  
    -   Se o valor **bd de distribuição instalado** no resultado definido for **0**, execute [sp_adddistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md) no Distribuidor no banco de dados mestre. Especifique o nome do banco de dados de distribuição para **@database**. Opcionalmente, você pode especificar o período máximo de retenção transacional para **@max_distretention** e o período de retenção de histórico para **@history_retention**. Se um banco de dados novo estiver sendo criado, especifique os parâmetros de propriedade de banco de dados desejados.  
  
2.  No Distribuidor, que também é o Publicador, execute [sp_adddistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md), especificando o compartilhamento UNC que será usado como pasta de instantâneo padrão para **@working_directory**.  
  
3.  No Editor, execute [sp_replicationdboption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md). Especifique o banco de dados que está sendo publicado para **@dbname**, o tipo de replicação para **@optname**e o valor **true** para **@value**.  
  
#### <a name="to-configure-publishing-using-a-remote-distributor"></a>Para configurar publicação usando um distribuidor remoto  
  
1.  Execute [sp_get_distributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-get-distributor-transact-sql.md) para determinar se o servidor já está configurado como um Distribuidor.  
  
    -   Se o valor **installed** no resultado definido for **0**, execute [sp_adddistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md) no Distribuidor no banco de dados mestre. Especifique uma senha forte para **@password**. Essa senha para a conta **distributor_admin** será usada pelo Publicador ao se conectar ao Distribuidor.  
  
    -   Se o valor **bd de distribuição instalado** no resultado definido for **0**, execute [sp_adddistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md) no Distribuidor no banco de dados mestre. Especifique o nome do banco de dados de distribuição para **@database**. Opcionalmente, você pode especificar o período máximo de retenção transacional para **@max_distretention** e o período de retenção de histórico para **@history_retention**. Se um banco de dados novo estiver sendo criado, especifique os parâmetros de propriedade de banco de dados desejados.  
  
2.  No Distribuidor, execute [sp_adddistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md), especificando o compartilhamento UNC que será usado como pasta de instantâneo padrão para **@working_directory**. Se o Distribuidor usar a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao se conectar ao Publicador, você também deverá especificar um valor de **0** para **@security_mode** e as informações de logon do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para **@login** e **@password**.  
  
3.  No Editor do banco de dados mestre, execute [sp_adddistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md). Especifique a senha forte usada na etapa 1 para **@password**. Essa senha será usada pelo Publicador ao se conectar ao Distribuidor.  
  
4.  No Editor, execute [sp_replicationdboption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md). Especifique o banco de dados que está sendo publicado para **@dbname**, o tipo de replicação para **@optname**, e o valor de verdadeiro para **@value**.  
  
###  <a name="TsqlExample"></a> Exemplo (Transact-SQL)  
 O exemplo a seguir mostra como configurar publicação e distribuição programaticamente. Nesse exemplo, o nome do servidor que está sendo configurado como publicador e um distribuidor local são fornecidos usando variáveis de script. Publicação e distribuição de replicação podem ser configuradas de forma programada, usando-se procedimentos de replicação armazenados.  
  
 [!code-sql[HowTo#AddDistPub](../../relational-databases/replication/codesnippet/tsql/configure-publishing-and_1.sql)]  
  
##  <a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
  
#### <a name="to-configure-publishing-and-distribution-on-a-single-server"></a>Para configurar a publicação e a distribuição em um único servidor  
  
1.  Crie uma conexão com o servidor usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection>.  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.ReplicationServer>. Passe o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da etapa 1.  
  
3.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.DistributionDatabase>.  
  
4.  Defina a propriedade <xref:Microsoft.SqlServer.Replication.DistributionDatabase.Name%2A> como o nome do banco de dados e defina a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> como <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da etapa 1.  
  
5.  Instale o Distribuidor chamando o método <xref:Microsoft.SqlServer.Replication.ReplicationServer.InstallDistributor%2A>. Passe o objeto <xref:Microsoft.SqlServer.Replication.DistributionDatabase> da etapa 3.  
  
6.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.DistributionPublisher>.  
  
7.  Defina as seguintes propriedades de <xref:Microsoft.SqlServer.Replication.DistributionPublisher>:  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Name%2A> – nome do Publicador.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> – a <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da etapa 1.  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.DistributionDatabase%2A> – o nome do banco de dados criado na etapa 5.  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.WorkingDirectory%2A> – o compartilhamento usado para acessar os arquivos de instantâneo.  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.PublisherSecurity%2A> – o modo de segurança usado ao se conectar ao Publicador. Recomenda-se <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A>.  
  
8.  Chame o método <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Create%2A>.  
  
#### <a name="to-configure-publishing-and-distribution-using-a-remote-distributor"></a>Para configurar a publicação e a distribuição usando um Distribuidor remoto  
  
1.  Crie uma conexão com o servidor do Distribuidor remoto usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection>.  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.ReplicationServer>. Passe o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da etapa 1.  
  
3.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.DistributionDatabase>.  
  
4.  Defina a propriedade <xref:Microsoft.SqlServer.Replication.DistributionDatabase.Name%2A> como o nome do banco de dados e defina a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> como <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da etapa 1.  
  
5.  Instale o Distribuidor chamando o método <xref:Microsoft.SqlServer.Replication.ReplicationServer.InstallDistributor%2A>. Especifique uma senha segura (usada pelo Publicador ao se conectar ao Distribuir remoto) e o objeto <xref:Microsoft.SqlServer.Replication.DistributionDatabase> da etapa 3. Para obter mais informações, consulte [Proteger o Distribuidor](../../relational-databases/replication/security/secure-the-distributor.md).  
  
    > **IMPORTANTE:** Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for preciso armazenar credenciais, use os serviços [criptográficos](http://go.microsoft.com/fwlink/?LinkId=34733) fornecidos pelo [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework do Windows.  
  
6.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.DistributionPublisher>.  
  
7.  Defina as seguintes propriedades de <xref:Microsoft.SqlServer.Replication.DistributionPublisher>:  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Name%2A> – nome do servidor do Publicador local.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> – a <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da etapa 1.  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.DistributionDatabase%2A> – o nome do banco de dados criado na etapa 5.  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.WorkingDirectory%2A> – o compartilhamento usado para acessar os arquivos de instantâneo.  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.PublisherSecurity%2A> – o modo de segurança usado ao se conectar ao Publicador. Recomenda-se <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A>.  
  
8.  Chame o método <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Create%2A>.  
  
9. Crie uma conexão com o servidor do Publicador local usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection>.  
  
10. Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.ReplicationServer>. Passe o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da etapa 9.  
  
11. Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationServer.InstallDistributor%2A>. Passe o nome do Distribuidor remoto e a senha para o Distribuidor remoto especificados na etapa 5.  
  
    > **IMPORTANTE:**  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for preciso armazenar credenciais, use os [serviços criptográficos](http://go.microsoft.com/fwlink/?LinkId=34733) fornecidos pelo Windows .NET Framework.  
  
###  <a name="PShellExample"></a> Exemplo (RMO)  
 Você pode configurar a replicação da publicação e da distribuição de forma programada usando o RMO (Replication Management Objects).  
  
 [!code-cs[HowTo#rmo_AddDistPub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_adddistpub)]  
  
 [!code-vb[HowTo#rmo_vb_AddDistPub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_adddistpub)]  
  
## <a name="see-also"></a>Consulte também  
 [Exibir e modificar propriedades de Publicador e Distribuidor](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [Replication System Stored Procedures Concepts](../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Configurar Distribuição](../../relational-databases/replication/configure-distribution.md)   
 [Replication Management Objects Concepts](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [Configurar a replicação para grupos de disponibilidade Sempre Ativo &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/configure-replication-for-always-on-availability-groups-sql-server.md)  
  
  

