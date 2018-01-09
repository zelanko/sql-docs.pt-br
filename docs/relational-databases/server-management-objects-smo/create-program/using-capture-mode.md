---
title: Usando o modo de captura | Microsoft Docs
ms.custom: 
ms.date: 08/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, capture mode
- capture mode [SMO]
- SMO [SQL Server], capture mode
ms.assetid: ace29bf0-705a-434f-82e4-db99d01c5008
caps.latest.revision: "39"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 76f407dc02ff95535c456f21debe3d208ff475e4
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="using-capture-mode"></a>Usando modo de captura
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Programas SMO podem capturar e registrar o equivalente [!INCLUDE[tsql](../../../includes/tsql-md.md)] declarações emitidas pelo programa no lugar de ou além de instruções que são executadas pelo programa. Você habilita o modo de captura usando o objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> ou a propriedade <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> do objeto <xref:Microsoft.SqlServer.Management.Smo.Server>.  
  
## <a name="example"></a>Exemplo  
Para usar qualquer exemplo de código fornecido, será necessário escolher o ambiente de programação, o modelo de programação e a linguagem de programação para criar o aplicativo. Para obter mais informações, consulte [criar um Visual C &#35; Projeto SMO no Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  

  
## <a name="enabling-capture-mode-in-visual-basic"></a>Habilitando o modo de captura no Visual Basic  
 Este exemplo de código habilita o modo de captura e exibe os comandos [!INCLUDE[tsql](../../../includes/tsql-md.md)] contidos no buffer de captura.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Set the execution mode to CaptureSql for the connection.
srv.ConnectionContext.SqlExecutionModes = SqlExecutionModes.CaptureSql
'Make a modification to the server that is to be captured.
srv.UserOptions.AnsiNulls = True
srv.Alter()
'Iterate through the strings in the capture buffer and display the captured statements.
Dim s As String
For Each s In srv.ConnectionContext.CapturedSql.Text
    Console.WriteLine(s)
Next
'Execute the captured statements.
srv.ConnectionContext.ExecuteNonQuery(srv.ConnectionContext.CapturedSql.Text)
'Revert to immediate execution mode. 
srv.ConnectionContext.SqlExecutionModes = SqlExecutionModes.ExecuteSql
```
  
## <a name="enabling-capture-mode-in-visual-c"></a>Habilitando o modo de captura no Visual C#  
 Este exemplo de código habilita o modo de captura e exibe os comandos [!INCLUDE[tsql](../../../includes/tsql-md.md)] contidos no buffer de captura.  
  
```csharp  
{   
// Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
// Set the execution mode to CaptureSql for the connection.   
srv.ConnectionContext.SqlExecutionModes = SqlExecutionModes.CaptureSql;   
// Make a modification to the server that is to be captured.   
srv.UserOptions.AnsiNulls = true;   
srv.Alter();   
// Iterate through the strings in the capture buffer and display the captured statements.   
string s;   
foreach ( String p_s in srv.ConnectionContext.CapturedSql.Text ) {   
   Console.WriteLine(p_s);   
}   
// Execute the captured statements.   
srv.ConnectionContext.ExecuteNonQuery(srv.ConnectionContext.CapturedSql.Text);   
// Revert to immediate execution mode.   
srv.ConnectionContext.SqlExecutionModes = SqlExecutionModes.ExecuteSql;   
}  
```  
  
  
