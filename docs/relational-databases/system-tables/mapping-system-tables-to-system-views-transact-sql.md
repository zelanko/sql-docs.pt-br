---
title: Mapeando tabelas do sistema para exibições do sistema (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- catalog views [SQL Server], mapping system tables to
- mapping system tables to system views [SQL Server]
- system tables [SQL Server], mapping to catalog views
ms.assetid: a616fce9-b4c1-49da-87a7-9d6f74911d8f
caps.latest.revision: 43
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 7b28a62aa35225f3942c2bfd88bf19ed31a0e7bf
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="mapping-system-tables-to-system-views-transact-sql"></a>Mapeando tabelas do sistema para exibições do sistema (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Este tópico mostra o mapeamento entre tabelas e funções do sistema e exibições e funções do sistema.  
  
 A tabela a seguir mapeia as tabelas de sistema para exibições ou funções de sistema correspondentes no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
|Tabela do sistema|Exibições ou funções de sistema|Tipo de exibição ou função|  
|------------------|-------------------------------|------------------------------|  
|sysaltfiles|[sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)|Exibição de catálogo|  
|syscacheobjects|[sys.dm_exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)<br /><br /> [sys.DM exec_plan_attributes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-plan-attributes-transact-sql.md)<br /><br /> [sys.dm_exec_sql_text](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)<br /><br /> [sys.dm_exec_cached_plan_dependent_objects](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plan-dependent-objects-transact-sql.md)|Exibição de gerenciamento dinâmico<br /><br /> Exibição de gerenciamento dinâmico<br /><br /> Exibição de gerenciamento dinâmico<br /><br /> Exibição de gerenciamento dinâmico|  
|syscharsets|[sys.syscharsets](../../relational-databases/system-compatibility-views/sys-syscharsets-transact-sql.md)|Exibição de compatibilidade|  
|sysconfigures|[sys.configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)|Exibição de catálogo|  
|syscurconfigs|[sys.configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)|Exibição de catálogo|  
|sysdatabases|[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)|Exibição de catálogo|  
|sysdevices|[sys.backup_devices](../../relational-databases/system-catalog-views/sys-backup-devices-transact-sql.md)|Exibição de catálogo|  
|syslanguages|[sys.syslanguages](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)|Exibição de compatibilidade|  
|syslockinfo|[sys.dm_tran_locks](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)|Exibição de gerenciamento dinâmico|  
|syslocks|[sys.dm_tran_locks](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)|Exibição de gerenciamento dinâmico|  
|syslogins|[sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)<br /><br /> [sys.sql_logins](../../relational-databases/system-catalog-views/sys-sql-logins-transact-sql.md)|Exibição de catálogo|  
|sysmessages|[sys.messages](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)|Exibição de catálogo|  
|sysoledbusers|[sys.linked_logins](../../relational-databases/system-catalog-views/sys-linked-logins-transact-sql.md)|Exibição de catálogo|  
|sysopentapes|[sys.dm_io_backup_tapes](../../relational-databases/system-dynamic-management-views/sys-dm-io-backup-tapes-transact-sql.md)|Exibição de gerenciamento dinâmico|  
|sysperfinfo|[sys.dm_os_performance_counters](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)|Exibição de gerenciamento dinâmico|  
|sysprocesses|[sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md)<br /><br /> [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)<br /><br /> [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)|Exibição de gerenciamento dinâmico<br /><br /> Exibição de gerenciamento dinâmico<br /><br /> Exibição de gerenciamento dinâmico|  
|sysremotelogins|[sys.remote_logins](../../relational-databases/system-catalog-views/sys-remote-logins-transact-sql.md)|Exibição de catálogo|  
|sysservers|[sys.servers](../../relational-databases/system-catalog-views/sys-servers-transact-sql.md)|Exibição de catálogo|  
  
 A tabela a seguir mapeia as tabelas ou funções de sistema que estão em todos os bancos de dados do [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] para suas exibições e funções de sistemas correspondentes no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
|Tabela ou função de sistema|Exibição ou função de sistema|Tipo de exibição ou função|  
|------------------------------|-----------------------------|------------------------------|  
|fn_virtualfilestats|[sys.dm_io_virtual_file_stats](../../relational-databases/system-dynamic-management-views/sys-dm-io-virtual-file-stats-transact-sql.md)|Exibição de gerenciamento dinâmico|  
|syscolumns|[sys.columns](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)|Exibição de catálogo|  
|syscomments|[sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)|Exibição de catálogo|  
|sysconstraints|[sys.check_constraints](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md)<br /><br /> [sys.default_constraints](../../relational-databases/system-catalog-views/sys-default-constraints-transact-sql.md)<br /><br /> [sys.key_constraints](../../relational-databases/system-catalog-views/sys-key-constraints-transact-sql.md)<br /><br /> [sys.foreign_keys](../../relational-databases/system-catalog-views/sys-foreign-keys-transact-sql.md)|Exibição de catálogo<br /><br /> Exibição de catálogo<br /><br /> Exibição de catálogo<br /><br /> Exibição de catálogo|  
|sysdepends|[sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)|Exibição de catálogo|  
|sysfilegroups|[sys.filegroups](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)|Exibição de catálogo|  
|sysfiles|[sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)|Exibição de catálogo|  
|sysforeignkeys|[sys.foreign_key_columns](../../relational-databases/system-catalog-views/sys-foreign-key-columns-transact-sql.md)|Exibição de catálogo|  
|sysindexes|[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)<br /><br /> [sys.partitions](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)<br /><br /> [sys.allocation_units](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)<br /><br /> [sys.dm_db_partition_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md)|Exibição de catálogo<br /><br /> Exibição de catálogo<br /><br /> Exibição de catálogo<br /><br /> Exibição de gerenciamento dinâmico|  
|sysindexkeys|[sys.index_columns](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)|Exibição de catálogo|  
|sysmembers|[sys.database_role_members](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)|Exibição de catálogo|  
|sysobjects|[sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)|Exibição de catálogo|  
|syspermissions|[sys.database_permissions](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)<br /><br /> [sys.server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)|Exibição de catálogo<br /><br /> Exibição de catálogo|  
|sysprotects|[sys.database_permissions](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)<br /><br /> [sys.server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)|Exibição de catálogo<br /><br /> Exibição de catálogo|  
|sysreferences|[sys.foreign_keys](../../relational-databases/system-catalog-views/sys-foreign-keys-transact-sql.md)|Exibição de catálogo|  
|systypes|[sys.types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)|Exibição de catálogo|  
|sysusers|[sys.database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)|Exibição de catálogo|  
|sysfulltextcatalogs|[sys.fulltext_catalogs](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md)|Exibição de catálogo|  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Tabelas do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
