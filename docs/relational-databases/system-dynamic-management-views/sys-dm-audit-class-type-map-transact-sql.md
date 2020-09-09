---
description: sys.dm_audit_class_type_map (Transact-SQL)
title: sys. dm_audit_class_type_map (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_audit_class_type_map
- sys.dm_audit_class_type_map_TSQL
- dm_audit_class_type_map
- dm_audit_class_type_map_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_audit_class_type_map dynamic management view
ms.assetid: e10b5431-1bb0-47ca-8fd0-c04bd73a4410
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9ec65fe175cf3723bcab9e00811915f15c4075c2
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544805"
---
# <a name="sysdm_audit_class_type_map-transact-sql"></a>sys.dm_audit_class_type_map (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  Retorna uma tabela que mapeia o campo class_type do log de auditoria para o campo class_desc em sys.dm_audit_actions. Para obter mais informações sobre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auditoria, consulte [SQL Server audit &#40;mecanismo de banco de dados&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  

|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**class_type**|**char(2)**|O tipo de classe da entidade que foi auditada. Mapeia para o class_type gravado no log de auditoria e retornado pela função **get_audit_file ()** . Não permite valor nulo.|  
|**class_type_desc**|**nvarchar(120)**|O nome da entidade auditável. Não permite valor nulo.|  
|**securable_class_desc**|**nvarchar(120)**|O objeto protegível que é mapeado para o class_type que está sendo auditado. Será NULL se o class_type não for mapeado para um objeto protegível. Pode ser relacionado a class_desc in sys.dm_audit_actions.|  
  
## <a name="permissions"></a>Permissões  
 A entidade de segurança deve ter a permissão **Select** . Por padrão, é concedida a Público.  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [CREATE SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [DROP SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [CREATE DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
 [ALTER DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-audit-specification-transact-sql.md)   
 [DROP DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-audit-specification-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sys.fn_get_audit_file &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)   
 [sys.server_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)   
 [sys.server_file_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [sys.server_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [sys.server_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)   
 [sys.database_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [sys.database_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [sys.dm_server_audit_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys. dm_audit_class_type_map](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [Criar uma auditoria de servidor e uma especificação de auditoria de servidor](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
