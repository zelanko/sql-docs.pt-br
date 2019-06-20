---
title: sys.dm_exec_compute_node_errors (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SYS.DM_EXEC_COMPUTE_NODE_ERRORS_TSQL
- DM_EXEC_COMPUTE_NODE_ERRORS
- DM_EXEC_COMPUTE_NODE_ERRORS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase
- PolyBase, views
- dm_exec_compute_node_errors
- sys.dm_exec_compute_node_errors management view
ms.assetid: 9a03c039-70e4-4974-95d8-d3fa45984ffb
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b5a11a5e7090f89f4a31ffd15f8ebbce78ea395a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63013395"
---
# <a name="sysdmexeccomputenodeerrors-transact-sql"></a>sys.dm_exec_compute_node_errors (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Erros de retorna que ocorrem no PolyBase nós de computação.  
  
|Nome da coluna|Tipo de Dados|Descrição|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|error_id|**nvarchar(36)**|Id numérico exclusivo associado ao erro.|Exclusivo em todos os erros de consulta no sistema|  
|source|**nvarchar(255)**|Descrição da fonte de thread ou processo||  
|type|**nvarchar(255)**|Tipo de erro.||  
|create_time|**datetime**|A hora da ocorrência do erro||  
|compute_node_id|**int**|Identificador do nó de computação específico|Consulte compute_node_id dos [DM exec_compute_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)|  
|rexecution_id|**nvarchar(36)**|Identificador da consulta do PolyBase, se houver.||  
|spid|**int**|Identificador da sessão do SQL Server||  
|thread_id|**int**|Identificador numérico do thread no qual ocorreu o erro.||  
|detalhes|nvarchar(4000)|Descrição completa dos detalhes do erro.||  
  
## <a name="see-also"></a>Consulte também  
 [Solução de problemas com exibições de gerenciamento dinâmico do PolyBase](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Banco de dados relacionados a exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
