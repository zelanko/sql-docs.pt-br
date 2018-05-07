---
title: sys.dm_db_xtp_index_stats (Transact-SQL) | Microsoft Docs
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
- sys.dm_db_xtp_index_stats
- dm_db_xtp_index_stats
- sys.dm_db_xtp_index_stats_TSQL
- dm_db_xtp_index_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_index_stats dynamic management view
ms.assetid: 8d0a50b8-2015-4576-930f-e3307dfc888e
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: ab42288073de559c6f691fd18672a7a4adc3f60e
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmdbxtpindexstats-transact-sql"></a>sys.dm_db_xtp_index_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Contém estatísticas coletadas desde a última reinicialização do banco de dados.  
  
 Para obter mais informações, consulte [OLTP na memória &#40;otimização na memória&#41; ](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md) e [diretrizes para usar índices em tabelas com otimização de memória](http://msdn.microsoft.com/library/16ef63a4-367a-46ac-917d-9eebc81ab29b).  

  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|object_id|**bigint**|ID do objeto ao qual este índice pertence.|  
|xtp_object_id|**bigint**|ID interna correspondente para a versão atual do objeto.<br /><br /> Observação: Se aplica a [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].|  
|index_id|**bigint**|ID do índice. O index_id só é exclusivo dentro do objeto.|  
|scans_started|**bigint**|Número de verificações de índice OLTP na memória executadas. Cada seleção, inserção, atualização ou exclusão exige uma verificação de índice.|  
|scans_retries|**bigint**|Número de verificações de índice que precisavam ser tentadas novamente,|  
|rows_returned|**bigint**|O número cumulativo de linhas retornadas desde que a tabela foi criada ou o início do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|rows_touched|**bigint**|O número cumulativo de linhas acessadas desde que a tabela foi criada ou o início do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|rows_expiring|**bigint**|Somente para uso interno.|  
|rows_expired|**bigint**|Somente para uso interno.|  
|rows_expired_removed|**bigint**|Somente para uso interno.|  
|phantom_scans_started|**bigint**|Somente para uso interno.|  
|phatom_scans_retries|**bigint**|Somente para uso interno.|  
|phantom_rows_touched|**bigint**|Somente para uso interno.|  
|phantom_expiring_rows_encountered|**bigint**|Somente para uso interno.|  
|phantom_expired_rows_encountered|**bigint**|Somente para uso interno.|  
|phantom_expired_removed_rows_encountered|**bigint**|Somente para uso interno.|  
|phantom_expired_rows_removed|**bigint**|Somente para uso interno.|  
|object_address|**varbinary(8)**|Somente para uso interno.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW DATABASE STATE no banco de dados atual.  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de gerenciamento dinâmico de tabela de otimização de memória &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
