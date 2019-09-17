---
title: SEND (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9a6c6993252ccad0335b177c31c9d20b40f520a5
ms.sourcegitcommit: 3de1fb410de2515e5a00a5dbf6dd442d888713ba
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2019
ms.locfileid: "70211431"
---
# <a name="send-transact-sql"></a>SEND (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

Envia uma mensagem usando uma ou mais conversas existentes.  
  
![Ícone de link do artigo](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do artigo") [Convenções de sintaxe do Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```sql
  
SEND  
   ON CONVERSATION [(]conversation_handle [,.. @conversation_handle_n][)]  
   [ MESSAGE TYPE message_type_name ]  
   [ ( message_body_expression ) ]  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
ON CONVERSATION *conversation_handle [.. @conversation_handle_n]*  
Especifica as conversas às quais a mensagem pertence. O *conversation_handle* deve conter um identificador de conversa válido. O mesmo identificador de conversa não pode ser usado mais de uma vez.  
  
MESSAGE TYPE *message_type_name*  
Especifica o tipo da mensagem enviada. Esse tipo de mensagem deve ser incluído nos contratos de serviço usado por essas conversas. Esses contratos devem permitir que o tipo de mensagem seja enviado desse lado da conversa. Por exemplo, os serviços de destino das conversas podem enviar somente mensagens especificadas no contrato como SENT BY TARGET ou SENT BY ANY. Se essa cláusula for omitida, a mensagem será do tipo DEFAULT.  
  
*message_body_expression*  
Fornece uma expressão que representa o corpo de mensagem. A *message_body_expression* é opcional. No entanto, se *message_body_expression* estiver presente a expressão deverá ser de um tipo que possa ser convertido em **varbinary(max)** . A expressão não pode ser NULL. Se essa cláusula for omitida, o corpo de mensagem será vazio.  
  
## <a name="remarks"></a>Remarks  
  
> [!IMPORTANT]  
>  Se a instrução SEND não for a primeira de um procedimento em lotes ou armazenado, a instrução anterior deverá ser encerrada com um ponto-e-vírgula (;).  
  
A instrução SEND transmite uma mensagem dos serviços em uma extremidade de uma ou mais conversas do [!INCLUDE[ssSB](../../includes/sssb-md.md)] para os serviços na outra extremidade dessas conversas. A instrução RECEIVE é usada então para recuperar a mensagem enviada das filas associadas aos serviços de destino.  
  
Os identificadores de conversação são fornecidos à cláusula ON CONVERSATION de uma de três fontes:  
  
- Quando uma mensagem enviada não é uma resposta a uma mensagem recebida de outro serviço, use o identificador de conversa que retorna da instrução BEGIN DIALOG que criou a conversa.  
  
- Quando uma mensagem enviada é uma resposta a uma mensagem recebida anteriormente de outro serviço, use o identificador de conversa retornado pela instrução RECEIVE que retornou a mensagem original.  
  
- O código que contém a instrução SEND é, às vezes, separado do código que contém as instruções BEGIN DIALOG ou RECEIVE que fornecem o identificador de conversa. Nesses casos, o identificador de conversa deve ser um dos itens de dados nas informações de estado passadas ao código que contém a instrução SEND.  
  
As mensagens que são enviadas a serviços em outras instâncias do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] são armazenadas em uma fila de transmissão no banco de dados atual até que possam ser transmitidas às filas do serviço nas instâncias remotas. As mensagens enviadas a serviços na mesma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] são colocadas diretamente nas filas associadas a esses serviços. Se uma condição evitar que uma mensagem local seja colocada diretamente na fila de serviço de destino, a fila de transmissão poderá armazená-la até que a condição seja resolvida. Exemplos disso incluem alguns tipos de erros ou a fila de serviço de destino ficando inativa. É possível usar o modo de exibição do sistema **sys.transmission_queue** para ver as mensagens na fila de transmissão.  
  
SEND é uma instrução atômica. Se uma instrução SEND que envia uma mensagem em várias conversas falhar, por exemplo, quando uma conversa está em um estado com erro, nenhuma mensagem será armazenada na fila de transmissão, nem colocada em nenhuma fila de serviço de destino.  
  
O Service Broker otimiza o armazenamento e a transmissão de mensagens enviadas em várias conversas na mesma instrução SEND.  
  
As mensagens nas filas de transmissão de uma instância são transmitidas em sequência, com base em:  
  
- Nível de prioridade de seu ponto de extremidade de conversação associado.  
  
- Dentro do nível de prioridade, sua sequência de envio na conversa.  
  
Os níveis de prioridade especificados em prioridades de conversa se aplicam apenas a mensagens na fila de transmissão caso a opção de banco de dados HONOR_BROKER_PRIORITY esteja definida como ON. Se HONOR_BROKER_PRIORITY estiver definida como OFF, todas as mensagens colocadas na fila de transmissão para aquele banco de dados serão atribuídas ao nível de prioridade padrão 5. Os níveis de prioridade não são aplicados a uma instrução SEND em que as mensagens são colocadas diretamente em uma fila de serviço na mesma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
A instrução SEND bloqueia cada conversa na qual uma mensagem é enviada separadamente para assegurar a entrega ordenada por conversa.  
  
SEND não é válida em uma função definida pelo usuário.  
  
## <a name="permissions"></a>Permissões  
Para enviar uma mensagem, o usuário atual deve ter a permissão RECEIVE na fila de cada serviço que envia a mensagem.  
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir abre uma caixa de diálogo e envia uma mensagem XML nela. Para enviar a mensagem, o exemplo converte o objeto xml em **varbinary(max)** .  
  
```sql
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
  
```sql
DECLARE @dialog_handle1 UNIQUEIDENTIFIER,  
        @dialog_handle2 UNIQUEIDENTIFIER,  
        @dialog_handle3 UNIQUEIDENTIFIER,  
        @OrderMsg XML ;  
  
SET @OrderMsg = < construct message as appropriate for the application > ;  
  
BEGIN DIALOG @dialog_handle1  
FROM SERVICE [//InitiatorDB/InitiatorService]  
TO SERVICE '//TargetDB1/TargetService'  
ON CONTRACT [//AllDBs/OrderProcessing] ;  
  
BEGIN DIALOG @dialog_handle2  
FROM SERVICE [//InitiatorDB/InitiatorService]  
TO SERVICE '//TargetDB2/TargetService'  
ON CONTRACT [//AllDBs/OrderProcessing] ;  
  
BEGIN DIALOG @dialog_handle3  
FROM SERVICE [//InitiatorDB/InitiatorService]  
TO SERVICE '//TargetDB3/TargetService'  
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
  
  
