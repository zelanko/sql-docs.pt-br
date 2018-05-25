---
title: sys.dm_pdw_dms_external_work (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
ms.assetid: 47345015-f861-451e-97c4-6e1cb81d1922
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: d980034474bc08e57044ecdcf555877b50a0c1f2
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmpdwdmsexternalwork-transact-sql"></a>sys.dm_pdw_dms_external_work (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] exibição do sistema que contém informações sobre todas as etapas de serviço de movimentação de dados (DMS) para operações externas.  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|Consulta que está usando este trabalhador DMS.<br /><br /> request_id, step_index e dms_step_index formam a chave para este modo de exibição.|Mesmo que request_id em [sys.dm_pdw_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|step_index|**Int**|Etapa de consulta que está invocando este trabalhador DMS.<br /><br /> request_id, step_index e dms_step_index formam a chave para este modo de exibição.|Mesmo que step_index em [sys.dm_pdw_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|dms_step_index|**Int**|Etapa atual no plano de DMS.<br /><br /> request_id, step_index e dms_step_index formam a chave para este modo de exibição.|Mesmo que dms___step_index em [sys.dm_pdw_dms_workers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-workers-transact-sql.md).|  
|pdw_node_id|**Int**|Nó que está executando o trabalho DMS.|Mesmo que node_id em [sys.dm_pdw_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|Tipo|**nvarchar(60)**|Tipo de operação externa que deste nó está em execução.<br /><br /> DIVISÃO de arquivo é uma operação em um arquivo do Hadoop externo foi dividido em várias fica menor.|'DIVISÃO DE ARQUIVO'|  
|work_id|**Int**|O arquivo dividido ID.|Maior que ou igual a 0.<br /><br /> Exclusivos em cada nó de computação.|  
|input_name|**nvarchar(60)**|Nome para a entrada que está sendo lida de cadeia de caracteres.|Para um arquivo do Hadoop, isso é o nome de arquivo do Hadoop.|  
|read_location|**bigint**|Deslocamento do local de leitura.||  
|estimated_bytes_processed|**bigint**|Número de bytes processados por este trabalhador.|Maior que ou igual a 0.|  
|comprimento|**bigint**|Número de bytes no arquivo de divisão.<br /><br /> Para Hadoop, esse é o tamanho do bloco de HDFS.|Definido pelo usuário. O padrão é 64 MB.|  
|status|**nvarchar(32)**|Estado do trabalhador.|Pendente, processando, concluído, falha, anulada|  
|start_time|**datetime**|Hora de início de execução deste trabalhador.|Maior que ou igual à hora de início da etapa de consulta este trabalho pertence. Consulte [sys.dm_pdw_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|end_time|**datetime**|Hora em que a execução foi encerrado, falhou ou foi cancelada.|NULL para os trabalhos em andamento ou em fila. Caso contrário, maior a start_time.|  
|total_elapsed_time|**Int**|Tempo total gasto na execução, em milissegundos.|Maior que ou igual a 0.<br /><br /> Se total_elapsed_time excede o valor máximo para um inteiro, total_elapsed_time continuará a ser o valor máximo. Essa condição gerará o aviso "o valor máximo foi excedido."<br /><br /> O valor máximo em milissegundos é equivalente a 24.8 dias.|  
  
 Para obter informações sobre o máximo de linhas mantido por esta exibição, consulte [valores máximos de modo de exibição de sistema](http://msdn.microsoft.com/en-us/5243f018-2713-45e3-9b61-39b2a57401b9).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições do sistema &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  
