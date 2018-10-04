---
title: Trabalhando com o provedor WMI para eventos de servidor | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- event notifications [WMI]
- permissions [WMI]
- connection strings [WMI]
- security [WMI]
- Service Broker [WMI]
- WMI Provider for Server Events, connection strings
- WMI Provider for Server Events, Service Broker
- notifications [WMI]
- WMI Provider for Server Events, security
ms.assetid: cd974b3b-2309-4a20-b9be-7cfc93fc4389
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: bd4def614340115bafc6046b4d0ea9d90f647e9e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48060159"
---
# <a name="working-with-the-wmi-provider-for-server-events"></a>Trabalhando com o Provedor WMI para Eventos de Servidor
  Este tópico fornece diretrizes que você deve considerar antes de programar o uso do Provedor WMI para Eventos de Servidor.  
  
## <a name="enabling-service-broker"></a>Habilitando o Service Broker  
 O Provedor WMI para Eventos de Servidor funciona traduzindo consultas WQL de eventos para notificações de eventos no banco de dados de destino. Um entendimento de como funcionam as notificações de eventos pode ser útil ao programar com base no provedor. Para obter mais informações, consulte [Provedor WMI para conceitos de eventos de servidor](http://technet.microsoft.com/library/ms180560.aspx).  
  
 Em particular, como as notificações de evento criadas pelo Provedor WMI usam o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para enviar mensagens sobre eventos de servidor, esse serviço precisa ser habilitado sempre que são gerados eventos. Se o programa consultar eventos em uma instância de servidor, o [!INCLUDE[ssSB](../../includes/sssb-md.md)] no msdb dessa instância precisará estar habilitado porque esse é o local do serviço de destino do [!INCLUDE[ssSB](../../includes/sssb-md.md)] (chamado SQL/Notifications/ProcessWMIEventProviderNotification/v1.0) criado pelo provedor. Se seu programa consultar eventos em um banco de dados ou em um objeto de banco de dados específico, deve ser habilitado o [!INCLUDE[ssSB](../../includes/sssb-md.md)] nesse banco de dados de destino. Se o [!INCLUDE[ssSB](../../includes/sssb-md.md)] correspondente não for habilitado após a implantação do aplicativo, quaisquer eventos gerados pela notificação de evento subjacente serão enviados para a fila do serviço usado pela notificação do evento, mas não serão retornados para o aplicativo de gerenciamento de WMI enquanto o [!INCLUDE[ssSB](../../includes/sssb-md.md)] não estiver habilitado.  
  
 A consulta a seguir determina quais Service Brokers são habilitados em uma instância de servidor, e o GUID de instância do Service Broker:  
  
```  
SELECT name, is_broker_enabled, service_broker_guid FROM sys.databases;  
```  
  
 A GUID do service broker do msdb é de interesse especial porque é o local do serviço de destino do provedor.  
  
 Para habilitar [!INCLUDE[ssSB](../../includes/sssb-md.md)] em um banco de dados, use a opção ENABLE_BROKER SET dos [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql) instrução.  
  
## <a name="specifying-a-connection-string"></a>Especificando uma cadeia de caracteres de conexão  
 Os aplicativos direcionam o Provedor WMI para Eventos de Servidor para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conectando-se a um namespace WMI definido pelo provedor. O serviço Windows WMI mapeia esse namespace para o DLL do provedor, Sqlwep.dll, e carrega-o na memória. Cada instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tem seu próprio namespace WMI, cujo padrão é: \\ \\.\\ *raiz*\Microsoft\SqlServer\ServerEvents\\*instance_name*. *nome_da_instância* é definido como MSSQLSERVER em uma instalação padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="permissions-and-server-authentication"></a>Permissões e autenticação do servidor  
 Para acessar o Provedor WMI para Eventos de Servidor, o cliente em que o aplicativo de gerenciamento de WMI se origina precisa corresponder ao grupo ou logon autenticado do Windows na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificado na cadeia de conexão do aplicativo.  
  
## <a name="permissions-and-event-notification-scope"></a>Permissões e escopo da notificação de eventos  
 O Provedor WMI para Eventos de Servidor traduz as consultas WQL para notificações de eventos no banco de dados de destino. Por isso, o aplicativo de chamada precisa ter não só as permissões mínimas necessárias para acessar o provedor, como também as permissões corretas no banco de dados para criar as notificações de eventos necessárias. A seguir estão as permissões:  
  
-   Para criar uma notificação de evento com escopo no banco de dados, no mínimo, é necessária a permissão CREATE DATABASE DDL EVENT NOTIFICATION no banco de dados atual.  
  
-   Para criar uma notificação de evento em uma instrução DDL com escopo no servidor, no mínimo, é necessária a permissão CREATE DDL EVENT NOTIFICATION no servidor.  
  
-   Para criar uma notificação de evento em um evento de rastreamento, no mínimo, é necessária a permissão CREATE TRACE EVENT NOTIFICATION no servidor.  
  
-   Para criar uma notificação de evento com escopo em uma fila, no mínimo, é necessária a permissão ALTER na fila.  
  
 Para obter informações sobre o escopo das consultas WQL, consulte [Usando o WQL com o Provedor WMI para eventos de servidor](http://technet.microsoft.com/library/ms180524\(v=sql.105\).aspx).  
  
 Para ilustrar escopo, considere um aplicativo de Provedor WMI que inclui a consulta WQL a seguir:  
  
```  
SELECT * FROM ALTER_TABLE  
WHERE DatabaseName = "AdventureWorks2012"   
    AND SchemaName = "Person"  
    AND ObjectName = "Person"  
    AND ObjectType = "TABLE";  
```  
  
 O provedor WMI traduz essa consulta para uma notificação de evento que é criada no banco de dados do [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. Isso significa que o chamador precisa ter as permissões necessárias para criar essa notificação de evento, especificamente a permissão CREATE DATABASE DDL EVENT NOTIFICATION no banco de dados do [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
 Se uma consulta WQL especifica uma notificação de evento com escopo no nível de servidor, por exemplo, emitindo a consulta SELECT * FROM ALTER_TABLE, o aplicativo de chamada precisará ter a permissão CREATE DDL EVENT NOTIFICATION no nível de servidor. Observe que notificações de evento com escopo no servidor são armazenadas no banco de dados mestre. Você pode usar o [server_event_notifications](/sql/relational-databases/system-catalog-views/sys-server-event-notifications-transact-sql) exibição para ver seus metadados de catálogo.  
  
> [!NOTE]  
>  O escopo da notificação de evento criada pelo Provedor WMI (servidor, banco de dados ou objeto) por fim depende do resultado do processo de verificação de permissões usado pelo provedor WMI. Isso é afetado pelo conjunto de permissões do usuário que está chamando o provedor e pela verificação do banco de dados que está sendo consultado.  
>   
>  No exemplo anterior, o provedor tenta primeiro criar uma notificação de evento com escopo no banco de dados (`ON DATABASE`). Se o provedor verifica que o banco de dados existe e que o chamador tem as permissões necessárias para criar uma notificação de evento nele, o registro é bem-sucedido. Se não for bem-sucedido, o provedor tentará criar uma notificação de evento no servidor (`ON SERVER`). Pressupondo que essa tentativa é bem-sucedida, todos os eventos `ALTER_TABLE` que ocorrem no servidor são enviados do processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o processo do Serviço WMI. Entretanto, o provedor filtra quaisquer eventos que não se aplicam ao banco de dados do `AdventureWorks` . Apesar de, por um lado, esse processo possivelmente aumentar a quantidade de tráfego de rede necessária para o escopo do evento, por outro, ele também oferece a flexibilidade de registrar consultas WQL no banco de dados antes de serem criadas e de receber os dados de evento depois de o banco de dados ser criado e a atividade de DDL ser iniciada nele.  
  
## <a name="permissions-and-message-verification"></a>Permissões e verificação de mensagem  
 O Provedor WMI não enviará mensagens para notificações de evento se ambas as condições a seguir forem verdadeiras:  
  
-   O usuário que criou a notificação de evento através do Provedor WMI não existe mais no banco de dados ou não tem mais a permissão necessária para criar uma notificação de evento semelhante.  
  
-   As notificações de evento são criadas nos eventos a seguir:  
  
    -   DROP_LOGIN  
  
    -   ALTER_LOGIN  
  
    -   DROP_USER  
  
    -   ALTER_USER  
  
    -   ADD_ROLE_MEMBER  
  
    -   DROP_ROLE_MEMBER  
  
    -   ADD_SERVER_ROLE_MEMBER  
  
    -   DROP_SERVER_ROLE_MEMBER  
  
    -   DENY ou REVOKE (Aplica-se somente às permissões ALTER DATABASE, ALTER ANY DATABASE EVENT NOTIFICATION, CREATE DATABASE DDL EVENT NOTIFICATION, CONTROL SERVER, ALTER ANY EVENT NOTIFICATION, CREATE DDL EVENT NOTIFICATION ou CREATE TRACE EVENT NOTIFICATION.)  
  
## <a name="working-with-event-data-on-the-client-side"></a>Trabalhando com dados de evento no lado do cliente  
 Depois que o provedor WMI para eventos de servidor cria a notificação de eventos necessários no banco de dados de destino, a notificação de evento envia dados ao serviço de destino no MSBD chamado **notificações/SQL/ProcessWMIEventProviderNotification /v1.0**. O serviço de destino coloca o evento em uma fila em `msdb` nomeada **WMIEventProviderNotificationQueue**. (O serviço e a fila são criados dinamicamente pelo provedor quando ele se conecta pela primeira vez ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].) O provedor lê os dados de evento XML dessa fila e os transforma em MOF (formato de objeto gerenciado) antes de devolvê-los ao aplicativo cliente. Os dados MOF consistem nas propriedades do evento que é solicitado pela consulta WQL como uma definição de classe de modelo CIM. Cada propriedade tem um tipo CIM correspondente. Por exemplo, a propriedade `SPID` é retornada como tipo CIM `Sint32`. Os tipos CIM para cada propriedade estão listados sob cada classe de evento em [provedor WMI para Classes de eventos do servidor e as propriedades](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-classes-and-properties.md).  
  
## <a name="see-also"></a>Consulte também  
 [Provedor WMI para conceitos de eventos de servidor](http://technet.microsoft.com/library/ms180560.aspx)  
  
  
