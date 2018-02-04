---
title: sys.dm_pdw_hadoop_operations (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5d2337d4-e2c7-48de-9c26-cdc7e6eb5d55
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8ccb851fc349e31206ca5e76f050a1413c8c7405
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmpdwhadoopoperations-transact-sql"></a>sys.dm_pdw_hadoop_operations (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contém uma linha para cada trabalho de Map-reduce é propagada para o Hadoop como parte da execução um [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] consulta em uma tabela externa do Hadoop. Cada trabalho de Map-reduce representa um dos predicados na consulta. Isso é usado apenas quando a aplicação de predicado é habilitada para consultas em tabelas externas do Hadoop.  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|ID para esta operação de Hadoop externa.|Mesmo que a ID em [sys.dm_pdw_exec_requests &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|step_index|**Int**|Índice da etapa de consulta que faz referência a esta operação Hadoop.|Mesmo que step_index em [sys.dm_pdw_request_steps &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|operation_type|**nvarchar(255)**|Descreve o tipo de operação externa.|'Operação Hadoop externo'|  
|operation_name|**nvarchar(4000)**|A ID do trabalho para um trabalho Map-reduce. Isto é retornado por Hadoop após [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] envia o trabalho.||  
|map_progress|**float**|A porcentagem de dados de entrada que foi consumidos até o momento pelo trabalho de mapa.|Um ponto flutuante número entre e incluindo 0 e 100.|  
|reduce_progress|**Int**|A porcentagem do trabalho reduza que foi concluída.|Um ponto flutuante número entre e incluindo 0 e 100.|  
  
## <a name="see-also"></a>Consulte também  
 [System Views &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  
