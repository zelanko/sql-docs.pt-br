---
title: syspolicy_policy_category_subscriptions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- syspolicy_policy_category_subscriptions_TSQL
- syspolicy_policy_category_subscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- syspolicy_policy_group_subscriptions view
ms.assetid: b3b3a7d7-0b78-46c0-9755-045f7a5692b9
caps.latest.revision: 16
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2fac13c1a1da914c658f9c7b6a01bfa5124810ed
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="syspolicypolicycategorysubscriptions-transact-sql"></a>syspolicy_policy_category_subscriptions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Exibe uma linha para cada assinatura do Gerenciamento Baseado em Política na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cada linha descreve um par de categoria de políticas e destino. A tabela a seguir descreve as colunas na exibição syspolicy_policy_group_subscriptions.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|policy_category_subscription_id|**Int**|Identificador deste registro.|  
|target_type|**sysname**|Tipo de objeto do banco de dados que é o destino desta assinatura.|  
|target_object|**sysname**|O nome do objeto de destino.|  
|policy_category_id|**Int**|ID da categoria de políticas que é aplicada ao destino.|  
  
## <a name="remarks"></a>Remarks  
 Esta exibição mostra os destinos com assinatura a categorias de políticas.  
  
## <a name="permissions"></a>Permissões  
 Requer a associação à função PolicyAdministratorRole no banco de dados msdb.  
  
## <a name="see-also"></a>Consulte também  
 [Administrar servidores com Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [Exibições de Gerenciamento Baseado em Políticas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
