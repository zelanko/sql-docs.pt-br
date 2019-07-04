---
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
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 25f9d67ee50f7c33391027d69c7db87aac8d7210
ms.sourcegitcommit: 869d4de6c807a37873b66e5479d2c5ceff9efb85
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67559424"
---
# <a name="spsetsessioncontext-transact-sql"></a>sp_set_session_context (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

Define um par chave-valor no contexto da sessão.  
  

 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sp_set_session_context [ @key= ] N'key', [ @value= ] 'value'  
    [ , [ @read_only = ] { 0 | 1 } ]  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @key= ] N'key'  
 A chave que está sendo definida, do tipo **sysname**. O tamanho de chave máximo é 128 bytes.  
  
 [ @value= ] 'value'  
 O valor para a chave especificada, do tipo **sql_variant**. Definir um valor NULL libera a memória. O tamanho máximo é 8.000 bytes.  
  
 [ @read_only= ] { 0 | 1 }  
 Um sinalizador de tipo **bit**. Se for 1, em seguida, o valor para a chave especificada não pode ser alterado novamente nessa conexão lógica. Se 0 (padrão) e, em seguida, o valor pode ser alterado.  
  
## <a name="permissions"></a>Permissões  
 Qualquer usuário pode definir um contexto de sessão para sua sessão.  
  
## <a name="remarks"></a>Comentários  
 Como outros procedimentos armazenados, apenas literais e variáveis (não a expressões ou chamadas de função) podem ser passadas como parâmetros.  
  
 O tamanho total do contexto da sessão é limitado a 1 MB. Se você definir um valor que faz com que esse limite ser excedido, a instrução falhará. Você pode monitorar o uso de memória global no [DM os_memory_objects &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md).  
  
 Você pode monitorar o uso de memória global consultando [DM os_memory_cache_counters &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-counters-transact-sql.md) da seguinte maneira: `SELECT * FROM sys.dm_os_memory_cache_counters WHERE type = 'CACHESTORE_SESSION_CONTEXT';`  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra como definir e, em seguida, retornar uma chave de contexto de sessões chamada linguagem com um valor de inglês.  
  
```  
EXEC sys.sp_set_session_context @key = N'language', @value = 'English';  
SELECT SESSION_CONTEXT(N'language');  
```  
  
 O exemplo a seguir demonstra o uso do sinalizador somente leitura opcional.  
  
```  
EXEC sys.sp_set_session_context @key = N'user_id', @value = 4, @read_only = 1;  
```  
  
## <a name="see-also"></a>Consulte também  
 [CURRENT_TRANSACTION_ID &#40;Transact-SQL&#41;](../../t-sql/functions/current-transaction-id-transact-sql.md)   
 [SESSION_CONTEXT &#40;Transact-SQL&#41;](../../t-sql/functions/session-context-transact-sql.md)   
 [Segurança em nível de linha](../../relational-databases/security/row-level-security.md)   
 [CONTEXT_INFO &#40;Transact-SQL&#41;](../../t-sql/functions/context-info-transact-sql.md)   
 [SET CONTEXT_INFO &#40;Transact-SQL&#41;](../../t-sql/statements/set-context-info-transact-sql.md)  
  
  
