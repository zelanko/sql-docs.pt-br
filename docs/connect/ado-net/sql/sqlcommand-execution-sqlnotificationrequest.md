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
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 892f11e2d81e3a0733a1f0747c0b72c72ebc79fc
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451942"
---
# <a name="sqlcommand-execution-with-a-sqlnotificationrequest"></a>Execução de SqlCommand com um SqlNotificationRequest

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Download ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Uma <xref:Microsoft.Data.SqlClient.SqlCommand> pode ser configurada para gerar uma notificação quando os dados forem alterados depois de terem sido buscados do servidor e o conjunto de resultados for diferente se a consulta tiver sido executada novamente. Isso é útil para cenários em que você deseja usar filas de notificação personalizadas no servidor ou quando não deseja manter objetos dinâmicos.

## <a name="creating-the-notification-request"></a>Criando a solicitação de notificação

Você pode usar um objeto <xref:Microsoft.Data.Sql.SqlNotificationRequest> para criar a solicitação de notificação ligando-a a um objeto `SqlCommand`. Depois que a solicitação for criada, você não precisará mais do objeto `SqlNotificationRequest`. Você pode consultar a fila para todas as notificações e responder adequadamente. As notificações podem ocorrer mesmo que o aplicativo seja desligado e subsequentemente reiniciado.

Quando o comando com a notificação associada é executado, qualquer alteração no gatilho do conjunto de resultados original envia uma mensagem para a fila de SQL Server que foi configurada na solicitação de notificação.

Como você sonda a fila de SQL Server e interpreta a mensagem é específica para seu aplicativo. O aplicativo é responsável por sondar a fila e reagir com base no conteúdo da mensagem.

> [!NOTE]
> Ao usar SQL Server solicitações de notificação com <xref:Microsoft.Data.SqlClient.SqlDependency>, crie seu próprio nome de fila em vez de usar o nome do serviço padrão.

Não há nenhum novo elemento de segurança do lado do cliente para <xref:Microsoft.Data.Sql.SqlNotificationRequest>. Isso é basicamente um recurso de servidor e o servidor criou privilégios especiais que os usuários precisam ter para solicitar uma notificação.

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
