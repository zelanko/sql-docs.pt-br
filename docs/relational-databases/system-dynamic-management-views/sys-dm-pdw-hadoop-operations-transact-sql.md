---
title: sys. dm_pdw_hadoop_operations (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5d2337d4-e2c7-48de-9c26-cdc7e6eb5d55
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: b4429585d735ee4eb51d2b0b421b53fdf06bf8ec
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67899387"
---
# <a name="sysdm_pdw_hadoop_operations-transact-sql"></a>sys. dm_pdw_hadoop_operations (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contém uma linha para cada trabalho de redução de mapa que é enviado para o Hadoop como parte da execução [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] de uma consulta em uma tabela do Hadoop externa. Cada trabalho de redução de mapa representa um dos predicados na consulta. Isso só é usado quando a aplicação de predicado está habilitada para consultas em tabelas externas do Hadoop.  
  
|Nome da coluna|Tipo de Dados|Descrição|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|ID para esta operação externa do Hadoop.|O mesmo que ID em [Sys. dm_pdw_exec_requests &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|step_index|**int**|Índice da etapa de consulta que se refere a esta operação do Hadoop.|O mesmo que step_index em [Sys. dm_pdw_request_steps &#40;&#41;do Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|operation_type|**nvarchar (255)**|Descreve o tipo de operação externa.|' Operação do Hadoop externa '|  
|operation_name|**nvarchar(4000)**|A ID do trabalho para um trabalho de redução de mapa. Isso é retornado pelo Hadoop depois [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] que o envia o trabalho.||  
|map_progress|**float**|A porcentagem de dados de entrada consumidos até agora pelo trabalho do mapa.|Um número de ponto flutuante entre e incluindo, 0 e 100.|  
|reduce_progress|**int**|A porcentagem do trabalho de redução que foi concluído..|Um número de ponto flutuante entre e incluindo, 0 e 100.|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições do sistema &#40;&#41;Transact-SQL](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  
