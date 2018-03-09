---
title: sys.securable_classes (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 12/01/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- securable_classes_TSQL
- securable_classes
- sys.securable_classes_TSQL
- sys.securable_classes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.securable_classes catalog view
ms.assetid: ae2bf589-17be-4cad-b5d5-05a34173b32d
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3d21b559f232a05ab8699962b4691aa3b4e3bea9
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2018
---
# <a name="syssecurableclasses-transact-sql"></a>sys.securable_classes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna uma lista de classes protegíveis  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**class_desc**|**sysname**|Nome da classe.|  
|**class**|**int**|Designação numérica da classe.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna as classes protegíveis com suporte desta instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```sql  
SELECT * FROM sys.securable_classes ORDER BY class;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Protegíveis](../../relational-databases/security/securables.md)  
  
  
