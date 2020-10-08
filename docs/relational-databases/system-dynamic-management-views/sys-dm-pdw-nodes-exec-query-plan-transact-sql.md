---
title: sys.dm_pdw_nodes_exec_query_plan (Transact-SQL) | Microsoft Docs
description: Exibição de gerenciamento dinâmico que retorna o Showplan em formato XML para o lote especificado pelo identificador de plano. O plano especificado pelo identificador do plano pode estar em cache ou estar sendo executado.
ms.custom: ''
ms.date: 10/14/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: ''
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: =azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 40f8c69f595665c4188c76aded00517512620bb1
ms.sourcegitcommit: 32135463a8494d9ed1600a58f51819359e3c09dc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/08/2020
ms.locfileid: "91834348"
---
# <a name="syspdw_nodes_dm_exec_query_plan-transact-sql"></a>sys.pdw_nodes_dm_exec_query_plan (Transact-SQL)
[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

Retorna o plano de execução em formato XML para o lote especificado pelo identificador de plano. O plano especificado pelo identificador do plano pode estar em cache ou estar sendo executado.  

## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**pdw_node_id**|**int**|ID numérica exclusiva associada ao nó.| 
|**DBID**|**smallint**|A ID do banco de dados de contexto em vigor quando a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] correspondente a esse plano foi compilada. Para instruções SQL não planejadas e preparadas, a ID do banco de dados em que as instruções foram compiladas.<br /><br /> A coluna é anulável.|  
|**objectid**|**int**|A identificação do objeto (por exemplo, procedimento armazenado ou função definida pelo usuário) para este plano de consulta. Para lotes ad hoc e preparados, essa coluna é **null**.<br /><br /> A coluna é anulável.|  
|**number**|**smallint**|Inteiro de procedimento armazenado numerado. Para lotes ad hoc e preparados, essa coluna é **null**.<br /><br /> A coluna é anulável.| 
|**criptografados**|**bit**|Indica se o procedimento armazenado correspondente está criptografado.<br /><br /> 0 = não criptografado<br /><br /> 1 = criptografado<br /><br /> A coluna não é anulável.|  
|**query_plan**|**xml**|Contém a representação de SHOWPLAN de tempo de compilação do plano de execução de consulta especificado com *plan_handle*. O Showplan está em formato XML. Um plano é gerado para cada lote que contém, por exemplo, instruções ad hoc [!INCLUDE[tsql](../../includes/tsql-md.md)], chamadas de procedimento armazenado e chamadas de função definidas pelo usuário.<br /><br /> A coluna é anulável.|  
  
## <a name="remarks"></a>Comentários  
Os mesmos comentários em [Sys.dm_exec_query_plan](./sys-dm-exec-query-plan-transact-sql.md?view=sql-server-ver15) se aplicam.  
  
## <a name="permissions"></a>Permissões  
 Exigir a função de servidor **sysadmin** ou `VIEW SERVER STATE` a permissão no servidor.  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de gerenciamento dinâmico de SQL Data Warehouse e paralelo data warehouse &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  

 ## <a name="next-steps"></a>Próximas etapas
 Para obter mais dicas de desenvolvimento, consulte [Visão geral de desenvolvimento do SQL Data Warehouse](/azure/sql-data-warehouse/sql-data-warehouse-overview-develop).