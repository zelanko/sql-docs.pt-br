---
title: sys.dm_pdw_exec_connections (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
ms.assetid: 2625466b-d0ef-4c71-bedc-6d13491a8351
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 201c0fe2d8396d5669f2a05ef43343522827c465
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmpdwexecconnections-transact-sql"></a>sys.dm_pdw_exec_connections (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Retorna informações sobre as conexões estabelecidas com essa instância do [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e os detalhes de cada conexão.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|session_id|**Int**|Identifica a sessão associada a esta conexão. Use `SESSION_ID()` para retornar o `session_id` da conexão atual.|  
|connect_time|**datetime**|Carimbo de data/hora de quando a conexão foi estabelecida. Não permite valor nulo.|  
|encrypt_option|**nvarchar(40)**|Indica a TRUE (a conexão é criptografada) ou falso (conexão não é enctypred).|  
|auth_scheme|**nvarchar(40)**|Especifica o esquema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/Autenticação do Windows usado com esta conexão. Não permite valor nulo.|  
|client_id|**varchar(48)**|Endereço IP do cliente que se conecta a esse servidor. Permite valor nulo.|  
|sql_spid|**Int**|A ID de processo do servidor da conexão. Use `@@SPID` para retornar o `sql_spid` da conexão atual. Para propósitos de mais, use o `session_id` em vez disso.|  
  
## <a name="permissions"></a>Permissões  
 Requer **VIEW SERVER STATE** permissão no servidor.  
  
## <a name="relationship-cardinalities"></a>Cardinalidades de relações  
  
||||  
|-|-|-|  
|dm_pdw_exec_sessions.session_id|dm_pdw_exec_connections.session_id|Um para um|  
|dm_pdw_exec_requests.connection_id|dm_pdw_exec_connections.connection_id|Muitos para um|  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Consulta típica para reunir informações sobre a própria conexão de consultas.  
  
```  
SELECT  
    c.session_id, c.encrypt_option,  
    c.auth_scheme, s.client_id, s.login_name,   
    s.status, s.query_count  
FROM sys.dm_pdw_exec_connections AS c  
JOIN sys.dm_pdw_exec_sessions AS s  
    ON c.session_id = s.session_id  
WHERE c.session_id = SESSION_ID();  
```  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse e exibições de gerenciamento dinâmico do Parallel Data Warehouse &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  

