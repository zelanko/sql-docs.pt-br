---
title: Notificação da conclusão da função assíncrona | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: c54e545bdbd1ae137c24f79c71b53502480cbca9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62690530"
---
# <a name="notification-of-asynchronous-function-completion"></a>Notificação de conclusão da função assíncrona
No SDK do Windows 8, ODBC adicionado um mecanismo para notificar aplicativos quando uma operação assíncrona é concluída, que nos referiremos a como "notificação de conclusão". (Consulte [execução assíncrona (método de notificação)](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md) para obter mais informações.) Este tópico discute alguns dos problemas para os desenvolvedores de driver.  
  
## <a name="the-interface-between-the-driver-manager-and-driver"></a>A Interface entre o Gerenciador de Driver e o Driver  
 Internamente, o Gerenciador de Driver fornece uma função de retorno de chamada [função SQLAsyncNotificationCallback](../../../odbc/reference/develop-driver/sqlasyncnotificationcallback-function.md). **SQLAsyncNotificationCallback** só pode ser chamado pelo driver – um aplicativo não pode chamá-la diretamente. O driver chama **SQLAsyncNotificationCallback** sempre que novos dados recebidos do servidor após a última SQL_STILL_EXECUTING retornando.  
  
 O Gerenciador de Driver fornece um mecanismo de retorno de chamada para que um driver pode notificar o Gerenciador de Driver quando algum progresso realmente foi feito na execução de uma operação assíncrona depois que a função correspondente retornará SQL_STILL_EXECUTING  
  
 O Gerenciador de Driver define o atributo SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK em um identificador de conexão de driver com um ponteiro de função não-nulo, o que é do tipo SQL_ASYNC_NOTIFICATION_CALLBACK, para o driver funcionar no modo de notificação para qualquer assíncrona operações nesse identificador. Da mesma forma, o Gerenciador de Driver define o atributo SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK em um identificador de instrução de driver com um ponteiro de função não-nulo, que também é do tipo SQL_ASYNC_NOTIFICATION_CALLBACK, para o driver funcionar no modo de notificação para as operações assíncronas nesse identificador.  
  
 Se uma operação assíncrona é executada em um identificador de driver, as funções assíncronas driver deverá funcionar em um estilo sem bloqueio. Se a operação não pode ser concluída imediatamente, a função do driver deve retornar SQL_STILL_EXECUTING. Esse requisito se aplica para o modo de sondagem e o modo de notificação.  
  
 Se um identificador está no modo assíncrono de notificação, o driver deve chamar a função de retorno de chamada de notificação, cujo endereço é o valor para o atributo SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK ou SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK, uma vez após retornando SQL_STILL_EXECUTING. Em outras palavras, um SQL_STILL_EXECUTING de retorno deve ser emparelhado com uma invocação da função de retorno de chamada de notificação. O driver deve usar o valor atual do atributo de identificador SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT ou SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT como o valor para o parâmetro de função de retorno de chamada *pContext*.  
  
 O driver não deve chamar de volta no thread que chama a função do driver; Não há nenhum motivo para notificar o andamento antes da função retorna. O driver deve usar seu próprio thread de retorno de chamada. O Gerenciador de Driver não usará o thread de retorno de chamada do driver para a execução de lógica de processamento extensivo.  
  
 O Gerenciador de Driver chamará a função original novamente depois que o driver chama de volta. O Gerenciador de Driver pode usar um thread que não é um thread de aplicativo nem um thread de driver. Se o driver usa algumas informações associadas ao thread (por exemplo, usuário ou token de identificador de segurança), o driver deve salvar as informações necessárias na chamada assíncrona inicial e usar o valor salvo antes da operação assíncrona toda é concluída. Geralmente, apenas **SQLDriverConnect**, **SQLConnect**, ou **SQLBrowseConnect** precisa usar esse tipo de informação.  
  
## <a name="see-also"></a>Consulte também  
 [Desenvolvendo um driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
