---
title: SEND (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SEND_ON_CONVERSATION_TSQL
- ON_CONVERSATION_TSQL
- SEND
- SEND_TSQL
- SEND ON CONVERSATION
- ON CONVERSATION
dev_langs:
- TSQL
helpviewer_keywords:
- conversations [Service Broker], message sending
- SEND statement
- messages [Service Broker], sending
- sending messages
ms.assetid: b6e66aeb-1714-4c2b-b7c2-d386d77b0d46
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7d40948dad23dca9dc4905d29a94995f087f78b1
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="send-transact-sql"></a>SEND (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Envia uma mensagem usando uma ou mais conversas existentes.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SEND  
   ON CONVERSATION [(]conversation_handle [,.. @conversation_handle_n][)]  
   [ MESSAGE TYPE message_type_name ]  
   [ ( message_body_expression ) ]  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 ON CONVERSATION *conversation_handle [.. @conversation_handle_n]*  
 Especifica as conversas às quais a mensagem pertence. O *conversation_handle* deve conter um identificador de conversa válido. O mesma identificador de conversação não pode ser usado mais de uma vez.  
  
 MESSAGE TYPE *message_type_name*  
 Especifica o tipo da mensagem enviada. Esse tipo de mensagem deve ser incluído nos contratos de serviço usado por essas conversas. Esses contratos devem permitir que o tipo de mensagem seja enviado desse lado da conversa. Por exemplo, os serviços de destino das conversas podem enviar somente mensagens especificadas no contrato como SENT BY TARGET ou SENT BY ANY. Se essa cláusula for omitida, a mensagem será do tipo DEFAULT.  
  
 *message_body_expression*  
 Fornece uma expressão que representa o corpo de mensagem. A *message_body_expression* é opcional. No entanto, se *message_body_expression* estiver presente a expressão deverá ser de um tipo que possa ser convertido em **varbinary(max)**. A expressão não pode ser NULL. Se essa cláusula for omitida, o corpo de mensagem será vazio.  
  
## <a name="remarks"></a>Remarks  
  
> [!IMPORTANT]  
>  Se a instrução SEND não for a primeira instrução de um procedimento em lote ou armazenado, a instrução anterior deverá ser encerrada com um ponto-e-vírgula (;).  
  
 A instrução SEND transmite uma mensagem dos serviços em uma extremidade de uma ou mais conversas do [!INCLUDE[ssSB](../../includes/sssb-md.md)] para os serviços na outra extremidade dessas conversas. A instrução RECEIVE é usada então para recuperar a mensagem enviada das filas associadas aos serviços de destino.  
  
 Os identificadores de conversação são fornecidos à cláusula ON CONVERSATION de uma de três fontes:  
  
-   Ao enviar uma mensagem que não é uma resposta a uma mensagem recebida de outro serviço, use o identificador de conversação retornado da instrução BEGIN DIALOG que criou a conversa.  
  
-   Ao enviar uma mensagem que é uma resposta a uma mensagem recebida anteriormente de outro serviço, use o identificador de conversação retornado pela instrução RECEIVE que retornou a mensagem original.  
  
 Em muitos casos, o código que contém a instrução SEND é separado do código que contém as instruções BEGIN DIALOG ou RECEIVE que fornecem o indicador de conversa. Nesses casos, o identificador de conversação deve ser um dos itens de dados nas informações de estado passadas ao código que contém a instrução SEND.  
  
 As mensagens que são enviadas a serviços em outras instâncias do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] são armazenadas em uma fila de transmissão no banco de dados atual até que possam ser transmitidas às filas do serviço nas instâncias remotas. As mensagens enviadas a serviços na mesma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] são colocadas diretamente nas filas associadas a esses serviços. Se uma condição evitar que uma mensagem local seja colocada diretamente na fila de serviço de destino, ela poderá ser armazenada na fila de transmissão até que a condição seja resolvida. Isso ocorre, por exemplo, quando há alguns tipos de erros ou a fila de serviço de destino está ficando inativa. É possível usar o modo de exibição do sistema **sys.transmission_queue** para ver as mensagens na fila de transmissão.  
  
 SEND é uma instrução atômica, ou seja, se uma instrução SEND que envia uma mensagem em várias conversas falhar, por exemplo, porque uma conversa está em um estado com erro, nenhuma mensagem será armazenada na fila de transmissão, nem colocada em nenhuma fila de serviço de destino.  
  
 O Service Broker otimiza o armazenamento e a transmissão de mensagens enviadas em várias conversas na mesma instrução SEND.  
  
 As mensagens nas filas de transmissão de uma instância são transmitidas em sequência, com base em:  
  
-   Nível de prioridade de seu ponto de extremidade de conversação associado.  
  
-   Dentro do nível de prioridade, sua sequência de envio na conversa.  
  
 Os níveis de prioridade especificados em prioridades de conversa se aplicam apenas a mensagens da fila de transmissão caso a opção de banco de dados HONOR_BROKER_PRIORITY esteja definida como ON. Se HONOR_BROKER_PRIORITY estiver definida como OFF, todas as mensagens colocadas na fila de transmissão para aquele banco de dados serão atribuídas ao nível de prioridade padrão 5. Os níveis de prioridade não são aplicados a uma instrução SEND em que as mensagens são colocadas diretamente em uma fila de serviço na mesma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 A instrução SEND bloqueia cada conversa na qual uma mensagem é enviada separadamente para assegurar a entrega ordenada por conversa.  
  
 SEND não é válida em uma função definida pelo usuário.  
  
## <a name="permissions"></a>Permissões  
 Para enviar uma mensagem, o usuário atual deve ter a permissão RECEIVE na fila de cada serviço que envia a mensagem.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir abre uma caixa de diálogo e envia uma mensagem XML nela. Para enviar a mensagem, o exemplo converte o objeto xml em **varbinary(max)**.  
  
```  
DECLARE @dialog_handle UNIQUEIDENTIFIER,  
        @ExpenseReport XML ;  
  
SET @ExpenseReport = < construct message as appropriate for the application > ;  
  
BEGIN DIALOG @dialog_handle  
FROM SERVICE [//Adventure-Works.com/Expenses/ExpenseClient]  
TO SERVICE '//Adventure-Works.com/Expenses'  
ON CONTRACT [//Adventure-Works.com/Expenses/ExpenseProcessing] ;  
  
SEND ON CONVERSATION @dialog_handle  
    MESSAGE TYPE [//Adventure-Works.com/Expenses/SubmitExpense]  
    (@ExpenseReport) ;  
```  
  
 O exemplo a seguir abre três caixas de diálogo e envia uma mensagem XML em cada uma delas.  
  
```  
DECLARE @dialog_handle1 UNIQUEIDENTIFIER,  
        @dialog_handle2 UNIQUEIDENTIFIER,  
        @dialog_handle3 UNIQUEIDENTIFIER,  
        @OrderMsg XML ;  
  
SET @OrderMsg = < construct message as appropriate for the application > ;  
  
BEGIN DIALOG @dialog_handle1  
FROM SERVICE [//InitiatorDB/InitiatorService]  
TO SERVICE '//TargetDB1/TargetService’  
ON CONTRACT [//AllDBs/OrderProcessing] ;  
  
BEGIN DIALOG @dialog_handle2  
FROM SERVICE [//InitiatorDB/InitiatorService]  
TO SERVICE '//TargetDB2/TargetService’  
ON CONTRACT [//AllDBs/OrderProcessing] ;  
  
BEGIN DIALOG @dialog_handle3  
FROM SERVICE [//InitiatorDB/InitiatorService]  
TO SERVICE '//TargetDB3/TargetService’  
ON CONTRACT [//AllDBs/OrderProcessing] ;  
  
SEND ON CONVERSATION (@dialog_handle1, @dialog_handle2, @dialog_handle3)  
    MESSAGE TYPE [//AllDBs/OrderMsg]  
    (@OrderMsg) ;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [BEGIN DIALOG CONVERSATION &#40;Transact-SQL&#41;](../../t-sql/statements/begin-dialog-conversation-transact-sql.md)   
 [END CONVERSATION &#40;Transact-SQL&#41;](../../t-sql/statements/end-conversation-transact-sql.md)   
 [RECEIVE &#40;Transact-SQL&#41;](../../t-sql/statements/receive-transact-sql.md)   
 [sys.transmission_queue &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-transmission-queue-transact-sql.md)  
  
  
