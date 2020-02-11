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
ms.openlocfilehash: 24a900409ae5979c13bdbff0d67d9d2670059208
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68770851"
---
# <a name="sp_add_agent_profile-transact-sql"></a>sp_add_agent_profile (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Cria um perfil novo para um agente de replicação. Esse procedimento armazenado é executado no Distribuidor em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @profile_id = ] profile_id`É a ID associada ao perfil recentemente inserido. *profile_id* é **int** e é um parâmetro de saída opcional. Se especificado, o valor será definido como a nova ID do perfil.  
  
`[ @profile_name = ] 'profile_name'`É o nome do perfil. *profile_name* é **sysname**, sem padrão.  
  
`[ @agent_type = ] 'agent_type'`É o tipo de agente de replicação. *agent_type* é **int**, sem padrão, e pode ser um desses valores.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**1**|Snapshot Agent|  
|**2**|Agente de Leitor de Log|  
|**Beta**|Agente de Distribuição|  
|**quatro**|Merge Agent|  
|**99**|Queue Reader Agent|  
  
`[ @profile_type = ] profile_type`É o tipo de perfil. *profile_type* é **int**, com um padrão de **1**.  
  
 **0** indica um perfil do sistema. **1** indica um perfil personalizado. Somente perfis personalizados podem ser criados usando esse procedimento armazenado; Portanto, o único valor válido é **1**. Cria [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] somente perfis de sistema.  
  
`[ @description = ] 'description'`É uma descrição do perfil. a *Descrição* é **nvarchar (3000)**, sem padrão.  
  
`[ @default = ] default`Indica se o perfil é o padrão para *agent_type * *.* o *padrão* é **bit**, com um padrão de **0**. **1** indica que o perfil que está sendo adicionado se tornará o novo perfil padrão para o agente especificado por *agent_type*.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_add_agent_profile** é usado na replicação de instantâneos, na replicação transacional e na replicação de mesclagem.  
  
 Perfis de agente personalizados são adicionados com os valores de parâmetro de agente padrão. Use [sp_change_agent_parameter &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-change-agent-parameter-transact-sql.md) para alterar esses valores padrão ou [Sp_add_agent_parameter &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md) para adicionar parâmetros adicionais.  
  
 Quando **sp_add_agent_profile** é executado, uma linha é adicionada ao novo perfil personalizado no [MSagent_profiles &#40;tabela de&#41;do Transact-SQL](../../relational-databases/system-tables/msagent-profiles-transact-sql.md) e os parâmetros padrão associados para esse perfil são adicionados à tabela MSAGENT_PARAMETERS &#40;[Transact-SQL](../../relational-databases/system-tables/msagent-parameters-transact-sql.md)&#41;.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar **sp_add_agent_profile**.  
  
## <a name="see-also"></a>Consulte Também  
 [Trabalhar com perfis do agente de replicação](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [Perfis do agente de replicação](../../relational-databases/replication/agents/replication-agent-profiles.md)   
 [&#41;&#40;Transact-SQL de sp_add_agent_parameter](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_change_agent_parameter](../../relational-databases/system-stored-procedures/sp-change-agent-parameter-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_change_agent_profile](../../relational-databases/system-stored-procedures/sp-change-agent-profile-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_drop_agent_parameter](../../relational-databases/system-stored-procedures/sp-drop-agent-parameter-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_drop_agent_profile](../../relational-databases/system-stored-procedures/sp-drop-agent-profile-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_help_agent_parameter](../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_help_agent_profile](../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)  
  
  
