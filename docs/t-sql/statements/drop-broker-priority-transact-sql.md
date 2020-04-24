---
title: DROP BROKER PRIORITY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_BROKER_PRIORITY_TSQL
- DROP BROKER PRIORITY
dev_langs:
- TSQL
helpviewer_keywords:
- DROP BROKER PRIORITY statement
ms.assetid: 09ee6c5b-af94-4a4b-a0e2-f9eac50e43aa
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b5308ac813b948dea45acf24751e3ada453a4d19
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81635795"
---
# <a name="drop-broker-priority-transact-sql"></a>DROP BROKER PRIORITY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove uma prioridade de conversa do banco de dados atual.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
  
DROP BROKER PRIORITY ConversationPriorityName  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *ConversationPriorityName*  
 Especifica o nome da prioridade de conversa a ser removido.  
  
## <a name="remarks"></a>Comentários  
 Quando você descarta uma prioridade de conversa, as conversas existentes continuam a funcionar com os níveis de prioridade atribuídos a partir da prioridade de conversa.  
  
## <a name="permissions"></a>Permissões  
 A permissão para criar uma prioridade de conversa assume como padrão os membros das funções de banco de dados fixas db_ddladmin ou db_owner e a função de servidor fixa sysadmin. Requer a permissão ALTER no banco de dados.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir descarta a prioridade de conversa denominada `InitiatorAToTargetPriority`.  
  
```  
DROP BROKER PRIORITY InitiatorAToTargetPriority;  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER BROKER PRIORITY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-broker-priority-transact-sql.md)   
 [CREATE BROKER PRIORITY &#40;Transact-SQL&#41;](../../t-sql/statements/create-broker-priority-transact-sql.md)   
 [sys.conversation_priorities &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-conversation-priorities-transact-sql.md)  
  
  
