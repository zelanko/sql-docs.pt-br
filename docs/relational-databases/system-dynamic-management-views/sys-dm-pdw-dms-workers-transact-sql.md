---
title: sys.dm_pdw_dms_workers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.suite: sql
ms.component: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 0a284d18-3c46-4ffa-bcc9-689e660ee8b4
caps.latest.revision: 7
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: c46c6b83d820d7c970d16e2e84a3a81a0e07b340
ms.sourcegitcommit: abd71294ebc39695d403e341c4f77829cb4166a8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2018
ms.locfileid: "36925907"
---
# <a name="sysdmpdwdmsworkers-transact-sql"></a>sys.dm_pdw_dms_workers (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contém informações sobre todos os trabalhadores concluindo as etapas do DMS.  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|Consulta que este trabalhador DMS faz parte.<br /><br /> request_id, step_index e dms_step_index formam a chave para esta exibição.|Consulte request_id na [DM pdw_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|step_index|**int**|Etapa que este trabalhador DMS faz parte de consulta.<br /><br /> request_id, step_index e dms_step_index formam a chave para esta exibição.|Consulte step_index na [DM pdw_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|dms_step_index|**int**|Etapa no plano de DMS que este trabalhador está executando.<br /><br /> request_id, step_index e dms_step_index formam a chave para esta exibição.||  
|pdw_node_id|**int**|Nó que o trabalhador está sendo executado.|Consulte node_id na [sys.dm_pdw_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|distribution_id|**Int**|Distribuição em que o trabalhador está em execução, se houver.|Consulte distribution_id na [sys.pdw_distributions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-distributions-transact-sql.md).|  
|Tipo|**nvarchar(32)**|Tipo de thread de trabalho do DMS que essa entrada representa.|'DIRECT_CONVERTER', 'DIRECT_READER', 'FILE_READER', 'HASH_CONVERTER', 'HASH_READER', 'ROUNDROBIN_CONVERTER', 'EXPORT_READER', 'EXTERNAL_READER', 'EXTERNAL_WRITER', 'PARALLEL_COPY_READER', 'REJECT_WRITER', 'WRITER'|  
|status|**nvarchar(32)**|Status do trabalho DMS.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|bytes_per_sec|**bigint**|Taxa de transferência de leitura ou gravação no último segundo.|Maior que ou igual a 0. NULL se a consulta foi cancelada ou falha antes de executar o trabalho.|  
|bytes_processed|**bigint**|Total de bytes processados por este trabalhador.|Maior que ou igual a 0. NULL se a consulta foi cancelada ou falha antes de executar o trabalho.|  
|rows_processed|**bigint**|Número de linhas lidas ou gravadas para este trabalhador.|Maior que ou igual a 0. NULL se a consulta foi cancelada ou falha antes de executar o trabalho.|  
|start_time|**datetime**|Hora de início a execução deste trabalhador.|Maior que ou igual à hora de início da etapa de consulta esse trabalho pertence. Ver [DM pdw_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|end_time|**datetime**|Hora em que a execução foi encerrado, falhou ou foi cancelada.|NULL para os trabalhos em andamento ou em fila. Caso contrário, maior que start_time.|  
|total_elapsed_time|**int**|Tempo total gasto na execução, em milissegundos.|Maior que ou igual a 0.<br /><br /> Tempo total decorrido desde que o sistema iniciar ou reiniciar. Se total_elapsed_time exceder o valor máximo para um inteiro (24,8 dias em milissegundos), ela causará falha de materialização devido a estouro.<br /><br /> O valor máximo em milissegundos é equivalente a 24,8 dias.|  
|cpu_time|**bigint**|Tempo de CPU consumido por este trabalhador, em milissegundos.|Maior que ou igual a 0.|  
|query_time|**int**|Período de tempo antes do SQL é iniciado retornando linhas para o thread, em milissegundos.|Maior que ou igual a 0.|  
|buffers_available|**int**|Número de buffers não utilizados.| NULL se a consulta foi cancelada ou falha antes de executar o trabalho.|  
|sql_spid|**int**|Id de sessão na instância do SQL Server executando o trabalho para este trabalhador DMS.||  
|dms_cpid|**int**|ID do processo de thread real em execução.||  
|error_id|**nvarchar(36)**|Identificador exclusivo do erro que ocorreu durante a execução deste trabalhador, se houver.|Consulte error_id na [DM pdw_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|source_info|**nvarchar(4000)**|Para um leitor, a especificação das tabelas de origem e colunas.||  
|destination_info|**nvarchar(4000)**|Para um gravador, a especificação de tabelas de destino.||  
  
 Para obter informações sobre o máximo de linhas mantido por esta exibição, consulte [valores máximos de modo de exibição de sistema](http://msdn.microsoft.com/en-us/5243f018-2713-45e3-9b61-39b2a57401b9).  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse e Parallel Data Warehouse exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
