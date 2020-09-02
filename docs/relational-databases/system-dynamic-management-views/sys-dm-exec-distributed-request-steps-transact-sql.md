---
description: sys. dm_exec_distributed_request_steps (Transact-SQL)
title: sys. dm_exec_distributed_request_steps (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SYS.DM_EXEC_DISTRIBUTED_REQUEST_STEPS_TSQL
- DM_EXEC_DISTRIBUTED_REQUEST_STEPS_TSQL
- DM_EXEC_DISTRIBUTED_REQUEST_STEPS
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- PolyBase
- dm_exec_distributed_request_steps
- sys.dm_exec_distributed_request_steps management view
ms.assetid: 1954541d-b716-4e03-8fcc-7022f428e01d
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 91cd131d3ebc226a8865710ef27161f55ac2ea1f
ms.sourcegitcommit: 5da46e16b2c9710414fe36af9670461fb07555dc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/01/2020
ms.locfileid: "89283707"
---
# <a name="sysdm_exec_distributed_request_steps-transact-sql"></a>sys. dm_exec_distributed_request_steps (Transact-SQL)
[!INCLUDE [sqlserver2016-asa-pdw](../../includes/applies-to-version/sqlserver2016-asa-pdw.md)]

  Contém informações sobre todas as etapas que compõem uma determinada solicitação ou consulta do polybase. Ele lista uma linha por etapa de consulta.  
  
|Nome da coluna|Tipo de Dados|DESCRIÇÃO|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**int**|execution_id e step_index compõem a chave para essa exibição. ID numérica exclusiva associada à solicitação.|Consulte a ID em [Sys. dm_exec_requests &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).|  
|step_index|**int**|A posição desta etapa na sequência de etapas que compõem a solicitação.|0 a (n-1) para uma solicitação com n etapas.|  
|operation_type|**nvarchar(128)**|Tipo da operação representada por esta etapa.|' MoveOperation ', ' OnOperation ', ' RandomIDOperation ', ' RemoteOperation ', ' ReturnOperation ', ' ShuffleMoveOperation ', ' TempTablePropertiesOperation ', ' DropDiagnosticsNotifyOperation ', ' HadoopShuffleOperation ', ' HadoopBroadCastOperation ', ' HadoopRoundRobinOperation '|  
|distribution_type|**nvarchar(32)**|Onde a etapa está em execução.|' AllComputeNodes ', ' aldistribuitions ', ' ComputeNode ', ' Distribution ', ' subnós ', ' SubsetNodes ', ' SubsetDistributions ', ' não especificado '.|  
|location_type|**nvarchar(32)**|Onde a etapa está em execução.|"Compute", "Head" ou "DMS". Todas as etapas de movimentação de dados mostram ' DMS '.|  
|status|**nvarchar(32)**|Status desta etapa|' Pendente ', ' em execução ', ' Concluído ', ' falha ', ' UndoFailed ', ' PendingCancel ', ' cancelado ', ' desfeito ', ' anulado '|  
|error_id|**nvarchar (36)**|ID exclusiva do erro associado a esta etapa, se houver|Consulte a ID de [Sys. dm_exec_compute_node_errors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-errors-transact-sql.md), NULL se não ocorreu nenhum erro.|  
|start_time|**datetime**|Hora em que a execução da etapa foi iniciada|Menor ou igual à hora atual e maior ou igual a end_compile_time da consulta à qual essa etapa pertence.|  
|end_time|**datetime**|A hora em que esta etapa concluiu a execução, foi cancelada ou falhou.|Menor ou igual à hora atual e maior ou igual a start_time, definido como nulo para as etapas atualmente em execução ou na fila.|  
|total_elapsed_time|**int**|Quantidade total de tempo que a etapa de consulta foi executada, em milissegundos|Entre 0 e a diferença entre end_time e start_time. 0 para etapas em fila.|  
|row_count|**bigint**|Número total de linhas alteradas ou retornadas por esta solicitação|0 para etapas que não mudaram ou retornarem dados, o número de linhas afetadas de outra forma. Defina como-1 para as etapas de DMS.|  
|.|nvarchar(4000)|Mantém o texto completo do comando desta etapa.|Qualquer cadeia de caracteres de solicitação válida para uma etapa. Truncado se tiver mais de 4000 caracteres.|  
  
## <a name="see-also"></a>Consulte Também  
 [Solução de problemas do polybase com exibições de gerenciamento dinâmico](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Exibições de gerenciamento dinâmico relacionadas ao banco de dados &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
