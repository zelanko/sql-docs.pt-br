---
title: sys.dm_pdw_request_steps (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.suite: sql
ms.component: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: cc563e88-0d34-436e-b914-b60d6ee0d50b
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 5a6fbf843d3a9aca9172a5ab6ea828a0c0b0a40a
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38060288"
---
# <a name="sysdmpdwrequeststeps-transact-sql"></a>sys.dm_pdw_request_steps (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contém informações sobre todas as etapas que compõem uma determinada solicitação ou consulta no [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. Ele lista uma linha para cada etapa de consulta.  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|request_id e step_index constituem a chave para esta exibição.<br /><br /> Id numérico exclusivo associado com a solicitação.|Consulte request_id na [DM pdw_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|step_index|**int**|request_id e step_index constituem a chave para esta exibição.<br /><br /> A posição dessa etapa na sequência de etapas que formam a solicitação.|0 (n-1) para uma solicitação de n etapas.|  
|operation_type|**nvarchar(35)**|Tipo de operação representada por essa etapa.|**Operações de plano de consulta do DMS:** 'ReturnOperation', 'PartitionMoveOperation', 'MoveOperation', 'BroadcastMoveOperation', 'ShuffleMoveOperation', 'TrimMoveOperation', 'CopyOperation', 'DistributeReplicatedTableMoveOperation'<br /><br /> **Operações de plano de consulta SQL:** 'OnOperation', 'RemoteOperation'<br /><br /> **Outras operações do plano de consulta:** 'MetaDataCreateOperation', 'RandomIDOperation'<br /><br /> **Operações externas para leituras:** 'HadoopShuffleOperation', 'HadoopRoundRobinOperation', 'HadoopBroadcastOperation'<br /><br /> **Operações externas para o MapReduce:** 'HadoopJobOperation', 'HdfsDeleteOperation'<br /><br /> **Operações externas para gravações:** 'ExternalExportDistributedOperation', 'ExternalExportReplicatedOperation', 'ExternalExportControlOperation'<br /><br /> Para obter mais informações, consulte "Noções básicas sobre planos de consulta" no [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].|  
|distribution_type|**nvarchar(32)**|Tipo de distribuição que passará por essa etapa.|'AllNodes', 'AllDistributions', 'AllComputeNodes', 'ComputeNode', 'Distribution', 'SubsetNodes', 'SubsetDistributions', 'Unspecified'|  
|location_type|**nvarchar(32)**|Em que a etapa está em execução.|'Calcular', 'Control', 'DMS'|  
|status|**nvarchar(32)**|Status desta etapa.|Pendente, executando, completo e com falha, UndoFailed, PendingCancel, cancelado, desfeita, anulada|  
|error_id|**nvarchar(36)**|Id exclusiva do erro associado a esta etapa, se houver.|Consulte error_id dos [sys.dm_pdw_errors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md). NULL se nenhum erro tiver ocorrido.|  
|start_time|**datetime**|Hora em que a etapa começou a execução.|Menor ou igual à hora atual e maior ou igual a end_compile_time da consulta ao qual pertence essa etapa. Para obter mais informações sobre consultas, consulte [DM pdw_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|end_time|**datetime**|Hora em que esta etapa concluiu a execução, foi cancelada ou falhou.|Menor ou igual à hora atual e maior ou igual a start_time. Definido como NULL para etapas atualmente em execução ou na fila.|  
|total_elapsed_time|**int**|Quantidade total de tempo que a etapa de consulta estiver sendo executado, em milissegundos.|Entre 0 e a diferença entre end_time e start_time. 0 para etapas em fila.<br /><br /> Se total_elapsed_time exceder o valor máximo para um número inteiro, o total_elapsed_time continuará a ser o valor máximo. Essa condição gerará o aviso "o valor máximo foi excedido."<br /><br /> O valor máximo em milissegundos é equivalente a 24,8 dias.|  
|row_count|**bigint**|Número total de linhas alteradas ou retornada por esta solicitação.|0 para obter as etapas que não alterar ou retornar dados. Caso contrário, número de linhas afetadas.|  
|command|**nvarchar(4000)**|Contém o texto completo do comando desta etapa.|Qualquer cadeia de caracteres de solicitação válida para uma etapa. NULO quando a operação é do tipo MetaDataCreateOperation. Truncado se for maior que 4000 caracteres.|  
  
 Para obter informações sobre o máximo de linhas mantido por esta exibição, consulte a seção de valores máximos de modo de exibição de sistema nos "Mínimo e máximo valores" no [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse e Parallel Data Warehouse exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
