---
title: sys.dm_db_xtp_transactions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_xtp_transactions
- sys.dm_db_xtp_transactions_TSQL
- dm_db_xtp_transactions
- dm_db_xtp_transactions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_transactions dynamic management view
ms.assetid: 5c1a0a7a-e851-4b6f-8dfd-c9655fbf5a51
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b7d8a993e93795d7aaa5d0e1da958aed89b8c20f
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmdbxtptransactions-transact-sql"></a>sys.dm_db_xtp_transactions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Relata as transações ativas no mecanismo de banco de dados OLTP na memória.  
  
 Para obter mais informações, veja [OLTP in-memory &#40;Otimização na memória&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
    
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|xtp_transaction_id|**bigint**|ID interna dessa transação no gerenciador de transações XTP.|  
|transaction_id|**bigint**|A ID da transação. Junções com a ID da transação em outros DMVs relacionados, como sys.dm_tran_active_transactions.<br /><br /> 0 para transações somente XTP, como as transações iniciadas por procedimentos armazenados compilados nativamente.|  
|session_id|**smallint**|O identificador da sessão que está executando essa transação. Junções com sys.dm_exec_sessions.|  
|begin_tsn|**bigint**|Número de série inicial da transação.|  
|end_tsn|**bigint**|Número de série final da transação.|  
|state|**Int**|O estado da transação:<br /><br /> 0=ACTIVE<br /><br /> 1=COMMITTED<br /><br /> 2=ABORTED<br /><br /> 3=VALIDATING|  
|state_desc|**nvarchar**|A descrição do estado da transação.|  
|result|**Int**|O resultado dessa transação. Veja os valores possíveis a seguir:<br /><br /> 0 - IN PROGRESS<br /><br /> 1 - SUCCESS<br /><br /> 2 = ERROR<br /><br /> 3 - COMMIT DEPENDENCY<br /><br /> 4 - VALIDATION FAILED (RR)<br /><br /> 5 - VALIDATION FAILED (SR)<br /><br /> 6 - ROLLBACK|  
|result_desc|**nvarchar**|O resultado dessa transação. Veja os valores possíveis a seguir:<br /><br /> IN PROGRESS<br /><br /> SUCCESS<br /><br /> ERROR<br /><br /> COMMIT DEPENDENCY<br /><br /> VALIDATION FAILED (RR)<br /><br /> VALIDATION FAILED (SR)<br /><br /> ROLLBACK|  
|last_error|**Int**|Somente para uso interno|  
|is_speculative|**bit**|Somente para uso interno|  
|is_prepared|**bit**|Somente para uso interno|  
|is_delayed_durability|**bit**|Somente para uso interno|  
|memory_address|**varbinary**|Somente para uso interno|  
|database_address|**varbinary**|Somente para uso interno|  
|thread_id|**Int**|Somente para uso interno|  
|read_set_row_count|**Int**|Somente para uso interno|  
|write_set_row_count|**Int**|Somente para uso interno|  
|scan_set_count|**Int**|Somente para uso interno|  
|savepoint_garbage_count|**Int**|Somente para uso interno|  
|log_bytes_required|**bigint**|Somente para uso interno|  
|count_of_allocations|**Int**|Somente para uso interno|  
|allocated_bytes|**Int**|Somente para uso interno|  
|reserved_bytes|**Int**|Somente para uso interno|  
|commit_dependency_count|**Int**|Somente para uso interno|  
|commit_dependency_total_attempt_count|**Int**|Somente para uso interno|  
|scan_area|**Int**|Somente para uso interno|  
|scan_area_desc|**nvarchar**|Somente para uso interno|  
|scan_location|**Int**|Somente para uso interno.|  
|dependent_1_address|**varbinary(8)**|Somente para uso interno|  
|dependent_2_address|**varbinary(8)**|Somente para uso interno|  
|dependent_3_address|**varbinary(8)**|Somente para uso interno|  
|dependent_4_address|**varbinary(8)**|Somente para uso interno|  
|dependent_5_address|**varbinary(8)**|Somente para uso interno|  
|dependent_6_address|**varbinary(8)**|Somente para uso interno|  
|dependent_7_address|**varbinary(8)**|Somente para uso interno|  
|dependent_8_address|**varbinary(8)**|Somente para uso interno|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW DATABASE STATE no servidor.  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de gerenciamento dinâmico de tabela de otimização de memória &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
