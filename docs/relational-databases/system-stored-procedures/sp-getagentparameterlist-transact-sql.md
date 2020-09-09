---
description: sp_getagentparameterlist (Transact-SQL)
title: sp_getagentparameterlist (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_getagentparameterlist
- sp_getagentparameterlist_TSQL
helpviewer_keywords:
- sp_getagentparameterlist
ms.assetid: 50d3d3c1-b9a1-417c-bad4-674089c9c60d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 18cfa88a02506846e004da36b84ec54205359859
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89535677"
---
# <a name="sp_getagentparameterlist-transact-sql"></a>sp_getagentparameterlist (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna uma lista de todos os parâmetros de agente de replicação que pode ser definida em um perfil de agente para o agente especificado. Esse procedimento armazenado é executado no Distribuidor, onde o agente está sendo executado, ou em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_getagentparameterlist [ @agent_type = ] 'agent_type'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @agent_type = ] 'agent_type'` É o agente de replicação para o qual o parâmetro está sendo adicionado. *agent_type* é **int**e pode ser um destes valores:  
  
|Valor|Agente|  
|-----------|-----------|  
|**1**|Instantâneo|  
|**2**|Log Reader|  
|**3**|Distribuição|  
|**4**|Mesclar|  
|**9**|Queue Reader|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar **sp_getagentparameter**.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_add_agent_parameter ](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_add_agent_profile ](../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_drop_agent_parameter ](../../relational-databases/system-stored-procedures/sp-drop-agent-parameter-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_help_agent_parameter ](../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)   
 [Perfis do agente de replicação](../../relational-databases/replication/agents/replication-agent-profiles.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
