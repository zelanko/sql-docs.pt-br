---
title: CONSTRAINT_TABLE_USAGE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-information-schema-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CONSTRAINT_TABLE_USAGE_TSQL
- CONSTRAINT_TABLE_USAGE
dev_langs:
- TSQL
helpviewer_keywords:
- CONSTRAINT_TABLE_USAGE view
- INFORMATION_SCHEMA.CONSTRAINT_TABLE_USAGE view
ms.assetid: 5770b696-6c04-4d5c-a8db-9eb92022fa42
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 74b4c55aafb5830eee79a2ec0498750a0f07b5dd
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="constrainttableusage-transact-sql"></a>CONSTRAINT_TABLE_USAGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna uma linha para cada tabela no banco de dados atual que tem uma restrição definida na tabela. Esta exibição de esquema de informações retorna informações sobre os objetos para os quais o usuário atual tem permissões.  
  
 Para recuperar informações dessas exibições, especifique o nome totalmente qualificado do **INFORMATION_SCHEMA.** *view_name*.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_CATALOG**|**nvarchar (**128**)**|Qualificador da tabela.|  
|**TABLE_SCHEMA**|**nvarchar (**128**)**|Nome do esquema que contém a tabela.<br /><br /> **\*\*Importante \* \***  não use exibições INFORMATION_SCHEMA para determinar o esquema de um objeto. O único modo seguro de localizar o esquema de um objeto é consultar a exibição de catálogo sys.objects.|  
|**TABLE_NAME**|**sysname**|Nome da tabela.|  
|**CONSTRAINT_CATALOG**|**nvarchar (**128**)**|Qualificador da restrição.|  
|**CONSTRAINT_SCHEMA**|**nvarchar (**128**)**|Nome do esquema que contém a restrição.<br /><br /> **\*\*Importante \* \***  não use exibições INFORMATION_SCHEMA para determinar o esquema de um objeto. O único modo seguro de localizar o esquema de um objeto é consultar a exibição de catálogo sys.objects.|  
|**CONSTRAINT_NAME**|**sysname**|Nome da restrição.|  
  
## <a name="see-also"></a>Consulte também  
 [Exibições do sistema &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Exibições do esquema de informações &#40; Transact-SQL &#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys. Objects &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys. CHECK_CONSTRAINTS &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md)   
 [sys. key_constraints &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-key-constraints-transact-sql.md)   
 [sys. foreign_keys &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-foreign-keys-transact-sql.md)  
  
  
