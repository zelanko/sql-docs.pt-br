---
title: database_audit_specifications (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/05/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- database_audit_specifications_TSQL
- sys.database_audit_specifications_TSQL
- sys.database_audit_specifications
- database_audit_specifications
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_audit_specifications catalog view
ms.assetid: bf80e5c6-0588-4eb7-86ff-aa7c73461335
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bf5f584a556db9e32fcaf1f53b907adcb8d08e25
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52522977"
---
# <a name="sysdatabaseauditspecifications-transact-sql"></a>database_audit_specifications (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém informações sobre as especificações de auditoria do banco de dados de uma auditoria do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em uma instância de servidor. Para obter mais informações, veja [Auditoria do SQL Server &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|Nome|**sysname**|Nome da especificação de auditoria.|  
|database_specification_id|**int**|ID da especificação do banco de dados.|  
|create_date|**datetime**|Data de criação da especificação de auditoria.|  
|modified_date|**datetime**|Data da última alteração feita na especificação de auditoria.|  
|is_state_enabled|**bit**|Estado da especificação de auditoria:<br /><br /> 0 - DESABILITADO<br /><br /> 1 - HABILITADO|  
|audit_GUID|**uniqueidentifer**|GUID da auditoria que contém essa especificação. É usada durante a enumeração das especificações de auditoria do banco de dados membro durante a anexação/inicialização do banco de dados.|  
  
## <a name="remarks"></a>Comentários  
 Se o banco de dados estiver no modo somente leitura, o recurso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Audit não poderá adicionar Especificações de Auditoria de Banco de Dados.  
  
## <a name="permissions"></a>Permissões  
 Entidades de segurança com o **ALTER ANY DATABASE AUDIT** ou **VIEW DEFINITION** permissões, a função dbo e os membros da função de banco de dados fixa db_owners têm acesso a essa exibição de catálogo. Além disso, a entidade de segurança não deve ser negada **VIEW DEFINITION** permissão.  
  
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
 [sys.database_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [sys.dm_server_audit_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys.dm_audit_actions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [sys.dm_audit_class_type_map &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [Criar uma auditoria de servidor e uma especificação de auditoria de servidor](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
