---
description: sys. dm_exec_external_work (Transact-SQL)
title: sys. dm_exec_external_work (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- DM_EXEC_EXTERNAL_WORK
- DM_EXEC_EXTERNAL_WORK_TSQL
- SYS.DM_EXEC_EXTERNAL_WORK_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_external_work management view
- dm_exec_external_work management view
- PolyBase,views
- PolyBase
ms.assetid: 7597d97b-1fde-4135-ac35-4af12968f300
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 660b41d250f8bfccfc8d0e123f0e1a6aafb5fcde
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548501"
---
# <a name="sysdm_exec_external_work-transact-sql"></a>sys. dm_exec_external_work (Transact-SQL)
[!INCLUDE [sqlserver2016-asa-pdw](../../includes/applies-to-version/sqlserver2016-asa-pdw.md)]

  Retorna informações sobre a carga de trabalho por trabalhador, em cada nó de computação.  
  
 Consulte sys. dm_exec_external_work para identificar o trabalho girado para se comunicar com a fonte de dados externa (por exemplo, Hadoop ou SQL Server externo).  
  
|Nome da coluna|Tipo de Dados|DESCRIÇÃO|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|`nvarchar(32)`|Identificador exclusivo para a consulta do polybase associado.|Consulte *request_ID* em [sys. dm_exec_requests &#40;&#41;do Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).|  
|step_index|`int`|A solicitação que esse trabalho está executando.|Consulte *step_index* em  [sys. dm_exec_requests &#40;&#41;do Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).|  
|dms_step_index|`int`|Etapa no plano DMS que esse trabalho está executando.|Consulte [Sys. dm_exec_dms_workers &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md).|  
|compute_node_id|`int`|O nó no qual o trabalho está sendo executado.|Consulte [Sys. dm_exec_compute_nodes &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md).|  
|tipo|`nvarchar(60)`|O tipo de trabalho externo.|' Divisão de arquivo '|  
|work_id|`int`|ID da divisão real.|Maior ou igual a 0.|  
|input_name|`nvarchar(4000)`|Nome da entrada a ser lida|Nome do arquivo ao usar o Hadoop.|  
|read_location|`bigint`|Deslocamento ou local de leitura.|Deslocamento do arquivo a ser lido.|  
|bytes_processed|`bigint`|Total de bytes alocados para processamento de dados por este trabalhador. Isso pode não representar necessariamente o total de dados que estão sendo retornados pela consulta |Maior ou igual a 0.|  
|comprimento|`bigint`|Comprimento do bloco Split ou HDFS no caso do Hadoop|Definido pelo usuário. O padrão é o 64M|  
|status|`nvarchar(32)`|Status do trabalhador|Pendente, processando, concluído, com falha, anulado|  
|start_time|`datetime`|Início do trabalho||  
|end_time|`datetime`|Fim do trabalho||  
|total_elapsed_time|`int`|Tempo total em milissegundos||
|compute_pool_id|`int`|Identificador exclusivo do pool.|

## <a name="see-also"></a>Consulte Também  
 [Solução de problemas do polybase com exibições de gerenciamento dinâmico](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Exibições de gerenciamento dinâmico relacionadas ao banco de dados &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
