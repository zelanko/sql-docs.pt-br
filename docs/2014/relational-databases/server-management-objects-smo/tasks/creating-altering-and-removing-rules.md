---
title: Criando, alterando e removendo regras | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- rules [SMO]
ms.assetid: 16981459-524e-4b39-a899-4370eaf763cc
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d201b20e0bdfd213c62c060250b5674589ab91cb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62519320"
---
# <a name="creating-altering-and-removing-rules"></a>Criando, alterando e removendo regras
  No SMO, as regras são representadas pelo objeto <xref:Microsoft.SqlServer.Management.Smo.Rule>. A regra é definida pela propriedade <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A> que é uma cadeia de caracteres de texto que contém uma expressão de condição que usa operadores ou predicados, como IN, LIKE ou BETWEEN. Uma regra não pode fazer referência a colunas ou a outros objetos de banco de dados. É possível incluir funções internas que não fazem referência a objetos de banco de dados.  
  
 A definição na propriedade <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A> deve conter uma variável relativa ao valor de dados digitados. Qualquer nome ou símbolo pode ser usado para representar o valor ao criar a regra, mas o primeiro caractere deve ser o \@ símbolo.  
  
## <a name="example"></a>Exemplo  
 Para usar qualquer exemplo de código fornecido, será necessário escolher o ambiente de programação, o modelo de programação e a linguagem de programação para criar o aplicativo. Para obter mais informações, consulte [criar um projeto do Visual Basic SMO no Visual Studio .NET](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) ou [criar um Visual C&#35; projeto de SMO no Visual Studio .NET](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-altering-and-removing-a-rule-in-visual-basic"></a>Criando, alterando e removendo uma regra no Visual Basic  
 Este exemplo de código mostra como criar uma regra, anexá-la a uma coluna, modificar propriedades do objeto <xref:Microsoft.SqlServer.Management.Smo.Rule>, desanexá-la da coluna e, em seguida, descartá-la.  
  
 A instrução `Dim` do objeto <xref:Microsoft.SqlServer.Management.Smo.Rule> é especificada com o caminho completo do assembly para evitar ambiguidades com um objeto <xref:Microsoft.SqlServer.Management.Smo.Rule> no assembly System.Data.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBRules1](SMO How to#SMO_VBRules1)]  -->  
  
## <a name="creating-altering-and-removing-a-rule-in-visual-c"></a>Criando, alterando e removendo uma regra no Visual C#  
 Este exemplo de código mostra como criar uma regra, anexá-la a uma coluna, modificar propriedades do objeto <xref:Microsoft.SqlServer.Management.Smo.Rule>, desanexá-la da coluna e, em seguida, descartá-la.  
  
 A instrução `Dim` do objeto <xref:Microsoft.SqlServer.Management.Smo.Rule> é especificada com o caminho completo do assembly para evitar ambiguidades com um objeto <xref:Microsoft.SqlServer.Management.Smo.Rule> no assembly System.Data.  
  
```  
{  
            //Connect to the local, default instance of SQL Server.   
            Server srv;  
            srv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database db;  
            db = srv.Databases["AdventureWorks2012"];  
  
            //Define a Rule object variable by supplying the parent database, name and schema in the constructor.   
            //Note that the full namespace must be given for the Rule type to differentiate it from other Rule types.   
            Microsoft.SqlServer.Management.Smo.Rule ru;  
            ru = new Rule(db, "TestRule", "Production");  
            //Set the TextHeader and TextBody properties to define the rule.   
            ru.TextHeader = "CREATE RULE [Production].[TestRule] AS";  
            ru.TextBody = "@value BETWEEN GETDATE() AND DATEADD(year,4,GETDATE())";  
            //Create the rule on the instance of SQL Server.   
            ru.Create();  
            //Bind the rule to a column in the Product table by supplying the table, schema, and   
            //column as arguments in the BindToColumn method.   
            ru.BindToColumn("Product", "SellEndDate", "Production");  
            //Unbind from the column before removing the rule from the database.   
            ru.UnbindFromColumn("Product", "SellEndDate", "Production");  
            ru.Drop();  
  
        }  
```  
  
## <a name="creating-altering-and-removing-a-rule-in-powershell"></a>Criando, alterando e removendo uma regra no PowerShell  
 Este exemplo de código mostra como criar uma regra, anexá-la a uma coluna, modificar propriedades do objeto <xref:Microsoft.SqlServer.Management.Smo.Rule>, desanexá-la da coluna e, em seguida, descartá-la.  
  
 A instrução `Dim` do objeto <xref:Microsoft.SqlServer.Management.Smo.Rule> é especificada com o caminho completo do assembly para evitar ambiguidades com um objeto <xref:Microsoft.SqlServer.Management.Smo.Rule> no assembly System.Data.  
  
```  
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = get-item Adventureworks2012  
  
# Define a Rule object variable by supplying the parent database, name and schema in the constructor.   
$ru = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Rule `  
-argumentlist $db, "TestRule", "Production"  
  
#Set the TextHeader and TextBody properties to define the rule.   
$ru.TextHeader = "CREATE RULE [Production].[TestRule] AS"  
$ru.TextBody = "@value BETWEEN GETDATE() AND DATEADD(year,4,GETDATE())"  
  
#Create the rule on the instance of SQL Server.   
$ru.Create()  
  
# Bind the rule to a column in the Product table by supplying the table, schema, and   
# column as arguments in the BindToColumn method.   
$ru.BindToColumn("Product", "SellEndDate", "Production")  
  
#Unbind from the column before removing the rule from the database.   
$ru.UnbindFromColumn("Product", "SellEndDate", "Production")  
$ru.Drop()  
```  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.SqlServer.Management.Smo.Rule>  
  
  
