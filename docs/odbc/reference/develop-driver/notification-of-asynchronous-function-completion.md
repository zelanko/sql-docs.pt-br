---
title: Notificação de conclusão de função assíncrona | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 336565da-4203-4745-bce2-4f011c08e357
author: MightyPen
ms.author: genemi
ms.openlocfilehash: de3496661f2ab329e5bf662a9cb8fa749cb81bfc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68129318"
---
# <a name="notification-of-asynchronous-function-completion"></a>Notificação de conclusão da função assíncrona
No SDK do Windows 8, o ODBC adicionou um mecanismo para notificar aplicativos quando uma operação assíncrona for concluída, para o qual iremos nos referir como "notificação sobre conclusão". (Consulte [execução assíncrona (método de notificação)](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md) para obter mais informações.) Este tópico discute alguns dos problemas para os desenvolvedores de driver.  
  
## <a name="the-interface-between-the-driver-manager-and-driver"></a>A interface entre o Gerenciador de driver e o driver  
 O Gerenciador de driver fornece internamente uma função de retorno de chamada [SQLAsyncNotificationCallback function](../../../odbc/reference/develop-driver/sqlasyncnotificationcallback-function.md). **SQLAsyncNotificationCallback** só pode ser chamado pelo driver – um aplicativo não pode chamá-lo diretamente. O driver chama **SQLAsyncNotificationCallback** sempre que novos dados recebidos do servidor após o último retorno de SQL_STILL_EXECUTING.  
  
 O Gerenciador de driver fornece um mecanismo de retorno de chamada para que um driver possa notificar o Gerenciador de driver quando algum progresso for feito na execução de uma operação assíncrona depois que a função correspondente retornar SQL_STILL_EXECUTING  
  
 O Gerenciador de driver define o atributo SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK em um identificador de conexão de driver com um ponteiro de função não nulo, que é do tipo SQL_ASYNC_NOTIFICATION_CALLBACK, para que o driver funcione no modo de notificação para qualquer serviço assíncrono operações nesse identificador. Da mesma forma, o Gerenciador de driver define o atributo SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK em um identificador de instrução de driver com um ponteiro de função não nulo, que também é do tipo SQL_ASYNC_NOTIFICATION_CALLBACK, para que o driver funcione no modo de notificação para quaisquer operações assíncronas nesse identificador.  
  
 Se uma operação assíncrona for executada em um identificador de driver, as funções de driver assíncronas devem funcionar em um estilo sem bloqueio. Se a operação não puder ser concluída imediatamente, a função de driver deverá retornar SQL_STILL_EXECUTING. Esse requisito é verdadeiro para o modo de sondagem e o modo de notificação.  
  
 Se um identificador estiver no modo assíncrono de notificação, o driver deverá chamar a função de retorno de chamada de notificação, cujo endereço é o valor para o atributo SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK ou SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK, uma vez após retornando SQL_STILL_EXECUTING. Em outras palavras, um retorno SQL_STILL_EXECUTING deve ser emparelhado com uma invocação da função de retorno de chamada de notificação. O driver deve usar o valor atual do SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT ou SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT atributo de identificador como o valor para o parâmetro de função de retorno de chamada *pContext*.  
  
 O driver não deve chamar de volta no thread que chama a função do driver; Não há motivo para notificar o progresso antes que a função retorne. O driver deve usar seu próprio thread para retorno de chamada. O Gerenciador de driver não usará o thread de retorno de chamada do driver para executar uma lógica de processamento extensivo.  
  
 O Gerenciador de driver chamará a função original novamente depois que o driver chamar de volta. O Gerenciador de driver pode usar um thread que não seja um thread de aplicativo nem um thread de driver. Se o driver usar algumas informações associadas ao thread (por exemplo, token de segurança ou identificador de usuário), o driver deverá salvar as informações necessárias na chamada assíncrona inicial e usar o valor salvo antes da operação assíncrona inteira conclusão. Normalmente, somente **SQLDriverConnect**, **SQLConnect**ou **SQLBrowseConnect** precisam usar esse tipo de informação.  
  
## <a name="see-also"></a>Consulte Também  
 [Desenvolver um driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
