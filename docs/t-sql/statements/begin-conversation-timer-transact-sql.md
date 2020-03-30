---
title: BEGIN CONVERSATION TIMER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CONVERSATION
- BEGIN_CONVERSATION_TSQL
- TIMER_TSQL
- TIMER
- CONVERSATION TIMER
- CONVERSATION_TIMER_TSQL
- BEGIN CONVERSATION TIMER
- BEGIN_CONVERSATION_TIMER_TSQL
- CONVERSATION_TSQL
- BEGIN CONVERSATION
dev_langs:
- TSQL
helpviewer_keywords:
- BEGIN CONVERSATION TIMER statement
- DialogTimer message
- dialogs [Service Broker], beginning
- timeouts [Service Broker]
- timer messages [Service Broker]
- conversations [Service Broker], timers
- starting timers [Service Broker]
- https://schemas.microsoft.com/SQL/ServiceBroker/DialogTimer message
ms.assetid: 98e49b3f-a38f-4180-8171-fa9cb30db4cb
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 65fbd94bac320994f9c1917e634210febd2ba878
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "70211219"
---
# <a name="begin-conversation-timer-transact-sql"></a>BEGIN CONVERSATION TIMER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Inicia um timer. Quando o tempo limite expirar, o [!INCLUDE[ssSB](../../includes/sssb-md.md)] colocará uma mensagem do tipo `https://schemas.microsoft.com/SQL/ServiceBroker/DialogTimer` na fila local para a conversa.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
BEGIN CONVERSATION TIMER ( conversation_handle )  
   TIMEOUT = timeout   
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 BEGIN CONVERSATION TIMER **(** _conversation\_handle_ **)**  
 Especifica a conversa a ser cronometrada. *conversation_handle* precisa ser do tipo **uniqueidentifier**.  
  
 TIMEOUT  
 Especifica, em segundos, o tempo de espera antes de colocar a mensagem na fila.  
  
## <a name="remarks"></a>Comentários  
 Um timer de conversa fornece uma maneira de um aplicativo receber uma mensagem em uma conversa depois de um período específico. Chamar BEGIN CONVERSATION TIMER em uma conversa antes de o timer expirar define o tempo limite para o novo valor. Diferentemente do tempo de vida da conversa, cada lado da conversa tem um timer de conversa independente. A mensagem **DialogTimer** chega na fila local sem afetar o lado remoto da conversa. Portanto, um aplicativo pode usar uma mensagem de timer para qualquer propósito.  
  
 Por exemplo, você pode usar o timer de conversa para evitar que um aplicativo espere demais por uma resposta atrasada. Se você espera que o aplicativo conclua um diálogo em 30 segundos, poderá definir o timer de conversa para esse diálogo como 60 segundos (30 segundos mais um período de tolerância de 30 segundos). Se o diálogo ainda estiver aberto depois de 60 segundos, o aplicativo receberá uma mensagem de tempo limite na fila para esse diálogo.  
  
 Como opção, um aplicativo pode usar um timer de conversa para solicitar ativação em um determinado momento. Por exemplo, você pode criar um serviço que informe o número de conexões ativas em intervalos de alguns minutos ou um serviço que informe o número de ordens de compra abertas toda noite. O serviço define um temporizador de conversa para expirar na hora desejada. Quando o temporizador expirar, o [!INCLUDE[ssSB](../../includes/sssb-md.md)] enviará uma mensagem **DialogTimer**. A mensagem **DialogTimer** faz com que o [!INCLUDE[ssSB](../../includes/sssb-md.md)] inicie o procedimento armazenado de ativação para a fila. O procedimento armazenado envia uma mensagem ao serviço remoto e reinicia o timer de conversa.  
  
 BEGIN DIALOG CONVERSATION TIMER não é válido em uma função definida pelo usuário.  
  
## <a name="permissions"></a>Permissões  
 A permissão para definir um tenporizador de conversa tem como padrão os usuários com permissões SEND no serviço para a conversa, os membros da função de servidor fixa **sysadmin** e os membros da função de banco de dados fixa **db_owner**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir define um intervalo de dois minutos na caixa de diálogo identificada por `@dialog_handle`.  
  
```  
-- @dialog_handle is of type uniqueidentifier and  
-- contains a valid conversation handle.  
  
BEGIN CONVERSATION TIMER (@dialog_handle)  
TIMEOUT = 120 ;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [BEGIN DIALOG CONVERSATION &#40;Transact-SQL&#41;](../../t-sql/statements/begin-dialog-conversation-transact-sql.md)   
 [END CONVERSATION &#40;Transact-SQL&#41;](../../t-sql/statements/end-conversation-transact-sql.md)   
 [RECEIVE &#40;Transact-SQL&#41;](../../t-sql/statements/receive-transact-sql.md)  
  
  
