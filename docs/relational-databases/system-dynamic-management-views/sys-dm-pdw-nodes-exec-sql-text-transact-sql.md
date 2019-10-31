---
title: sys. dm _pdw_nodes_exec_sql_text (Transact-SQL) | Microsoft Docs
description: Exibição de gerenciamento dinâmico que retorna o texto do lote SQL que é identificado pelo sql_handle especificado.
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
ms.openlocfilehash: fd886217b2fb2caf0fe3f32e88b7bf0215ece1a9
ms.sourcegitcommit: af6f66cc3603b785a7d2d73d7338961a5c76c793
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/30/2019
ms.locfileid: "73145671"
---
# <a name="syspdw_nodes_dm_exec_sql_text-transact-sql"></a>sys. PDW _nodes_dm_exec_sql_text (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Retorna o texto do lote SQL que é identificado pelo *sql_handle*especificado. Essa função com valor de tabela substitui a função de sistema **fn_get_sql**.  
   
## <a name="table-returned"></a>Tabela retornada  
|Nome da coluna|Tipo de Dados|Description|  
|-----------------|---------------|-----------------|  
|**pdw_node_id**|**Int**|ID numérica exclusiva associada ao nó.|
|**dbid**|**smallint**|ID do banco de dados.<br /><br /> Para instruções SQL não planejadas e preparadas, a ID do banco de dados em que as instruções foram compiladas.|  
|**objectid**|**Int**|ID do objeto.<br /><br /> É NULL para instruções SQL ad hoc e preparadas.|  
|**number**|**smallint**|Para um procedimento armazenado numerado, esta coluna retorna o número do procedimento armazenado. Para obter mais informações, consulte [Sys. &#40;NUMBERED_PROCEDURES Transact-&#41;SQL](../../relational-databases/system-catalog-views/sys-numbered-procedures-transact-sql.md).<br /><br /> É NULL para instruções SQL ad hoc e preparadas.|  
|**criptografados**|**bit**|1: o texto SQL é criptografado.<br /><br /> 0: o texto SQL não está criptografado.|  
|**texto**|**nvarchar(max)**|Texto da consulta SQL.<br /><br /> É NULL para objetos criptografados.|  

## <a name="remarks"></a>Remarks  
Os mesmos comentários em [Sys. dm _exec_sql_text](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql?view=sql-server-ver15) se aplicam.  
  
## <a name="permissions"></a>Permissões  
 Requer a função de servidor **sysadmin** ou a permissão `VIEW SERVER STATE` no servidor.  
  
## <a name="see-also"></a>Confira também  
 [Exibições &#40;de gerenciamento dinâmico SQL data warehouse e Parallel Data Warehouse TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  

  ## <a name="next-steps"></a>Próximas etapas
 Para obter mais dicas de desenvolvimento, consulte [visão geral do desenvolvimento de SQL data warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-develop).