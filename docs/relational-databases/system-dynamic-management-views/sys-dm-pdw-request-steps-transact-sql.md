---
description: sys. dm_pdw_request_steps (Transact-SQL)
title: sys. dm_pdw_request_steps (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/19/2020
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: cc563e88-0d34-436e-b914-b60d6ee0d50b
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 4144e068354d43e2e8a5f9ea5bd6af7ad40a0e6d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88489721"
---
# <a name="sysdm_pdw_request_steps-transact-sql"></a>sys. dm_pdw_request_steps (Transact-SQL)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Contém informações sobre todas as etapas que compõem uma determinada solicitação ou consulta no [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] . Ele lista uma linha por etapa de consulta.  
  
|Nome da coluna|Tipo de Dados|DESCRIÇÃO|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|request_id e step_index compõem a chave para essa exibição.<br /><br /> ID numérica exclusiva associada à solicitação.|Consulte request_id em [Sys. dm_pdw_exec_requests &#40;&#41;do Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|step_index|**int**|request_id e step_index compõem a chave para essa exibição.<br /><br /> A posição desta etapa na sequência de etapas que compõem a solicitação.|0 a (n-1) para uma solicitação com n etapas.|  
|operation_type|**nvarchar(35)**|Tipo de operação representada por esta etapa.|**Operações do plano de consulta DMS:** ' ReturnOperation ', ' PartitionMoveOperation ', ' MoveOperation ', ' BroadcastMoveOperation ', ' ShuffleMoveOperation ', ' TrimMoveOperation ', ' CopyOperation ', ' DistributeReplicatedTableMoveOperation '<br /><br /> **Operações do plano de consulta SQL:** ' OnOperation ', ' RemoteOperation '<br /><br /> **Outras operações do plano de consulta:** 'MetaDataCreateOperation', 'RandomIDOperation'<br /><br /> **Operações externas para leituras:** 'HadoopShuffleOperation', 'HadoopRoundRobinOperation', 'HadoopBroadcastOperation'<br /><br /> **Operações externas para o MapReduce:** 'HadoopJobOperation', 'HdfsDeleteOperation'<br /><br /> **Operações externas para gravações:** 'ExternalExportDistributedOperation', 'ExternalExportReplicatedOperation', 'ExternalExportControlOperation'<br /><br /> Para obter mais informações, consulte "Noções básicas sobre planos de consulta" no [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)] . <br /><br />  Um plano de consulta também pode ser afetado pelas configurações do banco de dados.  Verifique [as opções de ALTER DATABASE SET](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-set-options?toc=/azure/sql-data-warehouse/toc.json&bc=/azure/sql-data-warehouse/breadcrumb/toc.json&view=azure-sqldw-latest) para obter detalhes.|  
|distribution_type|**nvarchar(32)**|Tipo de distribuição que esta etapa passará.|' Subnós ', ' ' distribuições ', ' AllComputeNodes ', ' ComputeNode ', ' Distribution ', ' SubsetNodes ', ' SubsetDistributions ', ' não especificado '|  
|location_type|**nvarchar(32)**|Onde a etapa está em execução.|"Compute", "Control", "DMS"|  
|status|**nvarchar(32)**|Status desta etapa.|Pendente, em execução, concluído, com falha, UndoFailed, PendingCancel, cancelado, desfeito, anulado|  
|error_id|**nvarchar (36)**|ID exclusiva do erro associado a esta etapa, se houver.|Consulte error_id de [Sys. dm_pdw_errors &#40;&#41;do Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md). NULL se nenhum erro tiver ocorrido.|  
|start_time|**datetime**|Hora em que a execução da etapa foi iniciada.|Menor ou igual à hora atual e maior ou igual a end_compile_time da consulta à qual essa etapa pertence. Para obter mais informações sobre consultas, consulte [Sys. dm_pdw_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|end_time|**datetime**|A hora em que esta etapa concluiu a execução, foi cancelada ou falhou.|Menor ou igual à hora atual e maior ou igual a start_time. Defina como nulo para as etapas atualmente em execução ou na fila.|  
|total_elapsed_time|**int**|Quantidade total de tempo que a etapa de consulta está em execução, em milissegundos.|Entre 0 e a diferença entre end_time e start_time. 0 para etapas em fila.<br /><br /> Se total_elapsed_time exceder o valor máximo de um inteiro, total_elapsed_time continuará a ser o valor máximo. Essa condição irá gerar o aviso "o valor máximo foi excedido".<br /><br /> O valor máximo em milissegundos é equivalente a 24,8 dias.|  
|row_count|**bigint**|Número total de linhas alteradas ou retornadas por esta solicitação.|O número de linhas afetadas pela etapa.  Maior ou igual a zero para etapas de operação de dados.  -1 para etapas que não operam em dados.|  
|.|**nvarchar(4000)**|Mantém o texto completo do comando desta etapa.|Qualquer cadeia de caracteres de solicitação válida para uma etapa. NULL quando a operação é do tipo MetaDataCreateOperation. Truncado se tiver mais de 4000 caracteres.|  
  
 Para obter informações sobre o máximo de linhas retidas por essa exibição, consulte a seção máximo de valores de exibição do sistema em "valores mínimos e máximos" no [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)] .  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de gerenciamento dinâmico de SQL Data Warehouse e paralelo data warehouse &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
