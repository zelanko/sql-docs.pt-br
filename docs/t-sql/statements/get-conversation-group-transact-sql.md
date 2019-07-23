---
title: GET CONVERSATION GROUP (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- GET
- CONVERSATION_GROUP_TSQL
- GET_TSQL
- GET_CONVERSATION_GROUP_TSQL
- GET CONVERSATION GROUP
- CONVERSATION GROUP
- GET CONVERSATION
- GET_CONVERSATION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- GET CONVERSATION GROUP statement
- conversations [Service Broker], groups
ms.assetid: 4da8a855-33c0-43b2-a49d-527487cb3b5c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: bec815372c77e8433fdfdaeedc2cc95a41901738
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68084412"
---
# <a name="get-conversation-group-transact-sql"></a>GET CONVERSATION GROUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna o identificador de grupo de conversa para a próxima mensagem a ser recebida e bloqueia o grupo para a conversa que contém a mensagem. O identificador de grupo de conversa pode ser usado para recuperar informações de estado da conversa antes de recuperar a própria mensagem.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
[ WAITFOR ( ]  
   GET CONVERSATION GROUP @conversation_group_id  
      FROM <queue>  
[ ) ] [ , TIMEOUT timeout ]  
[ ; ]  
  
<queue> ::=  
{ database_name.schema_name.queue_name | schema_name.queue_name | queue_name }  
```  
  
## <a name="arguments"></a>Argumentos  
 WAITFOR  
 Especifica que a instrução GET CONVERSATION GROUP aguarde a chegada de uma mensagem na fila se nenhuma mensagem estiver presente.  
  
 *@conversation_group_id*  
 É uma variável usada para armazenar a ID de grupo de conversa retornada pela instrução GET CONVERSATION GROUP. A variável precisa ser do tipo **uniqueidentifier**. Se não houver grupos de conversa disponíveis, a variável será definida como NULL.  
  
 FROM  
 Especifica a fila na qual o grupo de conversa deve ser obtido.  
  
 *database_name*  
 É o nome do banco de dados que contém a fila na qual o grupo de conversa deve ser obtido. Quando não for fornecido nenhum *database_name*, o padrão será o banco de dados atual.  
  
 *schema_name*  
 É o nome do esquema proprietário da fila na qual o grupo de conversa deve ser obtido. Quando nenhum *schema_name* for fornecido, ele usará como padrão o esquema padrão do usuário atual.  
  
 *queue_name*  
 É o nome da fila na qual o grupo de conversa deve ser obtido.  
  
 TIMEOUT *timeout*  
 Especifica o intervalo de tempo, em milissegundos, que o Service Broker aguarda a chegada de uma mensagem na fila. Essa cláusula só pode ser usada com a cláusula WAITFOR. Se uma instrução que usa WAITFOR não incluir essa cláusula ou se *timeout* for -1, o tempo de espera será ilimitado. Se o tempo limite expirar, GET CONVERSATION GROUP definirá a variável *@conversation_group_id* como NULL.  
  
## <a name="remarks"></a>Remarks  
  
> [!IMPORTANT]  
>  Se a instrução GET CONVERSATION GROUP não for a primeira instrução em um lote ou em um procedimento armazenado, a instrução anterior precisará terminar com ponto e vírgula ( **;** ), o terminador de instrução do [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 Se a fila especificada na instrução GET CONVERSATION GROUP não estiver disponível, a instrução falhará com um erro [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 Essa instrução retorna o próximo grupo de conversa onde as seguintes afirmações são verdadeiras:  
  
-   O grupo de conversa pode ser bloqueado com êxito.  
  
-   O grupo de conversa possui mensagens disponível na fila.  
  
-   O grupo de conversa tem o nível de prioridade mais alto de todos os grupos de conversa que atendem aos critérios listados anteriormente. O nível de prioridade de um grupo de conversa é o mais alto atribuído a qualquer conversa que seja um membro do grupo e possua mensagens na fila.  
  
 As chamadas sucessivas a GET CONVERSATION GROUP na mesma transação podem bloquear mais de um grupo de conversa. Se nenhum grupo de conversa estiver disponível, a instrução retornará NULL como o identificador de grupo de conversa.  
  
 Quando a cláusula WAITFOR é especificada, a instrução aguarda o tempo limite especificado ou até um grupo de conversa estar disponível. Se a fila for descartada enquanto a instrução estiver aguardando, a instrução retornará um erro imediatamente.  
  
 GET CONVERSATION GROUP não é válida em uma função definida pelo usuário.  
  
## <a name="permissions"></a>Permissões  
 Para obter um identificador de grupo de conversa em uma fila, o usuário atual deve ter a permissão RECEIVE na fila.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-getting-a-conversation-group-waiting-indefinitely"></a>A. Obtendo um grupo de conversa, aguardando indefinidamente  
 O exemplo a seguir define `@conversation_group_id` como o identificador de grupo de conversa para a próxima mensagem disponível em `ExpenseQueue`. O comando aguarda até uma mensagem ficar disponível.  
  
```  
DECLARE @conversation_group_id UNIQUEIDENTIFIER ;  
  
WAITFOR (  
 GET CONVERSATION GROUP @conversation_group_id  
     FROM ExpenseQueue  
) ;  
```  
  
### <a name="b-getting-a-conversation-group-waiting-one-minute"></a>B. Obtendo um grupo de conversa, aguardando um minuto  
 O exemplo a seguir define `@conversation_group_id` como o identificador de grupo de conversa para a próxima mensagem disponível em `ExpenseQueue`. Se nenhuma mensagem ficar disponível dentro de um minuto, GET CONVERSATION GROUP retornará sem alterar o valor de `@conversation_group_id`.  
  
```  
DECLARE @conversation_group_id UNIQUEIDENTIFIER  
  
WAITFOR (  
    GET CONVERSATION GROUP @conversation_group_id   
    FROM ExpenseQueue ),  
TIMEOUT 60000 ;  
```  
  
### <a name="c-getting-a-conversation-group-returning-immediately"></a>C. Obtendo um grupo de conversa, retornando imediatamente  
 O exemplo a seguir define `@conversation_group_id` como o identificador de grupo de conversa para a próxima mensagem disponível em `ExpenseQueue`. Se nenhuma mensagem estiver disponível, `GET CONVERSATION GROUP` retornará imediatamente sem alterar `@conversation_group_id`.  
  
```  
DECLARE @conversation_group_id UNIQUEIDENTIFIER ;  
  
GET CONVERSATION GROUP @conversation_group_id  
FROM AdventureWorks.dbo.ExpenseQueue ;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [BEGIN DIALOG CONVERSATION &#40;Transact-SQL&#41;](../../t-sql/statements/begin-dialog-conversation-transact-sql.md)   
 [MOVE CONVERSATION &#40;Transact-SQL&#41;](../../t-sql/statements/move-conversation-transact-sql.md)  
  
  
