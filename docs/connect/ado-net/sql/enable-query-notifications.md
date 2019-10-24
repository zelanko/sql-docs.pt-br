---
title: Habilitando notificações de consulta
description: Discute como usar notificações de consulta, incluindo os requisitos para habilitá-las e usá-las.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: a5333e19-8e55-4aa9-82dc-ca8745e516ed
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 94b472a1fe040aa3a684d9f7b523ba09c82a651e
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452238"
---
# <a name="enabling-query-notifications"></a>Habilitando notificações de consulta

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Download ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Os aplicativos que consomem notificações de consulta têm um conjunto comum de requisitos. Sua fonte de dados deve ser configurada corretamente para dar suporte a notificações de consulta SQL e o usuário deve ter as permissões corretas do lado do cliente e do lado do servidor.  
  
Para usar as notificações de consulta, você deve:  
  
- Habilite as notificações de consulta para seu banco de dados.  
  
- Verifique se a ID de usuário usada para se conectar ao banco de dados tem as permissões necessárias.  
  
- Use um objeto <xref:Microsoft.Data.SqlClient.SqlCommand> para executar uma instrução SELECT válida com um objeto de notificação associado — seja <xref:Microsoft.Data.SqlClient.SqlDependency> ou <xref:Microsoft.Data.Sql.SqlNotificationRequest>.  
  
- Forneça o código para processar a notificação se os dados que estão sendo monitorados forem alterados.  
  
## <a name="query-notifications-requirements"></a>Requisitos de notificações de consulta  
As notificações de consulta têm suporte apenas para instruções SELECT que atendem a uma lista de requisitos específicos. A tabela a seguir fornece links para a documentação de Service Broker e notificações de consulta no Manuais Online do SQL Server.  
  
**Documentação do SQL Server**  
  
- [Criando uma consulta para notificação](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms181122(v=sql.105))  
  
- [Considerações de segurança para Service Broker](https://docs.microsoft.com/previous-versions/sql/sql-server-2005/ms166059(v=sql.90))  
  
- [Segurança e proteção (Service Broker)](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/bb522911(v=sql.105))  
  
- [Considerações de segurança para serviços de notificação](https://docs.microsoft.com/previous-versions/sql/sql-server-2005/ms172604(v=sql.90))  
  
- [Permissões de notificação de consulta](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms188311(v=sql.105))  
  
- [Considerações internacionais para Service Broker](https://docs.microsoft.com/previous-versions/sql/sql-server-2005/ms166028(v=sql.90))  
  
- [Considerações sobre design de solução (Service Broker)](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/bb522899(v=sql.105))  
  
- [Service Broker Developer InfoCenter](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms166100(v=sql.105))  
  
- [Guia do desenvolvedor (Service Broker)](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/bb522908(v=sql.105))  
  
## <a name="enabling-query-notifications-to-run-sample-code"></a>Habilitando notificações de consulta para executar o código de exemplo  
Para habilitar o Service Broker no banco de dados **AdventureWorks** usando o SQL Server Management Studio, execute a seguinte instrução Transact-SQL:  
  
`ALTER DATABASE AdventureWorks SET ENABLE_BROKER;`  
  
Para que os exemplos de notificação de consulta sejam executados corretamente, as instruções Transact-SQL a seguir devem ser executadas no servidor de banco de dados.  
  
```sql
CREATE QUEUE ContactChangeMessages;  
  
CREATE SERVICE ContactChangeNotifications  
  ON QUEUE ContactChangeMessages  
([http://schemas.microsoft.com/SQL/Notifications/PostQueryNotification]);  
```  
  
## <a name="query-notifications-permissions"></a>Permissões de notificações de consulta  
Os usuários que executam comandos que solicitam notificação devem ter a permissão de assinatura de banco de dados de notificações de consulta no servidor.  
  
O código do lado do cliente que é executado em uma situação de confiança parcial requer o <xref:Microsoft.Data.SqlClient.SqlClientPermission>.  
  
O código a seguir cria um objeto <xref:Microsoft.Data.SqlClient.SqlClientPermission>, definindo o <xref:System.Security.Permissions.PermissionState> como <xref:System.Security.Permissions.PermissionState.Unrestricted>. O <xref:System.Security.CodeAccessPermission.Demand%2A> forçará uma <xref:System.Security.SecurityException> em tempo de execução se todos os chamadores mais altos na pilha de chamadas não tiverem recebido a permissão.  
  
[!code-csharp[DataWorks SqlClientPermission_Demand#1](~/../sqlclient/doc/samples/SqlClientPermission_Demand.cs#1)]
  
## <a name="choosing-a-notification-object"></a>Escolhendo um objeto de notificação  
A API de notificações de consulta fornece dois objetos para processar notificações: <xref:Microsoft.Data.SqlClient.SqlDependency> e <xref:Microsoft.Data.Sql.SqlNotificationRequest>.
  
### <a name="using-sqldependency"></a>Usando SqlDependency  
Para usar <xref:Microsoft.Data.SqlClient.SqlDependency>, Service Broker deve ser habilitado para o banco de dados SQL Server que está sendo usado e os usuários devem ter permissões para receber notificações. Service Broker objetos, como a fila de notificação, são predefinidos.  
  
Além disso, <xref:Microsoft.Data.SqlClient.SqlDependency> inicia automaticamente um thread de trabalho para processar as notificações à medida que elas são postadas na fila; Ele também analisa a Service Broker mensagem, expondo as informações como dados de argumento de evento. <xref:Microsoft.Data.SqlClient.SqlDependency> deve ser inicializado chamando o método `Start` para estabelecer uma dependência para o banco de dados. Esse é um método estático que precisa ser chamado apenas uma vez durante a inicialização do aplicativo para cada conexão de banco de dados necessária. O método `Stop` deve ser chamado na terminação do aplicativo para cada conexão de dependência que foi feita.  
  
### <a name="using-sqlnotificationrequest"></a>Usando SqlNotificationRequest  
Por outro lado, <xref:Microsoft.Data.Sql.SqlNotificationRequest> exige que você implemente toda a infraestrutura de escuta por conta própria. Além disso, todos os objetos de Service Broker de suporte, como os tipos de fila, serviço e mensagem, com suporte da fila, devem ser definidos. Essa abordagem manual será útil se seu aplicativo exigir mensagens de notificação especiais ou comportamentos de notificação ou se seu aplicativo fizer parte de um aplicativo de Service Broker maior.  
  
## <a name="next-steps"></a>Próximas etapas
- [Notificações de consulta no SQL Server](query-notifications-sql-server.md)
