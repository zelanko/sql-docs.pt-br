---
description: sys.database_audit_specification_details (Transact-SQL)
title: sys. database_audit_specification_details (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/05/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- database_audit_specification_details
- sys.database_audit_specification_details_TSQL
- sys.database_audit_specification_details
- database_audit_specification_details_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_audit_specification_details catalog view
ms.assetid: 03fc60a9-1696-4109-b15e-a50046310859
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7130cda8c6c43b8bde1edda58d04c6d3fff0e5d0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88402352"
---
# <a name="sysdatabase_audit_specification_details-transact-sql"></a>sys.database_audit_specification_details (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contém informações sobre as especificações de auditoria de banco de dados em uma auditoria do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em uma instância de servidor para todos os bancos de dados. Para obter mais informações, veja [Auditoria do SQL Server &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md). Para obter uma lista de todos os audit_action_id e seus nomes, consulte [Sys. dm_audit_actions &#40;&#41;do Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md).  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**database_specification_id**|**int**|ID da especificação de auditoria.|  
|**audit_action_id**|**int**|ID da ação de auditoria.|  
|**audit_action_name**|**Sysname**|Nome de ação de auditoria ou do grupo de ações de auditoria|  
|**Classe**|**int**|Identifica a classe de objeto que está sendo auditado.|  
|**DESC class_**|**Nvarchar (60)**|Descrição da classe de objeto que está sendo auditado:<br /><br /> - SCHEMA<br /><br /> - TABLE|  
|**major_id**|**int**|ID principal do objeto que está sendo auditado, como uma ID de tabela de uma ação de Auditoria de Tabela.|  
|**minor_id**|**Int**|ID secundária do objeto que está sendo auditado, interpretada de acordo com a classe, como a ID de coluna de uma ação de Auditoria de Tabela.|  
|**audited_principal_id**|**int**|Entidade que está sendo examinada.|  
|**audited_result**|**Nvarchar (60)**|Resultados da ação de auditoria:<br /><br /> - SUCCESS AND FAILURE - SUCCESS<br /><br /> - FAILURE|  
|**is_group**|**Parte**|Mostra se o objeto é um grupo:<br /><br /> 0 – Não é um grupo<br /><br /> 1 – Grupo|  
  
## <a name="permissions"></a>Permissões  
 As entidades com as permissões **ALTER ANY DATABASE AUDIT** ou **View definition** , a função **dbo** e os membros da função de banco de dados fixa **db_owners** têm acesso a essa exibição de catálogo. Além disso, o principal não deve ter a permissão **View definition** negada.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [CRIAR auditoria de servidor &#40;&#41;Transact-SQL ](../../t-sql/statements/create-server-audit-transact-sql.md)   
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
 [sys.dm_server_audit_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys.dm_audit_actions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [sys.dm_audit_class_type_map &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [Criar uma auditoria de servidor e uma especificação de auditoria de servidor](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
