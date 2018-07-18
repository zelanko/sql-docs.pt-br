---
title: DM exec_distributed_request_steps (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f226ff8c5f18a0e812c6a457fe3382cb8f7b8d84
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37982588"
---
# <a name="sysdmexecdistributedrequeststeps-transact-sql"></a>sys.dm_exec_distributed_request_steps (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Contém informações sobre todas as etapas que compõem uma consulta ou uma determinada solicitação de PolyBase. Ele lista uma linha para cada etapa de consulta.  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**int**|execution_id e step_index constituem a chave para esta exibição. Id numérico exclusivo associado com a solicitação.|Consulte a ID na [. DM exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).|  
|step_index|**int**|A posição dessa etapa na sequência de etapas que formam a solicitação.|0 (n-1) para uma solicitação de n etapas.|  
|operation_type|**nvarchar(128)**|Tipo de operação representada por essa etapa.|'MoveOperation','OnOperation','RandomIDOperation','RemoteOperation','ReturnOperation','ShuffleMoveOperation','TempTablePropertiesOperation','DropDiagnosticsNotifyOperation', ‘HadoopShuffleOperation', ‘HadoopBroadCastOperation', ‘HadoopRoundRobinOperation'|  
|distribution_type|**nvarchar(32)**|Em que a etapa está em execução.|‘AllComputeNodes','AllDistributions','ComputeNode','Distribution','AllNodes','SubsetNodes','SubsetDistributions','Unspecified'.|  
|location_type|**nvarchar(32)**|Em que a etapa está em execução.|'Calcular', 'Principal' ou 'DMS'. Todas as etapas de movimentação de dados mostram 'DMS'.|  
|status|**nvarchar(32)**|Status desta etapa|'Pendente', 'Running', 'Completa', 'Falha', 'UndoFailed', 'PendingCancel', 'Cancelar', 'Desfeita', 'Anulada'|  
|error_id|**nvarchar(36)**|Id exclusiva do erro associado a esta etapa, se houver|Consulte a id da [sys.dm_exec_compute_node_errors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-errors-transact-sql.md), ele será nulo se nenhum erro ocorreu.|  
|start_time|**datetime**|Hora em que a etapa começou execução|Menor ou igual à hora atual e maior ou igual a end_compile_time da consulta ao qual pertence essa etapa.|  
|end_time|**datetime**|Hora em que esta etapa concluiu a execução, foi cancelada ou falhou.|Menor ou igual à hora atual e maior ou igual a start_time, definido como NULL para etapas atualmente em execução ou na fila.|  
|total_elapsed_time|**int**|Quantidade total de tempo de que execução a etapa de consulta, em milissegundos|Entre 0 e a diferença entre end_time e start_time. 0 para etapas em fila.|  
|row_count|**bigint**|Número total de linhas alteradas ou retornada por esta solicitação|0 para obter as etapas que não alterar ou retornar dados, o número de linhas afetadas, caso contrário. Defina como -1 para obter as etapas do DMS.|  
|command|nvarchar(4000)|Contém o texto completo do comando desta etapa.|Qualquer cadeia de caracteres de solicitação válida para uma etapa. Truncado se for maior que 4000 caracteres.|  
  
## <a name="see-also"></a>Consulte também  
 [Solução de problemas com exibições de gerenciamento dinâmico do PolyBase](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Banco de dados relacionados a exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
