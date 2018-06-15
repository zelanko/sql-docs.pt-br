---
title: ESQUEMAS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/08/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 41
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 9596aca9f81b81a7195ef816409e8f9434ba9219
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33240891"
---
# <a name="schemata-transact-sql"></a>SCHEMATA (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna uma linha para cada esquema no banco de dados atual. Para recuperar informações dessas exibições, especifique o nome totalmente qualificado do **INFORMATION_SCHEMA. * * * view_name*. Para recuperar informações sobre todos os bancos de dados em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulta o [sys. Databases &#40;Transact-SQL&#41; ](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) exibição do catálogo.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**CATALOG_NAME**|**sysname**|Nome do banco de dados atual|  
|**SCHEMA_NAME**|**nvarchar(** 128 **)**|Retorna o nome do esquema.|  
|**SCHEMA_OWNER**|**nvarchar(** 128 **)**|Nome do proprietário do esquema.<br /><br /> **\*\* Importante \* \***  não use exibições INFORMATION_SCHEMA para determinar o esquema de um objeto. O único modo seguro de localizar o esquema de um objeto é consultar a exibição do catálogo sys.objects.|  
|**DEFAULT_CHARACTER_SET_CATALOG**|**varchar (** 6 **)**|Sempre retorna NULL.|  
|**DEFAULT_CHARACTER_SET_SCHEMA**|**varchar (** 3 **)**|Sempre retorna NULL.|  
|**DEFAULT_CHARACTER_SET_NAME**|**sysname**|Retorna o nome do conjunto de caracteres padrão.|  

**Exemplo**  
O exemplo a seguir retorna informações sobre os esquemas de banco de dados mestre:  
```sql  
SELECT * FROM master.INFORMATION_SCHEMA.SCHEMATA;
```  

## <a name="see-also"></a>Consulte também  
 [Exibições do sistema &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Exibições do esquema de informações &#40;Transact-SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.schemas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md)   
 [sys. syscharsets &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syscharsets-transact-sql.md)  
  
  
