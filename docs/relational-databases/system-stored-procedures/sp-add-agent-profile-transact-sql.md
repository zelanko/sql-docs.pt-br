---
title: sp_add_agent_profile (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_add_agent_profile
- sp_add_agent_profile_TSQL
helpviewer_keywords:
- sp_add_agent_profile
ms.assetid: 5c246a33-2c21-4a77-9c2a-a2c9f0c5dda1
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: b6cd4013d3126442b02c660c54215c0b0b17e157
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67941794"
---
# <a name="spaddagentprofile-transact-sql"></a>sp_add_agent_profile (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria um perfil novo para um agente de replicação. Esse procedimento armazenado é executado no Distribuidor em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_add_agent_profile [ [ @profile_id= ] profile_id OUTPUT ]  
        , [ @profile_name= ] 'profile_name'   
        , [ @agent_type= ] 'agent_type' ]   
    [ , [ @profile_type= ] profile_type ]  
    [ , [ @description= ] 'description' ]  
    [ , [ @default= ] default ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @profile_id = ] profile_id` É a ID associada ao perfil recém-inserido. *profile_id* está **int** e é um parâmetro OUTPUT opcional. Se especificado, o valor será definido como a nova ID do perfil.  
  
`[ @profile_name = ] 'profile_name'` É o nome do perfil. *profile_name* está **sysname**, sem padrão.  
  
`[ @agent_type = ] 'agent_type'` É o tipo de agente de replicação. *agent_type* está **int**, sem padrão e pode ser um destes valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Snapshot Agent|  
|**2**|Agente de Leitor de Log|  
|**3**|Agente de Distribuição|  
|**4**|Merge Agent|  
|**9**|Queue Reader Agent|  
  
`[ @profile_type = ] profile_type` É o tipo de perfil. *profile_type* é **int**, com um padrão de **1**.  
  
 **0** indica um perfil de sistema. **1** indica um perfil personalizado. Somente perfis personalizados podem ser criados usando esse procedimento armazenado; Portanto, o único valor válido é **1**. Somente [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cria perfis de sistema.  
  
`[ @description = ] 'description'` É uma descrição do perfil. *Descrição* está **nvarchar(3000)** , sem padrão.  
  
`[ @default = ] default` Indica se o perfil é o padrão para *agent_type * *.* *padrão* está **bit**, com um padrão de **0**. **1** indica que o perfil que está sendo adicionado se torne o novo perfil padrão para o agente especificado por *agent_type*.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_add_agent_profile** é usado em replicação de instantâneo, replicação transacional e replicação de mesclagem.  
  
 Perfis de agente personalizados são adicionados com os valores de parâmetro de agente padrão. Use [sp_change_agent_parameter &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-change-agent-parameter-transact-sql.md) para alterar esses valores padrão ou [sp_add_agent_parameter &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md) para adicionar parâmetros adicionais.  
  
 Quando **sp_add_agent_profile** é executado, uma linha é adicionada para o novo perfil personalizado na [MSagent_profiles &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/msagent-profiles-transact-sql.md) tabela e os parâmetros padrão associados perfil são adicionados para o [MSagent_parameters &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/msagent-parameters-transact-sql.md) tabela.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** pode executar a função de servidor fixa **sp_add_agent_profile**.  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhar com perfis do Agente de Replicação](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [Perfis do agente de replicação](../../relational-databases/replication/agents/replication-agent-profiles.md)   
 [sp_add_agent_parameter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)   
 [sp_change_agent_parameter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-agent-parameter-transact-sql.md)   
 [sp_change_agent_profile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-agent-profile-transact-sql.md)   
 [sp_drop_agent_parameter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-parameter-transact-sql.md)   
 [sp_drop_agent_profile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-profile-transact-sql.md)   
 [sp_help_agent_parameter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)   
 [sp_help_agent_profile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)  
  
  
