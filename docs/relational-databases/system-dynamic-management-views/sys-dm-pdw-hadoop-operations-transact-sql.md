---
title: sys.dm_pdw_hadoop_operations (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5d2337d4-e2c7-48de-9c26-cdc7e6eb5d55
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: dfb2c3493e1d343107fb288320de30f5258b2eaa
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47718234"
---
# <a name="sysdmpdwhadoopoperations-transact-sql"></a>sys.dm_pdw_hadoop_operations (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contém uma linha para cada trabalho de Map-reduce que é propagada para o Hadoop como parte da execução um [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] consulta em uma tabela externa do Hadoop. Cada trabalho de Map-reduce representa um dos predicados na consulta. Isso é usado somente quando a aplicação de predicado está habilitada para consultas em tabelas externas do Hadoop.  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|ID para esta operação externa do Hadoop.|Mesmo que a ID na [DM pdw_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|step_index|**int**|Índice da etapa de consulta que faz referência a essa operação de Hadoop.|Mesmo que step_index na [DM pdw_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|operation_type|**nvarchar(255)**|Descreve o tipo de operação externa.|'Operation Hadoop externo'|  
|operation_name|**nvarchar(4000)**|A ID do trabalho para um trabalho de Map-reduce. Isto é retornado pelo Hadoop após [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] envia o trabalho.||  
|map_progress|**float**|A porcentagem de dados de entrada que foi consumidos até o momento pelo trabalho de mapa.|Entre e incluindo 0 e 100 de número de ponto flutuante.|  
|reduce_progress|**int**|A porcentagem do trabalho reduce que foi concluída...|Entre e incluindo 0 e 100 de número de ponto flutuante.|  
  
## <a name="see-also"></a>Consulte também  
 [Exibições do sistema &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  
