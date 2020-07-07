---
title: Usando coleções | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, collections
- SMO [SQL Server], collections
- collections [SMO]
ms.assetid: 209eb175-2514-4de1-bc32-b2e6a469d945
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4468e9819504efef135fd0dce689d4e6e126a366
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86008651"
---
# <a name="using-collections"></a>Usando coleções
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  Uma coleção é uma lista de objetos que foram construídos na mesma classe de objeto e que compartilham o mesmo objeto pai. O objeto de coleção sempre contém o nome do tipo de objeto com o sufixo Collection. Por exemplo, para acessar as colunas em uma tabela especificada, use o tipo de objeto <xref:Microsoft.SqlServer.Management.Smo.ColumnCollection>. Ele contém todos os objetos <xref:Microsoft.SqlServer.Management.Smo.Column> que pertencem ao mesmo objeto <xref:Microsoft.SqlServer.Management.Smo.Table>.  
  
 A instrução [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] **For...Each** ou a instrução [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[csprcs](../../../includes/csprcs-md.md)] **foreach** pode ser usada para iterar através de cada membro da coleção.  
  
## <a name="examples"></a>Exemplos  
Para usar qualquer exemplo de código fornecido, será necessário escolher o ambiente de programação, o modelo de programação e a linguagem de programação para criar o aplicativo. Para obter mais informações, consulte [criar um projeto do Visual C&#35; Smo no Visual Studio .net](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="referencing-an-object-by-using-a-collection-in-visual-basic"></a>Referenciando um objeto usando uma coleção no Visual Basic  
 Este exemplo de código mostra como definir uma propriedade de coluna usando as propriedades <xref:Microsoft.SqlServer.Management.Smo.TableViewTableTypeBase.Columns%2A>, <xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A> e <xref:Microsoft.SqlServer.Management.Smo.Server.Databases%2A>. Essas propriedades representam coleções, que podem ser usadas para identificar um determinado objeto quando usadas com um parâmetro que especifica o nome do objeto. São obrigatórios o nome e o esquema da propriedade do objeto de coleção <xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A>.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Modify a property using the Databases, Tables, and Columns collections to reference a column.
srv.Databases("AdventureWorks2012").Tables("Person", "Person").Columns("ModifiedDate").Nullable = True
'Call the Alter method to make the change on the instance of SQL Server.
srv.Databases("AdventureWorks2012").Tables("Person", "Person").Columns("ModifiedDate").Alter()
```
  
## <a name="referencing-an-object-by-using-a-collection-in-visual-c"></a>Referenciando um objeto usando uma coleção no Visual C#  
 Este exemplo de código mostra como definir uma propriedade de coluna usando as propriedades <xref:Microsoft.SqlServer.Management.Smo.TableViewTableTypeBase.Columns%2A>, <xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A> e <xref:Microsoft.SqlServer.Management.Smo.Server.Databases%2A>. Essas propriedades representam coleções, que podem ser usadas para identificar um determinado objeto quando usadas com um parâmetro que especifica o nome do objeto. São obrigatórios o nome e o esquema da propriedade do objeto de coleção <xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A>.  
  
```csharp  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Modify a property using the Databases, Tables, and Columns collections to reference a column.   
srv.Databases("AdventureWorks2012").Tables("Person", "Person").Columns("LastName").Nullable = true;   
//Call the Alter method to make the change on the instance of SQL Server.   
srv.Databases("AdventureWorks2012").Tables("Person", "Person").Columns("LastName").Alter();   
}  
```  
  
## <a name="iterating-through-the-members-of-a-collection-in-visual-basic"></a>Iterando através dos membros de uma coleção no Visual Basic  
 Este exemplo de código itera através da propriedade de coleção <xref:Microsoft.AnalysisServices.Server.Databases%2A> e exibe todas as conexões do banco de dados com a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
Dim count As Integer
Dim total As Integer
'Iterate through the databases and call the GetActiveDBConnectionCount method.
Dim db As Database
For Each db In srv.Databases
    count = srv.GetActiveDBConnectionCount(db.Name)
    total = total + count
    'Display the number of connections for each database.
    Console.WriteLine(count & " connections on " & db.Name)
Next
'Display the total number of connections on the instance of SQL Server.
Console.WriteLine("Total connections =" & total)
```
  
## <a name="iterating-through-the-members-of-a-collection-in-visual-c"></a>Iterando através dos membros de uma coleção no Visual C#  
 Este exemplo de código itera através da propriedade de coleção <xref:Microsoft.AnalysisServices.Server.Databases%2A> e exibe todas as conexões do banco de dados com a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
```csharp  
//Connect to the local, default instance of SQL Server.   
{   
Server srv = default(Server);   
srv = new Server();   
int count = 0;   
int total = 0;   
//Iterate through the databases and call the GetActiveDBConnectionCount method.   
Database db = default(Database);   
foreach ( db in srv.Databases) {   
  count = srv.GetActiveDBConnectionCount(db.Name);   
  total = total + count;   
  //Display the number of connections for each database.   
  Console.WriteLine(count + " connections on " + db.Name);   
}   
//Display the total number of connections on the instance of SQL Server.   
Console.WriteLine("Total connections =" + total);   
}   
```  
  
  
