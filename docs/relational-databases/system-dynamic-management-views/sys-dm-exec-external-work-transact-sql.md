---
title: sys.dm_exec_external_work (Transact-SQL) | Microsoft Docs
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
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: bb8054d49ecbcd3f4140c63e2adf460e4330b9e6
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39538466"
---
# <a name="sysdmexecexternalwork-transact-sql"></a>sys.dm_exec_external_work (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Retorna informações sobre a carga de trabalho por trabalho, em cada nó de computação.  
  
 Sys.dm_exec_external_work de consulta para identificar o trabalho é rotacionado para se comunicar com a fonte de dados externa (por exemplo, Hadoop ou SQL Server externo).  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**nvarchar(32)**|Identificador exclusivo para a consulta do PolyBase associado.|Ver *request_ID* na [. DM exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).|  
|step_index|**int**|A solicitação em que este trabalhador está executando.|Ver *step_index* na [. DM exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).|  
|dms_step_index|**int**|Etapa no plano de DMS que este trabalhador está em execução.|Ver [sys.dm_exec_dms_workers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md).|  
|compute_node_id|**int**|O nó do trabalhador está em execução.|Ver [DM exec_compute_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md).|  
|Tipo|**nvarchar(60)**|O tipo de trabalho externo.|Divisão de arquivos|  
|work_id|**int**|ID da divisão real.|Maior que ou igual a 0.|  
|input_name|**nvarchar(4000)**|Nome da entrada a ser lido|Nome do arquivo quando o uso do Hadoop.|  
|read_location|**bigint**|Deslocamento ou ler local.|Deslocamento do arquivo a ser lido.|  
|bytes_processed|**bigint**|Total de bytes processados por este trabalhador.|Maior que ou igual a 0.|  
|comprimento|**bigint**|Tamanho da divisão ou bloco HDFS em caso de Hadoop|Definíveis pelo usuário. O padrão é 64M|  
|status|**nvarchar(32)**|Status do trabalho|Pendente, processando, concluído, falha, anulado|  
|start_time|**datetime**|Início do trabalho||  
|end_time|**datetime**|Término do trabalho||  
|total_elapsed_time|**int**|Tempo total em milissegundos||  
  
## <a name="see-also"></a>Consulte também  
 [Solução de problemas com exibições de gerenciamento dinâmico do PolyBase](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Banco de dados relacionados a exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
