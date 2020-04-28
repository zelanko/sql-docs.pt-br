---
title: sys. server_audits (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/05/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- server_audits_TSQL
- sys.server_audits_TSQL
- sys.server_audits
- server_audits
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_audits catalog view
ms.assetid: c2c4a000-1127-46a8-b1e9-947fd1136e1e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0a00f6843a0ef379c12aa1d1d00df9380efbd139
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68125002"
---
# <a name="sysserver_audits-transact-sql"></a>sys.server_audits (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada auditoria do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em uma instância de servidor. Para obter mais informações, veja [Auditoria do SQL Server &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**audit_id**|**int**|ID da auditoria.|  
|**name**|**sysname**|Nome da auditoria.|  
|**audit_guid**|**uniqueidentifier**|GUID da auditoria usada para enumerar auditorias com servidor membro&#124;especificações de auditoria de banco de dados durante as operações de inicialização do servidor e de anexação do banco de dados.|  
|**create_date**|**datetime**|Data em UTC quando a auditoria foi criada.|  
|**modify_date**|**datetime**|Data em UTC da última alteração feita na especificação de auditoria.|  
|**principal_id**|**int**|ID do proprietário da auditoria, conforme registrado no servidor.|  
|**type**|**char(2)**|Tipo de auditoria:<br /><br /> SL-log de eventos de segurança NT<br /><br /> AL-log de eventos do aplicativo NT<br /><br /> FL-arquivo no sistema de arquivos|  
|**type_desc**|**nvarchar(60)**|SECURITY LOG<br /><br /> APPLICATION LOG<br /><br /> FILE|  
|**on_failure**|**tinyint**|Ao Falhar ao escrever uma entrada de ação:<br /><br /> 0-continuar<br /><br /> 1-instância do servidor de desligamento<br /><br /> 2-falha na operação|  
|**on_failure_desc**|**nvarchar(60)**|Ao Falhar ao escrever uma entrada de ação:<br /><br /> CONTINUE<br /><br /> SHUTDOWN SERVER INSTANCE<br /><br /> FAIL_OPERATION|  
|**is_state_enabled**|**tinyint**|0 - Desabilitado<br /><br /> 1 – Habilitado|  
|**queue_delay**|**int**|Tempo máximo, em milissegundos, de espera antes de gravar em disco. Se for 0, a auditoria garantirá uma gravação antes que o evento possa continuar.|  
|**predicado**|**nvarchar (3000)**|A expressão de predicado que é aplicada ao evento.|  
  
## <a name="permissions"></a>Permissões  
 As entidades com a permissão **ALTER ANY Server Audit** ou **View any Definition** têm acesso a essa exibição de catálogo. Além disso, a entidade de segurança não deve ser negada a permissão **View any Definition** .  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [CRIAR auditoria de servidor &#40;&#41;Transact-SQL](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [Descartar auditoria de servidor &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [CRIAR especificação de auditoria de servidor &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ESPECIFICAÇÃO de alteração de auditoria de servidor &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [ESPECIFICAÇÃO de auditoria DROP SERVER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [CRIAR especificação de auditoria de banco de dados &#40;&#41;Transact-SQL](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
 [ESPECIFICAÇÃO de auditoria ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-audit-specification-transact-sql.md)   
 [ESPECIFICAÇÃO de auditoria DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-audit-specification-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sys. fn_get_audit_file &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)   
 [sys. server_file_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [sys. server_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [sys. server_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)   
 [sys. database_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [sys. database_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [sys. dm_server_audit_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys. dm_audit_actions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [sys. dm_audit_class_type_map &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [Criar uma auditoria de servidor e uma especificação de auditoria de servidor](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
