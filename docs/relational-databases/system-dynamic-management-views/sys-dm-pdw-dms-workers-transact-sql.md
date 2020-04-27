---
title: sys. dm_pdw_dms_workers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 0a284d18-3c46-4ffa-bcc9-689e660ee8b4
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 6e5f295637db0e138caf324e3126707b9e0ea774
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67899500"
---
# <a name="sysdm_pdw_dms_workers-transact-sql"></a>sys. dm_pdw_dms_workers (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contém informações sobre todos os trabalhos concluindo as etapas de DMS.  
  
|Nome da coluna|Tipo de Dados|Descrição|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|Consulta de que esse trabalho DMS faz parte.<br /><br /> request_id, step_index e dms_step_index formam a chave para essa exibição.|Consulte request_id em [Sys. dm_pdw_exec_requests &#40;&#41;do Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|step_index|**int**|Etapa de consulta para a qual este trabalho DMS faz parte.<br /><br /> request_id, step_index e dms_step_index formam a chave para essa exibição.|Consulte step_index em [Sys. dm_pdw_request_steps &#40;&#41;do Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|dms_step_index|**int**|Etapa no plano DMS que esse trabalho está executando.<br /><br /> request_id, step_index e dms_step_index formam a chave para essa exibição.||  
|pdw_node_id|**int**|Nó no qual o trabalho está sendo executado.|Consulte node_id em [Sys. dm_pdw_nodes &#40;&#41;do Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|distribution_id|**Int**|A distribuição em que o trabalho está sendo executado, se houver.|Consulte distribution_id em [Sys. pdw_distributions &#40;&#41;do Transact-SQL ](../../relational-databases/system-catalog-views/sys-pdw-distributions-transact-sql.md).|  
|tipo|**nvarchar(32)**|Tipo de thread de trabalho do DMS que essa entrada representa.|' DIRECT_CONVERTER ', ' DIRECT_READER ', ' FILE_READER ', ' HASH_CONVERTER ', ' HASH_READER ', ' ROUNDROBIN_CONVERTER ', ' EXPORT_READER ', ' EXTERNAL_READER ', ' EXTERNAL_WRITER ', ' PARALLEL_COPY_READER ', ' REJECT_WRITER ', ' GRAVADOR '|  
|status|**nvarchar(32)**|Status do trabalho do DMS.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|bytes_per_sec|**bigint**|Taxa de transferência de leitura ou gravação no último segundo.|Maior ou igual a 0. NULL se a consulta foi cancelada ou falhou antes da execução do trabalho.|  
|bytes_processed|**bigint**|Total de bytes processados por este trabalhador.|Maior ou igual a 0. NULL se a consulta foi cancelada ou falhou antes da execução do trabalho.|  
|rows_processed|**bigint**|Número de linhas lidas ou gravadas para este trabalho.|Maior ou igual a 0. NULL se a consulta foi cancelada ou falhou antes da execução do trabalho.|  
|start_time|**datetime**|Hora em que a execução deste trabalhador foi iniciada.|Maior ou igual à hora de início da etapa de consulta à qual este trabalhador pertence. Consulte [Sys. dm_pdw_request_steps &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|end_time|**datetime**|Hora em que a execução terminou, falhou ou foi cancelada.|NULO para trabalhos em andamento ou em fila. Caso contrário, maior que start_time.|  
|total_elapsed_time|**int**|Tempo total gasto na execução, em milissegundos.|Maior ou igual a 0.<br /><br /> Tempo total decorrido desde a inicialização ou reinicialização do sistema. Se total_elapsed_time exceder o valor máximo de um inteiro (24,8 dias em milissegundos), isso causará falha de materialização devido ao estouro.<br /><br /> O valor máximo em milissegundos é equivalente a 24,8 dias.|  
|cpu_time|**bigint**|Tempo de CPU consumido por este trabalhador, em milissegundos.|Maior ou igual a 0.|  
|query_time|**int**|Período de tempo antes que o SQL comece a retornar linhas para o thread, em milissegundos.|Maior ou igual a 0.|  
|buffers_available|**int**|Número de buffers não utilizados.| NULL se a consulta foi cancelada ou falhou antes da execução do trabalho.|  
|sql_spid|**int**|ID da sessão na instância de SQL Server executando o trabalho para esse trabalho DMS.||  
|dms_cpid|**int**|ID de processo do thread real em execução.||  
|error_id|**nvarchar (36)**|Identificador exclusivo do erro que ocorreu durante a execução deste trabalhador, se houver.|Consulte error_id em [Sys. dm_pdw_request_steps &#40;&#41;do Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|source_info|**nvarchar(4000)**|Para um leitor, especificação das tabelas e colunas de origem.||  
|destination_info|**nvarchar(4000)**|Para um gravador, especificação das tabelas de destino.||  
  
 Para obter informações sobre o máximo de linhas retidas por essa exibição, consulte a seção de metadados no tópico [limites de capacidade](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) .  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de gerenciamento dinâmico de SQL Data Warehouse e paralelo data warehouse &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
