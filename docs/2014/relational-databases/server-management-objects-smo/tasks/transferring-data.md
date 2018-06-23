---
title: Transferência de dados | Microsoft Docs
ms.custom: ''
ms.date: 10/20/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- data transfers [SMO]
- transferring data
ms.assetid: eea255c3-8251-40f0-973b-fe4ef6cb5261
caps.latest.revision: 49
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: dc0b4f2e79564bbdc6ceaabb088cdb070636a3d5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36019794"
---
# <a name="transferring-data"></a>Transferindo dados
  A classe <xref:Microsoft.SqlServer.Management.Smo.Transfer> é uma classe de utilitário que fornece ferramentas para transferir objetos e dados.  
  
 Os objetos de um esquema de banco de dados são transferidos pela execução de um script gerado no servidor de destino. Os dados do <xref:Microsoft.SqlServer.Management.Smo.Table> são transferidos com um pacote DTS criado dinamicamente.  
  
 O objeto <xref:Microsoft.SqlServer.Management.Smo.Transfer> contém toda a funcionalidade dos objetos <xref:Microsoft.SqlServer.Management.Smo.Transfer> em DMO e a funcionalidade adicional do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. No entanto, no SMO no [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], o <xref:Microsoft.SqlServer.Management.Smo.Transfer> objeto usa o [SQLBulkCopy](http://msdn.microsoft.com/library/system.data.sqlclient.sqlbulkcopy\(v=VS.90\).aspx) API para transferir dados. Além disso, os métodos e propriedades usados para executar transferências de dados residem no objeto <xref:Microsoft.SqlServer.Management.Smo.Transfer> em vez de no objeto <xref:Microsoft.SqlServer.Management.Smo.Database>. A movimentação da funcionalidade de classes da instância para classes de utilitário é consistente com um modelo de objeto mais leve, pois o código para tarefas específicas só é carregado quando necessário.  
  
 O objeto <xref:Microsoft.SqlServer.Management.Smo.Transfer> não dá suporte a transferências de dados para um banco de dados de destino que tenha um <xref:Microsoft.SqlServer.Management.Smo.Database.CompatibilityLevel%2A> inferior à versão da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="example"></a>Exemplo  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
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
  
```  
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
  
```  
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
  
  