---
title: "Implementar notificações de evento | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- event notifications [SQL Server], target service
- target service [SQL Server]
- event notifications [SQL Server], creating
ms.assetid: 29ac8f68-a28a-4a77-b67b-a8663001308c
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: eac9804c15bfcafbb5581875258d4499df130db9
ms.lasthandoff: 04/11/2017

---
# <a name="implement-event-notifications"></a>Implementar notificações de evento
  Para implementar uma notificação de evento, antes é necessário criar um serviço de destino para receber as notificações de evento e só então a notificação.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssSB](../../includes/sssb-md.md)] deve ser configurada para notificações de eventos que enviam mensagens a um agente de serviços em um servidor remoto. A segurança de caixa de diálogo deve ser configurada manualmente, de acordo com o modelo de segurança completo.  
  
## <a name="creating-the-target-service"></a>Criando o serviço de destino  
 Não é necessário criar um serviço que inicie o [!INCLUDE[ssSB](../../includes/sssb-md.md)], pois o [!INCLUDE[ssSB](../../includes/sssb-md.md)] inclui o tipo de mensagem específica e o contrato de notificação de evento a seguir:  
  
```  
http://schemas.microsoft.com/SQL/Notifications/PostEventNotification  
```  
  
 O serviço de destino que recebe as notificações de eventos deve honrar esse contrato preexistente.  
  
 **Para criar um serviço de destino**:  
  
1.  Crie uma fila para receber mensagens.  
  
    > [!NOTE]  
    >  A fila recebe o seguinte tipo de mensagem: `http://schemas.microsoft.com/SQL/Notifications/QueryNotification`.  
  
2.  Crie um serviço na fila que faça referência ao contrato de notificações de evento.  
  
3.  Crie uma rota no serviço para definir o endereço para o qual o [!INCLUDE[ssSB](../../includes/sssb-md.md)] deve enviar mensagens para o serviço. Para notificações de evento que visem um serviço no mesmo banco de dados, especifique `ADDRESS = 'LOCAL'`.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssSB](../../includes/sssb-md.md)] roteamento determina o serviço que recebe as mensagens de notificação. Se a notificação de evento visar um serviço em um servidor remoto, tanto o servidor de origem, quanto o servidor de destino devem ter rotas definidas neles mesmos a fim de garantir a comunicação nas duas direções.  
  
 O exemplo a seguir cria uma fila, um serviço na fila e uma rota no serviço para manipular mensagens do contrato de notificação de evento.  
  
```  
CREATE QUEUE NotifyQueue ;  
GO  
CREATE SERVICE NotifyService  
ON QUEUE NotifyQueue  
(  
[http://schemas.microsoft.com/SQL/Notifications/PostEventNotification]  
);  
GO  
CREATE ROUTE NotifyRoute  
WITH SERVICE_NAME = 'NotifyService',  
ADDRESS = 'LOCAL';  
GO  
```  
  
## <a name="creating-the-event-notification"></a>Criando a notificação de evento  
 As notificações de evento são criadas por meio da instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE EVENT NOTIFICATION e descartadas pela instrução DROP EVENT NOTIFICATION. Para modificar uma notificação de evento, você deve descartar e recriar a notificação de evento.  
  
 O exemplo a seguir cria a notificação de evento `CreateDatabaseNotification`. Essa notificação envia uma mensagem sobre quaisquer eventos `CREATE_DATABASE` que ocorrerem no servidor para o serviço `NotifyService` criado previamente.  
  
```  
CREATE EVENT NOTIFICATION CreateDatabaseNotification  
ON SERVER  
FOR CREATE_DATABASE  
TO SERVICE 'NotifyService', '8140a771-3c4b-4479-8ac0-81008ab17984' ;  
```  
  
> [!CAUTION]  
>  Notificações de evento reconhecem eventos CREATE_SCHEMA e definições <schema_element> de instruções CREATE SCHEMA como eventos separados. Por exemplo, suponha que seja criada  uma notificação de evento nos eventos CREATE_SCHEMA e CREATE_TABLE e você execute o lote a seguir.  
>   
>  `CREATE SCHEMA s`  
>   
>  `CREATE TABLE t1 (col1 int)`  
>   
>  Nesse caso, a notificação de evento é emitida duas vezes: uma, quando ocorre o evento CREATE_SCHEMA e, outra vez, quando ocorre o evento CREATE_TABLE. Recomendamos evitar criar notificações de evento ao mesmo tempo em eventos CREATE_SCHEMA e em textos <schema_element> de quaisquer definições CREATE SCHEMA correspondentes ou criar lógica em seu aplicativo para evitar capturar dados de eventos indesejados.  
  
 **Para criar uma notificação de evento**  
  
-   [CREATE EVENT NOTIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-notification-transact-sql.md)  
  
 **Para descartar uma notificação de evento**  
  
-   [DROP EVENT NOTIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-event-notification-transact-sql.md)  
  
## <a name="see-also"></a>Consulte também  
 [Obter informações sobre notificações de eventos](../../relational-databases/service-broker/get-information-about-event-notifications.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
