---
description: sys.dm_db_xtp_object_stats (Transact-SQL)
title: sys.dm_db_xtp_object_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_xtp_object_stats_TSQL
- sys.dm_db_xtp_object_stats
- dm_db_xtp_object_stats
- sys.dm_db_xtp_object_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_object_stats dynamic management view
ms.assetid: 07300b59-3cab-4d3e-8138-5ea8f584f88f
author: markingmyname
ms.author: maghan
monikerRange: =azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a082e789e05a5ca59afb9db74790a5cfb54232d7
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97468467"
---
# <a name="sysdm_db_xtp_object_stats-transact-sql"></a>sys.dm_db_xtp_object_stats (Transact-SQL)
[!INCLUDE[sql-asdb-asdbmi](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

  Relata o número de linhas afetadas pelas operações em cada objeto [!INCLUDE[hek_2](../../includes/hek-2-md.md)] desde a última reinicialização do banco de dados. As estatísticas são atualizadas quando a operação é executada, independentemente de a transação ser confirmada ou revertida.  
  
 sys.dm_db_xtp_object_stats pode ajudar você a identificar quais tabelas com otimização de memória estão sendo mais alteradas. Você pode optar por remover os índices não utilizados ou raramente utilizados na tabela, já que cada índice afeta o desempenho. Se houver índices hash, você deve reavaliar periodicamente o número de buckets. Para obter mais informações, consulte [Determining the Correct Bucket Count for Hash Indexes](/previous-versions/sql/).  
  
 sys.dm_db_xtp_object_stats pode ajudar você a identificar quais tabelas com otimização de memória incorrerão em conflitos de gravação/gravação, o que pode afetar o desempenho do aplicativo. Por exemplo, se você tiver uma lógica de repetição de transação, a mesma instrução talvez precise ser executada mais de uma vez. Além disso, você pode usar essas informações para identificar as tabelas (e, portanto, a lógica de negócios) que requerem tratamento de erros de gravação/gravação.  
  
 A exibição contém uma linha para cada tabela com otimização de memória no banco de dados.  
  
 Para obter mais informações, veja [OLTP in-memory &#40;Otimização na memória&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|object_id|**bigint**|A ID do objeto.|  
|row_insert_attempts|**bigint**|O número de linhas inseridas na tabela desde a última reinicialização do banco de dados pelas transações confirmadas e anuladas.|  
|row_update_attempts|**bigint**|O número de linhas atualizadas na tabela desde a última reinicialização do banco de dados pelas transações confirmadas e anuladas.|  
|row_delete_attempts|**bigint**|O número de linhas excluídas da tabela desde a última reinicialização do banco de dados pelas transações confirmadas e anuladas.|  
|write_conflicts|**bigint**|O número de conflitos de gravação ocorridos desde a última reinicialização do banco de dados.|  
|unique_constraint_violations|**bigint**|O número de violações de restrição exclusivas que ocorreram desde a última reinicialização do banco de dados.|  
|object_address|**varbinary (8)**|Somente para uso interno.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW DATABASE STATE no banco de dados atual.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de gerenciamento dinâmico de tabela com otimização de memória &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
