---
title: sys.dm_pdw_dms_workers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 0a284d18-3c46-4ffa-bcc9-689e660ee8b4
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 68d4b12395172f8ea5c820e745abf2a3f5f4c7c8
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2018
ms.locfileid: "34467992"
---
# <a name="sysdmpdwdmsworkers-transact-sql"></a>sys.dm_pdw_dms_workers (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contém informações sobre todos os trabalhadores etapas DMS.  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|Consulta que este trabalhador DMS faz parte do.<br /><br /> request_id, step_index e dms_step_index formam a chave para este modo de exibição.|Consulte request_id em [sys.dm_pdw_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|step_index|**Int**|Etapa que este trabalhador DMS faz parte de consulta.<br /><br /> request_id, step_index e dms_step_index formam a chave para este modo de exibição.|Consulte step_index em [sys.dm_pdw_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|dms_step_index|**Int**|Etapa no plano de DMS que este trabalhador está em execução.<br /><br /> request_id, step_index e dms_step_index formam a chave para este modo de exibição.||  
|pdw_node_id|**Int**|Nó que o trabalho está em execução no.|Consulte node_id em [sys.dm_pdw_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|distribution_id|**Int**|Distribuição de que o trabalho está em execução, se houver.|Consulte distribution_id em [sys.pdw_distributions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-distributions-transact-sql.md).|  
|Tipo|**nvarchar(32)**|Tipo de thread de trabalho do DMS que representa esta entrada.|'DIRECT_CONVERTER', 'DIRECT_READER', 'FILE_READER', 'HASH_CONVERTER', 'HASH_READER', 'ROUNDROBIN_CONVERTER', 'EXPORT_READER', 'EXTERNAL_READER', 'EXTERNAL_WRITER', 'PARALLEL_COPY_READER', 'REJECT_WRITER', 'WRITER'|  
|status|**nvarchar(32)**|Status do trabalho no DMS.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|bytes_per_sec|**bigint**|Taxa de transferência de leitura ou gravação no último segundo.|Maior que ou igual a 0. NULL se a consulta foi cancelada ou com falha antes de executar o trabalho.|  
|bytes_processed|**bigint**|Total de bytes processados por este trabalhador.|Maior que ou igual a 0. NULL se a consulta foi cancelada ou com falha antes de executar o trabalho.|  
|rows_processed|**bigint**|Número de linhas lidas ou gravadas para este trabalhador.|Maior que ou igual a 0. NULL se a consulta foi cancelada ou com falha antes de executar o trabalho.|  
|start_time|**datetime**|Hora de início de execução deste trabalhador.|Maior que ou igual à hora de início da etapa de consulta este trabalho pertence. Consulte [sys.dm_pdw_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|end_time|**datetime**|Hora em que a execução foi encerrado, falhou ou foi cancelada.|NULL para os trabalhos em andamento ou em fila. Caso contrário, maior a start_time.|  
|total_elapsed_time|**Int**|Tempo total gasto na execução, em milissegundos.|Maior que ou igual a 0.<br /><br /> Tempo total decorrido desde que o sistema iniciar ou reiniciar. Se total_elapsed_time excede o valor máximo para um inteiro (24.8 dias em milissegundos), isso causará falha materialização devido ao estouro.<br /><br /> O valor máximo em milissegundos é equivalente a 24.8 dias.|  
|cpu_time|**bigint**|Tempo de CPU consumido por este trabalhador, em milissegundos.|Maior que ou igual a 0.|  
|query_time|**Int**|Período de tempo antes de SQL inicia retornando linhas para o thread, em milissegundos.|Maior que ou igual a 0.|  
|buffers_available|**Int**|Número de buffers não utilizados.| NULL se a consulta foi cancelada ou com falha antes de executar o trabalho.|  
|sql_spid|**Int**|Id da sessão na instância do SQL Server executando o trabalho para este trabalhador DMS.||  
|dms_cpid|**Int**|ID do processo do thread atual em execução.||  
|error_id|**nvarchar(36)**|Identificador exclusivo do erro que ocorreu durante a execução deste trabalhador, se houver.|Consulte error_id em [sys.dm_pdw_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|source_info|**nvarchar(4000)**|Para um leitor, a especificação das tabelas de origem e colunas.||  
|destination_info|**nvarchar(4000)**|Para um gravador, a especificação de tabelas de destino.||  
  
 Para obter informações sobre o máximo de linhas mantido por esta exibição, consulte [valores máximos de modo de exibição de sistema](http://msdn.microsoft.com/en-us/5243f018-2713-45e3-9b61-39b2a57401b9).  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse Parallel Data Warehouse e exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
