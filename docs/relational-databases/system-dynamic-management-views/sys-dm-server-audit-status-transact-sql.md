---
description: sys.dm_server_audit_status (Transact-SQL)
title: sys. dm_server_audit_status (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/19/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_server_audit_status_TSQL
- sys.dm_server_audit_status
- dm_server_audit_status
- sys.dm_server_audit_status_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_server_audit_status dynamic management view
ms.assetid: 4aa32d54-2ae1-437e-bbaa-7f1df1404b44
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b31883200fdbee9aa4039fca75e4b034ab75cebf
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543815"
---
# <a name="sysdm_server_audit_status-transact-sql"></a>sys.dm_server_audit_status (Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  Retorna uma linha para cada auditoria de servidor que indica o estado atual da auditoria. Para obter mais informações, veja [Auditoria do SQL Server &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**audit_id**|**int**|ID da auditoria. Mapeia para o campo **audit_id** na exibição do catálogo **Sys. Auditions** .|  
|**name**|**sysname**|Nome da auditoria. O mesmo que o campo **nome** na exibição de catálogo **Sys. server_audits** .|  
|**status**|**smallint**|Status numérico da auditoria de servidor:<br /><br /> 0 = não iniciado<br /><br /> 1 =<br />        Iniciado<br /><br /> 2 =<br />      Falha no tempo de execução<br /><br /> 3 = falha ao criar destino<br /><br /> 4 = desligando|  
|**status_desc**|**nvarchar(256)**|Cadeia de caracteres que mostra o status da auditoria de servidor:<br /><br /> NOT_STARTED<br /><br /> STARTED<br /><br /> RUNTIME_FAIL<br /><br /> TARGET_CREATION_FAILED<br /><br /> SHUTTING_DOWN|  
|**status_time**|**datetime2**|Carimbo de data e hora em UTC da última alteração de status da auditoria.|  
|**event_session_address**|**varbinary (8)**|Endereço da sessão de Eventos Estendidos associada à auditoria. Relacionado à exibição do catálogo **Sys. dm_xe_sessions. Address** .|  
|**audit_file_path**|**nvarchar(256)**|Caminho completo e nome de arquivo do destino do arquivo de auditoria que está sendo usado no momento. Populado somente para auditorias de arquivos.|  
|**audit_file_size**|**bigint**|Tamanho aproximado do arquivo de auditoria, em bytes. Populado somente para auditorias de arquivos.|  
  
## <a name="permissions"></a>Permissões  
 As entidades de segurança devem ter o **estado do servidor de exibição** e as permissões **selecionadas** .  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
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
 [sys. dm_server_audit_status](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys.dm_audit_actions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [sys.dm_audit_class_type_map &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [Criar uma auditoria de servidor e uma especificação de auditoria de servidor](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
