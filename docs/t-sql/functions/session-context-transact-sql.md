---
title: SESSION_CONTEXT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/22/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SESSION_CONTEXT
- sys.SESSION_CONTEXT
- SESSION_CONTEXT_TSQL
- sys.SESSION_CONTEXT_TSQL
helpviewer_keywords:
- SESSION_CONTEXT function
ms.assetid: b6bdbc54-331a-43cc-ab3d-3872d6a12100
caps.latest.revision: 11
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 9f27e101de22ee92b912febfbb33c907a62aae4f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sessioncontext-transact-sql"></a>SESSION_CONTEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Retorna o valor da chave especificada no contexto de sessão atual. O valor é definido com o procedimento [sp_set_session_context &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
SESSION_CONTEXT(N'key')  
```  
  
## <a name="arguments"></a>Argumentos  
 'key'  
 A chave (tipo sysname) do valor que está sendo recuperado.  
  
## <a name="return-type"></a>Tipo de retorno  
 **sql_variant**  
  
## <a name="return-value"></a>Valor retornado  
 O valor associado à chave especificada no contexto de sessão ou NULL se nenhum valor foi definido para essa chave.  
  
## <a name="permissions"></a>Permissões  
 Qualquer usuário pode ler o contexto de sessão de sua sessão.  
  
## <a name="remarks"></a>Remarks  
 O comportamento de MARS de SESSION_CONTEXT é semelhante ao de CONTEXT_INFO. Se um lote MARS definir um par chave-valor, o novo valor não será retornado em outros lotes MARS na mesma conexão, a menos que eles tenham sido iniciados após a conclusão do lote que definiu o novo valor. Se vários lotes MARS estiverem ativos em uma conexão, os valores não poderão ser definidos como "read_only". Isso impede condições de corrida e não determinismo sobre qual valor "vence".  
  
## <a name="examples"></a>Exemplos  
 O exemplo simples a seguir define o valor de contexto de sessão para a chave `user_id` como 4 e, em seguida, usa a função **SESSION_CONTEXT** para recuperar o valor.  
  
```  
EXEC sp_set_session_context 'user_id', 4;  
SELECT SESSION_CONTEXT(N'user_id');  
```  
  
## <a name="see-also"></a>Consulte Também  
 [sp_set_session_context &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md)   
 [CURRENT_TRANSACTION_ID &#40;Transact-SQL&#41;](../../t-sql/functions/current-transaction-id-transact-sql.md)   
 [Segurança em nível de linha](../../relational-databases/security/row-level-security.md)   
 [CONTEXT_INFO &#40;Transact-SQL&#41;](../../t-sql/functions/context-info-transact-sql.md)   
 [SET CONTEXT_INFO &#40;Transact-SQL&#41;](../../t-sql/statements/set-context-info-transact-sql.md)  
  
  
