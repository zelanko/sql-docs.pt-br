---
description: CREATE EVENT NOTIFICATION (Transact-SQL)
title: CREATE EVENT NOTIFICATION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE_EVENT_NOTIFICATION_TSQL
- NOTIFICATION_TSQL
- EVENT
- NOTIFICATION
- CREATE EVENT NOTIFICATION
- EVENT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE EVENT NOTIFICATION statement
- events [SQL Server], notifications
- event notifications [SQL Server], creating
ms.assetid: dbbff0e8-9e25-4f12-a1ba-e12221d16ac2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f814c52713663a1977038f772ea1fc0389e87d09
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96128020"
---
# <a name="create-event-notification-transact-sql"></a>CREATE EVENT NOTIFICATION (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Cria um objeto que envia informações sobre um banco de dados ou evento de servidor para um serviço do Service Broker. As notificações de evento são criadas somente com instruções [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
CREATE EVENT NOTIFICATION event_notification_name   
ON { SERVER | DATABASE | QUEUE queue_name }   
[ WITH FAN_IN ]  
FOR { event_type | event_group } [ ,...n ]  
TO SERVICE 'broker_service' , { 'broker_instance_specifier' | 'current database' }  
[ ; ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *event_notification_name*  
 É o nome da notificação de eventos. O nome de uma notificação de eventos deve estar em conformidade com as regras para [identificadores](../../relational-databases/databases/database-identifiers.md) e deve ser exclusivo no escopo em que é criado: SERVER, DATABASE ou *object_name*.  
  
 SERVER  
 Aplica o escopo da notificação de eventos à instância atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se for especificada, a notificação será acionada sempre que o evento especificado na cláusula FOR ocorrer em qualquer lugar na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Essa opção não está disponível em um banco de dados independente.  
  
 DATABASE  
 Aplica o escopo da notificação de eventos ao banco de dados atual. Se for especificada, a notificação será acionada sempre que o evento especificado na cláusula FOR ocorrer no banco de dados atual.  
  
 QUEUE  
 Aplica o escopo da notificação em uma fila específica no banco de dados atual. QUEUE pode ser especificado somente se FOR QUEUE_ACTIVATION ou FOR BROKER_QUEUE_DISABLED também for especificado.  
  
 *queue_name*  
 É o nome da fila para a qual a notificação de eventos se aplica. *queue_name* poderá ser especificado apenas se QUEUE for especificado.  
  
 WITH FAN_IN  
 Instrui o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a enviar somente uma mensagem por evento para qualquer serviço especificado para todas as notificações de eventos que:  
  
-   São criadas no mesmo evento.  
  
-   São criadas pelo mesmo principal (conforme identificado pelo mesmo SID).  
  
-   Especifique o mesmo serviço e *broker_instance_specifier*.  
  
-   Especificam WITH FAN_IN.  
  
 Por exemplo, três notificações de eventos são criadas. Todas as notificações de eventos especificam FOR ALTER_TABLE, WITH FAN_IN, a mesma cláusula TO SERVICE e são criadas pelo mesmo SID. Quando uma instrução ALTER TABLE é executada, as mensagens criadas por essas três notificações de eventos são mescladas em uma. Portanto, o serviço de destino recebe só uma mensagem do evento.  
  
 *event_type*  
 É o nome de um tipo de evento que faz com que a notificação de eventos seja executada. *event_type* pode ser um tipo de evento DDL [!INCLUDE[tsql](../../includes/tsql-md.md)], um tipo de evento de Rastreamento do SQL ou um tipo de evento [!INCLUDE[ssSB](../../includes/sssb-md.md)]. Para obter uma lista dos tipos de evento [!INCLUDE[tsql](../../includes/tsql-md.md)] DDL qualificados, consulte [DDL Events](../../relational-databases/triggers/ddl-events.md). Os tipos de evento [!INCLUDE[ssSB](../../includes/sssb-md.md)] são QUEUE_ACTIVATION e BROKER_QUEUE_DISABLED. Para obter mais informações, consulte [Event Notifications](../../relational-databases/service-broker/event-notifications.md).  
  
 *event_group*  
 É o nome de um grupo predefinido de tipos de evento [!INCLUDE[tsql](../../includes/tsql-md.md)] ou de Rastreamento do SQL. Uma notificação de eventos pode ser acionada depois da execução de qualquer evento que pertence a um grupo de eventos. Para obter uma lista dos grupos de eventos DDL, os eventos [!INCLUDE[tsql](../../includes/tsql-md.md)] abrangidos por eles e o escopo em que podem ser definidos, consulte [DDL Event Groups](../../relational-databases/triggers/ddl-event-groups.md).  
  
 *event_group* também age como uma macro, quando a instrução CREATE EVENT NOTIFICATION termina, com a adição dos tipos de evento abrangidos à exibição do catálogo **sys.events**.  
  
 **'** *broker_service* **'**  
 Especifica o serviço de destino que recebe os dados da instância de eventos. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] abre uma ou mais conversas com o serviço de destino para a notificação de eventos. Esse serviço deve respeitar o mesmo tipo de mensagem de eventos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o contrato usados para enviar a mensagem.  
  
 As conversas permanecem abertas até que a notificação de eventos seja descartada. Alguns erros podem fazer as conversas fecharem antes. O encerramento explícito de algumas ou todas as conversas pode impedir que o serviço de destino receba mais mensagens.  
  
 { **'** _broker\_instance\_specifier_ **'**  |  **'current database'** }  
 Especifica uma instância do Service Broker na qual *broker_service* é resolvido. O valor para um agente de serviços específico pode ser adquirido ao consultar a coluna **service_broker_guid** da exibição do catálogo **sys.databases**. Use **'current database'** para especificar a instância do Service Broker no banco de dados atual. **'current database'** é um literal de cadeia de caracteres que não diferencia maiúsculas de minúsculas.  
  
> [!NOTE]  
>  Essa opção não está disponível em um banco de dados independente.  
  
## <a name="remarks"></a>Comentários  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] inclui um tipo de mensagem e contrato específicos para notificações de eventos. Portanto, um serviço de inicialização do Service Broker não precisa ser criado porque já existe um serviço que especifica o seguinte nome de contrato: `https://schemas.microsoft.com/SQL/Notifications/PostEventNotification`  
  
 O serviço de destino que recebe as notificações de eventos deve honrar esse contrato preexistente.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssSB](../../includes/sssb-md.md)] deve ser configurada para notificações de eventos que enviam mensagens a um agente de serviços em um servidor remoto. A segurança de caixa de diálogo deve ser configurada manualmente, de acordo com o modelo de segurança completo. Para obter mais informações, veja [Configurar a segurança de diálogo para notificações de evento](../../relational-databases/service-broker/configure-dialog-security-for-event-notifications.md).  
  
 Se uma transação de eventos que ativa uma notificação for revertida, o envio da notificação de eventos também será revertido. As notificações de eventos não são acionadas por uma ação definida em um gatilho quando a transação é confirmada ou revertida no gatilho. Como os eventos de rastreamento não são associados por transações, as notificações de eventos baseadas nos eventos de rastreamentos são enviadas independentemente de a transação que as acionou estar revertida.  
  
 Se a conversa entre o servidor e o serviço de destino for quebrada após o acionamento de uma notificação de eventos, um erro será relatado e a notificação de eventos será descartada.  
  
 A transação de eventos que iniciou originalmente a notificação não é afetada pelo êxito ou pela falha do envio da notificação de eventos.  
  
 Qualquer falha de envio de uma notificação de eventos é registrada.  
  
## <a name="permissions"></a>Permissões  
 Para criar uma notificação de eventos com escopo no banco de dados (ON DATABASE), requer a permissão CREATE DATABASE DDL EVENT NOTIFICATION no banco de dados atual.  
  
 Para criar uma notificação de eventos em uma instrução DDL com escopo no servidor (ON SERVER), requer a permissão CREATE DDL EVENT NOTIFICATION no servidor.  
  
 Para criar uma notificação de eventos em um evento de rastreamento, requer a permissão CREATE TRACE EVENT NOTIFICATION no servidor.  
  
 Para criar uma notificação de eventos com escopo em uma fila, requer a permissão ALTER na fila.  
  
## <a name="examples"></a>Exemplos  
  
> [!NOTE]  
>  Nos exemplos A e B abaixo, o GUID na cláusula `TO SERVICE 'NotifyService'` ('8140a771-3c4b-4479-8ac0-81008ab17984') é específico do computador no qual o exemplo foi configurado. Para essa instância, esse era o GUID para o banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
>   
>  Para copiar e executar esses exemplos, é necessário substituir esse GUID pelo GUID do seu computador e pela instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Conforme explicado na seção Argumentos acima, você pode adquirir **'** _broker\_instance\_specifier_ **'** consultando a coluna service_broker_guid da exibição de catálogo sys.databases.  
  
### <a name="a-creating-an-event-notification-that-is-server-scoped"></a>a. Criando uma notificação de eventos no escopo do servidor  
 O exemplo a seguir cria os objetos obrigatórios para configurar um serviço de destino usando o [!INCLUDE[ssSB](../../includes/sssb-md.md)]. O serviço de destino faz referência ao tipo de mensagem e ao contrato do serviço de inicialização específico para notificações de eventos. Em seguida, uma notificação de evento é criada nesse serviço de destino, que envia uma notificação sempre que um evento de rastreamento `Object_Created` acontece na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```sql  
--Create a queue to receive messages.  
CREATE QUEUE NotifyQueue ;  
GO  

--Create a service on the queue that references  
--the event notifications contract.  
CREATE SERVICE NotifyService  
ON QUEUE NotifyQueue  
([https://schemas.microsoft.com/SQL/Notifications/PostEventNotification]);  
GO  

--Create a route on the service to define the address   
--to which Service Broker sends messages for the service.  
CREATE ROUTE NotifyRoute  
WITH SERVICE_NAME = 'NotifyService',  
ADDRESS = 'LOCAL';  
GO 

--Create the event notification.  
CREATE EVENT NOTIFICATION log_ddl1   
ON SERVER   
FOR Object_Created   
TO SERVICE 'NotifyService',  
    '8140a771-3c4b-4479-8ac0-81008ab17984' ;  
```  
  
### <a name="b-creating-an-event-notification-that-is-database-scoped"></a>B. Criando uma notificação de eventos no escopo do banco de dados  
 O exemplo a seguir cria uma notificação de eventos no mesmo serviço de destino do exemplo anterior. A notificação de eventos é acionada depois que um evento `ALTER_TABLE` ocorre no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] de amostra.  
  
```sql  
CREATE EVENT NOTIFICATION Notify_ALTER_T1  
ON DATABASE  
FOR ALTER_TABLE  
TO SERVICE 'NotifyService',  
    '8140a771-3c4b-4479-8ac0-81008ab17984';  
```  
  
### <a name="c-getting-information-about-an-event-notification-that-is-server-scoped"></a>C. Obtendo informações sobre uma notificação de eventos no escopo do servidor  
 O exemplo a seguir consulta a exibição do catálogo `sys.server_event_notifications` para obter os metadados sobre a notificação de eventos `log_ddl1` que foi criada no escopo de servidor.  
  
```sql  
SELECT * FROM sys.server_event_notifications  
WHERE name = 'log_ddl1';  
```  
  
### <a name="d-getting-information-about-an-event-notification-that-is-database-scoped"></a>D. Obtendo informações sobre uma notificação de eventos no escopo do banco de dados  
 O exemplo a seguir consulta a exibição do catálogo `sys.event_notifications` para obter os metadados sobre a notificação de eventos `Notify_ALTER_T1` que foi criada no escopo de banco de dados.  
  
```sql  
SELECT * FROM sys.event_notifications  
WHERE name = 'Notify_ALTER_T1';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Notificações de eventos](../../relational-databases/service-broker/event-notifications.md)   
 [DROP EVENT NOTIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-event-notification-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.event_notifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-event-notifications-transact-sql.md)   
 [sys.server_event_notifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-notifications-transact-sql.md)   
 [sys.events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-events-transact-sql.md)   
 [sys.server_events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-events-transact-sql.md)  
  
  
