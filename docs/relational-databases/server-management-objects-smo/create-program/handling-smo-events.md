---
title: Manipulando eventos SMO | Microsoft Docs
ms.custom: 
ms.date: 08/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- events [SMO]
- SQL Server Management Objects, events
- SMO [SQL Server], events
- events [SMO], about events
ms.assetid: b4f120dd-ba78-46ff-99c5-e47effac8544
caps.latest.revision: "48"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ee676a0f3eca14164b44b19f3e5a1dfc7258c997
ms.sourcegitcommit: cb2f9d4db45bef37c04064a9493ac2c1d60f2c22
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/12/2018
---
# <a name="handling-smo-events"></a>Manipulando eventos SMO
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  Há tipos de eventos de servidor que podem ser assinados usando um manipulador de eventos e o objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>.  
  
 Muitas das classes de instância no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects (SMO) podem disparar eventos quando ocorrem determinadas ações no servidor.  
  
 Esses eventos podem ser tratados programaticamente através da configuração de um manipulador de eventos e da inscrição nos eventos associados. Esse tipo de manipulação de eventos é transitório pois todas as assinaturas são removidas quando o programa cliente SMO é desativado.  
  
## <a name="connectioncontext-event-handling"></a>Manipulação de eventos do ConnectionContext  
 O objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> dá suporte a vários tipos de eventos. A propriedade do evento deve ser definida como uma instância de um manipulador de eventos apropriado, e o objeto do manipulador de eventos deve ser definido como uma função protegida que manipula o evento.  
  
## <a name="event-subscription"></a>Assinatura do evento  
 Para manipular eventos, escreva uma classe de manipulador de evento, crie uma instância dela, atribua o manipulador de eventos ao objeto pai e faça a assinatura do evento.  
  
 Uma classe de manipulador de eventos deve ser escrita para manipular eventos. A classe do manipulador de eventos pode conter mais de uma função de manipulador de eventos e deve ser instalada para os eventos a serem manipulados. As funções de manipulador de eventos recebem informações sobre o evento a partir de *ServerEventNotificatificationArgs* parâmetro que pode ser usado para relatar informações sobre o evento.  
  
 Os tipos de eventos de banco de dados e o servidor que podem ser manipulados são listados no <xref:Microsoft.SqlServer.Management.Smo.DatabaseEventSet> classe e o <xref:Microsoft.SqlServer.Management.Smo.ServerEventSet>classe.  
  
## <a name="example"></a>Exemplo  
Para usar qualquer exemplo de código fornecido, será necessário escolher o ambiente de programação, o modelo de programação e a linguagem de programação para criar o aplicativo. Para obter mais informações, consulte [criar um Visual C &#35; Projeto SMO no Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  

  
## <a name="registering-event-handlers-and-subscribing-to-event-handling-in-visual-basic"></a>Registrando manipuladores de eventos e assinando a manipulação de eventos no Visual Basic  
 Este exemplo de código mostra como configurar o manipulador de eventos e como assinar os eventos de banco de dados.  
  
```VBNET
'Create an event handler subroutine that runs when a table is created.
Private Sub MyCreateEventHandler(ByVal sender As Object, ByVal e As ServerEventArgs)
    Console.WriteLine("A table has just been added to the AdventureWorks2012 2008 database.")
End Sub
'Create an event handler subroutine that runs when a table is deleted.
Private Sub MyDropEventHandler(ByVal sender As Object, ByVal e As ServerEventArgs)
    Console.WriteLine("A table has just been dropped from the AdventureWorks2012 2008 database.")
End Sub
Sub Main()
    'Connect to the local, default instance of SQL Server.
    Dim srv As Server
    srv = New Server
    'Reference the AdventureWorks2012 database.
    Dim db As Database
    db = srv.Databases("AdventureWorks2012")
    'Create a database event set that contains the CreateTable event only.
    Dim databaseCreateEventSet As New DatabaseEventSet
    databaseCreateEventSet.CreateTable = True
    'Create a server event handler and set it to the first event handler subroutine.
    Dim serverCreateEventHandler As ServerEventHandler
    serverCreateEventHandler = New ServerEventHandler(AddressOf MyCreateEventHandler)
    'Subscribe to the first server event handler when a CreateTable event occurs.
    db.Events.SubscribeToEvents(databaseCreateEventSet, serverCreateEventHandler)
    'Create a database event set that contains the DropTable event only.
    Dim databaseDropEventSet As New DatabaseEventSet
    databaseDropEventSet.DropTable = True
    'Create a server event handler and set it to the second event handler subroutine.
    Dim serverDropEventHandler As ServerEventHandler
    serverDropEventHandler = New ServerEventHandler(AddressOf MyDropEventHandler)
    'Subscribe to the second server event handler when a DropTable event occurs.
    db.Events.SubscribeToEvents(databaseDropEventSet, serverDropEventHandler)
    'Start event handling.
    db.Events.StartEvents()
    'Create a table on the database.
    Dim tb As Table
    tb = New Table(db, "Test_Table")
    Dim mycol1 As Column
    mycol1 = New Column(tb, "Name", DataType.NChar(50))
    mycol1.Collation = "Latin1_General_CI_AS"
    mycol1.Nullable = True
    tb.Columns.Add(mycol1)
    tb.Create()
    'Remove the table.
    tb.Drop()
    'Wait until the events have occured.
    Dim x As Integer
    Dim y As Integer
    For x = 1 To 1000000000
        y = x * 2
    Next
    'Stop event handling.
    db.Events.StopEvents()

End Sub
``` 
  
## <a name="registering-event-handlers-and-subscribing-to-event-handling-in-visual-c"></a>Registrando manipuladores de eventos e assinando a manipulação de eventos no Visual C#  
 Este exemplo de código mostra como configurar o manipulador de eventos e como assinar os eventos de banco de dados.  
  
```csharp  
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
  
  
