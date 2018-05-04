---
title: sys.dm_exec_external_work (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
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
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 79de7b54f8d662107014d740ca157055f0085c78
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmexecexternalwork-transact-sql"></a>sys.dm_exec_external_work (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Retorna informações sobre a carga de trabalho por trabalho, em cada nó de computação.  
  
 Girado sys.dm_exec_external_work de consulta para identificar o trabalho de backup para se comunicar com a fonte de dados externa (por exemplo, Hadoop ou externa do SQL Server).  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**nvarchar(32)**|Identificador exclusivo de consulta PolyBase associado.|Consulte *request_ID* na [exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).|  
|step_index|**Int**|A solicitação que este trabalhador está executando.|Consulte *step_index* na [exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).|  
|dms_step_index|**Int**|Etapa no plano de DMS que este trabalhador está executando.|Consulte [sys.dm_exec_dms_workers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md).|  
|compute_node_id|**Int**|O nó que o trabalho está em execução.|Consulte [sys.DM exec_compute_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md).|  
|Tipo|**nvarchar(60)**|O tipo de trabalho externo.|Divisão de arquivo|  
|work_id|**Int**|ID da divisão real.|Maior que ou igual a 0.|  
|input_name|**nvarchar(4000)**|Nome da entrada a ser lido|Nome do arquivo ao usar o Hadoop.|  
|read_location|**bigint**|Deslocamento ou ler local.|Deslocamento de arquivo para leitura.|  
|bytes_processed|**bigint**|Total de bytes processados por este trabalhador.|Maior que ou igual a 0.|  
|comprimento|**bigint**|Comprimento da divisão ou bloco HDFS no caso de Hadoop|Definido pelo usuário. O padrão é 64M|  
|status|**nvarchar(32)**|Status do trabalhador|Pendente, processando, concluído, falha, anulada|  
|start_time|**datetime**|Início do trabalho||  
|end_time|**datetime**|Término do trabalho||  
|total_elapsed_time|**Int**|Tempo total em milissegundos||  
  
## <a name="see-also"></a>Consulte também  
 [PolyBase, solucionando problemas com exibições de gerenciamento dinâmico](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Banco de dados relacionados a exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
