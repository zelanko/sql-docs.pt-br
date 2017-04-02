---
title: "Exibir e modificar propriedades de Publicador e Distribuidor | Microsoft Docs"
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
  - "viewing replication properties"
  - "Distributors [SQL Server replication], modifying"
  - "modifying replication properties, Distributors"
  - "Distribuidores [replicação do SQL Server], propriedades"
ms.assetid: 5dae1d59-c377-4c6e-adc9-b68c5b328f79
caps.latest.revision: 43
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 43
---
# Exibir e modificar propriedades de Publicador e Distribuidor
  Este tópico descreve como exibir e modificar propriedades do Distribuidor e do Publicador no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)], ou RMO (Replication Management Objects).  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para exibir e modificar as propriedades do Distribuidor e do Publicador, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO (Replication Management Objects)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Nas versões de Publicadores anteriores ao [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], um usuário na função de servidor fixa **sysadmin** pode registrar Assinantes na página **Assinantes** . A partir do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], não é mais necessário registrar Assinantes explicitamente para replicação.  
  
###  <a name="Security"></a> Segurança  
 Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### Para exibir e modificar as propriedades do Distribuidor  
  
1.  Conecte-se ao Distribuidor no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e, em seguida, expanda o nó de servidor.  
  
2.  Clique com botão direito do **replicação** pasta e clique **Propriedades do distribuidor**.  
  
3.  Exibir e modificar propriedades de **Propriedades do distribuidor - \< distribuidor>** caixa de diálogo.  
  
    -   Para exibir e modificar as propriedades de um banco de dados de distribuição, clique no botão Propriedades (**...**) para o banco de dados de **geral** página da caixa de temesses.  
  
    -   Para exibir e modificar propriedades do publicador associadas ao distribuidor, clique no botão Propriedades (**...**) para o publicador de **editores** página da caixa de diálogo.  
  
    -   Para acessar os perfis para os agentes de replicação, clique no botão **Padrões de Perfil** na página **Geral** da caixa de diálogo. Para obter mais informações, consulte [Replication Agent Profiles](../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
    -   Para alterar a senha da conta usada quando os procedimentos administrativos armazenados são executados no Publicador e para atualizar as informações no Distribuidor, digite uma senha nova nas caixas **Senha** e **Confirmar senha** na página **Publicadores** da caixa de diálogo. Para obter mais informações, consulte [proteger o distribuidor](../../relational-databases/replication/security/secure-the-distributor.md).  
  
4.  Modifique propriedades, se necessário, depois clique em **OK**.  
  
#### Para exibir e modificar as propriedades do Publicador  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e expanda o nó do servidor.  
  
2.  Clique com botão direito do **replicação** pasta e clique **Propriedades do publicador**.  
  
3.  Exibir e modificar propriedades de **Propriedades do publicador - \< publicador >** caixa de diálogo.  
  
    -   Um usuário na função de servidor fixa **sysadmin** pode ativar bancos de dados para replicação na página **Bancos de Dados de Publicação** . Habilitar um banco de dados não publica esse banco de dados; em vez disso, ele permite que qualquer usuário do **db_owner** função fixa de banco de dados para criar uma ou mais publicações no banco de dados do banco de dados.  
  
4.  Modifique propriedades, se necessário, depois clique em **OK**.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 As propriedades do Publicador e do Distribuidor podem ser exibidas programaticamente usando os procedimentos armazenados de replicação.  
  
#### Para exibir as propriedades do banco de dados de distribuição e do Distribuidor  
  
1.  Executar [sp_helpdistributor](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md) para retornar informações sobre o distribuidor, o banco de dados de distribuição e o diretório de trabalho.  
  
2.  Executar [sp_helpdistributiondb](../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md) para retornar propriedades de um banco de dados de distribuição especificado.  
  
#### Para alterar as propriedades do banco de dados de distribuição e do Distribuidor  
  
1.  No distribuidor, execute [sp_changedistributor_property](../../relational-databases/system-stored-procedures/sp-changedistributor-property-transact-sql.md) para modificar propriedades do distribuidor.  
  
2.  No distribuidor, execute [sp_changedistributiondb](../../relational-databases/system-stored-procedures/sp-changedistributiondb-transact-sql.md) para modificar propriedades de banco de dados de distribuição.  
  
3.  No distribuidor, execute [sp_changedistributor_password](../../relational-databases/system-stored-procedures/sp-changedistributor-password-transact-sql.md) para alterar a senha do distribuidor.  
  
    > [!IMPORTANT]  
    >  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se você precisar armazenar credenciais em um arquivo de script, proteja o arquivo para evitar acesso não autorizado.  
  
4.  No distribuidor, execute [sp_changedistpublisher](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md) para alterar as propriedades de um editor usando o distribuidor.  
  
###  <a name="TsqlExample"></a> Exemplos (Transact-SQL)  
 O seguinte exemplo de script [!INCLUDE[tsql](../../includes/tsql-md.md)] retorna as informações sobre o Distribuidor e o banco de dados de distribuição.  
  
 [!code-sql[HowTo#sp_helpdistributor](../../relational-databases/replication/codesnippet/tsql/view-and-modify-distribu_1.sql)]  
  
 [!code-sql[HowTo#sp_helpdistributiondb](../../relational-databases/replication/codesnippet/tsql/view-and-modify-distribu_2.sql)]  
  
 Esse exemplo altera os períodos de retenção para o Distribuidor, a senha usada quando conectando-se ao Distribuidor, e o intervalo no qual o Distribuidor verifica o status de vários agentes de replicação (também conhecidos como intervalo de heartbeat).  
  
> [!IMPORTANT]  
>  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se você precisar armazenar credenciais em um arquivo de script, proteja o arquivo para evitar acesso não autorizado.  
  
 [!code-sql[HowTo#sp_changedistributor_property](../../relational-databases/replication/codesnippet/tsql/view-and-modify-distribu_3.sql)]  
  
 [!code-sql[HowTo#sp_changedistributiondb](../../relational-databases/replication/codesnippet/tsql/view-and-modify-distribu_4.sql)]  
  
 [!code-sql[HowTo#sp_changedistributor_password](../../relational-databases/replication/codesnippet/tsql/view-and-modify-distribu_5.sql)]  
  
##  <a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
  
#### Para exibir e modificar as propriedades do Distribuidor  
  
1.  Criar uma conexão com o distribuidor usando a <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.ReplicationServer> classe. Passar o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> objeto da etapa 1.  
  
3.  (Opcional) Verifique o <xref:Microsoft.SqlServer.Replication.ReplicationServer.IsDistributor%2A> propriedade para verificar se o servidor conectado no momento é um distribuidor.  
  
4.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationObject.Load%2A> método para obter as propriedades do servidor.  
  
5.  (Opcional) Para alterar propriedades, defina um novo valor para uma ou mais das propriedades do distribuidor que podem ser definidas na <xref:Microsoft.SqlServer.Replication.ReplicationServer> objeto.  
  
6.  (Opcional) Se o <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> propriedade o <xref:Microsoft.SqlServer.Replication.ReplicationServer> objeto é definido como **true**, chame o <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> método para confirmar as alterações para o servidor.  
  
#### Para exibir e modificar as propriedades do banco de dados de distribuição  
  
1.  Criar uma conexão com o distribuidor usando a <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.DistributionDatabase> classe. Especifique a propriedade name e passar o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> objeto da etapa 1.  
  
3.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obter as propriedades do servidor. Se esse método retornar **false**, o banco de dados com o nome especificado não existe no servidor.  
  
4.  (Opcional) Para alterar propriedades, defina um novo valor para uma da <xref:Microsoft.SqlServer.Replication.DistributionDatabase> propriedades que podem ser definidas.  
  
5.  (Opcional) Se o <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> propriedade o <xref:Microsoft.SqlServer.Replication.DistributionDatabase> objeto é definido como **true**, chame o <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> método para confirmar as alterações para o servidor.  
  
#### Para exibir e modificar as propriedades do Publicador  
  
1.  Criar uma conexão com o publicador usando o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.DistributionPublisher> classe. Especifique o <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Name%2A> propriedade e passe o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> objeto da etapa 1.  
  
3.  (Opcional) Para alterar propriedades, defina um novo valor para uma da <xref:Microsoft.SqlServer.Replication.DistributionPublisher> propriedades que podem ser definidas.  
  
4.  (Opcional) Se o <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> propriedade o <xref:Microsoft.SqlServer.Replication.DistributionPublisher> objeto é definido como **true**, chame o <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> método para confirmar as alterações para o servidor.  
  
#### Para alterar a senha para a conexão administrativa do Publicador para o Distribuidor  
  
1.  Criar uma conexão com o distribuidor usando a <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.ReplicationServer> classe.  
  
3.  Definir o <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propriedade para a conexão criada na etapa 1.  
  
4.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationObject.Load%2A> método para obter as propriedades do objeto.  
  
5.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationServer.ChangeDistributorPassword%2A> método. Passe o novo valor de senha para o parâmetro *password* .  
  
    > [!IMPORTANT]  
    >  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for preciso armazenar credenciais, use os serviços [criptográficos](http://go.microsoft.com/fwlink/?LinkId=34733) fornecidos pelo [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework do Windows.  
  
6.  (Opcional) Execute as etapas seguintes para alterar a senha em cada Publicador remoto que usa esse Distribuidor:  
  
    1.  Criar uma conexão com o publicador usando o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
    2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.ReplicationServer> classe.  
  
    3.  Definir o <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propriedade para a conexão criada na etapa 6a.  
  
    4.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationObject.Load%2A> método para obter as propriedades do objeto.  
  
    5.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationServer.ChangeDistributorPassword%2A> método. Passe o novo valor de senha da etapa 5 para o parâmetro *password* .  
  
###  <a name="PShellExample"></a> Exemplo (RMO)  
 Este exemplo mostra como alterar a Distribuição e as propriedades do banco de dados de distribuição.  
  
> [!IMPORTANT]  
>  Para evitar credenciais de armazenagem no código, a nova senha do Distribuidor é fornecida a tempo de execução.  
  
 [!code-csharp[HowTo#rmo_ChangeDistPub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_changedistpub)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeDistPub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_changedistpub)]  
  
## Consulte também  
 [Conceitos de Replication Management Objects](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [Desabilitar publicação e distribuição](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [Configurar a distribuição](../../relational-databases/replication/configure-distribution.md)   
 [Conceitos de Replication Management Objects](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [Script de informações do Distribuidor e Publicador](../../relational-databases/replication/administration/distributor-and-publisher-information-script.md)   
 [Conceitos dos procedimentos armazenados do sistema de replicação](../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Exibir informações e executar tarefas para um publicador & #40. Monitor de replicação e 41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md)  
  
  