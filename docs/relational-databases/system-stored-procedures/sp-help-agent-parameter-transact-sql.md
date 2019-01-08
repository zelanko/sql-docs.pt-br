---
title: sp_help_agent_parameter (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_help_agent_parameter
- sp_help_agent_parameter_TSQL
helpviewer_keywords:
- sp_help_agent_parameter
ms.assetid: 8fb4a9c3-19af-4a34-8004-572729ba3d15
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f7c9120872253706d45c813f78b8c437b3ff0484
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52786228"
---
# <a name="sphelpagentparameter-transact-sql"></a>sp_help_agent_parameter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna todos os parâmetros de um perfil do [MSagent_parameters &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/msagent-parameters-transact-sql.md) tabela do sistema. Esse procedimento armazenado é executado no Distribuidor, onde o agente está sendo executado, ou em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_agent_parameter [ [ @profile_id = ] profile_id ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@profile_id=**] *profile_id*  
 É a ID do perfil a partir de [MSagent_parameters &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/msagent-parameters-transact-sql.md) tabela. *profile_id* está **int**, com um padrão de **-1**, que retorna todos os parâmetros.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**profile_id**|**int**|ID do perfil do agente.|  
|**parameter_name**|**sysname**|Nome do parâmetro.|  
|**value**|**nvarchar(255)**|Valor do parâmetro.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_help_agent_parameter** é usado em todos os tipos de replicação.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou o **replmonitor** banco de dados fixa podem executar **sp_help_agent_parameter**.  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhar com perfis do Agente de Replicação](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [sp_add_agent_parameter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)   
 [sp_drop_agent_parameter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-parameter-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
