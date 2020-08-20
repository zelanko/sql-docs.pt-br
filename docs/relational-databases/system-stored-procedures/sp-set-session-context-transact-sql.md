---
description: sp_set_session_context (Transact-SQL)
title: sp_set_session_context (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/14/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_set_session_context
- sp_set_session_context_TSQL
- sys.sp_set_session_context
- sys.sp_set_session_context_TSQL
helpviewer_keywords:
- sp_set_session_context
ms.assetid: 7a3a3b2a-1408-4767-a376-c690e3c1fc5b
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7f1aff8d7d8496604983c54099f818e98fffbf18
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88493042"
---
# <a name="sp_set_session_context-transact-sql"></a>sp_set_session_context (Transact-SQL)
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

Define um par chave-valor no contexto da sessão.  
  

 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sp_set_session_context [ @key= ] N'key', [ @value= ] 'value'  
    [ , [ @read_only = ] { 0 | 1 } ]  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @key =] N'key '  
 A chave que está sendo definida, do tipo **sysname**. O tamanho máximo da chave é 128 bytes.  
  
 [ @value =] ' valor '  
 O valor da chave especificada, do tipo **sql_variant**. A definição de um valor nulo libera a memória. O tamanho máximo é 8.000 bytes.  
  
 [ @read_only =] {0 | 1}  
 Um sinalizador do tipo **bit**. Se for 1, o valor da chave especificada não poderá ser alterado novamente nesta conexão lógica. Se for 0 (padrão), o valor poderá ser alterado.  
  
## <a name="permissions"></a>Permissões  
 Qualquer usuário pode definir um contexto de sessão para sua sessão.  
  
## <a name="remarks"></a>Comentários  
 Assim como outros procedimentos armazenados, somente literais e variáveis (não expressões ou chamadas de função) podem ser passados como parâmetros.  
  
 O tamanho total do contexto da sessão é limitado a 1 MB. Se você definir um valor que faz com que esse limite seja excedido, a instrução falhará. Você pode monitorar o uso geral de memória em [Sys. dm_os_memory_objects &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md).  
  
 Você pode monitorar o uso de memória geral consultando [Sys. dm_os_memory_cache_counters &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-counters-transact-sql.md) da seguinte maneira: `SELECT * FROM sys.dm_os_memory_cache_counters WHERE type = 'CACHESTORE_SESSION_CONTEXT';`  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra como definir e, em seguida, retornar uma chave de contexto de sessões chamada idioma com um valor de inglês.  
  
```  
EXEC sys.sp_set_session_context @key = N'language', @value = 'English';  
SELECT SESSION_CONTEXT(N'language');  
```  
  
 O exemplo a seguir demonstra o uso do sinalizador opcional somente leitura.  
  
```  
EXEC sys.sp_set_session_context @key = N'user_id', @value = 4, @read_only = 1;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de CURRENT_TRANSACTION_ID ](../../t-sql/functions/current-transaction-id-transact-sql.md)   
 [&#41;&#40;Transact-SQL de SESSION_CONTEXT ](../../t-sql/functions/session-context-transact-sql.md)   
 [Segurança em nível de linha](../../relational-databases/security/row-level-security.md)   
 [&#41;&#40;Transact-SQL de CONTEXT_INFO ](../../t-sql/functions/context-info-transact-sql.md)   
 [SET CONTEXT_INFO &#40;Transact-SQL&#41;](../../t-sql/statements/set-context-info-transact-sql.md)  
  
  
