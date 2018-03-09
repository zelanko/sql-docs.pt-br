---
title: syspolicy_policy_categories (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- syspolicy_policy_categories
- syspolicy_policy_categories_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syspolicy_policy_groups view
ms.assetid: 65f080c7-771f-4cf6-a7a0-88882c637f8d
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d133b241116b9bc17bf068f07bf8ee566e83f842
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="syspolicypolicycategories-transact-sql"></a>syspolicy_policy_categories (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Exibe uma linha para cada categoria de política do Gerenciamento Baseado em Políticas na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Categorias de políticas ajudam a organizar as políticas quando você tem muitas políticas. A tabela a seguir descreve as colunas na exibição syspolicy_policy_groups.  
 
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|policy_category_id|**Int**|Identificador da categoria da política.|  
|name|**sysname**|Nome da categoria de política.|  
|mandate_database_subscriptions|**bit**|Indica se a categoria da política aplica-se a todos os bancos de dados de uma instância sem uma assinatura explícita (1) ou se a categoria da política deve ser aplicada a um banco de dados usando uma assinatura explícita (0).|  
  
## <a name="remarks"></a>Remarks  
 Exibe uma lista dos grupos de políticas do Gerenciamento Baseado em Política.  
  
## <a name="permissions"></a>Permissões  
 Requer a associação à função PolicyAdministratorRole no banco de dados msdb.  
  
## <a name="see-also"></a>Consulte também  
 [Administrar servidores com Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [Exibições de Gerenciamento Baseado em Políticas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
