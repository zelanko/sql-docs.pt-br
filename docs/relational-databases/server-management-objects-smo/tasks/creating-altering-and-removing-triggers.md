---
title: Criando, alterando e removendo gatilhos | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: smo
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- triggers [SMO]
ms.assetid: 8ddbe23b-6e31-4f8e-8a70-17bd5072413e
caps.latest.revision: 48
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: e4a6de9693ec4328fc60c060443292b10c6541e7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="creating-altering-and-removing-triggers"></a>Criando, alterando e removendo gatilhos
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]
  No SMO, gatilhos são representados por meio do uso do objeto <xref:Microsoft.SqlServer.Management.Smo.Trigger>. O [!INCLUDE[tsql](../../../includes/tsql-md.md)] código que é executado quando o gatilho é acionado é definido pelo <xref:Microsoft.SqlServer.Management.Smo.Trigger.TextBody%2A> propriedade do objeto de gatilho. O tipo de gatilho é definido através de outras propriedades do objeto <xref:Microsoft.SqlServer.Management.Smo.Trigger>, como, por exemplo, a propriedade <xref:Microsoft.SqlServer.Management.Smo.Trigger.Update%2A>. Essa é uma propriedade booliana que especifica se o gatilho é acionado por um **UPDATE** de registros na tabela pai.  
  
 O objeto <xref:Microsoft.SqlServer.Management.Smo.Trigger> representa gatilhos tradicionais da DML (linguagem de manipulação de dados). No [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] e em versões posteriores, também há suporte a gatilhos da DDL (linguagem de definição de dados). Os gatilhos da DDL são representados pelos objetos <xref:Microsoft.SqlServer.Management.Smo.DatabaseDdlTrigger> e <xref:Microsoft.SqlServer.Management.Smo.ServerDdlTrigger>.  
  
## <a name="example"></a>Exemplo  
Para usar qualquer exemplo de código fornecido, será necessário escolher o ambiente de programação, o modelo de programação e a linguagem de programação para criar o aplicativo. Para obter mais informações, consulte [criar um Visual C&#35; projeto SMO no Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
 
  
## <a name="creating-altering-and-removing-a-trigger-in-visual-basic"></a>Criando, alterando e removendo um gatilho no Visual Basic  
 Este exemplo de código mostra como criar e inserir um gatilho de atualização em uma tabela existente, chamada `Sales`, no banco de dados [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)]. O gatilho envia uma mensagem de lembrete quando a tabela é atualizada ou um novo registro é inserido.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim mysrv As Server
mysrv = New Server
'Reference the AdventureWorks2012 2008R2 database.
Dim mydb As Database
mydb = mysrv.Databases("AdventureWorks2012")
'Declare a Table object variable and reference the Customer table.
Dim mytab As Table
mytab = mydb.Tables("Customer", "Sales")
'Define a Trigger object variable by supplying the parent table, schema ,and name in the constructor.
Dim tr As Trigger
tr = New Trigger(mytab, "Sales")
'Set TextMode property to False, then set other properties to define the trigger.
tr.TextMode = False
tr.Insert = True
tr.Update = True
tr.InsertOrder = Agent.ActivationOrder.First
Dim stmt As String
stmt = " RAISERROR('Notify Customer Relations',16,10) "
tr.TextBody = stmt
tr.ImplementationType = ImplementationType.TransactSql
'Create the trigger on the instance of SQL Server.
tr.Create()
'Remove the trigger.
tr.Drop()
``` 
  
## <a name="creating-altering-and-removing-a-trigger-in-visual-c"></a>Criando, alterando e removendo um gatilho no Visual C#  
 Este exemplo de código mostra como criar e inserir um gatilho de atualização em uma tabela existente, chamada `Sales`, no banco de dados [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)]. O gatilho envia uma mensagem de lembrete quando a tabela é atualizada ou um novo registro é inserido.  
  
```csharp  
{  
            //Connect to the local, default instance of SQL Server.   
            Server mysrv;  
            mysrv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database mydb;  
            mydb = mysrv.Databases["AdventureWorks2012"];  
            //Declare a Table object variable and reference the Customer table.   
            Table mytab;  
            mytab = mydb.Tables["Customer", "Sales"];  
            //Define a Trigger object variable by supplying the parent table, schema ,and name in the constructor.   
            Trigger tr;  
            tr = new Trigger(mytab, "Sales");  
            //Set TextMode property to False, then set other properties to define the trigger.   
            tr.TextMode = false;  
            tr.Insert = true;  
            tr.Update = true;  
            tr.InsertOrder = ActivationOrder.First;  
            string stmt;  
            stmt = " RAISERROR('Notify Customer Relations',16,10) ";  
            tr.TextBody = stmt;  
            tr.ImplementationType = ImplementationType.TransactSql;  
            //Create the trigger on the instance of SQL Server.   
            tr.Create();  
            //Remove the trigger.   
            tr.Drop();  
        }  
```  
  
## <a name="creating-altering-and-removing-a-trigger-in-powershell"></a>Criando, alterando e removendo um gatilho no PowerShell  
 Este exemplo de código mostra como criar e inserir um gatilho de atualização em uma tabela existente, chamada `Sales`, no banco de dados [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)]. O gatilho envia uma mensagem de lembrete quando a tabela é atualizada ou um novo registro é inserido.  
  
```powershell  
# Set the path context to the local, default instance of SQL Server and to the  
#database tables in Adventureworks2012  
CD \sql\localhost\default\databases\AdventureWorks2012\Tables\  
  
#Get reference to the trigger's target table  
$mytab = get-item Sales.Customer  
  
# Define a Trigger object variable by supplying the parent table, schema ,and name in the constructor.  
$tr  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Trigger `  
-argumentlist $mytab, "Sales"  
  
# Set TextMode property to False, then set other properties to define the trigger.   
$tr.TextMode = $false  
$tr.Insert = $true  
$tr.Update = $true  
$tr.InsertOrder = [Microsoft.SqlServer.Management.SMO.Agent.ActivationOrder]::First  
$tr.TextBody = " RAISERROR('Notify Customer Relations',16,10) "  
$tr.ImplementationType = [Microsoft.SqlServer.Management.SMO.ImplementationType]::TransactSql  
  
# Create the trigger on the instance of SQL Server.   
$tr.Create()  
  
#Remove the trigger.   
$tr.Drop()  
```  
  
  
