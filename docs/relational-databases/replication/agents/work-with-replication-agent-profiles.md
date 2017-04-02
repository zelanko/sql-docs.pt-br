---
title: "Trabalhar com perfis do agente de replica&#231;&#227;o | Microsoft Docs"
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
  - "replicação [SQL Server], agentes e perfis"
  - "perfis de agente de replicação [SQL Server]"
  - "agentes [replicação do SQL Server], perfis"
  - "perfis [SQL Server], agente de replicação"
ms.assetid: 9c290a88-4e9f-4a7e-aab5-4442137a9918
caps.latest.revision: 49
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 49
---
# Trabalhar com perfis do agente de replica&#231;&#227;o
  Este tópico descreve como trabalhar com perfis do Agente de Replicação no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou o RMO (Replication Management Objects). O comportamento de cada agente de replicação é controlado por um conjunto de parâmetros que podem ser definidos através dos perfis de agente. Cada agente tem um perfil padrão, e alguns têm perfis adicionais predefinidos; em um determinado momento, apenas um perfil está ativo para um agente.  
  
 **Neste tópico**  
  
-   **Para trabalhar com perfis do Agente de Replicação, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
    -   Acesse a caixa de diálogo Perfis de Agente  
  
    -   Especifique um perfil para um agente  
  
    -   Crie um perfil  
  
    -   Modifique um perfil  
  
    -   Exclua um perfil  
  
     [Transact-SQL](#TsqlProcedure)  
  
    -   Crie um perfil  
  
    -   Modifique um perfil  
  
    -   Exclua um perfil  
  
    -   Use perfis de agente durante a sincronização  
  
    -   Exemplo de Transact-SQL  
  
     [Replication Management Objects](#RMOProcedure)  
  
    -   Crie um perfil  
  
    -   Modifique um perfil  
  
    -   Exclua um perfil  
  
-   **Acompanhamento:**  [depois de alterar parâmetros do agente](#FollowUp)  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
###  <a name="Access_SSMS"></a> Para acessar a caixa de diálogo Perfis do Agente a partir do SQL Server Management Studio  
  
1.  Na **geral** página o **Propriedades do distribuidor - \< distribuidor>** caixa de diálogo, clique em **padrões de perfil**.  
  
#### Para acessar a caixa de diálogo Perfis do Agente a partir do Replication Monitor  
  
-   Para abrir a caixa de diálogo para todos os agentes, um editor de atalho e, em seguida, clique em **perfis de agente**.  
  
-   Para abrir a caixa de diálogo para um único agente:  
  
    1.  Expanda um Grupo do publicador no painel esquerdo do Replication Monitor, expanda um Publicador e, em seguida, clique em uma publicação.  
  
    2.  Para os perfis de agente de distribuição e o agente de mesclagem, clique uma assinatura de **todas as assinaturas** guia e, em seguida, clique em **perfil de agente**. Para outros agentes, clique o agente a **agentes** guia e, em seguida, clique em **perfil de agente**.  
  
###  <a name="Specify_SSMS"></a> Para especificar o perfil para um agente  
  
1.  Se a caixa de diálogo **Perfis do Agente** exibir perfis para mais de um agente, selecione um agente.  
  
2.  Selecione um perfil na coluna **Padrão para Novo** da grade **Perfis do Agente** . Por padrão, o perfil só é aplicado aos agentes para publicações e assinaturas novas.  
  
3.  Para especificar que todos os agentes de um tipo selecionado para publicações ou assinaturas existentes usem esse perfil, clique em **Alterar agentes existentes**.  
  
###  <a name="Modify_SSMS"></a> Para exibir e editar os parâmetros associados a um perfil  
  
1.  Se a caixa de diálogo **Perfis do Agente** exibir perfis para mais de um agente, selecione um agente.  
  
2.  Clique no botão Propriedades (**...**) ao lado do perfil.  
  
3.  Exibir os parâmetros e valores de **\< ProfileName> Propriedades de perfil** caixa de diálogo.  
  
    -   Os parâmetros em perfis definidos pelo usuário podem ser editados; os parâmetros em perfis de sistema predefinidos não podem.  
  
    -   Para exibir todos os parâmetros de um agente, desmarque a caixa de seleção **Mostrar apenas os parâmetros usados neste perfil** . Para obter informações sobre parâmetros de agente, consulte os links no final deste tópico.  
  
4.  Clique em **Fechar**.  
  
###  <a name="Create_SSMS"></a> Para criar um perfil definido pelo usuário  
  
1.  Se a caixa de diálogo **Perfis do Agente** exibir perfis para mais de um agente, selecione um agente.  
  
2.  Clique em **Nova**.  
  
3.  Na caixa de diálogo de inicialização **Novo Perfil do Agente** , selecione um perfil existente no qual o novo perfil será baseado.  
  
4.  Na caixa de diálogo **Novo Perfil do Agente** , digite os valores nas caixas de texto **Nome** e **Descrição** .  
  
5.  Modificar parâmetros para personalizar o perfil. Para exibir todos os parâmetros de um agente, desmarque a caixa de seleção **Mostrar apenas os parâmetros usados neste perfil** . Para obter informações sobre parâmetros de agente, consulte os links no final deste tópico.  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
###  <a name="Delete_SSMS"></a> Para excluir um perfil definido pelo usuário  
  
1.  Se a caixa de diálogo **Perfis do Agente** exibir perfis para mais de um agente, selecione um agente.  
  
2.  Se um perfil for associado a um ou mais agentes, altere o perfil para esses agentes:  
  
    1.  Selecione um perfil diferente na grade **Perfis do Agente** .  
  
    2.  Clique em **Alterar Agentes Existentes**.  
  
        > [!NOTE]  
        >  Isso alterará o perfil para todos os agentes do tipo selecionado para publicações ou assinaturas existentes, não apenas para os que usam o perfil que se deseja excluir.  
  
3.  Selecione o perfil a ser excluído e, em seguida, clique em **Excluir**.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
###  <a name="Create_tsql"></a> Para criar um perfil novo de agente  
  
1.  No distribuidor, execute [sp_add_agent_profile & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md). Especifique **@name**, um valor de **1** para **@profile_type**, e um dos seguintes valores para **@agent_type**:  
  
    -   **1** - [agente de instantâneo de replicação](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [replication Log Reader Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [agente de distribuição de replicação](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [agente de mesclagem de replicação](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     Se esse perfil se tornar o novo perfil padrão para seu tipo de agente de replicação, especifique o valor **1** para **@default**. O identificador para o novo perfil for retornado com o **@profile_id** parâmetro de saída. Isso cria um perfil novo com um conjunto de parâmetros de perfis baseado no perfil padrão para o tipo de agente especificado.  
  
2.  Depois que o perfil novo for criado, adicione, remova ou modifique os parâmetros padrão para personalizar o perfil.  
  
###  <a name="Modify_tsql"></a> Para modificar um perfil de agente existente  
  
1.  No distribuidor, execute [sp_help_agent_profile & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md). Especifique um dos valores a seguir para **@agent_type**:  
  
    -   **1** - [agente de instantâneo de replicação](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [replication Log Reader Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [agente de distribuição de replicação](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [agente de mesclagem de replicação](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     Isso retorna todos os perfis para o tipo especificado de agente. Observe o valor de **profile_id** no conjunto de resultados para o perfil a ser alterado.  
  
2.  No distribuidor, execute [sp_help_agent_parameter & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md). Especifique o identificador do perfil da etapa 1 para **@profile_id**. Isso retorna todos os parâmetros para o perfil. Observe o nome de qualquer parâmetro a modificar ou remover do perfil.  
  
3.  Para alterar o valor de um parâmetro em um perfil, execute [sp_change_agent_profile & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-change-agent-profile-transact-sql.md). Especifique o identificador do perfil da etapa 1 para **@profile_id**, o nome do parâmetro para alterar para **@property**, e um novo valor para o parâmetro **@value**.  
  
    > [!NOTE]  
    >  Você não pode alterar um perfil de agente existente para se tornar o perfil padrão para um agente. Em vez disso, você deve criar um perfil novo como perfil padrão, como mostrado no procedimento anterior.  
  
4.  Para remover um parâmetro de um perfil, execute [sp_drop_agent_parameter & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-drop-agent-parameter-transact-sql.md). Especifique o identificador do perfil da etapa 1 para **@profile_id** e o nome do parâmetro para remover para **@parameter_name**.  
  
5.  Para adicionar um parâmetro novo a um perfil, você deve fazer o seguinte:  
  
    -   Consulta o [MSagentparameterlist & #40. O Transact-SQL e 41;](../../../relational-databases/system-tables/msagentparameterlist-transact-sql.md) tabela no distribuidor para determinar quais parâmetros de perfil podem ser definidos para cada tipo de agente.  
  
    -   No distribuidor, execute [sp_add_agent_parameter & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md). Especifique o identificador do perfil da etapa 1 para **@profile_id**, o nome de um parâmetro válido para adicionar para **@parameter_name**, e o valor do parâmetro para **@parameter_value**.  
  
###  <a name="Delete_tsql"></a> Para excluir um perfil de agente  
  
1.  No distribuidor, execute [sp_help_agent_profile & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md). Especifique um dos valores a seguir para **@agent_type**:  
  
    -   **1** - [agente de instantâneo de replicação](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [replication Log Reader Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [agente de distribuição de replicação](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [agente de mesclagem de replicação](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     Isso retorna todos os perfis para o tipo especificado de agente. Observe o valor de **profile_id** no conjunto de resultados para o perfil a remover.  
  
2.  No distribuidor, execute [sp_drop_agent_profile & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-drop-agent-profile-transact-sql.md). Especifique o identificador do perfil da etapa 1 para **@profile_id**.  
  
###  <a name="Synch_tsql"></a> Para usar perfis de agente durante sincronização  
  
1.  No distribuidor, execute [sp_help_agent_profile & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md). Especifique um dos valores a seguir para **@agent_type**:  
  
    -   **1** - [agente de instantâneo de replicação](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [replication Log Reader Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [agente de distribuição de replicação](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [agente de mesclagem de replicação](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     Isso retorna todos os perfis para o tipo especificado de agente. Observe o valor de **profile_name** no conjunto de resultados para o perfil a ser usado.  
  
2.  Se o agente é iniciado de um trabalho do agente, edite a etapa de trabalho que inicia o agente para especificar o valor de **profile_name** obtido na etapa 1 após o **- ProfileName** parâmetro de linha de comando. Para obter mais informações, consulte [Exibir e modificar os parâmetros do Prompt de comando do Replication Agent & #40. SQL Server Management Studio e 41;](../../../relational-databases/replication/agents/view and modify replication agent command prompt parameters.md).  
  
3.  Quando o agente a partir do prompt de comando, especifique o valor de **profile_name** obtido na etapa 1 após o **- ProfileName** parâmetro de linha de comando.  
  
###  <a name="TsqlExample"></a> Exemplo (Transact-SQL)  
 Este exemplo cria um perfil personalizado para o Merge Agent denominado **custom_merge**, altera o valor da **- UploadReadChangesPerBatch** parâmetro, adiciona um novo **- ExchangeType** parâmetro e retorna informações sobre o perfil é criado.  
  
 [!code-sql[HowTo#sp_addagentprofileparam](../../../relational-databases/replication/codesnippet/tsql/work-with-replication-ag_1.sql)]  
  
##  <a name="RMOProcedure"></a> Usando RMO  
  
###  <a name="Create_RMO"></a> Para criar um perfil novo de agente  
  
1.  Criar uma conexão com o distribuidor usando uma instância do <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.AgentProfile> classe.  
  
3.  Defina as seguintes propriedades no objeto:  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.Name%2A> -o nome do perfil.  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.AgentType%2A> - uma <xref:Microsoft.SqlServer.Replication.AgentType> valor que especifica o tipo de agente de replicação para o qual o perfil está sendo criado.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> - o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> criado na etapa 1.  
  
    -   (Opcional) <xref:Microsoft.SqlServer.Replication.AgentProfile.Description%2A> -uma descrição do perfil.  
  
    -   (Opcional) <xref:Microsoft.SqlServer.Replication.AgentProfile.Default%2A> -Defina essa propriedade como **true** se todos os novos trabalhos de agente para este <xref:Microsoft.SqlServer.Replication.AgentType> usarão este perfil por padrão.  
  
4.  Chamar o <xref:Microsoft.SqlServer.Replication.AgentProfile.Create%2A> método para criar o perfil no servidor.  
  
5.  Uma vez que o perfil existir no servidor, você poderá personalizá-lo adicionando, removendo ou modificando os valores dos parâmetros do agente de replicação.  
  
6.  Para atribuir o perfil a um trabalho do agente de replicação existente, chame o <xref:Microsoft.SqlServer.Replication.AgentProfile.AssignToAgent%2A> método. Passe o nome do banco de dados de distribuição para *distributionDBName* e a ID do trabalho para *agentID*.  
  
###  <a name="Modify_RMO"></a> Para modificar um perfil de agente existente  
  
1.  Criar uma conexão com o distribuidor usando uma instância do <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.ReplicationServer> classe. Passar o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> objeto criado na etapa 1.  
  
3.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método. Se esse método retornar **false**, verifique se o Distribuidor existe.  
  
4.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationServer.EnumAgentProfiles%2A> método. Passar um <xref:Microsoft.SqlServer.Replication.AgentType> o valor para restringir os perfis retornados a um tipo específico de agente de replicação.  
  
5.  Obter a desejada <xref:Microsoft.SqlServer.Replication.AgentProfile> objeto do retornado <xref:System.Collections.ArrayList>, onde o <xref:Microsoft.SqlServer.Replication.AgentProfile.Name%2A> propriedade do objeto corresponde ao nome do perfil.  
  
6.  Chame um dos seguintes métodos de <xref:Microsoft.SqlServer.Replication.AgentProfile> para alterar o perfil:  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.AddParameter%2A> -adiciona um parâmetro com suporte para o perfil, onde *nome* é o nome do parâmetro do agente de replicação e *valor* é o valor especificado. Para enumerar todos os parâmetros de agente com suporte para um determinado tipo de agente, chame o <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameterInfo%2A> método. Esse método retorna um <xref:System.Collections.ArrayList> de <xref:Microsoft.SqlServer.Replication.AgentProfileParameterInfo> objetos que representam os parâmetros tudo isso com suporte.  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.RemoveParameter%2A> -Remove um parâmetro existente do perfil, onde *nome* é o nome do parâmetro do agente de replicação. Para enumerar todos os parâmetros de agente atuais definidos para o perfil, chame o <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameters%2A> método. Esse método retorna um <xref:System.Collections.ArrayList> de <xref:Microsoft.SqlServer.Replication.AgentProfileParameter> objetos que representam o parâmetro existente para esse perfil.  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.ChangeParameter%2A> -altera a configuração de um parâmetro existente no perfil, onde *nome* é o nome do parâmetro do agente e *newValue* é o valor para o qual o parâmetro está sendo alterado. Para enumerar todos os parâmetros de agente atuais definidos para o perfil, chame o <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameters%2A> método. Esse método retorna um <xref:System.Collections.ArrayList> de <xref:Microsoft.SqlServer.Replication.AgentProfileParameter> objetos que representam o parâmetro existente para esse perfil. Para enumerar todas as configurações de parâmetro de agente de suporte, chame o <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameterInfo%2A> método. Esse método retorna um <xref:System.Collections.ArrayList> de <xref:Microsoft.SqlServer.Replication.AgentProfileParameterInfo> objetos que representam os valores com suporte para todos os parâmetros.  
  
###  <a name="Delete_RMO"></a> Para excluir um perfil de agente  
  
1.  Criar uma conexão com o distribuidor usando uma instância do <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.AgentProfile> classe. Defina o nome do perfil de <xref:Microsoft.SqlServer.Replication.AgentProfile.Name%2A> e o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da etapa 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método. Se este método retornar **false**, o banco de dados com o nome especificado estava incorreto ou o perfil não existe no servidor.  
  
4.  Verifique o <xref:Microsoft.SqlServer.Replication.AgentProfile.Type%2A> está definida como <xref:Microsoft.SqlServer.Replication.AgentProfileTypeOption.User>, que indica um perfil de cliente. Você não deve remover um perfil que possui um valor de <xref:Microsoft.SqlServer.Replication.AgentProfileTypeOption.System> para <xref:Microsoft.SqlServer.Replication.AgentProfile.Type%2A>.  
  
5.  Chamar o <xref:Microsoft.SqlServer.Replication.AgentProfile.Remove%2A> método para remover o perfil definido pelo usuário representado por esse objeto do servidor.  
  
##  <a name="FollowUp"></a> Acompanhamento: depois de alterar parâmetros de agente  
 As alterações do parâmetro de agente entrarão em vigor na próxima vez o agente for iniciado. Se o agente ficar executando continuamente, será necessário parar e reiniciar o agente.  
  
## Consulte também  
 [Perfis do Agente de Replicação](../../../relational-databases/replication/agents/replication-agent-profiles.md)   
 [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)   
 [Replication Agente de Leitor de Log](../../../relational-databases/replication/agents/replication-log-reader-agent.md)   
 [Agente de Distribuição de Replicação](../../../relational-databases/replication/agents/replication-distribution-agent.md)   
 [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)   
 [Replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
  