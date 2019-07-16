---
title: Criando, alterando e removendo exibições | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- views [SMO]
ms.assetid: 7d445c0e-77ef-4734-993b-e022de31df23
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1f19027d4707220306accfe451314f52a22cfe35
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68211888"
---
# <a name="creating-altering-and-removing-views"></a>Criando, alterando e removendo exibições
  No [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects (SMO), as exibições do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] são representadas pelo objeto <xref:Microsoft.SqlServer.Management.Smo.View>.  
  
 A propriedade <xref:Microsoft.SqlServer.Management.Smo.View.TextBody%2A> do objeto <xref:Microsoft.SqlServer.Management.Smo.View> define a exibição. É equivalente à instrução SELECT do [!INCLUDE[tsql](../../../includes/tsql-md.md)] para criar uma exibição.  
  
## <a name="example"></a>Exemplo  
 Para usar qualquer exemplo de código fornecido, será necessário escolher o ambiente de programação, o modelo de programação e a linguagem de programação para criar o aplicativo. Para obter mais informações, consulte [criar um projeto do Visual Basic SMO no Visual Studio .NET](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) ou [criar um Visual C&#35; projeto de SMO no Visual Studio .NET](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-altering-and-removing-a-view-in-visual-basic"></a>Criando, alterando e removendo uma exibição no Visual Basic  
 Este exemplo de código mostra como criar uma exibição de duas tabelas usando uma junção interna. A exibição é criada usando o modo de texto; então, a propriedade <xref:Microsoft.SqlServer.Management.Smo.View.TextHeader%2A> deve ser definida.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBViews1](SMO How to#SMO_VBViews1)]  -->  
  
## <a name="creating-altering-and-removing-a-view-in-visual-c"></a>Criando, alterando e removendo uma exibição no Visual C#  
 Este exemplo de código mostra como criar uma exibição de duas tabelas usando uma junção interna. A exibição é criada usando o modo de texto; então, a propriedade <xref:Microsoft.SqlServer.Management.Smo.View.TextHeader%2A> deve ser definida.  
  
```  
{  
        //Connect to the local, default instance of SQL Server.   
        Server srv;   
        srv = new Server();   
        //Reference the AdventureWorks2012 database.   
        Database db;   
        db = srv.Databases["AdventureWorks2012"];   
        //Define a View object variable by supplying the parent database, view name and schema in the constructor.   
        View myview;   
        myview = new View(db, "Test_View", "Sales");   
        //Set the TextHeader and TextBody property to define the view.   
        myview.TextHeader = "CREATE VIEW [Sales].[Test_View] AS";   
        myview.TextBody = "SELECT h.SalesOrderID, d.OrderQty FROM Sales.SalesOrderHeader AS h INNER JOIN Sales.SalesOrderDetail AS d ON h.SalesOrderID = d.SalesOrderID";   
        //Create the view on the instance of SQL Server.   
        myview.Create();   
        //Remove the view.   
        myview.Drop();   
        }  
```  
  
## <a name="creating-altering-and-removing-a-view-in-powershell"></a>Criando, alterando e removendo uma exibição no PowerShell  
 Este exemplo de código mostra como criar uma exibição de duas tabelas usando uma junção interna. A exibição é criada usando o modo de texto; então, a propriedade <xref:Microsoft.SqlServer.Management.Smo.View.TextHeader%2A> deve ser definida.  
  
```  
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = get-item Adventureworks2012  
  
# Define a View object variable by supplying the parent database, view name and schema in the constructor.   
$myview  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.View `  
-argumentlist $db, "Test_View", "Sales"  
  
# Set the TextHeader and TextBody property to define the view.   
$myview.TextHeader = "CREATE VIEW [Sales].[Test_View] AS"  
$myview.TextBody ="SELECT h.SalesOrderID, d.OrderQty FROM Sales.SalesOrderHeader AS h INNER JOIN Sales.SalesOrderDetail AS d ON h.SalesOrderID = d.SalesOrderID"  
  
# Create the view on the instance of SQL Server.   
$myview.Create()  
  
# Remove the view.   
$myview.Drop();  
```  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.SqlServer.Management.Smo.View>  
  
  
