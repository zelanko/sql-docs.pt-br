---
title: Exibições de gerenciamento dinâmico da tabela com otimização de memória (Transact-SQL)
description: Saiba mais sobre as exibições de gerenciamento dinâmico SQL Server e exibições de catálogo de objetos usadas com In-Memory OLTP no SQL Server.
ms.custom: seo-dt-2019
ms.date: 02/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: ccd82fed-1a3f-47de-85c4-1c9bdd80b027
author: markingmyname
ms.author: maghan
monikerRange: =azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2b34047560dcf36f606ff1b95105c1bb64427c0b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97411484"
---
# <a name="memory-optimized-table-dynamic-management-views-transact-sql"></a>Exibições de gerenciamento dinâmico da tabela com otimização de memória (Transact-SQL)
[!INCLUDE[sql-asdb-asdbmi](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

  As seguintes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DMVs (exibições de gerenciamento dinâmico) são usadas com o OLTP In-Memory:  
  
 Para obter mais informações, veja [OLTP in-memory &#40;Otimização na memória&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  

:::row:::
    :::column:::
        [&#41;&#40;Transact-SQL de sys.dm_db_xtp_checkpoint_stats ](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-stats-transact-sql.md)

        [&#41;&#40;Transact-SQL de sys.dm_db_xtp_gc_cycle_stats ](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-gc-cycle-stats-transact-sql.md)

        [sys.dm_db_xtp_index_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-index-stats-transact-sql.md)

        [sys.dm_db_xtp_merge_requests (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-merge-requests-transact-sql.md)

        [sys.dm_db_xtp_nonclustered_index_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-nonclustered-index-stats-transact-sql.md)

        [&#41;&#40;Transact-SQL de sys.dm_db_xtp_transactions ](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-transactions-transact-sql.md)

        [&#41;&#40;Transact-SQL de sys.dm_xtp_gc_stats ](../../relational-databases/system-dynamic-management-views/sys-dm-xtp-gc-stats-transact-sql.md)

        [&#41;&#40;Transact-SQL de sys.dm_xtp_transaction_stats ](../../relational-databases/system-dynamic-management-views/sys-dm-xtp-transaction-stats-transact-sql.md)
    :::column-end:::
    :::column:::
        [&#41;&#40;Transact-SQL de sys.dm_db_xtp_checkpoint_files ](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql.md)

        [sys.dm_db_xtp_hash_index_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-hash-index-stats-transact-sql.md)

        [sys.dm_db_xtp_memory_consumers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-memory-consumers-transact-sql.md)

        [sys.dm_db_xtp_object_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-object-stats-transact-sql.md)

        [sys.dm_db_xtp_table_memory_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-table-memory-stats-transact-sql.md)

        [&#41;&#40;Transact-SQL de sys.dm_xtp_gc_queue_stats ](../../relational-databases/system-dynamic-management-views/sys-dm-xtp-gc-queue-stats-transact-sql.md)

        [&#41;&#40;Transact-SQL de sys.dm_xtp_system_memory_consumers ](../../relational-databases/system-dynamic-management-views/sys-dm-xtp-system-memory-consumers-transact-sql.md)
    :::column-end:::
:::row-end:::

### <a name="object-catalog-views"></a>Exibições do catálogo de objeto

As exibições de catálogo de objetos a seguir são usadas especificamente com In-Memory OLTP.

:::row:::
    :::column:::
        [sys.hash_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-hash-indexes-transact-sql.md)
    :::column-end:::
    :::column:::
        [sys.memory_optimized_tables_internal_attributes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-memory-optimized-tables-internal-attributes-transact-sql.md)
    :::column-end:::
:::row-end:::

### <a name="internal-dmvs"></a>DMVs internos

Há DMVs adicionais que se destinam somente ao uso interno e para os quais não fornecemos nenhuma documentação direta. Na área de tabelas com otimização de memória, DMVs não documentados incluem o seguinte:

- sys.dm_xtp_threads
- sys.dm_xtp_transaction_recent_rows

