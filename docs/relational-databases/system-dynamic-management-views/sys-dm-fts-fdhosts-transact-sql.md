---
title: sys.dm_fts_fdhosts (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_fts_fdhosts
- dm_fts_fdhosts_TSQL
- sys.dm_fts_fdhosts
- sys.dm_fts_fdhosts_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_fdhosts dynamic management view
- troubleshooting [SQL Server], full-text search
ms.assetid: d42a6334-4362-4361-83da-f8324fe55ec7
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 0cd3980a605d3ec5d922eccda0799c78a5415beb
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmftsfdhosts-transact-sql"></a>sys.dm_fts_fdhosts (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna informações sobre a atividade atual do host (ou hosts) daemon do filtro da instância de servidor.  
  
 
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**fdhost_id**|**Int**|ID do host daemon do filtro.|  
|**fdhost_name**|**nvarchar(120)**|Nome de host daemon do filtro.|  
|**fdhost_process_id**|**Int**|ID de processo do Windows do host daemon do filtro.|  
|**fdhost_type**|**nvarchar(120)**|Tipo de documento que está sendo processado pelo host daemon do filtro, um de:<br /><br /> Thread único<br /><br /> Multi-thread<br /><br /> Documento enorme|  
|**max_thread**|**Int**|Número de máximo de threads no host daemon do filtro.|  
|**batch_count**|**Int**|Número de lotes que estão sendo processados no host daemon do filtro.|  
  
## <a name="permissions"></a>Permissões  

Em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requer o `VIEW DATABASE STATE` no banco de dados.   

## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna o nome do host daemon do filtro e seu número máximo de threads. Ele também monitora quantos lotes estão sendo processados no daemon do filtro. Essa informação pode ser usada para diagnosticar o desempenho.  
  
```  
SELECT fdhost_name, batch_count, max_thread FROM sys.dm_fts_fdhosts;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Pesquisa de texto completo e funções e exibições de gerenciamento dinâmico de pesquisa semântica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [Pesquisa de Texto Completo](../../relational-databases/search/full-text-search.md)  
  
  
