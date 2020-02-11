---
title: Usando o modo de captura | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, capture mode
- capture mode [SMO]
- SMO [SQL Server], capture mode
ms.assetid: ace29bf0-705a-434f-82e4-db99d01c5008
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9ab758f83bde2cb587d3cfab8764fd7eb8fe2577
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68197995"
---
# <a name="using-capture-mode"></a>Usando modo de captura
  Os programas SMO podem capturar e registrar as instruções [!INCLUDE[tsql](../../../includes/tsql-md.md)] equivalentes emitidas pelo programa no lugar das, ou além das, instruções executadas pelo programa. Você habilita o modo de captura usando o objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> ou a propriedade <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> do objeto <xref:Microsoft.SqlServer.Management.Smo.Server>.  
  
## <a name="example"></a>Exemplo  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="enabling-capture-mode-in-visual-basic"></a>Habilitando o modo de captura no Visual Basic  
 Este exemplo de código habilita o modo de captura e exibe os comandos [!INCLUDE[tsql](../../../includes/tsql-md.md)] contidos no buffer de captura.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBCapture1](SMO How to#SMO_VBCapture1)]  -->  
  
## <a name="enabling-capture-mode-in-visual-c"></a>Habilitando o modo de captura no Visual C#  
 Este exemplo de código habilita o modo de captura e exibe os comandos [!INCLUDE[tsql](../../../includes/tsql-md.md)] contidos no buffer de captura.  
  
```  
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
  
  
