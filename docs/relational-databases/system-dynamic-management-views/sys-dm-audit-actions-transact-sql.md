---
title: sys.dm_audit_actions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_audit_actions_TSQL
- sys.dm_audit_actions
- dm_audit_actions_TSQL
- dm_audit_actions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_audit_actions dynamic management view
ms.assetid: b987c2b9-998a-4a5f-a82d-280dc6963cbe
caps.latest.revision: 19
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 70880a3dbc4f4f7ba76d8beaec6f8371a4e8de39
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmauditactions-transact-sql"></a>sys.dm_audit_actions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha para cada ação de auditoria que pode ser reportada no log de auditoria e para cada grupo de ação de auditoria que pode ser configurado como parte do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Audit. Para obter mais informações sobre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auditoria, consulte [SQL Server Audit &#40;mecanismo de banco de dados&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**action_id**|**varchar(4)**|ID da ação de auditoria. Relacionados para o **action_id** valor gravado para cada registro de auditoria. Permite valor nulo. É NULL para grupos de auditoria.|  
|**action_in_log**|**bit**|Indica se uma ação pode ser gravada em um log de auditoria. Os valores são da seguinte maneira:<br /><br /> 1 = Sim<br /><br /> 0 = Não|  
|**name**|**sysname**|Nome da ação de auditoria ou do grupo de ações de auditoria. Não permite valor nulo.|  
|**class_desc**|**nvarchar(120)**|O nome da classe do objeto ao qual a ação de auditoria aplica-se. Pode ser qualquer objeto do escopo Servidor, Banco de dados ou Esquema, mas não inclui objetos Esquema. Não permite valor nulo.|  
|**parent_class_desc**|**nvarchar(120)**|Nome da classe pai do objeto descrito por class_desc. Será NULL se class_desc for Servidor.|  
|**covering_parent_action_name**|**nvarchar(120)**|Nome da ação de auditoria ou do grupo de auditoria que contém a ação de auditoria descrita nesta linha. É usada para criar uma hierarquia de ações e ações abrangentes. Permite valor nulo.|  
|**configuration_level**|**nvarchar(10)**|Indica que a ação ou o grupo de ações especificado nessa linha são configuráveis no nível do Grupo ou da Ação. Será NULL se a ação não for configurável.|  
|**containing_group_name**|**nvarchar(120)**|O nome do grupo de auditoria que contém a ação especificada. Será NULL se o valor em name for um grupo.|  
  
## <a name="permissions"></a>Permissões  
 As entidades devem ter **selecione** permissão. Por padrão, é concedida a Público.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]. Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT  &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT  &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
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
 [sys.dm_audit_class_type_map &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [Criar uma auditoria de servidor e uma especificação de auditoria de servidor](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
