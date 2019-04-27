---
title: syspolicy_system_health_state (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syspolicy_system_health_state_TSQL
- syspolicy_system_health_state
dev_langs:
- TSQL
helpviewer_keywords:
- syspolicy_system_health_state view
ms.assetid: 00815106-9fe4-481d-a9e1-a256101887f4
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 115883fa460f370f618c9286b9529e3cf221d12c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62671606"
---
# <a name="syspolicysystemhealthstate-transact-sql"></a>syspolicy_system_health_state (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Exibe uma linha para cada combinação de expressão de consulta de destino e política do Gerenciamento Baseado em Política. Use a exibição syspolicy_system_health_state para verificar de forma programática a saúde da política do servidor. A tabela a seguir descreve as colunas na exibição  syspolicy_system_health_state.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|health_state_id|**bigint**|Identificador do registro do estado da saúde da política.|  
|policy_id|**int**|Identificador da política.|  
|last_run_date|**datetime**|Data e hora em que a política foi executada pela última vez.|  
|target_query_expression_with_id|**nvarchar(400)**|A expressão de destino com valores atribuídos a variáveis de identidade que define o destino contra o qual a política é avaliada.|  
|target_query_expression|**nvarchar(max)**|A expressão que define o destino no qual a política é avaliada.|  
|result|**bit**|O estado de saúde desse destino em relação à política:<br /><br /> 0 = Falha<br /><br /> 1 = Êxito|  
  
## <a name="remarks"></a>Comentários  
 O exibição syspolicy_system_health_state mostra o estado mais recente da saúde da expressão de consulta de destino para cada política ativa (ativada). As página Pesquisador de Objetos e Detalhes do Pesquisador de Objetos do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] agrega a saúde da política desta exibição para mostrar o estado de saúde crítico.  
  
## <a name="permissions"></a>Permissões  
 Requer a associação à função PolicyAdministratorRole no banco de dados msdb.  
  
## <a name="see-also"></a>Consulte também  
 [Administrar servidores com Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [Exibições de Gerenciamento Baseado em Políticas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
