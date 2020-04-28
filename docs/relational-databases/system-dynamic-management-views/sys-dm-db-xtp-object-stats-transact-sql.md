---
title: sys. dm_db_xtp_object_stats (Transact-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e14d5162c15f38cf741ceead94c2bacb230c42a8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68043168"
---
# <a name="sysdm_db_xtp_object_stats-transact-sql"></a>sys.dm_db_xtp_object_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Relata o número de linhas afetadas pelas operações em cada objeto [!INCLUDE[hek_2](../../includes/hek-2-md.md)] desde a última reinicialização do banco de dados. As estatísticas são atualizadas quando a operação é executada, independentemente de a transação ser confirmada ou revertida.  
  
 sys.dm_db_xtp_object_stats pode ajudar você a identificar quais tabelas com otimização de memória estão sendo mais alteradas. Você pode optar por remover os índices não utilizados ou raramente utilizados na tabela, já que cada índice afeta o desempenho. Se houver índices hash, você deve reavaliar periodicamente o número de buckets. Para obter mais informações, consulte [Determining the Correct Bucket Count for Hash Indexes](https://msdn.microsoft.com/library/6d1ac280-87db-4bd8-ad43-54353647d8b5).  
  
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
  
  
