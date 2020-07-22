---
title: MOVE CONVERSATION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- MOVE_CONVERSATION_TSQL
- MOVE CONVERSATION
- MOVE_TSQL
- MOVE
dev_langs:
- TSQL
helpviewer_keywords:
- moving conversations
- MOVE CONVERSATION statement
- relocating conversations
- conversations [Service Broker], groups
- conversations [Service Broker], moving
ms.assetid: 1da4d2c9-e767-434e-b49b-615711a7f626
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c06776bc9d3c8080349607a6d349b3bd0b7505de
ms.sourcegitcommit: edba1c570d4d8832502135bef093aac07e156c95
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/20/2020
ms.locfileid: "86484041"
---
# <a name="move-conversation-transact-sql"></a>MOVE CONVERSATION (Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  Move uma conversa a um grupo de conversa diferente.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
  
MOVE CONVERSATION conversation_handle  
   TO conversation_group_id  
[ ; ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *conversation_handle*  
 É uma variável ou constante que contém o identificador de conversa da conversa a ser movida. *conversation_handle* precisa ser do tipo **uniqueidentifier**.  
  
 TO *conversation_group_id*  
 É uma variável ou constante que contém o identificador do grupo de conversa para o qual a conversa será movida. *conversation_group_id* precisa ser do tipo **uniqueidentifier**.  
  
## <a name="remarks"></a>Comentários  
 A instrução MOVE CONVERSATION move a conversa especificada por *conversation_handle* para o grupo de conversa identificado por *conversation_group_id*. Os diálogos só podem ser redirecionados entre grupos de conversa que são associados com a mesma fila.  
  
> [!IMPORTANT]  
>  Se a instrução MOVE CONVERSATION não for a primeira instrução de um procedimento em lote ou armazenado, a instrução anterior deverá ser terminada com ponto e vírgula ( **;** ), o terminador de instrução do [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 A instrução MOVE CONVERSATION bloqueia o grupo de conversa associado a *conversation_handle* e o grupo de conversa especificado por *conversation_group_id* até que a transação que contém a instrução seja confirmada ou revertida.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [BEGIN DIALOG CONVERSATION &#40;Transact-SQL&#41;](../../t-sql/statements/begin-dialog-conversation-transact-sql.md)   
 [GET CONVERSATION GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/get-conversation-group-transact-sql.md)   
 [END CONVERSATION &#40;Transact-SQL&#41;](../../t-sql/statements/end-conversation-transact-sql.md)   
 [sys.conversation_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-conversation-groups-transact-sql.md)   
 [sys.conversation_endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-conversation-endpoints-transact-sql.md)  
  
  
