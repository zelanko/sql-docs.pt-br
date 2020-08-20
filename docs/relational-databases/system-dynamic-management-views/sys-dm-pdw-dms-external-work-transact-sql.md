---
description: sys. dm_pdw_dms_external_work (Transact-SQL)
title: sys. dm_pdw_dms_external_work (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 47345015-f861-451e-97c4-6e1cb81d1922
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 8633a363aa6ba486be4113bdf4826f2dc2e1a579
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474782"
---
# <a name="sysdm_pdw_dms_external_work-transact-sql"></a>sys. dm_pdw_dms_external_work (Transact-SQL)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] exibição do sistema que contém informações sobre todas as etapas do serviço de movimentação de dados (DMS) para operações externas.  
  
|Nome da coluna|Tipo de Dados|DESCRIÇÃO|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|Consulta que está usando este trabalho DMS.<br /><br /> request_id, step_index e dms_step_index formam a chave para essa exibição.|O mesmo que request_id em [Sys. dm_pdw_exec_requests &#40;&#41;do Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|step_index|**int**|Etapa de consulta que está invocando este trabalho DMS.<br /><br /> request_id, step_index e dms_step_index formam a chave para essa exibição.|O mesmo que step_index em [Sys. dm_pdw_request_steps &#40;&#41;do Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|dms_step_index|**int**|Etapa atual no plano do DMS.<br /><br /> request_id, step_index e dms_step_index formam a chave para essa exibição.|O mesmo que dms___step_index em [Sys. dm_pdw_dms_workers &#40;&#41;do Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-workers-transact-sql.md).|  
|pdw_node_id|**int**|Nó que está executando o trabalho DMS.|O mesmo que node_id em [Sys. dm_pdw_nodes &#40;&#41;do Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|type|**nvarchar(60)**|Tipo de operação externa que este nó está executando.<br /><br /> A divisão de arquivo é uma operação em um arquivo Hadoop externo que foi dividido em vários enquadrados menores.|' DIVISÃO DE ARQUIVO '|  
|work_id|**int**|A ID de divisão do arquivo.|Maior ou igual a 0.<br /><br /> Exclusivo por nó de computação.|  
|input_name|**nvarchar(60)**|Nome da cadeia de caracteres para a entrada que está sendo lida.|Para um arquivo Hadoop, esse é o nome do arquivo do Hadoop.|  
|read_location|**bigint**|Deslocamento do local de leitura.||  
|estimated_bytes_processed|**bigint**|Número de bytes processados por este trabalhador.|Maior ou igual a 0.|  
|comprimento|**bigint**|Número de bytes na divisão do arquivo.<br /><br /> Para o Hadoop, esse é o tamanho do bloco HDFS.|Definido pelo usuário. O padrão é 64 MB.|  
|status|**nvarchar(32)**|Estado do trabalho.|Pendente, processando, concluído, com falha, anulado|  
|start_time|**datetime**|Hora em que a execução deste trabalhador foi iniciada.|Maior ou igual à hora de início da etapa de consulta à qual este trabalhador pertence. Consulte [Sys. dm_pdw_request_steps &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|end_time|**datetime**|Hora em que a execução terminou, falhou ou foi cancelada.|NULO para trabalhos em andamento ou em fila. Caso contrário, maior que start_time.|  
|total_elapsed_time|**int**|Tempo total gasto na execução, em milissegundos.|Maior ou igual a 0.<br /><br /> Se total_elapsed_time exceder o valor máximo de um inteiro, total_elapsed_time continuará a ser o valor máximo. Essa condição irá gerar o aviso "o valor máximo foi excedido".<br /><br /> O valor máximo em milissegundos é equivalente a 24,8 dias.|  
  
 Para obter informações sobre o máximo de linhas retidas por essa exibição, consulte a seção de metadados no tópico [limites de capacidade](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) .
  
## <a name="see-also"></a>Consulte Também  
 [Exibições do sistema &#40;&#41;Transact-SQL ](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  
