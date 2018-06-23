---
title: Chamando métodos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- methods [SMO]
- calling methods
- SQL Server Management Objects, method calling
- SMO [SQL Server], method calling
ms.assetid: c88d5c5f-9ff0-4f84-b2b6-24c6b90fa15e
caps.latest.revision: 44
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 345e3b217933f544239c849e5a279d8fcc3623e8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36019546"
---
# <a name="calling-methods"></a>Chamando métodos
  Os métodos executam tarefas específicas relacionadas ao objeto, como emitir uma `Checkpoint` em um banco de dados ou solicitar uma lista enumerada de logons para a instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Os métodos executam uma operação em um objeto. Podem assumir parâmetros e frequentemente têm um valor de retorno. O valor de retorno pode ser um tipo de dados simples, um objeto complexo ou uma estrutura que contém muitos membros.  
  
 Use o tratamento de exceções para detectar se o método obteve êxito. Para obter mais informações, consulte [Handling SMO Exceptions](handling-smo-exceptions.md).  
  
## <a name="examples"></a>Exemplos  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="using-a-simple-smo-method-in-visual-basic"></a>Usando um método SMO simples no Visual Basic  
 Neste exemplo, o método <xref:Microsoft.SqlServer.Management.Smo.Database.Create%2A> não utiliza nenhum parâmetro e não tem nenhum valor de retorno.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBMethods1](SMO How to#SMO_VBMethods1)]  -->  
  
## <a name="using-a-simple-smo-method-in-visual-c"></a>Usando um método SMO simples no Visual C#  
 Neste exemplo, o método <xref:Microsoft.SqlServer.Management.Smo.Database.Create%2A> não utiliza nenhum parâmetro e não tem nenhum valor de retorno.  
  
```  
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
 O <xref:Microsoft.SqlServer.Management.Smo.Table> objeto tem um método chamado <xref:Microsoft.SqlServer.Management.Smo.Table.RebuildIndexes%2A>. Esse método exige um parâmetro numérico que especifica o `FillFactor`.  
  
```  
Dim srv As Server  
srv = New Server  
Dim tb As Table  
tb = srv.Databases("AdventureWorks2012").Tables("Employee", "HumanResources")  
tb.RebuildIndexes(70)  
```  
  
## <a name="using-an-smo-method-with-a-parameter-in-visual-c"></a>Usando um método SMO com um parâmetro no Visual C#  
 O <xref:Microsoft.SqlServer.Management.Smo.Table> objeto tem um método chamado <xref:Microsoft.SqlServer.Management.Smo.Table.RebuildIndexes%2A>. Esse método exige um parâmetro numérico que especifica o `FillFactor`.  
  
```  
{   
Server srv = default(Server);   
srv = new Server();   
Table tb = default(Table);   
tb = srv.Databases("AdventureWorks2012").Tables("Employee", "HumanResources");   
tb.RebuildIndexes(70);   
}   
```  
  
## <a name="using-an-enumeration-method-that-returns-a-datatable-object-in-visual-basic"></a>Usando um método de enumeração que retorna um objeto DataTable no Visual Basic  
 Esta seção descreve como chamar um método de enumeração e como tratar os dados no retornado <xref:System.Data.DataTable> objeto.  
  
 O método <xref:Microsoft.SqlServer.Management.Smo.Server.EnumCollations%2A> retorna um objeto <xref:System.Data.DataTable>, que exige navegação adicional para acessar todas as informações de agrupamento disponíveis sobre a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
```  
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
 Esta seção descreve como chamar um método de enumeração e como tratar os dados no retornado <xref:System.Data.DataTable> objeto.  
  
 O <xref:Microsoft.SqlServer.Management.Smo.Server.EnumCollations%2A> método retorna um sistema <xref:System.Data.DataTable> objeto. O <xref:System.Data.DataTable> objeto exige navegação adicional para acessar todas as informações de agrupamento disponíveis sobre a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
```  
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
 O construtor de qualquer objeto pode ser chamado usando o operador `New`. O construtor do objeto <xref:Microsoft.SqlServer.Management.Smo.Database> é sobrecarregado e a versão do construtor do objeto <xref:Microsoft.SqlServer.Management.Smo.Database> que é usada no exemplo utiliza dois parâmetros: o objeto <xref:Microsoft.SqlServer.Management.Smo.Server> pai ao qual o banco de dados pertence e uma cadeia de caracteres que representa o nome do novo banco de dados.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBMethods4](SMO How to#SMO_VBMethods4)]  -->  
  
## <a name="constructing-an-object-in-visual-c"></a>Construindo um objeto no Visual C#  
 O construtor de qualquer objeto pode ser chamado usando o operador `New`. O construtor do objeto <xref:Microsoft.SqlServer.Management.Smo.Database> é sobrecarregado e a versão do construtor do objeto <xref:Microsoft.SqlServer.Management.Smo.Database> que é usada no exemplo utiliza dois parâmetros: o objeto <xref:Microsoft.SqlServer.Management.Smo.Server> pai ao qual o banco de dados pertence e uma cadeia de caracteres que representa o nome do novo banco de dados.  
  
```  
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
 Este exemplo de código usa o <xref:Microsoft.SqlServer.Management.Common.ServerConnection.Copy%2A> método para criar uma cópia do <xref:Microsoft.SqlServer.Management.Smo.Server> objeto. O <xref:Microsoft.SqlServer.Management.Smo.Server> objeto representa uma conexão a uma instância de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VCMethods6](SMO How to#SMO_VCMethods6)]  -->  
  
## <a name="copying-an-smo-object-in-visual-c"></a>Copiando um objeto SMO no Visual C#  
 Este exemplo de código usa o <xref:Microsoft.SqlServer.Management.Common.ServerConnection.Copy%2A> método para criar uma cópia do <xref:Microsoft.SqlServer.Management.Smo.Server> objeto. O <xref:Microsoft.SqlServer.Management.Smo.Server> objeto representa uma conexão a uma instância de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
```  
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
 Você pode obter as informações de tipo de status atuais sobre a instância de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] por meio de métodos de enumeração. O exemplo de código usa o método <xref:Microsoft.SqlServer.Management.Smo.Server.EnumProcesses%2A> para descobrir informações sobre os processos atuais. Ele também demonstra como trabalhar com as colunas e linhas no objeto <xref:System.Data.DataTable> retornado.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBMethods5](SMO How to#SMO_VBMethods5)]  -->  
  
## <a name="monitoring-server-processes-in-visual-c"></a>Monitorando processos de servidor no Visual C#  
 Você pode obter as informações de tipo de status atuais sobre a instância de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] por meio de métodos de enumeração. O exemplo de código usa o método <xref:Microsoft.SqlServer.Management.Smo.Server.EnumProcesses%2A> para descobrir informações sobre os processos atuais. Ele também demonstra como trabalhar com as colunas e linhas no objeto <xref:System.Data.DataTable> retornado.  
  
```  
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
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.SqlServer.Management.Smo.Server>   
 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>  
  
  