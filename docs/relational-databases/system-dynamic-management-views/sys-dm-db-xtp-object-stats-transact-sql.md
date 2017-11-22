---
title: sys.DM db_xtp_object_stats (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/29/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_db_xtp_object_stats_TSQL
- sys.dm_db_xtp_object_stats
- dm_db_xtp_object_stats
- sys.dm_db_xtp_object_stats_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_db_xtp_object_stats dynamic management view
ms.assetid: 07300b59-3cab-4d3e-8138-5ea8f584f88f
caps.latest.revision: "18"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7b07eb152c42c2f9c991d99ff6e3256b62d1cef8
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmdbxtpobjectstats-transact-sql"></a>sys.dm_db_xtp_object_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Relata o número de linhas afetadas pelas operações em cada objeto [!INCLUDE[hek_2](../../includes/hek-2-md.md)] desde a última reinicialização do banco de dados. As estatísticas são atualizadas quando a operação é executada, independentemente de a transação ser confirmada ou revertida.  
  
 sys.dm_db_xtp_object_stats pode ajudar você a identificar quais tabelas com otimização de memória estão sendo mais alteradas. Você pode optar por remover os índices não utilizados ou raramente utilizados na tabela, já que cada índice afeta o desempenho. Se houver índices hash, você deve reavaliar periodicamente o número de buckets. Para obter mais informações, consulte [determinando o número de buckets correto para índices de Hash](http://msdn.microsoft.com/library/6d1ac280-87db-4bd8-ad43-54353647d8b5).  
  
 sys.dm_db_xtp_object_stats pode ajudar você a identificar quais tabelas com otimização de memória incorrerão em conflitos de gravação/gravação, o que pode afetar o desempenho do aplicativo. Por exemplo, se você tiver uma lógica de repetição de transação, a mesma instrução talvez precise ser executada mais de uma vez. Além disso, você pode usar essas informações para identificar as tabelas (e, portanto, a lógica de negócios) que requerem tratamento de erros de gravação/gravação.  
  
 A exibição contém uma linha para cada tabela com otimização de memória no banco de dados.  
  
 Para obter mais informações, veja [OLTP in-memory &#40;Otimização na memória&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
||  
|-|  
|**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
|Nome da coluna|Tipo de dados|Description|  
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
  
## <a name="see-also"></a>Consulte também  
 [Exibições de gerenciamento dinâmico de tabela com otimização de memória &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
