---
title: Criando, alterando e removendo padrões | Microsoft Docs
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
- defaults [SMO]
ms.assetid: c30ac3b9-8150-4264-ba4c-c549f44261ab
caps.latest.revision: 43
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: d7daddec0a7c96776938f2824635b719341ecbe4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36008385"
---
# <a name="creating-altering-and-removing-defaults"></a>Criando, alterando e removendo padrões
  No [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects (SMO), a restrição padrão é representada pelo objeto <xref:Microsoft.SqlServer.Management.Smo.Default>.  
  
 A propriedade <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A> do objeto <xref:Microsoft.SqlServer.Management.Smo.Default> é usada para definir o valor a ser inserido. Ela pode ser uma constante ou uma instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)] que retorna um valor constante, como GETDATE(). A propriedade <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A> não pode ser modificada usando o método <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A>. Em vez disso, o objeto <xref:Microsoft.SqlServer.Management.Smo.Default> deve ser descartado e recriado.  
  
## <a name="example"></a>Exemplo  
 Para usar qualquer exemplo de código fornecido, será necessário escolher o ambiente de programação, o modelo de programação e a linguagem de programação para criar o aplicativo. Para obter mais informações, consulte [criar um projeto Visual Basic SMO no Visual Studio .NET](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) ou [criar um Visual C&#35; projeto SMO no Visual Studio .NET](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-altering-and-removing-a-default-in-visual-basic"></a>Criando, alterando e removendo um padrão no Visual Basic  
 Este exemplo de código mostra como criar um padrão que seja texto simples e outro padrão que seja uma instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)]. O padrão deve ser anexado à coluna através do método <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.BindToColumn%2A> e desanexado através do método <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.UnbindFromColumn%2A>.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBDefaults1](SMO How to#SMO_VBDefaults1)]  -->  
  
## <a name="creating-altering-and-removing-a-default-in-visual-c"></a>Criando, alterando e removendo um padrão no Visual C#  
 Este exemplo de código mostra como criar um padrão que seja texto simples e outro padrão que seja uma instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)]. O padrão deve ser anexado à coluna através do método <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.BindToColumn%2A> e desanexado através do método <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.UnbindFromColumn%2A>.  
  
```  
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
  
```  
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
  
  