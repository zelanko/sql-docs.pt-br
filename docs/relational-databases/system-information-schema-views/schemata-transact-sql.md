---
title: ESQUEMAS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/08/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-information-schema-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SCHEMATA_TSQL
- SCHEMATA
dev_langs:
- TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.SCHEMATA view
- SCHEMATA view
ms.assetid: 69617642-0f54-4b25-b62f-5f39c8909601
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ac71e5f401f0eb411f7356d8bc4c15fa0a57c901
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="schemata-transact-sql"></a>SCHEMATA (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna uma linha para cada esquema no banco de dados atual. Para recuperar informações dessas exibições, especifique o nome totalmente qualificado do **INFORMATION_SCHEMA.** *view_name*. Para recuperar informações sobre todos os bancos de dados em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulta o [sys. Databases &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) exibição do catálogo.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**CATALOG_NAME**|**sysname**|Nome do banco de dados atual|  
|**SCHEMA_NAME**|**nvarchar (**128**)**|Retorna o nome do esquema.|  
|**SCHEMA_OWNER**|**nvarchar (**128**)**|Nome do proprietário do esquema.<br /><br /> **\*\*Importante \* \***  não use exibições INFORMATION_SCHEMA para determinar o esquema de um objeto. O único modo seguro de localizar o esquema de um objeto é consultar a exibição do catálogo sys.objects.|  
|**DEFAULT_CHARACTER_SET_CATALOG**|**varchar (**6**)**|Sempre retorna NULL.|  
|**DEFAULT_CHARACTER_SET_SCHEMA**|**varchar (**3**)**|Sempre retorna NULL.|  
|**DEFAULT_CHARACTER_SET_NAME**|**sysname**|Retorna o nome do conjunto de caracteres padrão.|  

**Exemplo**  
O exemplo a seguir retorna informações sobre os esquemas de banco de dados mestre:  
```sql  
SELECT * FROM master.INFORMATION_SCHEMA.SCHEMATA;
```  

## <a name="see-also"></a>Consulte também  
 [Exibições do sistema &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Exibições do esquema de informações &#40; Transact-SQL &#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [schemas &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md)   
 [sys. syscharsets &#40; Transact-SQL &#41;](../../relational-databases/system-compatibility-views/sys-syscharsets-transact-sql.md)  
  
  
