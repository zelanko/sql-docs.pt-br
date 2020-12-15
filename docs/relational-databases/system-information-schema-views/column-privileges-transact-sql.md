---
description: COLUMN_PRIVILEGES (Transact-SQL)
title: COLUMN_PRIVILEGES (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d45392345f469a4f4c2afbbb2428ac3b1e31b3e3
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97474687"
---
# <a name="column_privileges-transact-sql"></a>COLUMN_PRIVILEGES (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Retorna uma linha para cada coluna com um privilégio concedido para ou concedido pelo usuário atual no banco de dados atual.  
  
 Para recuperar informações dessas exibições, especifique o nome totalmente qualificado de **INFORMATION_SCHEMA.** _view_name_.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**GRANTOR**|**nvarchar (** 128 **)**|Concessor do privilégio.|  
|**GRANTEE**|**nvarchar (** 128 **)**|Beneficiado do privilégio.|  
|**TABLE_CATALOG**|**nvarchar (** 128 **)**|Qualificador da tabela.|  
|**TABLE_SCHEMA**|**nvarchar (** 128 **)**|Nome do esquema que contém a tabela.<br /><br /> **&#42;&#42; importantes &#42;&#42;** Não use INFORMATION_SCHEMA exibições para determinar o esquema de um objeto. INFORMATION_SCHEMA exibições representam apenas um subconjunto dos metadados de um objeto. O único modo seguro de localizar o esquema de um objeto é consultar a exibição de catálogo sys.objects.|  
|**TABLE_NAME**|**sysname**|Nome da tabela.|  
|**COLUMN_NAME**|**sysname**|Nome da coluna.|  
|**PRIVILEGE_TYPE**|**varchar (** 10 **)**|Tipo de privilégio.|  
|**IS_GRANTABLE**|**varchar (** 3 **)**|Especifica se o beneficiado pode conceder permissões a outros.|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições do sistema &#40;&#41;Transact-SQL ](../../t-sql/language-reference.md)   
 [Exibições do esquema de informações &#40;&#41;Transact-SQL ](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.database_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)   
 [sys.server_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)  
  
