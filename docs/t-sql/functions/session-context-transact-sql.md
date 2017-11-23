---
title: SESSION_CONTEXT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/22/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SESSION_CONTEXT
- sys.SESSION_CONTEXT
- SESSION_CONTEXT_TSQL
- sys.SESSION_CONTEXT_TSQL
helpviewer_keywords: SESSION_CONTEXT function
ms.assetid: b6bdbc54-331a-43cc-ab3d-3872d6a12100
caps.latest.revision: "11"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3bf9da8f88f28b71e4133900384f27d37729d695
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="sessioncontext-transact-sql"></a>SESSION_CONTEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Retorna o valor da chave especificada no contexto da sessão atual. O valor é definido usando o [sp_set_session_context &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md) procedimento.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
SESSION_CONTEXT(N'key')  
```  
  
## <a name="arguments"></a>Argumentos  
 'key'  
 A chave (tipo sysname) do valor que está sendo recuperado.  
  
## <a name="return-type"></a>Tipo de retorno  
 **sql_variant**  
  
## <a name="return-value"></a>Valor de retorno  
 O valor associado com a chave especificada no contexto de sessão, ou nulo se nenhum valor foi definido para essa chave.  
  
## <a name="permissions"></a>Permissões  
 Qualquer usuário pode ler o contexto de sessão para sua sessão.  
  
## <a name="remarks"></a>Comentários  
 Comportamento de MARS do SESSION_CONTEXT é semelhante ao de CONTEXT_INFO. Se um lote MARS define um par chave-valor, o novo valor não retornará em outros lotes MARS na conexão a mesma, a menos que eles começaram a após o lote que definiu o novo valor. Se vários lotes MARS estão ativos em uma conexão, os valores não podem ser definidos como "read_only." Isso evita as condições de corrida e determinismo sobre qual valor de "wins".  
  
## <a name="examples"></a>Exemplos  
 O exemplo simples a seguir define o valor de contexto de sessão para a chave `user_id` 4 e, em seguida, usa o **SESSION_CONTEXT** função para recuperar o valor.  
  
```  
EXEC sp_set_session_context 'user_id', 4;  
SELECT SESSION_CONTEXT(N'user_id');  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_set_session_context &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md)   
 [CURRENT_TRANSACTION_ID &#40; Transact-SQL &#41;](../../t-sql/functions/current-transaction-id-transact-sql.md)   
 [Segurança em nível de linha](../../relational-databases/security/row-level-security.md)   
 [CONTEXT_INFO &#40; Transact-SQL &#41;](../../t-sql/functions/context-info-transact-sql.md)   
 [Definir CONTEXT_INFO &#40; Transact-SQL &#41;](../../t-sql/statements/set-context-info-transact-sql.md)  
  
  
