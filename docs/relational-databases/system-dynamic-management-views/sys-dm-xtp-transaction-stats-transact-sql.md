---
title: sys. dm_xtp_transaction_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_xtp_transaction_stats_TSQL
- dm_xtp_transaction_stats
- sys.dm_xtp_transaction_stats_TSQL
- sys.dm_xtp_transaction_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xtp_transaction_stats dynamic management view
ms.assetid: 9389f48d-0de5-47bd-9821-4db8f04504e4
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9d238313d97ff3e509803d284efa3cfd9b8d6a9f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85647978"
---
# <a name="sysdm_xtp_transaction_stats-transact-sql"></a>sys.dm_xtp_transaction_stats (Transact-SQL)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Relata estatísticas sobre as transações que foram executadas desde que o servidor foi iniciado.  
  
 Para obter mais informações, veja [OLTP in-memory &#40;Otimização na memória&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|total_count|**bigint**|O número total de transações que foram executadas no mecanismo de banco de dados OLTP na memória.|  
|read_only_count|**bigint**|O número de transações somente leitura.|  
|total_aborts|**bigint**|Número total de transações que foram anuladas, por meio de anulação de usuário ou de sistema.|  
|user_aborts|**bigint**|Número de anulações iniciadas pelo sistema. Por exemplo, devido a conflitos de gravação, falhas de validação ou falhas de dependência.|  
|validation_failures|**bigint**|O número de vezes que uma transação foi anulada devido a uma falha de validação.|  
|dependencies_taken|**bigint**|Somente para uso interno.|  
|dependencies_failed|**bigint**|O número de vezes que uma transação foi anulada porque uma transação da qual ela era dependente foi anulada.|  
|savepoint_create|**bigint**|O número de pontos de salvamento criados. Um novo ponto de salvamento é criado para cada bloco atômico.|  
|savepoint_rollbacks|**bigint**|O número de reversões para um ponto de salvamento anterior.|  
|savepoint_refreshes|**bigint**|Somente para uso interno.|  
|log_bytes_written|**bigint**|Número total de bytes escritos nos registros de log de OLTP na memória.|  
|log_IO_count|**bigint**|Número total de transações que exigem E/S de log. Considera apenas as transações em tabelas duráveis.|  
|phantom_scans_started|**bigint**|Somente para uso interno.|  
|phatom_scans_retries|**bigint**|Somente para uso interno.|  
|phantom_rows_touched|**bigint**|Somente para uso interno.|  
|phantom_rows_expiring|**bigint**|Somente para uso interno.|  
|phantom_rows_expired|**bigint**|Somente para uso interno.|  
|phantom_rows_expired_removed|**bigint**|Somente para uso interno.|  
|scans_started|**bigint**|Somente para uso interno.|  
|scans_retried|**bigint**|Somente para uso interno.|  
|rows_returned|**bigint**|Somente para uso interno.|  
|rows_touched|**bigint**|Somente para uso interno.|  
|rows_expiring|**bigint**|Somente para uso interno.|  
|rows_expired|**bigint**|Somente para uso interno.|  
|rows_expired_removed|**bigint**|Somente para uso interno.|  
|rows_inserted|**bigint**|Somente para uso interno.|  
|rows_updated|**bigint**|Somente para uso interno.|  
|rows_deleted|**bigint**|Somente para uso interno.|  
|write_conflicts|**bigint**|Somente para uso interno.|  
|unique_constraint_violations|**bigint**|Número total de violações de restrição exclusiva.|  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de gerenciamento dinâmico de tabela com otimização de memória &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
