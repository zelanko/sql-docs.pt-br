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
ms.openlocfilehash: 398e1eebbb269fa1f1507725fefff820c5174f58
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68771506"
---
# <a name="sp_help_agent_parameter-transact-sql"></a>sp_help_agent_parameter (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Retorna todos os parâmetros de um perfil do MSagent_parameters &#40;tabela do sistema [&#41;Transact-SQL](../../relational-databases/system-tables/msagent-parameters-transact-sql.md) . Esse procedimento armazenado é executado no Distribuidor, onde o agente está sendo executado, ou em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_agent_parameter [ [ @profile_id = ] profile_id ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @profile_id = ] profile_id`É a ID do perfil do [MSagent_parameters &#40;tabela&#41;Transact-SQL](../../relational-databases/system-tables/msagent-parameters-transact-sql.md) . *profile_id* é **int**, com um padrão de **-1**, que retorna todos os parâmetros.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**profile_id**|**int**|ID do perfil do agente.|  
|**parameter_name**|**sysname**|Nome do parâmetro.|  
|**value**|**nvarchar (255)**|Valor do parâmetro.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_help_agent_parameter** é usado em todos os tipos de replicação.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou da função de banco de dados fixa **replmonitor** podem executar **sp_help_agent_parameter**.  
  
## <a name="see-also"></a>Consulte Também  
 [Trabalhar com perfis do agente de replicação](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [&#41;&#40;Transact-SQL de sp_add_agent_parameter](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_drop_agent_parameter](../../relational-databases/system-stored-procedures/sp-drop-agent-parameter-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
