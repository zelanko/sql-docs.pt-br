---
title: sys.dm_pdw_request_steps (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/01/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: dmv's
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: cc563e88-0d34-436e-b914-b60d6ee0d50b
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3c98aeb3ebc26d6ffd762e301c915b1522ce888a
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmpdwrequeststeps-transact-sql"></a>sys.dm_pdw_request_steps (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contém informações sobre todas as etapas que compõem uma determinada solicitação ou de consulta em [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. Ele lista uma linha por etapa de consulta.  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|request_id e step_index constituem a chave para este modo de exibição.<br /><br /> Id numérico exclusivo associado à solicitação.|Consulte request_id em [sys.dm_pdw_exec_requests &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|step_index|**Int**|request_id e step_index constituem a chave para este modo de exibição.<br /><br /> A posição dessa etapa na sequência de etapas que compõem a solicitação.|0 (n-1) para uma solicitação de n etapas.|  
|operation_type|**nvarchar(35)**|Tipo de operação representado por essa etapa.|**Operações do plano de consulta do DMS:** 'ReturnOperation', 'PartitionMoveOperation', 'MoveOperation', 'BroadcastMoveOperation', 'ShuffleMoveOperation', 'TrimMoveOperation', 'CopyOperation', 'DistributeReplicatedTableMoveOperation'<br /><br /> **Operações de plano de consulta SQL:** 'OnOperation', 'RemoteOperation'<br /><br /> **Outras operações do plano de consulta:** 'MetaDataCreateOperation', 'RandomIDOperation'<br /><br /> **Operações externas para leituras:** 'HadoopShuffleOperation', 'HadoopRoundRobinOperation', 'HadoopBroadcastOperation'<br /><br /> **Operações externas de MapReduce:** 'HadoopJobOperation', 'HdfsDeleteOperation'<br /><br /> **Operações externas para gravações:** 'ExternalExportDistributedOperation', 'ExternalExportReplicatedOperation', 'ExternalExportControlOperation'<br /><br /> Para obter mais informações, consulte "Noções básicas sobre planos de consulta" o [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].|  
|distribution_type|**nvarchar(32)**|Tipo de distribuição que passará por essa etapa.|'AllNodes', 'AllDistributions', 'AllComputeNodes', 'ComputeNode', 'Distribution', 'SubsetNodes', 'SubsetDistributions', 'Unspecified'|  
|location_type|**nvarchar(32)**|Onde a etapa está em execução.|'Compute', 'Controle', 'DMS'|  
|status|**nvarchar(32)**|Status desta etapa.|Pendente, executando, completo e com falha, UndoFailed, PendingCancel, cancelado, desfeita, cancelada|  
|error_id|**nvarchar(36)**|Id exclusiva do erro associado a essa etapa, se houver algum.|Consulte error_id de [sys.dm_pdw_errors &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md). NULL se nenhum erro ocorreu.|  
|start_time|**datetime**|Hora em que a etapa iniciou a execução.|Menor ou igual à hora atual e maior ou igual a end_compile_time da consulta ao qual pertence essa etapa. Para obter mais informações sobre consultas, consulte [sys.dm_pdw_exec_requests &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|end_time|**datetime**|Hora em que esta etapa concluiu a execução, foi cancelada ou falha.|Menor ou igual à hora atual e maior ou igual a start_time. Definido como NULL para etapas atualmente em execução ou na fila.|  
|total_elapsed_time|**Int**|Quantidade total de tempo que a etapa de consulta está em execução, em milissegundos.|Entre 0 e a diferença entre start_time e end_time. 0 para etapas em fila.<br /><br /> Se total_elapsed_time excede o valor máximo para um inteiro, total_elapsed_time continuará a ser o valor máximo. Essa condição gerará o aviso "o valor máximo foi excedido."<br /><br /> O valor máximo em milissegundos é equivalente a 24.8 dias.|  
|row_count|**bigint**|Número total de linhas alteradas ou retornado por essa solicitação.|0 para as etapas que não alterar ou retornar dados. Caso contrário, número de linhas afetadas.|  
|command|**nvarchar(4000)**|Contém o texto completo do comando desta etapa.|Qualquer cadeia de caracteres de solicitação válida para uma etapa. NULL quando a operação é do tipo MetaDataCreateOperation. Truncado se mais de 4000 caracteres.|  
  
 Para obter informações sobre o máximo de linhas mantido por esta exibição, consulte a seção de valores máximos de modo de exibição de sistema nos "Mínimo e máximo valores" no [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse e exibições de gerenciamento dinâmico do Parallel Data Warehouse &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
