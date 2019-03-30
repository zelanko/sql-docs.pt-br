---
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
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 24bcf44fe2e1e0d35610dba9fb40d64ac2c819bb
ms.sourcegitcommit: 706f3a89fdb98e84569973f35a3032f324a92771
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2019
ms.locfileid: "58658000"
---
# <a name="sysdmpdwsqlrequests-transact-sql"></a>sys.dm_pdw_sql_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contém informações sobre todas as distribuições de consulta do SQL Server como parte de uma etapa SQL na consulta.  
  
|Nome da coluna|Tipo de Dados|Descrição|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|Identificador exclusivo da consulta ao qual pertence essa distribuição de consulta SQL.<br /><br /> request_id, step_index e distribution_id formam a chave para esta exibição.|Consulte request_id na [DM pdw_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|step_index|**int**|Índice da etapa de consulta que essa distribuição é parte do.<br /><br /> request_id, step_index e distribution_id formam a chave para esta exibição.|Consulte step_index na [DM pdw_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|pdw_node_id|**int**|Identificador exclusivo do nó em que essa distribuição de consulta é executada.|Consulte node_id na [sys.dm_pdw_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|distribution_id|**int**|Identificador exclusivo da distribuição em que essa distribuição de consulta é executada.<br /><br /> request_id, step_index e distribution_id formam a chave para esta exibição.|Consulte distribution_id na [sys.pdw_distributions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-distributions-transact-sql.md). Defina como -1 para solicitações que são executados no escopo do nó, não o escopo de distribuição.|  
|status|**nvarchar(32)**|Status atual da distribuição de consulta.|Pendente, que executa, com falha, cancelada ou concluída, interrompida, CancelSubmitted|  
|error_id|**nvarchar(36)**|Identificador exclusivo do erro associado a essa distribuição de consulta, se houver.|Consulte error_id na [sys.dm_pdw_errors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md). Definido como NULL se nenhum erro ocorreu.|  
|start_time|**datetime**|Hora na qual consulta distribuição iniciou a execução.|Menor ou igual à hora atual e maior ou igual a start_time da etapa de consulta essa distribuição consulta pertence|  
|end_time|**datetime**|Hora em que essa distribuição consulta concluiu a execução, foi cancelada ou falhou.|Maior ou igual à hora de início ou definido como NULL se a distribuição de consulta está em andamento ou em fila.|  
|total_elapsed_time|**int**|Representa a hora em que a distribuição de consulta estiver sendo executado, em milissegundos.|Maior ou igual a 0. Igual ao delta de start_time e end_time para concluído, falhou ou cancelado distribuições de consulta.<br /><br /> Se total_elapsed_time exceder o valor máximo para um número inteiro, o total_elapsed_time continuará a ser o valor máximo. Essa condição gerará o aviso "o valor máximo foi excedido."<br /><br /> O valor máximo em milissegundos é equivalente a 24,8 dias.|  
|row_count|**bigint**|Número de linhas alteradas ou lidos por essa distribuição de consulta.|-1 para operações que não alteram nem retornar dados, como CREATE TABLE e DROP TABLE.|  
|spid|**int**|Id de sessão na instância do SQL Server que executam a distribuição de consulta.||  
|command|**nvarchar(4000)**|Texto completo do comando para essa distribuição de consulta.|Qualquer cadeia de consulta ou solicitação válida.|  
  
 Para obter informações sobre o máximo de linhas mantido por esta exibição, consulte a seção de metadados na [limites de capacidade](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) tópico.  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse e Parallel Data Warehouse exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
