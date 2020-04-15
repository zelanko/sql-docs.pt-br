---
title: Notificação de Conclusão de Função Assíncrona | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 336565da-4203-4745-bce2-4f011c08e357
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a453967f2ffdda4af2a44429737f700f4a994cf8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287816"
---
# <a name="notification-of-asynchronous-function-completion"></a>Notificação de conclusão da função assíncrona
No SDK do Windows 8, o ODBC adicionou um mecanismo para notificar os aplicativos quando uma operação assíncrona for concluída, que nos referiremos como "notificação sobre a conclusão". (Consulte [Execução Assíncrona (Método de Notificação)](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md) para obter mais informações.) Este tópico discute algumas das questões para os desenvolvedores de drivers.  
  
## <a name="the-interface-between-the-driver-manager-and-driver"></a>A interface entre o driver manager e o driver  
 O Gerenciador de driver fornece internamente uma função de retorno de chamada [SQLAsyncFunçãoNotificationCallback Function](../../../odbc/reference/develop-driver/sqlasyncnotificationcallback-function.md). **SQLAsyncNotificationCallback** só pode ser chamado pelo driver -- um aplicativo não pode chamá-lo diretamente. O driver chama **SQLAsyncNotificationCallback** sempre que novos dados recebidos do servidor após o último retorno SQL_STILL_EXECUTING.  
  
 O Driver Manager fornece um mecanismo de retorno de chamada para que o motorista possa notificar o Driver Manager quando algum progresso tiver sido feito na execução de uma operação assíncrona após o retorno da função correspondente SQL_STILL_EXECUTING  
  
 O Driver Manager define o atributo SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK em uma alça de conexão do driver com um ponteiro de função não NULA, que é do tipo SQL_ASYNC_NOTIFICATION_CALLBACK, para que o motorista trabalhe no modo de notificação para quaisquer operações assíncronas nessa alça. Da mesma forma, o Driver Manager define o atributo SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK em uma alça de declaração do driver com um ponteiro de função não-NULL, que também é do tipo SQL_ASYNC_NOTIFICATION_CALLBACK, para que o motorista trabalhe no modo de notificação para quaisquer operações assíncronas nessa alça.  
  
 Se uma operação assíncrona for realizada em uma alça do driver, as funções do driver assíncrono devem funcionar em um estilo de não-bloqueio. Se a operação não puder ser concluída imediatamente, a função do driver deve retornar SQL_STILL_EXECUTING. Este requisito é válido tanto para o modo de votação quanto para o modo de notificação.  
  
 Se uma alça estiver no modo assíncrono de notificação, o motorista deverá ligar para a função de retorno de chamada de notificação, cujo endereço é o valor para o atributo SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK ou SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK, uma vez após retornar SQL_STILL_EXECUTING. Em outras palavras, um SQL_STILL_EXECUTING retornando deve ser emparelhado com uma invocação da função de retorno de chamada de notificação. O driver deve usar o valor atual do atributo de SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT ou SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT como o valor para o parâmetro de função de chamada de volta *pContext*.  
  
 O driver não deve chamar de volta no segmento que chama a função do driver; não há razão para notificar o progresso antes que a função retorne. O motorista deve usar seu próprio fio para religar. O Driver Manager não usará o segmento de retorno de chamada do driver para executar uma lógica de processamento extensiva.  
  
 O Driver Manager ligará novamente para a função original depois que o driver ligar de volta. O Driver Manager pode usar um segmento que não é nem um segmento de aplicativo nem um thread driver. Se o driver usar algumas informações associadas ao segmento (por exemplo, token de segurança ou identificador de usuário), o motorista deverá salvar as informações necessárias na chamada assíncrona inicial e usar o valor salvo antes que toda a operação assíncrona seja concluída. Normalmente, apenas **SQLDriverConnect,** **SQLConnect**ou **SQLBrowseConnect** precisam usar esse tipo de informação.  
  
## <a name="see-also"></a>Consulte Também  
 [Desenvolvendo um driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
