---
title: sys. dm_pdw_nodes_exec_sql_text (Transact-SQL) | Microsoft Docs
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
ms.openlocfilehash: dcfa1bf254bc60ee1bd2c65ddb813851d0bd369e
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87394314"
---
# <a name="syspdw_nodes_dm_exec_sql_text-transact-sql"></a>sys. pdw_nodes_dm_exec_sql_text (Transact-SQL)
[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

Retorna o texto do lote SQL que é identificado pelo *sql_handle*especificado. Esta função com valor de tabela substitui a função do sistema **fn_get_sql**.  
   
## <a name="table-returned"></a>Tabela retornada  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**pdw_node_id**|**int**|ID numérica exclusiva associada ao nó.|
|**DBID**|**smallint**|ID do banco de dados.<br /><br /> Para instruções SQL não planejadas e preparadas, a ID do banco de dados em que as instruções foram compiladas.|  
|**ObjectID**|**int**|ID do objeto.<br /><br /> É NULL para instruções SQL ad hoc e preparadas.|  
|**number**|**smallint**|Para um procedimento armazenado numerado, esta coluna retorna o número do procedimento armazenado. Para obter mais informações, consulte [Sys. numbered_procedures &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-numbered-procedures-transact-sql.md).<br /><br /> É NULL para instruções SQL ad hoc e preparadas.|  
|**criptografados**|**bit**|1: o texto SQL é criptografado.<br /><br /> 0: o texto SQL não está criptografado.|  
|**text**|**nvarchar(max)**|Texto da consulta SQL.<br /><br /> É NULL para objetos criptografados.|  

## <a name="remarks"></a>Comentários  
Os mesmos comentários em [Sys. dm_exec_sql_text](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql?view=sql-server-ver15) se aplicam.  
  
## <a name="permissions"></a>Permissões  
 Exigir a função de servidor **sysadmin** ou `VIEW SERVER STATE` a permissão no servidor.  
  
## <a name="see-also"></a>Confira também  
 [Exibições de gerenciamento dinâmico de SQL Data Warehouse e paralelo data warehouse &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  

  ## <a name="next-steps"></a>Próximas etapas
 Para obter mais dicas de desenvolvimento, consulte [Visão geral de desenvolvimento do SQL Data Warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-develop).