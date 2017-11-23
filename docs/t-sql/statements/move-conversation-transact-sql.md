---
title: Mover a CONVERSA (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- MOVE_CONVERSATION_TSQL
- MOVE CONVERSATION
- MOVE_TSQL
- MOVE
dev_langs: TSQL
helpviewer_keywords:
- moving conversations
- MOVE CONVERSATION statement
- relocating conversations
- conversations [Service Broker], groups
- conversations [Service Broker], moving
ms.assetid: 1da4d2c9-e767-434e-b49b-615711a7f626
caps.latest.revision: "28"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7367254b7dad104c7503c33777d26316a542b4ca
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="move-conversation-transact-sql"></a>MOVE CONVERSATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Move uma conversa a um grupo de conversa diferente.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
MOVE CONVERSATION conversation_handle  
   TO conversation_group_id  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *conversation_handle*  
 É uma variável ou constante que contém o identificador de conversa da conversa a ser movida. *conversation_handle* deve ser do tipo **uniqueidentifier**.  
  
 PARA *conversation_group_id*  
 É uma variável ou constante que contém o identificador do grupo de conversa para o qual a conversa será movida. *conversation_group_id* deve ser do tipo **uniqueidentifier**.  
  
## <a name="remarks"></a>Comentários  
 A instrução MOVE CONVERSATION move a conversa especificada por *conversation_handle* para o grupo de conversa identificado por *conversation_group_id*. Os diálogos só podem ser redirecionados entre grupos de conversa que são associados com a mesma fila.  
  
> [!IMPORTANT]  
>  Se a instrução MOVE CONVERSATION não é a primeira instrução em um lote ou procedimento armazenado, a instrução anterior deverá ser encerrada com um ponto e vírgula (**;**), o [!INCLUDE[tsql](../../includes/tsql-md.md)] terminador de instrução.  
  
 A instrução MOVE CONVERSATION bloqueia o grupo de conversação associado *conversation_handle* e o grupo de conversa especificado por *conversation_group_id* até que a transação que contém a instrução é confirmada ou revertida.  
  
 MOVE CONVERSATION não é válida em uma função definida pelo usuário.  
  
## <a name="permissions"></a>Permissões  
 Para mover uma conversa, o usuário atual deve ser o proprietário da conversa e do grupo de conversa, ou um membro da função de servidor fixa sysadmin, ou um membro da função de banco de dados fixa db_owner fixed.  
  
## <a name="examples"></a>Exemplos  
 O exemplo seguinte move uma conversa a um grupo de conversa diferente.  
  
```  
DECLARE @conversation_handle UNIQUEIDENTIFIER,  
        @conversation_group_id UNIQUEIDENTIFIER ;  
  
SET @conversation_handle =  
    <retrieve conversation handle from database> ;  
SET @conversation_group_id =  
    <retrieve conversation group ID from database> ;  
  
MOVE CONVERSATION @conversation_handle TO @conversation_group_id ;  
```  
  
## <a name="see-also"></a>Consulte também  
 [BEGIN DIALOG CONVERSATION &#40; Transact-SQL &#41;](../../t-sql/statements/begin-dialog-conversation-transact-sql.md)   
 [OBTER grupo de conversação &#40; Transact-SQL &#41;](../../t-sql/statements/get-conversation-group-transact-sql.md)   
 [Instrução END CONVERSATION &#40; Transact-SQL &#41;](../../t-sql/statements/end-conversation-transact-sql.md)   
 [conversation_groups &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-conversation-groups-transact-sql.md)   
 [conversation_endpoints &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-conversation-endpoints-transact-sql.md)  
  
  
