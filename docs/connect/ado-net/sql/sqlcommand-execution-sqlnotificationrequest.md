---
title: Execução de SqlCommand com um SqlNotificationRequest
description: Demonstra como configurar um objeto SqlCommand para trabalhar com uma notificação de consulta.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 1776f48f-9bea-41f6-83a4-c990c7a2c991
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: b4ec71c2bd693599106692a45f9e9aa10a63babd
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "78896232"
---
# <a name="sqlcommand-execution-with-a-sqlnotificationrequest"></a>Execução de SqlCommand com um SqlNotificationRequest

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Um <xref:Microsoft.Data.SqlClient.SqlCommand> pode ser configurado para gerar uma notificação quando os dados forem alterados após terem sido obtidos do servidor. Além disso, o conjunto de resultados seria diferente caso a consulta seja executada novamente. Isso é útil para cenários em que você deseja usar filas de notificação personalizadas no servidor ou quando não quiser manter objetos dinâmicos.

## <a name="creating-the-notification-request"></a>Como criar a solicitação de notificação

É possível usar um objeto <xref:Microsoft.Data.Sql.SqlNotificationRequest> para criar a solicitação de notificação associando-o a um objeto `SqlCommand`. Depois que a solicitação for criada, o objeto `SqlNotificationRequest` não será mais necessário. É possível consultar a fila para todas as notificações e responder adequadamente. As notificações podem ocorrer mesmo que o aplicativo seja desligado e reiniciado em seguida.

Quando o comando é executado com a notificação associada, qualquer alteração no conjunto de resultados original dispara o envio de uma mensagem para a fila do SQL Server configurada na solicitação de notificação.

A forma de sondar a fila do SQL Server e interpretar a mensagem é específica para seu aplicativo. O aplicativo é responsável pela sondagem da fila e por reagir com base no conteúdo da mensagem.

> [!NOTE]
> Ao usar as solicitações de notificação do SQL Server com <xref:Microsoft.Data.SqlClient.SqlDependency>, crie um nome de fila próprio em vez de usar o nome de serviço padrão.

Não há elementos novos de segurança do lado do cliente para <xref:Microsoft.Data.Sql.SqlNotificationRequest>. Esse é basicamente um recurso do servidor. Ele criou privilégios especiais que os usuários devem ter para solicitar uma notificação.

### <a name="example"></a>Exemplo

O fragmento de código a seguir demonstra como criar um <xref:Microsoft.Data.Sql.SqlNotificationRequest> e associá-lo a um <xref:Microsoft.Data.SqlClient.SqlCommand>.

```csharp
// Assume connection is an open SqlConnection.
// Create a new SqlCommand object.
SqlCommand command=new SqlCommand(
 "SELECT ShipperID, CompanyName, Phone FROM dbo.Shippers", connection);

// Create a SqlNotificationRequest object.
SqlNotificationRequest notificationRequest=new SqlNotificationRequest();
notificationRequest.id="NotificationID";
notificationRequest.Service="mySSBQueue";

// Associate the notification request with the command.
command.Notification=notificationRequest;
// Execute the command.
command.ExecuteReader();
// Process the DataReader.
// You can use Transact-SQL syntax to periodically poll the
// SQL Server queue to see if you have a new message.
```

## <a name="next-steps"></a>Próximas etapas
- [Notificações de consulta no SQL Server](query-notifications-sql-server.md)
