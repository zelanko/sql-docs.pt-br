---
description: Transferindo dados
title: Transferindo dados | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- data transfers [SMO]
- transferring data
ms.assetid: eea255c3-8251-40f0-973b-fe4ef6cb5261
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: de139744d0c14668d0d7e67ada36be1142721762
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91869236"
---
# <a name="transferring-data"></a>Transferindo dados
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  A classe <xref:Microsoft.SqlServer.Management.Smo.Transfer> é uma classe de utilitário que fornece ferramentas para transferir objetos e dados.  
  
 Os objetos de um esquema de banco de dados são transferidos pela execução de um script gerado no servidor de destino. Os dados do <xref:Microsoft.SqlServer.Management.Smo.Table> são transferidos com um pacote DTS criado dinamicamente.  
  
 O <xref:Microsoft.SqlServer.Management.Smo.Transfer> objeto usa a API [SQLBulkCopy](/dotnet/api/system.data.sqlclient.sqlbulkcopy) para transferir dados. Além disso, os métodos e propriedades usados para executar transferências de dados residem no objeto <xref:Microsoft.SqlServer.Management.Smo.Transfer> em vez de no objeto <xref:Microsoft.SqlServer.Management.Smo.Database>. A movimentação da funcionalidade de classes da instância para classes de utilitário é consistente com um modelo de objeto mais leve, pois o código para tarefas específicas só é carregado quando necessário.  
  
 O objeto <xref:Microsoft.SqlServer.Management.Smo.Transfer> não dá suporte a transferências de dados para um banco de dados de destino que tenha um <xref:Microsoft.SqlServer.Management.Smo.Database.CompatibilityLevel%2A> inferior à versão da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="example"></a>Exemplo  
Para usar qualquer exemplo de código fornecido, será necessário escolher o ambiente de programação, o modelo de programação e a linguagem de programação para criar o aplicativo. Para obter mais informações, consulte [criar um projeto do Visual C&#35; Smo no Visual Studio .net](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
 
  
## <a name="transferring-schema-and-data-from-one-database-to-another-in-visual-basic"></a>Transferindo esquema e dados de um banco de dados para outro no Visual Basic  
 Este exemplo de código mostra como transferir esquema e dados de um banco de dados para outro usando o objeto <xref:Microsoft.SqlServer.Management.Smo.Transfer>.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Reference the AdventureWorks2012 2008R2 database
Dim db As Database
db = srv.Databases("AdventureWorks2012")
'Create a new database that is to be destination database.
Dim dbCopy As Database
dbCopy = New Database(srv, "AdventureWorks2012Copy")
dbCopy.Create()
'Define a Transfer object and set the required options and properties.
Dim xfr As Transfer
xfr = New Transfer(db)
xfr.CopyAllTables = True
xfr.Options.WithDependencies = True
xfr.Options.ContinueScriptingOnError = True
xfr.DestinationDatabase = "AdventureWorks2012Copy"
xfr.DestinationServer = srv.Name
xfr.DestinationLoginSecure = True
xfr.CopySchema = True
'Script the transfer. Alternatively perform immediate data transfer with TransferData method.
xfr.ScriptTransfer()
```
  
## <a name="transferring-schema-and-data-from-one-database-to-another-in-visual-c"></a>Transferindo esquema e dados de um banco de dados para outro no Visual C#  
 Este exemplo de código mostra como transferir esquema e dados de um banco de dados para outro usando o objeto <xref:Microsoft.SqlServer.Management.Smo.Transfer>.  
  
```csharp  
{  
            Server srv;  
            srv = new Server();  
            //Reference the AdventureWorks2012 database   
            Database db;  
            db = srv.Databases["AdventureWorks2012"];  
            //Create a new database that is to be destination database.   
            Database dbCopy;  
            dbCopy = new Database(srv, "AdventureWorks2012Copy");  
            dbCopy.Create();  
            //Define a Transfer object and set the required options and properties.   
            Transfer xfr;  
            xfr = new Transfer(db);  
            xfr.CopyAllTables = true;  
            xfr.Options.WithDependencies = true;  
            xfr.Options.ContinueScriptingOnError = true;  
            xfr.DestinationDatabase = "AdventureWorks2012Copy";  
            xfr.DestinationServer = srv.Name;  
            xfr.DestinationLoginSecure = true;  
            xfr.CopySchema = true;  
            //Script the transfer. Alternatively perform immediate data transfer   
            // with TransferData method.   
            xfr.ScriptTransfer();  
        }   
```  
  
## <a name="transferring-schema-and-data-from-one-database-to-another-in-powershell"></a>Transferindo esquema e dados de um banco de dados para outro no PowerShell  
 Este exemplo de código mostra como transferir esquema e dados de um banco de dados para outro usando o objeto <xref:Microsoft.SqlServer.Management.Smo.Transfer>.  
  
```powershell  
#Connect to the local, default instance of SQL Server.  
  
#Get a server object which corresponds to the default instance  
$srv = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#Reference the AdventureWorks2012 database.  
$db = $srv.Databases["AdventureWorks2012"]  
  
#Create a database to hold the copy of AdventureWorks  
$dbCopy = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Database -argumentlist $srv, "AdventureWorksCopy"  
$dbCopy.Create()  
  
#Define a Transfer object and set the required options and properties.  
$xfr = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Transfer -argumentlist $db  
  
#Set this objects properties  
$xfr.CopyAllTables = $true  
$xfr.Options.WithDependencies = $true  
$xfr.Options.ContinueScriptingOnError = $true  
$xfr.DestinationDatabase = "AdventureWorksCopy"  
$xfr.DestinationServer = $srv.Name  
$xfr.DestinationLoginSecure = $true  
$xfr.CopySchema = $true  
"Scripting Data Transfer"  
#Script the transfer. Alternatively perform immediate data transfer with TransferData method.  
$xfr.ScriptTransfer()  
```  
  
