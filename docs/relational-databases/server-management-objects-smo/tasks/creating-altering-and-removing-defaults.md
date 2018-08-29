---
title: Criando, alterando e removendo padrões | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: smo
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- defaults [SMO]
ms.assetid: c30ac3b9-8150-4264-ba4c-c549f44261ab
caps.latest.revision: 46
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 53b64a652f02ed9a0c55de035cacb0ecddc2c23b
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43085779"
---
# <a name="creating-altering-and-removing-defaults"></a>Criando, alterando e removendo padrões
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  No [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects (SMO), a restrição padrão é representada pelo objeto <xref:Microsoft.SqlServer.Management.Smo.Default>.  
  
 A propriedade <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A> do objeto <xref:Microsoft.SqlServer.Management.Smo.Default> é usada para definir o valor a ser inserido. Ela pode ser uma constante ou uma instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)] que retorna um valor constante, como GETDATE(). A propriedade <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A> não pode ser modificada usando o método <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A>. Em vez disso, o objeto <xref:Microsoft.SqlServer.Management.Smo.Default> deve ser descartado e recriado.  
  
## <a name="example"></a>Exemplo  
 Para usar qualquer exemplo de código fornecido, será necessário escolher o ambiente de programação, o modelo de programação e a linguagem de programação para criar o aplicativo. Para obter mais informações, consulte [criar um Visual C&#35; projeto do SMO no Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-altering-and-removing-a-default-in-visual-basic"></a>Criando, alterando e removendo um padrão no Visual Basic  
 Este exemplo de código mostra como criar um padrão que seja texto simples e outro padrão que seja uma instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)]. O padrão deve ser anexado à coluna através do método <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.BindToColumn%2A> e desanexado através do método <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.UnbindFromColumn%2A>.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Reference the AdventureWorks2012 database.
Dim db As Database
db = srv.Databases("AdventureWorks2012")
'Define a Default object variable by supplying the parent database and the default name 
'in the constructor.
Dim def As [Default]
def = New [Default](db, "Test_Default2")
'Set the TextHeader and TextBody properties that define the default.
def.TextHeader = "CREATE DEFAULT [Test_Default2] AS"
def.TextBody = "GetDate()"
'Create the default on the instance of SQL Server.
def.Create()
'Declare a Column object variable and reference a column in the AdventureWorks2012 database.
Dim col As Column
col = db.Tables("SpecialOffer", "Sales").Columns("StartDate")
'Bind the default to the column.
def.BindToColumn("SpecialOffer", "StartDate", "Sales")
'Unbind the default from the column and remove it from the database.
def.UnbindFromColumn("SpecialOffer", "StartDate", "Sales")
def.Drop()
```
  
## <a name="creating-altering-and-removing-a-default-in-visual-c"></a>Criando, alterando e removendo um padrão no Visual C#  
 Este exemplo de código mostra como criar um padrão que seja texto simples e outro padrão que seja uma instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)]. O padrão deve ser anexado à coluna através do método <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.BindToColumn%2A> e desanexado através do método <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.UnbindFromColumn%2A>.  
  
```csharp  
{  
  
          Server srv = new Server();  
  
            //Reference the AdventureWorks2012 database.   
            Database  db = srv.Databases["AdventureWorks2012"];  
  
            //Define a Default object variable by supplying the parent database and the default name   
            //in the constructor.   
            Default def = new Default(db, "Test_Default2");  
  
            //Set the TextHeader and TextBody properties that define the default.   
            def.TextHeader = "CREATE DEFAULT [Test_Default2] AS";  
            def.TextBody = "GetDate()";  
  
            //Create the default on the instance of SQL Server.   
            def.Create();  
  
            //Bind the default to a column in a table in AdventureWorks2012  
            def.BindToColumn("SpecialOffer", "StartDate", "Sales");  
  
            //Unbind the default from the column and remove it from the database.   
            def.UnbindFromColumn("SpecialOffer", "StartDate", "Sales");  
            def.Drop();  
        }  
```  
  
## <a name="creating-altering-and-removing-a-default-in-powershell"></a>Criando, alterando e removendo um padrão no PowerShell  
 Este exemplo de código mostra como criar um padrão que seja texto simples e outro padrão que seja uma instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)]. O padrão deve ser anexado à coluna através do método <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.BindToColumn%2A> e desanexado através do método <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.UnbindFromColumn%2A>.  
  
```powershell   
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = get-item Adventureworks2012  
  
#Define a Default object variable by supplying the parent database and the default name in the constructor.  
$def = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Default `  
-argumentlist $db, "Test_Default2"  
  
#Set the TextHeader and TextBody properties that define the default.   
$def.TextHeader = "CREATE DEFAULT [Test_Default2] AS"  
$def.TextBody = "GetDate()"  
  
#Create the default on the instance of SQL Server.   
$def.Create()  
  
#Bind the default to the column.   
$def.BindToColumn("SpecialOffer", "StartDate", "Sales")  
  
#Unbind the default from the column and remove it from the database.   
$def.UnbindFromColumn("SpecialOffer", "StartDate", "Sales")  
$def.Drop()  
```  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.SqlServer.Management.Smo.Default>  
  
  
