---
title: sys.dm_pdw_sql_requests (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 44e19609-902c-46cf-acdf-19ea75011365
caps.latest.revision: 10
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 8fb8dc47d288470bedb8692ab38d00b0d810a1f6
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmpdwsqlrequests-transact-sql"></a>sys.dm_pdw_sql_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contém informações sobre todas as distribuições de consulta do SQL Server como parte de uma etapa SQL na consulta.  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|Identificador exclusivo da consulta ao qual pertence essa distribuição de consulta SQL.<br /><br /> request_id, step_index e distribution_id formam a chave para este modo de exibição.|Consulte request_id em [sys.dm_pdw_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|step_index|**Int**|Índice da etapa de consulta que essa distribuição é parte do.<br /><br /> request_id, step_index e distribution_id formam a chave para este modo de exibição.|Consulte step_index em [sys.dm_pdw_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|pdw_node_id|**Int**|Identificador exclusivo do nó em que a distribuição de consultas é executada.|Consulte node_id em [sys.dm_pdw_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|distribution_id|**Int**|Identificador exclusivo da distribuição em que a distribuição de consultas é executada.<br /><br /> request_id, step_index e distribution_id formam a chave para este modo de exibição.|Consulte distribution_id em [sys.pdw_distributions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-distributions-transact-sql.md). Definido como -1 para solicitações que são executados no escopo do nó, não o escopo de distribuição.|  
|status|**nvarchar(32)**|Status atual da distribuição de consulta.|Pendente, que executa, com falha, cancelada ou concluída, interrompida, CancelSubmitted|  
|error_id|**nvarchar(36)**|Identificador exclusivo do erro associados a essa distribuição de consulta, se houver.|Consulte error_id em [sys.dm_pdw_errors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md). Definido como NULL se nenhum erro ocorreu.|  
|start_time|**datetime**|Hora na qual consulta distribuição começou execução.|Menor ou igual à hora atual e maior ou igual a start_time da etapa de consulta distribuição esta consulta pertence|  
|end_time|**datetime**|Hora em que a distribuição de consultas concluiu a execução, foi cancelada ou falha.|Maior ou igual à hora de início ou definido como NULL se a distribuição de consulta está em andamento ou em fila.|  
|total_elapsed_time|**Int**|Representa a hora em que a distribuição de consulta está em execução, em milissegundos.|Maior ou igual a 0. Igual ao delta de start_time e end_time for concluído, falhou ou cancelado distribuições de consulta.<br /><br /> Se total_elapsed_time excede o valor máximo para um inteiro, total_elapsed_time continuará a ser o valor máximo. Essa condição gerará o aviso "o valor máximo foi excedido."<br /><br /> O valor máximo em milissegundos é equivalente a 24.8 dias.|  
|row_count|**bigint**|Número de linhas alteradas ou lidos por essa distribuição de consulta.|-1 para operações que não alteram nem retornar dados, como CREATE TABLE e DROP TABLE.|  
|spid|**Int**|Id da sessão na instância do SQL Server em execução a distribuição de consulta.||  
|command|**nvarchar(4000)**|Texto completo do comando para a distribuição de consultas.|Qualquer cadeia de consulta ou solicitação válida.|  
  
 Para obter informações sobre o máximo de linhas mantido por esta exibição, consulte a seção de valores máximos de modo de exibição de sistema no [valores mínimo e máximo (SQL Server PDW)](http://msdn.microsoft.com/en-us/5243f018-2713-45e3-9b61-39b2a57401b9) tópico.  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse Parallel Data Warehouse e exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
