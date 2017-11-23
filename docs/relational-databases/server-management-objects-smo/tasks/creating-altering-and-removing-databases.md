---
title: Criando, alterando e removendo bancos de dados | Microsoft Docs
ms.custom: 
ms.date: 08/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- databases [SMO]
- databases [SMO], creating
- databases [SMO], modifying
- databases [SMO], deleting
ms.assetid: fcfb3ec2-7556-4f72-971a-501295892cb0
caps.latest.revision: "41"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: e195aeb11109743b5ff17748e16b17ba3790694e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="creating-altering-and-removing-databases"></a>Criando, alterando e removendo bancos de dados
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]No SMO, um banco de dados é representado pelo <xref:Microsoft.SqlServer.Management.Smo.Database> objeto.  
  
 Não é necessário criar um objeto <xref:Microsoft.SqlServer.Management.Smo.Database> para modificá-lo ou removê-lo. O banco de dados pode ser referenciado usando uma coleção.  
  
## <a name="example"></a>Exemplo  
 Para usar qualquer exemplo de código fornecido, será necessário escolher o ambiente de programação, o modelo de programação e a linguagem de programação para criar o aplicativo. Para obter mais informações, consulte [criar um Visual C &#35; Projeto SMO no Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-altering-and-removing-a-database-in-visual-basic"></a>Criando, alterando e removendo um banco de dados no Visual Basic  
 Este exemplo de código cria um novo banco de dados. Arquivos e grupos de arquivos são criados automaticamente para o banco de dados.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Define a Database object variable by supplying the server and the database name arguments in the constructor.
Dim db As Database
db = New Database(srv, "Test_SMO_Database")
'Create the database on the instance of SQL Server.
db.Create()
'Reference the database and display the date when it was created.
db = srv.Databases("Test_SMO_Database")
Console.WriteLine(db.CreateDate)
'Remove the database.
db.Drop()
```
  
## <a name="creating-altering-and-removing-a-database-in-visual-c"></a>Criando, alterando e removendo um banco de dados no Visual C#  
 Este exemplo de código cria um novo banco de dados. Arquivos e grupos de arquivos são criados automaticamente para o banco de dados.  
  
```csharp  
{  
                //Connect to the local, default instance of SQL Server.   
                Server srv;  
                srv = new Server();  
                //Define a Database object variable by supplying the server and the database name arguments in the constructor.   
                Database db;  
                db = new Database(srv, "Test_SMO_Database");  
                //Create the database on the instance of SQL Server.   
                db.Create();  
                //Reference the database and display the date when it was created.   
                db = srv.Databases["Test_SMO_Database"];  
                Console.WriteLine(db.CreateDate);  
                //Remove the database.   
                db.Drop();  
            }  
```  
  
## <a name="creating-altering-and-removing-a-database-in-powershell"></a>Criando, alterando e removendo um banco de dados no PowerShell  
 Este exemplo de código cria um novo banco de dados. Arquivos e grupos de arquivos são criados automaticamente para o banco de dados.  
  
```powershell  
#Get a server object which corresponds to the default instance  
cd \sql\localhost\  
$srv = get-item default  
  
#Create a new database  
$db = New-Object -TypeName Microsoft.SqlServer.Management.Smo.Database -argumentlist $srv, "Test_SMO_Database"  
$db.Create()  
  
#Reference the database and display the date when it was created.   
$db = $srv.Databases["Test_SMO_Database"]  
$db.CreateDate  
  
#Drop the database  
$db.Drop()  
```  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.SqlServer.Management.Smo.Database>  
  
  
