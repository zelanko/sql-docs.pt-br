---
title: END CONVERSATION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- END DIALOG
- END CONVERSATION
- END_DIALOG_TSQL
- END_CONVERSATION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- errors [Service Broker], conversations
- dialogs [Service Broker], ending
- closing conversations
- END CONVERSATION statement
- conversations [Service Broker], ending
- ending conversations [SQL Server]
ms.assetid: 4415a126-cd22-4a5e-b84a-d8c68515c83b
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 26051de067dd496d25cfcc3c2cb0f71715ed3145
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "70211354"
---
# <a name="end-conversation-transact-sql"></a>END CONVERSATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Encerra um lado de uma conversa existente.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
END CONVERSATION conversation_handle  
   [   [ WITH ERROR = failure_code DESCRIPTION = 'failure_text' ]  
     | [ WITH CLEANUP ]  
    ]  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *conversation_handle*  
 É o identificador de conversa para que a conversa termine.  
  
 WITH ERROR =*failure_code*  
 É o código de erro. O *failure_code* é do tipo **int**. O código de falha é um código definido pelo usuário que é incluído na mensagem de erro enviada ao outro lado da conversa. O código de falha deve ser maior que 0.  
  
 DESCRIPTION =*failure_text*  
 É a mensagem de erro. O *failure_text* é do tipo **nvarchar(3000)** . O texto da falha é um texto definido pelo usuário que é incluído na mensagem de erro enviada ao outro lado da conversa.  
  
 WITH CLEANUP  
 Remove todas as mensagens e entradas da exibição do catálogo para um lado de uma conversa que não pode ser concluída normalmente. O outro lado da conversa não é notificado da limpeza. O [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] remove o ponto de extremidade da conversa, todas as mensagens da conversa na fila de transmissão e todas as mensagens da conversa na fila de serviço. Os administradores podem usar essa opção para remover conversas que não podem ser concluídas normalmente. Por exemplo, se o serviço remoto tiver sido removido permanentemente, um administrador poderá usar WITH CLEANUP para remover conversas para esse serviço. Não use WITH CLEANUP no código de um aplicativo do [!INCLUDE[ssSB](../../includes/sssb-md.md)]. Se END CONVERSATION WITH CLEANUP for executado antes de o ponto de extremidade de recepção confirmar o recebimento de uma mensagem, o ponto de extremidade de envio enviará a mensagem novamente. Isto poderá executar novamente o diálogo.  
  
## <a name="remarks"></a>Comentários  
 O encerramento de uma conversa bloqueia o grupo de conversa ao qual o *conversation_handle* fornecido pertence. Quando uma conversa é encerrada, o [!INCLUDE[ssSB](../../includes/sssb-md.md)] remove todas as mensagens para ela da fila de serviço.  
  
 Após o término de uma conversa, um aplicativo não pode mais enviar ou receber mensagens para essa conversa. Ambos os participantes em uma conversa devem chamar END CONVERSATION para concluir a conversa. Se o [!INCLUDE[ssSB](../../includes/sssb-md.md)] não tiver recebido uma mensagem de término do diálogo ou uma mensagem de erro do outro participante, o [!INCLUDE[ssSB](../../includes/sssb-md.md)] notificará o outro participante de que a conversa terminou. Neste caso, embora o identificador da conversa não seja mais válido, o ponto de extremidade de conversa permanece ativo até a instância que hospeda o serviço remoto confirmar a mensagem.  
  
 Se o [!INCLUDE[ssSB](../../includes/sssb-md.md)] ainda não tiver processado uma mensagem de término do diálogo ou de erro para a conversa, o [!INCLUDE[ssSB](../../includes/sssb-md.md)] notificará o lado remoto de que a conversa terminou. As mensagens que o [!INCLUDE[ssSB](../../includes/sssb-md.md)] envia ao serviço remoto dependem das opções especificadas:  
  
-   Se a conversa terminar sem erros e a conversa com o serviço remoto ainda estiver ativa, o [!INCLUDE[ssSB](../../includes/sssb-md.md)] enviará uma mensagem do tipo `https://schemas.microsoft.com/SQL/ServiceBroker/EndDialog` ao serviço remoto. O [!INCLUDE[ssSB](../../includes/sssb-md.md)] acionará essa mensagem à fila de transmissão na ordem da conversa. O [!INCLUDE[ssSB](../../includes/sssb-md.md)] envia todas as mensagens dessa conversa que estão atualmente na fila de transmissão antes de enviar esta mensagem.  
  
-   Se a conversa terminar com um erro e a conversa com o serviço remoto ainda estiver ativa, o [!INCLUDE[ssSB](../../includes/sssb-md.md)] enviará uma mensagem do tipo `https://schemas.microsoft.com/SQL/ServiceBroker/Error` ao serviço remoto. [!INCLUDE[ssSB](../../includes/sssb-md.md)] remove qualquer outra mensagem desta conversa atualmente na fila de transmissão.  
  
-   A cláusula WITH CLEANUP permite que um administrador de banco de dados remova conversas que não são concluídas normalmente. Essa opção remove todas as mensagens e entradas da exibição do catálogo para a conversa. Observe que, neste caso, o lado remoto da conversa não recebe nenhuma indicação de que a conversa terminou, e talvez não receba mensagens que tenham sido enviadas por um aplicativo e ainda não transmitidas pela rede. Evite essa opção a menos que a conversa não possa ser concluída normalmente.  
  
 Quando uma conversa termina, uma instrução SEND [!INCLUDE[tsql](../../includes/tsql-md.md)] que especifica o identificador de conversa gera um erro [!INCLUDE[tsql](../../includes/tsql-md.md)]. Se as mensagens para esta conversa chegarem do outro lado da conversa, o [!INCLUDE[ssSB](../../includes/sssb-md.md)] as descartará  
  
 Se uma conversa terminar enquanto o serviço remoto ainda não tiver enviado mensagens para ela, o serviço remoto descartará as mensagens não enviadas. Isso não é considerado um erro, e o serviço remoto não recebe nenhuma notificação de que mensagens foram descartadas.  
  
 Os códigos de falha especificados na cláusula WITH ERROR devem ser números positivos. Os números negativos são reservados para mensagens de erro do [!INCLUDE[ssSB](../../includes/sssb-md.md)].  
  
 END CONVERSATION não é válida em uma função definida pelo usuário.  
  
## <a name="permissions"></a>Permissões  
 Para terminar uma conversa ativa, o usuário atual deve ser o proprietário da conversa, um membro da função de servidor fixa sysadmin ou um membro da função de banco de dados fixa db_owner.  
  
 Um membro da função de servidor fixa sysadmin ou um membro da função de banco de dados fixa db_owner poderá usar WITH CLEANUP para remover os metadados para uma conversa que já foi concluída.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-ending-a-conversation"></a>a. Terminando uma conversa  
 O exemplo a seguir encerra o diálogo especificado por `@dialog_handle`.  
  
```  
END CONVERSATION @dialog_handle ;  
```  
  
### <a name="b-ending-a-conversation-with-an-error"></a>B. Terminando uma conversa com um erro  
 O exemplo a seguir encerrará o diálogo especificado por `@dialog_handle` com um erro se a instrução de processamento informar um erro. Observe que esta é uma abordagem simplista de tratamento de erros, e pode não ser apropriada para alguns aplicativos.  
  
```  
DECLARE @dialog_handle UNIQUEIDENTIFIER,  
        @ErrorSave INT,  
        @ErrorDesc NVARCHAR(100) ;  
BEGIN TRANSACTION ;  
  
<receive and process message>  
  
SET @ErrorSave = @@ERROR ;  
  
IF (@ErrorSave <> 0)  
  BEGIN  
      ROLLBACK TRANSACTION ;  
      SET @ErrorDesc = N'An error has occurred.' ;  
      END CONVERSATION @dialog_handle   
      WITH ERROR = @ErrorSave DESCRIPTION = @ErrorDesc ;  
  END  
ELSE  
  
COMMIT TRANSACTION ;  
```  
  
### <a name="c-cleaning-up-a-conversation-that-cannot-complete-normally"></a>C. Limpando uma conversa que não pode ser concluída normalmente  
 O exemplo a seguir encerra o diálogo especificado por `@dialog_handle`. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] remove imediatamente todas as mensagens da fila de serviço e da fila de transmissão, sem notificar o serviço remoto. Como o término de uma caixa de diálogo com a limpeza não notifica o serviço remoto, você deve usar isso apenas nos casos em que o serviço remoto não está disponível para receber uma mensagem **EndDialog** ou **Error**.  
  
```  
END CONVERSATION @dialog_handle WITH CLEANUP ;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [BEGIN CONVERSATION TIMER &#40;Transact-SQL&#41;](../../t-sql/statements/begin-conversation-timer-transact-sql.md)   
 [BEGIN DIALOG CONVERSATION &#40;Transact-SQL&#41;](../../t-sql/statements/begin-dialog-conversation-transact-sql.md)   
 [sys.conversation_endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-conversation-endpoints-transact-sql.md)  
  
  
