---
title: sys. dm _pdw_nodes_exec_text_query_plan (Transact-SQL) | Microsoft Docs
description: Exibição de gerenciamento dinâmico que retorna o Showplan no formato de texto para um lote TSQL ou para uma instrução específica dentro do lote.
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
ms.openlocfilehash: 45f26c9569950c2450318abf546a838632e06f20
ms.sourcegitcommit: af6f66cc3603b785a7d2d73d7338961a5c76c793
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/30/2019
ms.locfileid: "73145661"
---
# <a name="sysdm_pdw_nodes_exec_text_query_plan--transact-sql"></a>sys. dm _pdw_nodes_exec_text_query_plan (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Retorna o plano de execução em formato de texto para um lote [!INCLUDE[tsql](../../includes/tsql-md.md)] ou para uma instrução específica dentro do lote.

## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de Dados|Description|  
|-----------------|---------------|-----------------|  
|**pdw_node_ID**|**Int**|ID numérica exclusiva associada ao nó.|
|**dbid**|**smallint**|A ID do banco de dados de contexto em vigor quando a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] correspondente a esse plano foi compilada. Para instruções SQL preparadas e ad hoc, a ID do banco de dados no qual as instruções foram compiladas.<br /><br /> A coluna é anulável.|  
|**objectid**|**Int**|A identificação do objeto (por exemplo, procedimento armazenado ou função definida pelo usuário) para este plano de consulta. Para lotes ad hoc e preparados, essa coluna é **nula**.<br /><br /> A coluna é anulável.|  
|**number**|**smallint**|Inteiro de procedimento armazenado numerado. Para lotes ad hoc e preparados, essa coluna é **nula**.<br /><br /> A coluna é anulável.| 
|**criptografados**|**bit**|Indica se o procedimento armazenado correspondente está criptografado.<br /><br /> 0 = não criptografado<br /><br /> 1 = criptografado<br /><br /> A coluna não é anulável.|  
|**query_plan**|**nvarchar(max)**|Contém a representação de SHOWPLAN de tempo de compilação do plano de execução de consulta especificado com *plan_handle*. O Showplan está em formato de texto. Um plano é gerado para cada lote que contém, por exemplo, instruções ad hoc [!INCLUDE[tsql](../../includes/tsql-md.md)], chamadas de procedimento armazenado e chamadas de função definidas pelo usuário.<br /><br /> A coluna é anulável.|  

## <a name="remarks"></a>Remarks  
Os mesmos comentários em [Sys. dm _exec_text_query_plan](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-text-query-plan-transact-sql?view=sql-server-ver15) se aplicam.  

## <a name="permissions"></a>Permissões  
 Requer a função de servidor **sysadmin** ou a permissão `VIEW SERVER STATE` no servidor.  
  
## <a name="see-also"></a>Confira também  
 [Exibições &#40;de gerenciamento dinâmico SQL data warehouse e Parallel Data Warehouse TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  

  ## <a name="next-steps"></a>Próximas etapas
 Para obter mais dicas de desenvolvimento, consulte [visão geral do desenvolvimento de SQL data warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-develop).