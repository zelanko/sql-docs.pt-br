---
title: sys.DM exec_input_buffer (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_input_buffer
- sys.dm_exec_input_buffer _tsql
- dm_exec_input_buffer
- dm_exec_input_buffer_tsql
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_input_buffer dynamic management function
ms.assetid: fb34a560-bde9-4ad9-aa96-0d4baa4fc104
caps.latest.revision: 12
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 30ee3c91cbe526180f1df47023963bd8bd167c48
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmexecinputbuffer-transact-sql"></a>sys.dm_exec_input_buffer (Transact-SQL)
[!INCLUDE[tsql-appliesto-2014sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2014sp2-asdb-xxxx-xxx-md.md)]

  Retorna informações sobre instruções enviadas a uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sys.dm_exec_input_buffer ( session_id , request_id )
```  
  
## <a name="arguments"></a>Argumentos  
*session_id*  
A id de sessão está executando o lote a ser pesquisado. *session_id* é **smallint**. *session_id* pode ser obtido dos seguintes objetos de gerenciamento dinâmico:  
  
-   [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
-   [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)  
  
-   [sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md)   
  
*request_id*  
Request_id de [exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md). *request_id* é **int**.  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**event_type**|**nvarchar(256)**|O tipo de evento no buffer de entrada para determinado spid.|  
|**parameters**|**smallint**|Quaisquer parâmetros fornecidos para a instrução.|  
|**event_info**|**nvarchar(max)**|O texto da instrução no buffer de entrada para determinado spid.|  
  
## <a name="permissions"></a>Permissões  
 Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se o usuário tem permissão VIEW SERVER STATE, o usuário verá a execução de todas as sessões na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; caso contrário, o usuário verá apenas a sessão atual.  
  
 Em [!INCLUDE[ssSDS](../../includes/sssds-md.md)], se o usuário for o proprietário do banco de dados, o usuário verá a execução de todas as sessões no [!INCLUDE[ssSDS](../../includes/sssds-md.md)]; caso contrário, o usuário verá apenas a sessão atual.  
  
## <a name="remarks"></a>Remarks  
 Essa função de gerenciamento dinâmico pode ser usada em conjunto com Sys.DM exec_sessions ou sys.DM exec_requests fazendo **CROSS APPLY**.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-simple-example"></a>A. Exemplo simples  
 O exemplo a seguir demonstra como passar uma id de sessão (SPID) e uma id de solicitação para a função.  
  
```sql  
SELECT * FROM sys.dm_exec_input_buffer (52, 0);
GO
```  
  
### <a name="b-using-cross-apply-to-additional-information"></a>B. Com o uso entre aplicam-se para obter informações adicionais  
 O exemplo a seguir lista o buffer de entrada para sessões com a id de sessão maior que 50.  
  
```sql  
SELECT es.session_id, ib.event_info   
FROM sys.dm_exec_sessions AS es  
CROSS APPLY sys.dm_exec_input_buffer(es.session_id, NULL) AS ib  
WHERE es.session_id > 50;
GO
```  
  
## <a name="see-also"></a>Consulte também  
 [Funções e exibições de gerenciamento dinâmico relacionadas à execução &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [DBCC INPUTBUFFER &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-inputbuffer-transact-sql.md)  
