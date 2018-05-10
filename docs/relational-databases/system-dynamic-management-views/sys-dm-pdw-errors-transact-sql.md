---
title: sys.dm_pdw_errors (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 944eac31-5691-432b-b9f5-f1e11c05191f
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 4dcabf9fdc35bfb074164f340b0bd70d7a8894fd
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmpdwerrors-transact-sql"></a>sys.dm_pdw_errors (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contém informações sobre todos os erros encontrados durante a execução de uma solicitação ou a consulta.  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|error_id|**nvarchar(36)**|Chave para este modo de exibição.<br /><br /> Id numérico exclusivo associado ao erro.|Exclusivo entre todos os erros de consulta no sistema.|  
|origem|**nvarchar(64)**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|Tipo|**nvarchar(4000)**|Tipo do erro ocorrido.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|create_time|**datetime**|Hora em que o erro ocorreu.|Menor ou igual à hora atual.|  
|pwd_node_id|**Int**|Identificador do nó específico envolvido, se houver. Para obter informações adicionais sobre as ids de nó, consulte [sys.dm_pdw_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).||  
|session_id|**nvarchar(32)**|Identificador da sessão envolvida, se houver. Para obter informações adicionais sobre as ids da sessão, consulte [sys.dm_pdw_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md).||  
|request_id|**nvarchar(32)**|Identificador da solicitação envolvida, se houver. Para obter informações adicionais sobre as ids de solicitação, consulte [sys.dm_pdw_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).||  
|spid|**Int**|SPID da sessão do SQL Server envolvida, se houver.||  
|thread_id|**Int**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|detalhes|**nvarchar(4000)**|Contém a descrição de texto de erro completa.||  
  
 Para obter informações sobre o máximo de linhas mantido por esta exibição, consulte a seção de valores máximos de modo de exibição de sistema no [valores mínimo e máximo (SQL Server PDW)](http://msdn.microsoft.com/en-us/5243f018-2713-45e3-9b61-39b2a57401b9) tópico.  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse Parallel Data Warehouse e exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
