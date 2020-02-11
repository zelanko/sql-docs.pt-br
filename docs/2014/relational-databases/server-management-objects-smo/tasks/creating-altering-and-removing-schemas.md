---
title: Criando, alterando e removendo esquemas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- schemas [SMO]
ms.assetid: 3e3619de-c6a2-4280-b2be-4ec9924608fb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 073cdba829845c940c67d60a92b0346d4ed7541d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "72782261"
---
# <a name="creating-altering-and-removing-schemas"></a>Criando, alterando e removendo esquemas
  O objeto <xref:Microsoft.SqlServer.Management.Smo.Schema> representa um contexto de propriedade do objeto de banco de dados. A propriedade <xref:Microsoft.SqlServer.Management.Smo.Database.Schemas%2A> do objeto <xref:Microsoft.SqlServer.Management.Smo.Database> representa uma coleção de objetos do <xref:Microsoft.SqlServer.Management.Smo.Schema>.  
  
## <a name="example"></a>Exemplo  
 Para usar qualquer exemplo de código fornecido, será necessário escolher o ambiente de programação, o modelo de programação e a linguagem de programação para criar o aplicativo. Para obter mais informações, consulte [criar um projeto Visual Basic Smo no Visual Studio .net](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) ou [criar um projeto do Visual C&#35; Smo no Visual Studio .net](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-altering-and-removing-a-schema-in-visual-basic"></a>Criando, alterando e removendo um esquema no Visual Basic  
 Este exemplo de código demonstra como criar um esquema e atribuí-lo a um objeto de banco de dados. Então, o programa concede permissão a um usuário e cria uma tabela nova no esquema.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBSchemas1](SMO How to#SMO_VBSchemas1)]  -->  
  
## <a name="creating-altering-and-removing-a-schema-in-visual-c"></a>Criando, alterando e removendo um esquema no Visual C#  
 Este exemplo de código demonstra como criar um esquema e atribuí-lo a um objeto de banco de dados. Então, o programa concede permissão a um usuário e cria uma tabela nova no esquema.  
  
```csharp
{  
         //Connect to the local, default instance of SQL Server.   
         Server srv = new Server();   
        //Reference the AdventureWorks2012 database.   
        Database db = srv.Databases["AdventureWorks2012"];   
        //Define a Schema object variable by supplying the parent database and name arguments in the constructor.   
        Schema sch = new Schema(db, "MySchema1");   
        sch.Owner = "dbo";   
  
        //Create the schema on the instance of SQL Server.   
        sch.Create();   
  
        //Define an ObjectPermissionSet that contains the Update and Select object permissions.   
        ObjectPermissionSet obperset = new ObjectPermissionSet();   
        obperset.Add(ObjectPermission.Select);   
        obperset.Add(ObjectPermission.Update);   
  
        //Grant the set of permissions on the schema to the guest account.   
        sch.Grant(obperset, "guest");   
  
        //Define a Table object variable by supplying the parent database, name and schema arguments in the constructor.   
        Table tb = new Table(db, "MyTable", "MySchema1");   
       Column mycol = new Column(tb, "Date", DataType.DateTime);   
        tb.Columns.Add(mycol);   
        tb.Create();   
  
        //Modify the owner of the schema and run the Alter method to make the change on the instance of SQL Server.   
        sch.Owner = "guest";   
        sch.Alter();   
  
        //Run the Drop method for the table and the schema to remove them.   
        tb.Drop();   
        sch.Drop();   
}  
```  
  
## <a name="creating-altering-and-removing-a-schema-in-powershell"></a>Criando, alterando e removendo um esquema no PowerShell  
 Este exemplo de código demonstra como criar um esquema e atribuí-lo a um objeto de banco de dados. Então, o programa concede permissão a um usuário e cria uma tabela nova no esquema.  
  
```powershell
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = Get-Item Adventureworks2012  
  
# Define a schema object variable by supplying the parent database and name arguments in the constructor.
$sch  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Schema -argumentlist $db, "MySchema1"  
  
# Set schema owner  
$sch.Owner = "dbo"
  
# Create the schema on the instance of SQL Server.
$sch.Create()  
  
# Define an ObjectPermissionSet that contains the Update and Select object permissions.
$obperset  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.ObjectPermissionSet  
$obperset.Add([Microsoft.SqlServer.Management.SMO.ObjectPermission]::Select)  
$obperset.Add([Microsoft.SqlServer.Management.SMO.ObjectPermission]::Update)  
  
# Grant the set of permissions on the schema to the guest account.
$sch.Grant($obperset, "guest")  
  
#Create a SMO Table with one column and add it to the database  
$tb = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Table -argumentlist $db, "MyTable", "MySchema1"  
$Type = [Microsoft.SqlServer.Management.SMO.DataType]::DateTime  
$mycol =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.Column -argumentlist $tb,"Date", $Type  
$tb.Columns.Add($mycol)  
$tb.Create()
  
# Modify the owner of the schema and run the Alter method to make the change on the instance of SQL Server.
$sch.Owner = "guest"  
$sch.Alter()  
  
# Run the Drop method for the table and the schema to remove them.
$tb.Drop()  
$sch.Drop()  
```
