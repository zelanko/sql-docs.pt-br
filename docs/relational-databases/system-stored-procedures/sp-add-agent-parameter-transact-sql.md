---
description: sp_add_agent_parameter (Transact-SQL)
title: sp_add_agent_parameter (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_add_agent_parameter_TSQL
- sp_add_agent_parameter
helpviewer_keywords:
- sp_add_agent_parameter
ms.assetid: 055f4765-0574-47c3-bf7d-6ef6e9bd8b34
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: abd0a36fe9699c3fc72db4848d08ad6469ae3dc0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88481616"
---
# <a name="sp_add_agent_parameter-transact-sql"></a>sp_add_agent_parameter (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Adiciona um novo parâmetro e seu valor a um perfil de agente. Esse procedimento armazenado é executado no Distribuidor em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_add_agent_parameter [ @profile_id = ] profile_id  
        , [ @parameter_name = ] 'parameter_name'   
        , [ @parameter_value = ] 'parameter_value'   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @profile_id = ] profile_id` É a ID do perfil da tabela de **MSagent_profiles** no banco de dados **msdb** . *profile_id* é **int**, sem padrão.  
  
 Para descobrir qual tipo de agente este *profile_id* representa, localize o *profile_id* na tabela [MSagent_profiles &#40;Transact-SQL&#41;](../../relational-databases/system-tables/msagent-profiles-transact-sql.md) e observe o valor do campo *agent_type* . Os valores são os seguintes:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Snapshot Agent|  
|**2**|Agente de Leitor de Log|  
|**3**|Agente de Distribuição|  
|**4**|Merge Agent|  
|**9**|Queue Reader Agent|  
  
`[ @parameter_name = ] 'parameter_name'` É o nome do parâmetro. *parameter_name* é **sysname**, sem padrão. Para obter uma lista de parâmetros já definidos em perfis de sistema, consulte [perfis do agente de replicação](../../relational-databases/replication/agents/replication-agent-profiles.md). Para uma lista completa de parâmetros válidos para cada agente, consulte os seguintes tópicos:  
  
-   [Replication Snapshot Agent](../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
-   [Agente do Leitor de Log de Replicação](../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
-   [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
-   [Replication Merge Agent](../../relational-databases/replication/agents/replication-merge-agent.md)  
  
-   [Agente de Leitor de Fila de Replicação](../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
`[ @parameter_value = ] 'parameter_value'` É o valor a ser atribuído ao parâmetro. *parameter_value* é **nvarchar (255)**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_add_agent_parameter** é usado na replicação de instantâneos, na replicação transacional e na replicação de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar **sp_add_agent_parameter**.  
  
## <a name="see-also"></a>Consulte Também  
 [Trabalhar com perfis do Agente de Replicação](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [Perfis do agente de replicação](../../relational-databases/replication/agents/replication-agent-profiles.md)   
 [&#41;&#40;Transact-SQL de sp_add_agent_profile ](../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_change_agent_profile ](../../relational-databases/system-stored-procedures/sp-change-agent-profile-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_change_agent_parameter ](../../relational-databases/system-stored-procedures/sp-change-agent-parameter-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_drop_agent_parameter ](../../relational-databases/system-stored-procedures/sp-drop-agent-parameter-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_help_agent_parameter ](../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)  
  
  
