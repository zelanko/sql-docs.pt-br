---
title: Exibir e modificar propriedades de Publicador e Distribuidor | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- viewing replication properties
- Distributors [SQL Server replication], modifying
- modifying replication properties, Distributors
- Distributors [SQL Server replication], properties
ms.assetid: 5dae1d59-c377-4c6e-adc9-b68c5b328f79
caps.latest.revision: "43"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dbc553f4f6e7013eb613f7bc2c89fc020c947801
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="view-and-modify-distributor-and-publisher-properties"></a>Exibir e modificar propriedades de Publicador e Distribuidor
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
  
#### <a name="to-view-and-modify-distributor-properties"></a>Para exibir e modificar as propriedades do Distribuidor  
  
1.  Conecte-se ao Distribuidor no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e, em seguida, expanda o nó de servidor.  
  
2.  Clique com o botão direito do mouse na pasta **Replicação** e em seguida clique em **Propriedades do Distribuidor**.  
  
3.  Exibir e modificar as propriedades na caixa de diálogo **Propriedades do Distribuidor – \<Distribuidor>**.  
  
    -   Para exibir e modificar as propriedades de um banco de dados de distribuição, clique no botão de propriedades (**...**) do banco de dados na página **Geral** da caixa de diálogo.  
  
    -   Para exibir e modificar as propriedades do Publicador associado ao Distribuidor, clique no botão de propriedades (**…**) para o Publicador na página **Publicadores** da caixa de diálogo.  
  
    -   Para acessar os perfis para os agentes de replicação, clique no botão **Padrões de Perfil** na página **Geral** da caixa de diálogo. Para obter mais informações, consulte [Replication Agent Profiles](../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
    -   Para alterar a senha da conta usada quando os procedimentos administrativos armazenados são executados no Publicador e para atualizar as informações no Distribuidor, digite uma senha nova nas caixas **Senha** e **Confirmar senha** na página **Publicadores** da caixa de diálogo. Para obter mais informações, consulte [Proteger o Distribuidor](../../relational-databases/replication/security/secure-the-distributor.md).  
  
4.  Modifique propriedades, se necessário, depois clique em **OK**.  
  
#### <a name="to-view-and-modify-publisher-properties"></a>Para exibir e modificar as propriedades do Publicador  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e expanda o nó de servidor.  
  
2.  Clique com o botão direito do mouse na pasta **Replicação** e, em seguida, em **Propriedades do Publicador**.  
  
3.  Exibir e modificar as propriedades da caixa de diálogo **Propriedades do Publicador – < Publisher>**.  
  
    -   Um usuário na função de servidor fixa **sysadmin** pode ativar bancos de dados para replicação na página **Bancos de Dados de Publicação** . Habilitando um banco de dados não publica esse banco de dados, mas permite que qualquer usuário na função de banco de dados fixa **db_owner** para aquele banco de dados crie uma ou mais publicações no banco de dados.  
  
4.  Modifique propriedades, se necessário, depois clique em **OK**.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 As propriedades do Publicador e do Distribuidor podem ser exibidas programaticamente usando os procedimentos armazenados de replicação.  
  
#### <a name="to-view-distributor-and-distribution-database-properties"></a>Para exibir as propriedades do banco de dados de distribuição e do Distribuidor  
  
1.  Execute [sp_helpdistributor](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md) para retornar informações sobre o Distribuidor, banco de dados de distribuição e diretório de funcionamento.  
  
2.  Execute [sp_helpdistributiondb](../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md) para retornar propriedades de um banco de dados de distribuição especificado.  
  
#### <a name="to-change-distributor-and-distribution-database-properties"></a>Para alterar as propriedades do banco de dados de distribuição e do Distribuidor  
  
1.  No Distribuidor, execute [sp_changedistributor_property](../../relational-databases/system-stored-procedures/sp-changedistributor-property-transact-sql.md) para modificar as propriedades do Distribuidor.  
  
2.  No Distribuidor, execute [sp_changedistributiondb](../../relational-databases/system-stored-procedures/sp-changedistributiondb-transact-sql.md) para modificar as propriedades do banco de dados de distribuição.  
  
3.  No Distribuidor, execute [sp_changedistributor_password](../../relational-databases/system-stored-procedures/sp-changedistributor-password-transact-sql.md) para alterar a senha do Distribuidor.  
  
    > [!IMPORTANT]  
    >  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se você precisar armazenar credenciais em um arquivo de script, proteja o arquivo para evitar acesso não autorizado.  
  
4.  No Distribuidor, execute [sp_changedistpublisher](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md) para alterar as propriedades de um Publicador usando o Distribuidor.  
  
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
  
#### <a name="to-view-and-modify-distributor-properties"></a>Para exibir e modificar as propriedades do Distribuidor  
  
1.  Crie uma conexão com o Distribuidor usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.ReplicationServer> . Passe o objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da etapa 1.  
  
3.  (Opcional) Verificar a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationServer.IsDistributor%2A> para verificar se o servidor conectado no momento é um Distribuidor.  
  
4.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.Load%2A> para obter as propriedades do servidor.  
  
5.  (Opcional) Para alterar as propriedades, defina um novo valor para uma ou mais propriedades do Distribuidor que podem ser definidas no objeto <xref:Microsoft.SqlServer.Replication.ReplicationServer> .  
  
6.  (Opcional) Se a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> no objeto <xref:Microsoft.SqlServer.Replication.ReplicationServer> é definida para **true**, chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> para confirmar as alterações para o servidor.  
  
#### <a name="to-view-and-modify-distribution-database-properties"></a>Para exibir e modificar as propriedades do banco de dados de distribuição  
  
1.  Crie uma conexão com o Distribuidor usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.DistributionDatabase> . Especifique o nome da propriedade e passe o objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da etapa 1.  
  
3.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as propriedades do servidor. Se este método retornar **false**, o banco de dados com o nome especificado não existirá no servidor.  
  
4.  (Opcional) Para alterar propriedades, defina um novo valor para uma das propriedades <xref:Microsoft.SqlServer.Replication.DistributionDatabase> que podem ser definidas.  
  
5.  (Opcional) Se a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> no objeto <xref:Microsoft.SqlServer.Replication.DistributionDatabase> é definida para **true**, chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> para confirmar as alterações para o servidor.  
  
#### <a name="to-view-and-modify-publisher-properties"></a>Para exibir e modificar as propriedades do Publicador  
  
1.  Crie uma conexão com o Publicador usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.DistributionPublisher> . Especifique a propriedade <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Name%2A> e passe o objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da etapa 1.  
  
3.  (Opcional) Para alterar propriedades, defina um novo valor para uma das propriedades <xref:Microsoft.SqlServer.Replication.DistributionPublisher> que podem ser definidas.  
  
4.  (Opcional) Se a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> no objeto <xref:Microsoft.SqlServer.Replication.DistributionPublisher> é definida para **true**, chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> para confirmar as alterações para o servidor.  
  
#### <a name="to-change-the-password-for-the-administrative-connection-from-the-publisher-to-the-distributor"></a>Para alterar a senha para a conexão administrativa do Publicador para o Distribuidor  
  
1.  Crie uma conexão com o Distribuidor usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.ReplicationServer> .  
  
3.  Defina a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> para a conexão criada na etapa 1.  
  
4.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.Load%2A> para obter as propriedades do objeto.  
  
5.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationServer.ChangeDistributorPassword%2A> . Passe o novo valor de senha para o parâmetro *password* .  
  
    > [!IMPORTANT]  
    >  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for preciso armazenar credenciais, use os serviços [criptográficos](http://go.microsoft.com/fwlink/?LinkId=34733) fornecidos pelo [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework do Windows.  
  
6.  (Opcional) Execute as etapas seguintes para alterar a senha em cada Publicador remoto que usa esse Distribuidor:  
  
    1.  Crie uma conexão com o Publicador usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
    2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.ReplicationServer> .  
  
    3.  Defina a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> para a conexão criada na etapa 6a.  
  
    4.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.Load%2A> para obter as propriedades do objeto.  
  
    5.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationServer.ChangeDistributorPassword%2A> . Passe o novo valor de senha da etapa 5 para o parâmetro *password* .  
  
###  <a name="PShellExample"></a> Exemplo (RMO)  
 Este exemplo mostra como alterar a Distribuição e as propriedades do banco de dados de distribuição.  
  
> [!IMPORTANT]  
>  Para evitar credenciais de armazenagem no código, a nova senha do Distribuidor é fornecida a tempo de execução.  
  
 [!code-cs[HowTo#rmo_ChangeDistPub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_changedistpub)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeDistPub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_changedistpub)]  
  
## <a name="see-also"></a>Consulte também  
 [Conceitos de objetos de gerenciamento de replicação](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [Desabilitar a publicação e a distribuição](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [Configurar Distribuição](../../relational-databases/replication/configure-distribution.md)   
 [Replication Management Objects Concepts](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [Script de informações do Distribuidor e Publicador](../../relational-databases/replication/administration/distributor-and-publisher-information-script.md)   
 [Replication System Stored Procedures Concepts](../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Exibir informações e executar tarefas para um Publicador &#40;Replication Monitor&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md)  
  
  
