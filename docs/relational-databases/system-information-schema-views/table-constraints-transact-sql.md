---
description: TABLE_CONSTRAINTS (Transact-SQL)
title: TABLE_CONSTRAINTS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- TABLE_CONSTRAINTS
- TABLE_CONSTRAINTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.TABLE_CONSTRAINTS view
- TABLE_CONSTRAINTS view
ms.assetid: 687f3284-2849-4853-8a5c-fc936deceae0
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f0a7dbf03a4cb71424276a734057997028fbd9ef
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88481612"
---
# <a name="table_constraints-transact-sql"></a>TABLE_CONSTRAINTS (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Retorna uma linha para cada restrição de tabela no banco de dados atual. Esta exibição de esquema de informações retorna informações sobre os objetos para os quais o usuário atual tem permissões.  
  
 Para recuperar informações dessas exibições, especifique o nome totalmente qualificado de **INFORMATION_SCHEMA.** _view_name_.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**CONSTRAINT_CATALOG**|**nvarchar (** 128 **)**|Qualificador da restrição.|  
|**CONSTRAINT_SCHEMA**|**nvarchar (** 128 **)**|Nome do esquema que contém a restrição.<br /><br /> Importante somente a maneira confiável de localizar o esquema de um objeto é consultar a exibição do catálogo sys. Objects. <strong> \* \* \* \* </strong>|  
|**CONSTRAINT_NAME**|**sysname**|Nome da restrição.|  
|**TABLE_CATALOG**|**nvarchar (** 128 **)**|Qualificador da tabela.|  
|**TABLE_SCHEMA**|**nvarchar (** 128 **)**|Nome do esquema que contém a tabela.<br /><br /> Importante somente a maneira confiável de localizar o esquema de um objeto é consultar a exibição do catálogo sys. Objects. <strong> \* \* \* \* </strong>|  
|**TABLE_NAME**|**sysname**|Nome da tabela.|  
|**CONSTRAINT_TYPE**|**varchar (** 11 **)**|Tipo de restrição:<br /><br /> CHECK<br /><br /> UNIQUE<br /><br /> PRIMARY KEY<br /><br /> FOREIGN KEY|  
|**IS_DEFERRABLE**|**varchar (** 2 **)**|Especifica se a verificação de restrição é adiável. Sempre retorna NO.|  
|**INITIALLY_DEFERRED**|**varchar (** 2 **)**|Especifica se a verificação de restrição é inicialmente adiada. Sempre retorna NO.|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições do sistema &#40;&#41;Transact-SQL ](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Exibições do esquema de informações &#40;&#41;Transact-SQL ](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys. Objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys. key_constraints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-key-constraints-transact-sql.md)   
 [sys. check_constraints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md)   
 [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)  
  
  
