---
title: CURRENT_TRANSACTION_ID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CURRENT_TRANSACTION_ID
- CURRENT_TRANSACTION_ID_TSQL
- sys.CURRENT_TRANSACTION_ID
- sys.CURRENT_TRANSACTION_ID_TSQL
helpviewer_keywords:
- CURRENT_TRANSACTION_ID function
ms.assetid: 82cd9f92-d935-45a0-a433-620d6e15b467
caps.latest.revision: 6
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 73a9583e40d73a48b7e8ddfdf8eddf8d38b743c7
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="currenttransactionid-transact-sql"></a>CURRENT_TRANSACTION_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Essa função retorna a ID da transação atual na sessão atual.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
CURRENT_TRANSACTION_ID( )  
  
```  
  
## <a name="return-types"></a>Tipos de retorno
**bigint**
  
## <a name="return-value"></a>Valor retornado  
A ID da transação atual na sessão atual, obtida em [sys.dm_tran_current_transaction &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-current-transaction-transact-sql.md).
  
## <a name="permissions"></a>Permissões  
Qualquer usuário pode retornar a ID da transação da sessão atual.
  
## <a name="examples"></a>Exemplos  
Este exemplo retorna a ID da transação da sessão atual:
  
```sql
SELECT CURRENT_TRANSACTION_ID();  
```  
  
## <a name="see-also"></a>Confira também
[sp_set_session_context &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md)  
[SESSION_CONTEXT &#40;Transact-SQL&#41;](../../t-sql/functions/session-context-transact-sql.md)  
[Segurança em nível de linha](../../relational-databases/security/row-level-security.md)  
[CONTEXT_INFO &#40;Transact-SQL&#41;](../../t-sql/functions/context-info-transact-sql.md)  
[SET CONTEXT_INFO &#40;Transact-SQL&#41;](../../t-sql/statements/set-context-info-transact-sql.md)
  
  
