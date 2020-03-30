---
title: DROP EVENT SESSION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_EVENT_SESSION_TSQL
- DROP EVENT SESSION
dev_langs:
- TSQL
helpviewer_keywords:
- event sessions [SQL Server]
- DROP EVENT SESSION statement
ms.assetid: 92eabe4b-24e2-43b1-978c-31a199964b90
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b408b030a27b1e6ebe0fc94db8b6ee32cbb837ed
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "67898044"
---
# <a name="drop-event-session-transact-sql"></a>DROP EVENT SESSION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove uma sessão de evento.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```    
DROP EVENT SESSION event_session_name  
ON SERVER  
```  
  
## <a name="arguments"></a>Argumentos  
 *event_session_name*  
 É o nome de uma sessão de evento existente.  
  
## <a name="remarks"></a>Comentários  
 Quando você descartar uma sessão de evento, todas as informações de configuração, como parâmetros de destinos e sessão, serão completamente removidas.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão `ALTER ANY EVENT SESSION`.  
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir mostra como descartar uma sessão de evento.  
  
```sql  
DROP EVENT SESSION evt_spin_lock_diagnosis ON SERVER;
GO
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md)   
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-event-session-transact-sql.md)   
 [sys.server_event_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql.md)  
  
  
