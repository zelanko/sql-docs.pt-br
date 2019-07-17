---
title: sys. server_file_audits (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/05/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- server_file_audits_TSQL
- sys.server_file_audits_TSQL
- sys.server_file_audits
- server_file_audits
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_file_audits catalog view
ms.assetid: 553288a0-be57-4d79-ae53-b7cbd065e127
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7b3ed8e08d333c4aed2576154c645a0050ebf4df
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68133128"
---
# <a name="sysserverfileaudits-transact-sql"></a>sys.server_file_audits (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém informações estendidas sobre o tipo de auditoria de arquivo em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de auditoria em uma instância de servidor. Para obter mais informações, veja [Auditoria do SQL Server &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|audit_id|**int**|ID da auditoria.|  
|name|**sysname**|Nome da auditoria.|  
|audit_guid|**uniqueidentifier**|GUID da auditoria.|  
|create_date|**datetime**|Data UTC quando a auditoria do arquivo foi criada.|  
|modify_date|**datatime**|Data em UTC quando a auditoria do arquivo foi modificada pela última vez.|  
|principal_id|**int**|ID do proprietário da auditoria conforme registrado no servidor.|  
|type|**char(2)**|Tipo de auditoria:<br /><br /> 0 = log de eventos de Segurança do NT<br /><br /> 1 = log de eventos de Aplicativos do NT<br /><br /> 2= arquivo no sistema de arquivos|  
|type_desc|**nvarchar(60)**|Descrição do tipo da auditoria.|  
|on_failure|**tinyint**|Condição Ao falhar:<br /><br /> 0 = Continuar<br /><br /> 1 = Encerrar a instância de servidor<br /><br /> 2 = Operação com falha|  
|on_failure_desc|**nvarchar(60)**|Ao Falhar ao escrever uma entrada de ação:<br /><br /> CONTINUE<br /><br /> SHUTDOWN SERVER INSTANCE<br /><br /> FAIL OPERATION|  
|is_state_enabled|**tinyint**|0 = Desabilitado<br /><br /> 1 = Habilitado|  
|queue_delay|**int**|Tempo máximo sugerido, em milissegundos, para espera antes de gravar no disco. Se for 0, a auditoria garantirá uma gravação para que o evento possa continuar.|  
|predicate|**nvarchar(8000)**|Expressão de predicado que é aplicada ao evento.|  
|max_file_size|**bigint**|Tamanho máximo, em megabytes, da auditoria:<br /><br /> 0 = Ilimitado/Não aplicável ao tipo de auditoria selecionada.|  
|max_rollover_files|**int**|Número máximo de arquivos a serem usados com a opção de substituição.|  
|max_files|**int**|Número máximo de arquivos a serem usados sem a opção de substituição.|  
|reserved_disk_space|**int**|Quantidade de espaço em disco a ser reservada por arquivo.|  
|log_file_path|**nvarchar(260)**|Caminho onde a auditoria está localizada. Caminho de arquivo para auditoria de arquivo, caminho de log de aplicativo para auditoria de log de aplicativo.|  
|log_file_name|**nvarchar(260)**|Nome de base do arquivo de log fornecido em CREATE AUDIT DDL. Um número incremental é adicionado ao arquivo base_log_name como um sufixo para criar o nome de arquivo de log.|  
  
## <a name="permissions"></a>Permissões  
 Entidades de segurança com o **ALTER ANY SERVER AUDIT** ou **VIEW ANY DEFINITION** permissão têm acesso a esta exibição do catálogo. Além disso, a entidade de segurança não deve ser negada **VIEW ANY DEFINITION** permissão.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
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
 [sys. server_file_audits (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [sys.server_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [sys.database_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [sys.database_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [sys.dm_server_audit_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys.dm_audit_actions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [sys.dm_audit_class_type_map &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [Criar uma auditoria de servidor e uma especificação de auditoria de servidor](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
