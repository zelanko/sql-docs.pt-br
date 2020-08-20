---
description: Chamando métodos
title: Chamando métodos | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- methods [SMO]
- calling methods
- SQL Server Management Objects, method calling
- SMO [SQL Server], method calling
ms.assetid: c88d5c5f-9ff0-4f84-b2b6-24c6b90fa15e
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: bfcb45457c5b9625bb4f1eda3704c37e9e89cbc8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88498546"
---
# <a name="calling-methods"></a>Chamando métodos
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  Os métodos executam tarefas específicas relacionadas ao objeto, como emitir um **Checkpoint** em um banco de dados ou solicitar uma lista enumerada de logons para a instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Os métodos executam uma operação em um objeto. Podem assumir parâmetros e frequentemente têm um valor de retorno. O valor de retorno pode ser um tipo de dados simples, um objeto complexo ou uma estrutura que contém muitos membros.  
  
 Use o tratamento de exceções para detectar se o método obteve êxito. Para obter mais informações, consulte [Handling SMO Exceptions](../../../relational-databases/server-management-objects-smo/create-program/handling-smo-exceptions.md).  
  
## <a name="examples"></a>Exemplos  
Para usar qualquer exemplo de código fornecido, será necessário escolher o ambiente de programação, o modelo de programação e a linguagem de programação para criar o aplicativo. Para obter mais informações, consulte  [criar um projeto do Visual C&#35; Smo no Visual Studio .net](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
 
  
## <a name="using-a-simple-smo-method-in-visual-basic"></a>Usando um método SMO simples no Visual Basic  
 Neste exemplo, o método <xref:Microsoft.SqlServer.Management.Smo.Database.Create%2A> não utiliza nenhum parâmetro e não tem nenhum valor de retorno.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Define a Database object variable by supplying the parent server and the database name arguments in the constructor.
Dim db As Database
db = New Database(srv, "Test_SMO_Database")
'Call the Create method to create the database on the instance of SQL Server. 
db.Create()
```
  
## <a name="using-a-simple-smo-method-in-visual-c"></a>Usando um método SMO simples no Visual C#  
 Neste exemplo, o método <xref:Microsoft.SqlServer.Management.Smo.Database.Create%2A> não utiliza nenhum parâmetro e não tem nenhum valor de retorno.  
  
```csharp  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Define a Database object variable by supplying the parent server and the database name arguments in the constructor.   
Database db;   
db = new Database(srv, "Test_SMO_Database");   
//Call the Create method to create the database on the instance of SQL Server.   
db.Create();   
```  
  
 }  
  
## <a name="using-an-smo-method-with-a-parameter-in-visual-basic"></a>Usando um método SMO com um parâmetro no Visual Basic  
 O objeto <xref:Microsoft.SqlServer.Management.Smo.Table> tem um método chamado <xref:Microsoft.SqlServer.Management.Smo.Table.RebuildIndexes%2A>. Esse método exige um parâmetro numérico que especifica o **FillFactor**.  
  
```VBNET
Dim srv As Server  
srv = New Server  
Dim tb As Table  
tb = srv.Databases("AdventureWorks2012").Tables("Employee", "HumanResources")  
tb.RebuildIndexes(70)  
```  
  
## <a name="using-an-smo-method-with-a-parameter-in-visual-c"></a>Usando um método SMO com um parâmetro no Visual C#  
 O objeto <xref:Microsoft.SqlServer.Management.Smo.Table> tem um método chamado <xref:Microsoft.SqlServer.Management.Smo.Table.RebuildIndexes%2A>. Esse método exige um parâmetro numérico que especifica o `FillFactor`.  
  
```csharp  
{   
Server srv = default(Server);   
srv = new Server();   
Table tb = default(Table);   
tb = srv.Databases("AdventureWorks2012").Tables("Employee", "HumanResources");   
tb.RebuildIndexes(70);   
}   
```  
  
## <a name="using-an-enumeration-method-that-returns-a-datatable-object-in-visual-basic"></a>Usando um método de enumeração que retorna um objeto DataTable no Visual Basic  
 Esta seção descreve como chamar um método de enumeração e tratar os dados no objeto <xref:System.Data.DataTable> retornado.  
  
 O método <xref:Microsoft.SqlServer.Management.Smo.Server.EnumCollations%2A> retorna um objeto <xref:System.Data.DataTable>, que exige navegação adicional para acessar todas as informações de ordenação disponíveis sobre a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
```VBNET
'Connect to the local, default instance of SQL Server.  
Dim srv As Server  
srv = New Server  
'Call the EnumCollations method and return collation information to DataTable variable.  
Dim d As DataTable  
'Select the returned data into an array of DataRow.  
d = srv.EnumCollations  
'Iterate through the rows and display collation details for the instance of SQL Server.  
Dim r As DataRow  
Dim c As DataColumn  
For Each r In d.Rows  
    Console.WriteLine("==")  
    For Each c In r.Table.Columns  
        Console.WriteLine(c.ColumnName + " = " + r(c).ToString)  
    Next  
Next  
```  
  
## <a name="using-an-enumeration-method-that-returns-a-datatable-object-in-visual-c"></a>Usando um método de enumeração que retorna um objeto DataTable no Visual C#  
 Esta seção descreve como chamar um método de enumeração e tratar os dados no objeto <xref:System.Data.DataTable> retornado.  
  
 O método <xref:Microsoft.SqlServer.Management.Smo.Server.EnumCollations%2A> retorna um objeto <xref:System.Data.DataTable> de sistema. O objeto <xref:System.Data.DataTable> exige navegação adicional para acessar todas as informações de ordenação disponíveis sobre a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
```csharp  
//Connect to the local, default instance of SQL Server.   
{   
Server srv = default(Server);   
srv = new Server();   
//Call the EnumCollations method and return collation information to DataTable variable.   
DataTable d = default(DataTable);   
//Select the returned data into an array of DataRow.   
d = srv.EnumCollations;   
//Iterate through the rows and display collation details for the instance of SQL Server.   
DataRow r = default(DataRow);   
DataColumn c = default(DataColumn);   
foreach ( r in d.Rows) {   
  Console.WriteLine("=========");   
  foreach ( c in r.Table.Columns) {   
    Console.WriteLine(c.ColumnName + " = " + r(c).ToString);   
  }   
}   
}   
```  
  
## <a name="constructing-an-object-in-visual-basic"></a>Construindo um objeto no Visual Basic  
 O construtor de qualquer objeto pode ser chamado usando o operador **New** . O construtor do objeto <xref:Microsoft.SqlServer.Management.Smo.Database> é sobrecarregado e a versão do construtor do objeto <xref:Microsoft.SqlServer.Management.Smo.Database> que é usada no exemplo utiliza dois parâmetros: o objeto <xref:Microsoft.SqlServer.Management.Smo.Server> pai ao qual o banco de dados pertence e uma cadeia de caracteres que representa o nome do novo banco de dados.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Declare and define a Database object by supplying the parent server and the database name arguments in the constructor.
Dim d As Database
d = New Database(srv, "Test_SMO_Database")
'Create the database on the instance of SQL Server.
d.Create()
Console.WriteLine(d.Name)
```
  
## <a name="constructing-an-object-in-visual-c"></a>Construindo um objeto no Visual C#  
 O construtor de qualquer objeto pode ser chamado usando o operador **New** . O construtor do objeto <xref:Microsoft.SqlServer.Management.Smo.Database> é sobrecarregado e a versão do construtor do objeto <xref:Microsoft.SqlServer.Management.Smo.Database> que é usada no exemplo utiliza dois parâmetros: o objeto <xref:Microsoft.SqlServer.Management.Smo.Server> pai ao qual o banco de dados pertence e uma cadeia de caracteres que representa o nome do novo banco de dados.  
  
```csharp  
{   
Server srv;   
srv = new Server();   
Table tb;   
tb = srv.Databases("AdventureWorks2012").Tables("Employee", "HumanResources");   
tb.RebuildIndexes(70);   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Declare and define a Database object by supplying the parent server and the database name arguments in the constructor.   
Database d;   
d = new Database(srv, "Test_SMO_Database");   
//Create the database on the instance of SQL Server.   
d.Create();   
Console.WriteLine(d.Name);   
}  
```  
  
## <a name="copying-an-smo-object-in-visual-basic"></a>Copiando um objeto SMO no Visual Basic  
 Este exemplo de código usa o método <xref:Microsoft.SqlServer.Management.Common.ServerConnection.Copy%2A> para criar uma cópia do objeto <xref:Microsoft.SqlServer.Management.Smo.Server>. O objeto <xref:Microsoft.SqlServer.Management.Smo.Server> representa uma conexão com uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
```VBNET  
'Connect to the local, default instance of SQL Server.
Dim srv1 As Server
srv1 = New Server()
'Modify the default database and the timeout period for the connection.
srv1.ConnectionContext.DatabaseName = "AdventureWorks2012"
srv1.ConnectionContext.ConnectTimeout = 30
'Make a second connection using a copy of the ConnectionContext property and verify settings.
Dim srv2 As Server
srv2 = New Server(srv1.ConnectionContext.Copy)
Console.WriteLine(srv2.ConnectionContext.ConnectTimeout.ToString)
```
  
## <a name="copying-an-smo-object-in-visual-c"></a>Copiando um objeto SMO no Visual C#  
 Este exemplo de código usa o método <xref:Microsoft.SqlServer.Management.Common.ServerConnection.Copy%2A> para criar uma cópia do objeto <xref:Microsoft.SqlServer.Management.Smo.Server>. O objeto <xref:Microsoft.SqlServer.Management.Smo.Server> representa uma conexão com uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
```csharp  
{   
//Connect to the local, default instance of SQL Server.   
Server srv1;   
srv1 = new Server();   
//Modify the default database and the timeout period for the connection.   
srv1.ConnectionContext.DatabaseName = "AdventureWorks2012";   
srv1.ConnectionContext.ConnectTimeout = 30;   
//Make a second connection using a copy of the ConnectionContext property and verify settings.   
Server srv2;   
srv2 = new Server(srv1.ConnectionContext.Copy);   
Console.WriteLine(srv2.ConnectionContext.ConnectTimeout.ToString);   
}  
```  
  
## <a name="monitoring-server-processes-in-visual-basic"></a>Monitorando processos de servidor no Visual Basic  
 Você pode obter as informações de tipo de status atuais sobre a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] através dos métodos de enumeração. O exemplo de código usa o método <xref:Microsoft.SqlServer.Management.Smo.Server.EnumProcesses%2A> para descobrir informações sobre os processos atuais. Ele também demonstra como trabalhar com as colunas e linhas no objeto <xref:System.Data.DataTable> retornado.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Call the EnumCollations method and return collation information to DataTable variable.
Dim d As DataTable
'Select the returned data into an array of DataRow.
d = srv.EnumProcesses
'Iterate through the rows and display collation details for the instance of SQL Server.
Dim r As DataRow
Dim c As DataColumn
For Each r In d.Rows
    Console.WriteLine("============================================")
    For Each c In r.Table.Columns
        Console.WriteLine(c.ColumnName + " = " + r(c).ToString)
    Next
Next
```
  
## <a name="monitoring-server-processes-in-visual-c"></a>Monitorando processos de servidor no Visual C#  
 Você pode obter as informações de tipo de status atuais sobre a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] através dos métodos de enumeração. O exemplo de código usa o método <xref:Microsoft.SqlServer.Management.Smo.Server.EnumProcesses%2A> para descobrir informações sobre os processos atuais. Ele também demonstra como trabalhar com as colunas e linhas no objeto <xref:System.Data.DataTable> retornado.  
  
```csharp  
//Connect to the local, default instance of SQL Server.   
{   
Server srv = default(Server);   
srv = new Server();   
//Call the EnumCollations method and return collation information to DataTable variable.   
DataTable d = default(DataTable);   
//Select the returned data into an array of DataRow.   
d = srv.EnumProcesses;   
//Iterate through the rows and display collation details for the instance of SQL Server.   
DataRow r = default(DataRow);   
DataColumn c = default(DataColumn);   
foreach ( r in d.Rows) {   
  Console.WriteLine("=====");   
  foreach ( c in r.Table.Columns) {   
    Console.WriteLine(c.ColumnName + " = " + r(c).ToString);   
  }   
}   
}   
```  
  
## <a name="see-also"></a>Consulte Também  
 <xref:Microsoft.SqlServer.Management.Smo.Server>   
 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>  
  
  
