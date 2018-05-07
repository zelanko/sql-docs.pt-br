---
title: sp_set_session_context (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server 2016 Preview
f1_keywords:
- sp_set_session_context
- sp_set_session_context_TSQL
- sys.sp_set_session_context
- sys.sp_set_session_context_TSQL
helpviewer_keywords:
- sp_set_session_context
ms.assetid: 7a3a3b2a-1408-4767-a376-c690e3c1fc5b
caps.latest.revision: 7
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 2d1396ef79eb69b96a40f075c50cd38b6ad77d24
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="spsetsessioncontext-transact-sql"></a>sp_set_session_context (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Define um par chave-valor no contexto da sessão.  
  

 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sp_set_session_context [ @key= ] 'key', [ @value= ] 'value'  
    [ , [ @read_only = ] { 0 | 1 } ]  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @key=] 'key'  
 A chave que está sendo definida, do tipo **sysname**. O tamanho de chave máximo é 128 bytes.  
  
 [ @value=] 'value'  
 O valor para a chave especificada, do tipo **sql_variant**. Definir um valor NULL libera a memória. O tamanho máximo é 8.000 bytes.  
  
 [ @read_only= ] { 0 | 1 }  
 Um sinalizador de tipo **bit**. Se for 1, em seguida, o valor para a chave especificada não pode ser alterado novamente essa conexão lógica. Se 0 (padrão) e, em seguida, o valor pode ser alterado.  
  
## <a name="permissions"></a>Permissões  
 Qualquer usuário pode definir um contexto de sessão para sua sessão.  
  
## <a name="remarks"></a>Remarks  
 Como outros procedimentos armazenados, apenas literais e variáveis (não expressões ou chamadas de função) podem ser passados como parâmetros.  
  
 O tamanho total do contexto da sessão é limitado a 256 kb. Se definir um valor que faz com que esse limite ser excedido, a instrução falhará. Você pode monitorar o uso de memória global em [sys.DM os_memory_objects &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md).  
  
 Você pode monitorar o uso de memória global consultando [sys.DM os_memory_cache_counters &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-counters-transact-sql.md) da seguinte maneira: `SELECT * FROM sys.dm_os_memory_cache_counters WHERE type = 'CACHESTORE_SESSION_CONTEXT';`  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra como definir e, em seguida, retornar uma chave de contexto de sessões chamada linguagem com um valor de inglês.  
  
```  
EXEC sp_set_session_context 'language', 'English';  
SELECT SESSION_CONTEXT(N'language');  
```  
  
 O exemplo a seguir demonstra o uso do sinalizador somente leitura opcional.  
  
```  
EXEC sp_set_session_context 'user_id', 4, @read_only = 1;  
```  
  
## <a name="see-also"></a>Consulte também  
 [CURRENT_TRANSACTION_ID &#40;Transact-SQL&#41;](../../t-sql/functions/current-transaction-id-transact-sql.md)   
 [SESSION_CONTEXT &#40;Transact-SQL&#41;](../../t-sql/functions/session-context-transact-sql.md)   
 [Segurança em nível de linha](../../relational-databases/security/row-level-security.md)   
 [CONTEXT_INFO &#40;Transact-SQL&#41;](../../t-sql/functions/context-info-transact-sql.md)   
 [SET CONTEXT_INFO &#40;Transact-SQL&#41;](../../t-sql/statements/set-context-info-transact-sql.md)  
  
  
