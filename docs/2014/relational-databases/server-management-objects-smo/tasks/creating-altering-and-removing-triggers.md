---
title: Criando, alterando e removendo gatilhos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- triggers [SMO]
ms.assetid: 8ddbe23b-6e31-4f8e-8a70-17bd5072413e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 31430674d88d8aa5b820823a16dc18d110b9dd9a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "72782308"
---
# <a name="creating-altering-and-removing-triggers"></a>Criando, alterando e removendo gatilhos
  No SMO, gatilhos são representados por meio do uso do objeto <xref:Microsoft.SqlServer.Management.Smo.Trigger>. O [!INCLUDE[tsql](../../../includes/tsql-md.md)] código que é executado quando o gatilho é acionado é definido pela <xref:Microsoft.SqlServer.Management.Smo.Trigger.TextBody%2A> Propriedade do objeto de gatilho. O tipo de gatilho é definido através de outras propriedades do objeto <xref:Microsoft.SqlServer.Management.Smo.Trigger>, como, por exemplo, a propriedade <xref:Microsoft.SqlServer.Management.Smo.Trigger.Update%2A>. Essa é uma propriedade booliana que especifica se o gatilho é acionado por um `UPDATE` de registros na tabela pai.  
  
 O objeto <xref:Microsoft.SqlServer.Management.Smo.Trigger> representa gatilhos tradicionais da DML (linguagem de manipulação de dados). No [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] e em versões posteriores, também há suporte a gatilhos da DDL (linguagem de definição de dados). Os gatilhos da DDL são representados pelos objetos <xref:Microsoft.SqlServer.Management.Smo.DatabaseDdlTrigger> e <xref:Microsoft.SqlServer.Management.Smo.ServerDdlTrigger>.  
  
## <a name="example"></a>Exemplo  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="creating-altering-and-removing-a-trigger-in-visual-basic"></a>Criando, alterando e removendo um gatilho no Visual Basic  
 Este exemplo de código mostra como criar e inserir um gatilho de atualização em uma tabela existente, chamada `Sales`, no banco de dados [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] . O gatilho envia uma mensagem de lembrete quando a tabela é atualizada ou um novo registro é inserido.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBTriggers1](SMO How to#SMO_VBTriggers1)]  -->  
  
## <a name="creating-altering-and-removing-a-trigger-in-visual-c"></a>Criando, alterando e removendo um gatilho no Visual C#  
 Este exemplo de código mostra como criar e inserir um gatilho de atualização em uma tabela existente, chamada `Sales`, no banco de dados [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] . O gatilho envia uma mensagem de lembrete quando a tabela é atualizada ou um novo registro é inserido.  
  
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
 Este exemplo de código mostra como criar e inserir um gatilho de atualização em uma tabela existente, chamada `Sales`, no banco de dados [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] . O gatilho envia uma mensagem de lembrete quando a tabela é atualizada ou um novo registro é inserido.  
  
```powershell
# Set the path context to the local, default instance of SQL Server and to the  
#database tables in Adventureworks2012  
CD \sql\localhost\default\databases\AdventureWorks2012\Tables\  
  
#Get reference to the trigger's target table  
$mytab = Get-Item Sales.Customer  
  
# Define a Trigger object variable by supplying the parent table, schema ,and name in the constructor.  
$tr = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Trigger -argumentlist $mytab, "Sales"  
  
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
