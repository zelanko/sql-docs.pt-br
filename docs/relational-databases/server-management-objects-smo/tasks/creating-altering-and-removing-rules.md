---
title: Criando, alterando e removendo regras
ms.custom: seo-dt-2019
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- rules [SMO]
ms.assetid: 16981459-524e-4b39-a899-4370eaf763cc
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b2f918e611a4bc88c1a77ad7d539a9101f3f8dac
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/14/2019
ms.locfileid: "74095524"
---
# <a name="creating-altering-and-removing-rules"></a>Criando, alterando e removendo regras
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  No SMO, as regras são representadas pelo objeto <xref:Microsoft.SqlServer.Management.Smo.Rule>. A regra é definida pela propriedade <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A> que é uma cadeia de caracteres de texto que contém uma expressão de condição que usa operadores ou predicados, como IN, LIKE ou BETWEEN. Uma regra não pode fazer referência a colunas ou a outros objetos de banco de dados. É possível incluir funções internas que não fazem referência a objetos de banco de dados.  
  
 A definição na propriedade <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A> deve conter uma variável relativa ao valor de dados digitados. Qualquer nome ou símbolo pode ser usado para representar o valor ao criar a regra, mas o primeiro caractere deve ser o \@ símbolo.  
  
## <a name="example"></a>Exemplo  
 Para usar qualquer exemplo de código fornecido, será necessário escolher o ambiente de programação, o modelo de programação e a linguagem de programação para criar o aplicativo. Para obter mais informações, consulte [criar um projeto&#35; do Visual C Smo no Visual Studio .net](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-altering-and-removing-a-rule-in-visual-basic"></a>Criando, alterando e removendo uma regra no Visual Basic  
 Este exemplo de código mostra como criar uma regra, anexá-la a uma coluna, modificar propriedades do objeto <xref:Microsoft.SqlServer.Management.Smo.Rule>, desanexá-la da coluna e, em seguida, descartá-la.  
  
 A instrução **Dim** para o objeto <xref:Microsoft.SqlServer.Management.Smo.Rule> é especificada com o caminho completo do assembly para evitar ambigüidade com um objeto <xref:Microsoft.SqlServer.Management.Smo.Rule> no assembly System. Data.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Reference the AdventureWorks2012 database.
Dim db As Database
db = srv.Databases("AdventureWorks2012")
'Declare a Table object variable and reference the Product table.
Dim tb As Table
tb = db.Tables("Product", "Production")
'Define a Rule object variable by supplying the parent database, name and schema in the constructor. 
'Note that the full namespace must be given for the Rule type to differentiate it from other Rule types.
Dim ru As Microsoft.SqlServer.Management.Smo.Rule
ru = New Rule(db, "TestRule", "Production")
'Set the TextHeader and TextBody properties to define the rule.
ru.TextHeader = "CREATE RULE [Production].[TestRule] AS"
ru.TextBody = "@value BETWEEN GETDATE() AND DATEADD(year,4,GETDATE())"
'Create the rule on the instance of SQL Server.
ru.Create()
'Bind the rule to a column in the Product table by supplying the table, schema, and 
'column as arguments in the BindToColumn method.
ru.BindToColumn("Product", "SellEndDate", "Production")
'Unbind from the column before removing the rule from the database.
ru.UnbindFromColumn("Product", "SellEndDate", "Production")
ru.Drop()
```
  
## <a name="creating-altering-and-removing-a-rule-in-visual-c"></a>Criando, alterando e removendo uma regra no Visual C#  
 Este exemplo de código mostra como criar uma regra, anexá-la a uma coluna, modificar propriedades do objeto <xref:Microsoft.SqlServer.Management.Smo.Rule>, desanexá-la da coluna e, em seguida, descartá-la.  
  
 A instrução **Dim** para o objeto <xref:Microsoft.SqlServer.Management.Smo.Rule> é especificada com o caminho completo do assembly para evitar ambigüidade com um objeto <xref:Microsoft.SqlServer.Management.Smo.Rule> no assembly System. Data.  
  
```csharp  
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
  
 A instrução **Dim** para o objeto <xref:Microsoft.SqlServer.Management.Smo.Rule> é especificada com o caminho completo do assembly para evitar ambigüidade com um objeto <xref:Microsoft.SqlServer.Management.Smo.Rule> no assembly System. Data.  
  
```powershell   
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
  
  
