---
title: Manipulando eventos SMO | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- events [SMO]
- SQL Server Management Objects, events
- SMO [SQL Server], events
- events [SMO], about events
ms.assetid: b4f120dd-ba78-46ff-99c5-e47effac8544
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d0d309103880a369a88952e19b252fc15693fdd4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63191922"
---
# <a name="handling-smo-events"></a>Manipulando eventos SMO
  Há tipos de eventos de servidor que podem ser assinados usando um manipulador de eventos e o objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>.  
  
 Muitas das classes de instância no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects (SMO) podem disparar eventos quando ocorrem determinadas ações no servidor.  
  
 Esses eventos podem ser tratados programaticamente através da configuração de um manipulador de eventos e da inscrição nos eventos associados. Esse tipo de manipulação de eventos é transitório pois todas as assinaturas são removidas quando o programa cliente SMO é desativado.  
  
## <a name="connectioncontext-event-handling"></a>Manipulação de eventos do ConnectionContext  
 O objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> dá suporte a vários tipos de eventos. A propriedade do evento deve ser definida como uma instância de um manipulador de eventos apropriado, e o objeto do manipulador de eventos deve ser definido como uma função protegida que manipula o evento.  
  
## <a name="event-subscription"></a>Assinatura do evento  
 Para manipular eventos, escreva uma classe de manipulador de evento, crie uma instância dela, atribua o manipulador de eventos ao objeto pai e faça a assinatura do evento.  
  
 Uma classe de manipulador de eventos deve ser escrita para manipular eventos. A classe do manipulador de eventos pode conter mais de uma função de manipulador de eventos e deve ser instalada para os eventos a serem manipulados. As funções do manipulador de eventos recebem informações sobre o evento do parâmetro *ServerEventNotificatificationArgs* que pode ser usado para relatar informações sobre o evento.  
  
 Os tipos de eventos de servidor e banco de dados que podem ser manipulados <xref:Microsoft.SqlServer.Management.Smo.DatabaseEventSet> são listados na <xref:Microsoft.SqlServer.Management.Smo.ServerEventSet>classe e na classe.  
  
## <a name="example"></a>Exemplo  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="registering-event-handlers-and-subscribing-to-event-handling-in-visual-basic"></a>Registrando manipuladores de eventos e assinando a manipulação de eventos no Visual Basic  
 Este exemplo de código mostra como configurar o manipulador de eventos e como assinar os eventos de banco de dados.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBEvents1](SMO How to#SMO_VBEvents1)]  -->  
  
## <a name="registering-event-handlers-and-subscribing-to-event-handling-in-visual-c"></a>Registrando manipuladores de eventos e assinando a manipulação de eventos no Visual C#  
 Este exemplo de código mostra como configurar o manipulador de eventos e como assinar os eventos de banco de dados.  
  
```  
//Create an event handler subroutine that runs when a table is created.   
private void MyCreateEventHandler(object sender, ServerEventArgs e)   
{   
Console.WriteLine("A table has just been added to the AdventureWorks2012 database.");   
}   
//Create an event handler subroutine that runs when a table is deleted.   
private void MyDropEventHandler(object sender, ServerEventArgs e)   
{   
Console.WriteLine("A table has just been dropped from the AdventureWorks2012 database.");   
}   
public void Main()   
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Reference the AdventureWorks2012 database.   
Database db;   
db = srv.Databases("AdventureWorks2012");   
//Create a database event set that contains the CreateTable event only.   
DatabaseEventSet databaseCreateEventSet = new DatabaseEventSet();   
databaseCreateEventSet.CreateTable = true;   
//Create a server event handler and set it to the first event handler subroutine.   
ServerEventHandler serverCreateEventHandler;   
serverCreateEventHandler = new ServerEventHandler(MyCreateEventHandler);   
//Subscribe to the first server event handler when a CreateTable event occurs.   
db.Events.SubscribeToEvents(databaseCreateEventSet, serverCreateEventHandler);   
    //Create a database event set that contains the DropTable event only.   
DatabaseEventSet databaseDropEventSet = new DatabaseEventSet();   
databaseDropEventSet.DropTable = true;   
//Create a server event handler and set it to the second event handler subroutine.   
ServerEventHandler serverDropEventHandler;   
serverDropEventHandler = new ServerEventHandler(MyDropEventHandler);   
//Subscribe to the second server event handler when a DropTable event occurs.   
db.Events.SubscribeToEvents(databaseDropEventSet, serverDropEventHandler);   
//Start event handling.   
db.Events.StartEvents();   
//Create a table on the database.   
Table tb;   
tb = new Table(db, "Test_Table");   
Column mycol1;   
mycol1 = new Column(tb, "Name", DataType.NChar(50));   
mycol1.Collation = "Latin1_General_CI_AS";   
mycol1.Nullable = true;   
tb.Columns.Add(mycol1);   
tb.Create();   
//Remove the table.   
tb.Drop();   
//Wait until the events have occured.   
int x;   
int y;   
for (x = 1; x <= 1000000000; x++) {   
    y = x * 2;   
}   
//Stop event handling.   
db.Events.StopEvents();   
}  
```  
  
  
