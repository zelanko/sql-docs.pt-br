---
description: sys.dm_pdw_sql_requests (Transact-SQL)
title: sys.dm_pdw_sql_requests (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 44e19609-902c-46cf-acdf-19ea75011365
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 3bbf99db3971ecb9979c1ef234d1f57c1761afa9
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92035199"
---
# <a name="sysdm_pdw_sql_requests-transact-sql"></a>sys.dm_pdw_sql_requests (Transact-SQL)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Contém informações sobre todas as SQL Server distribuições de consulta como parte de uma etapa SQL na consulta.  
  
|Nome da coluna|Tipo de Dados|DESCRIÇÃO|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|Identificador exclusivo da consulta à qual esta distribuição de consulta SQL pertence.<br /><br /> request_id, step_index e distribution_id formam a chave para essa exibição.|Consulte request_id em [sys.dm_pdw_exec_requests &#40;&#41;do Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|step_index|**int**|Índice da etapa de consulta da qual essa distribuição faz parte.<br /><br /> request_id, step_index e distribution_id formam a chave para essa exibição.|Consulte step_index em [sys.dm_pdw_request_steps &#40;&#41;do Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|pdw_node_id|**int**|Identificador exclusivo do nó no qual essa distribuição de consulta é executada.|Consulte node_id em [sys.dm_pdw_nodes &#40;&#41;do Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|distribution_id|**int**|Identificador exclusivo da distribuição na qual essa distribuição de consulta é executada.<br /><br /> request_id, step_index e distribution_id formam a chave para essa exibição.|Consulte distribution_id em [sys.pdw_distributions &#40;&#41;do Transact-SQL ](../../relational-databases/system-catalog-views/sys-pdw-distributions-transact-sql.md). Defina como-1 para solicitações que são executadas no escopo do nó, não no escopo de distribuição.|  
|status|**nvarchar(32)**|Status atual da distribuição de consulta.|Pendente, em execução, com falha, cancelado, concluído, anulado, CancelSubmitted|  
|error_id|**nvarchar (36)**|Identificador exclusivo do erro associado a essa distribuição de consulta, se houver.|Consulte error_id em [sys.dm_pdw_errors &#40;&#41;do Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md). Defina como NULL se nenhum erro tiver ocorrido.|  
|start_time|**datetime**|Hora em que a distribuição da consulta iniciou a execução.|Menor ou igual à hora atual e maior ou igual a start_time da etapa de consulta à qual esta distribuição de consulta pertence|  
|end_time|**datetime**|A hora em que esta distribuição de consulta concluiu a execução, foi cancelada ou falhou.|Maior ou igual à hora de início ou definido como NULL se a distribuição da consulta estiver em andamento ou em fila.|  
|total_elapsed_time|**int**|Representa a hora em que a distribuição de consultas está em execução, em milissegundos.|Maior ou igual a 0. Igual ao Delta de start_time e end_time para distribuições de consultas concluídas, com falha ou canceladas.<br /><br /> Se total_elapsed_time exceder o valor máximo de um inteiro, total_elapsed_time continuará a ser o valor máximo. Essa condição irá gerar o aviso "o valor máximo foi excedido".<br /><br /> O valor máximo em milissegundos é equivalente a 24,8 dias.|  
|row_count|**bigint**|Número de linhas alteradas ou lidas por essa distribuição de consulta.|-1 para operações que não alteram nem retornam dados, como CREATE TABLE e DROP TABLE.|  
|spid|**int**|ID da sessão na instância de SQL Server que executa a distribuição de consulta.||  
|.|**nvarchar(4000)**|Texto completo do comando para esta distribuição de consulta.|Qualquer consulta ou cadeia de caracteres de solicitação válida.|  
  
 Para obter informações sobre o máximo de linhas retidas por essa exibição, consulte a seção de metadados no tópico [limites de capacidade](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) .  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de gerenciamento dinâmico do Azure Synapse Analytics e Parallel data warehouse &#40;&#41;de Transact-SQL ](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
