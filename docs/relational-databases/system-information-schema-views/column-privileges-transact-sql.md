---
title: COLUMN_PRIVILEGES (Transact-SQL) | Microsoft Docs
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
- COLUMN_PRIVILEGES
- COLUMN_PRIVILEGES_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- COLUMN_PRIVILEGES view
- INFORMATION_SCHEMA.COLUMN_PRIVILEGES view
ms.assetid: 8ae29a85-2b77-48db-a2b9-a1720287b271
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 01df1be992fcebfe7b3f3df9dc52e66849b654ca
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="columnprivileges-transact-sql"></a>COLUMN_PRIVILEGES (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna uma linha para cada coluna com um privilégio concedido para ou concedido pelo usuário atual no banco de dados atual.  
  
 Para recuperar informações dessas exibições, especifique o nome totalmente qualificado do **INFORMATION_SCHEMA.** *view_name*.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**CONCESSOR**|**nvarchar (**128**)**|Concessor do privilégio.|  
|**USUÁRIO AUTORIZADO**|**nvarchar (**128**)**|Beneficiado do privilégio.|  
|**TABLE_CATALOG**|**nvarchar (**128**)**|Qualificador da tabela.|  
|**TABLE_SCHEMA**|**nvarchar (**128**)**|Nome do esquema que contém a tabela.<br /><br /> **\*\*Importante \* \***  não use exibições INFORMATION_SCHEMA para determinar o esquema de um objeto. O único modo seguro de localizar o esquema de um objeto é consultar a exibição de catálogo sys.objects.|  
|**TABLE_NAME**|**sysname**|Nome da tabela.|  
|**NOME DA COLUNA**|**sysname**|Nome da coluna.|  
|**PRIVILEGE_TYPE**|**varchar (**10**)**|Tipo de privilégio.|  
|**IS_GRANTABLE**|**varchar (**3**)**|Especifica se o beneficiado pode conceder permissões a outros.|  
  
## <a name="see-also"></a>Consulte também  
 [Exibições do sistema &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Exibições do esquema de informações &#40; Transact-SQL &#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys. Objects &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [database_permissions &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)   
 [server_permissions &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)  
  
  
