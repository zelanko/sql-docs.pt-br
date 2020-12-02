---
description: Conectando tarefas programaticamente
title: Conectar tarefas programaticamente | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- tasks [Integration Services], precedence constraints
- precedence constraints [Integration Services], connecting tasks
- constraints [Integration Services]
ms.assetid: 23668e88-cef4-4009-a9cf-38e607eab7a2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8fbe6beb6556db9e5dfddc6f63e6922a34ae6fe5
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96123801"
---
# <a name="connecting-tasks-programmatically"></a>Conectando tarefas programaticamente

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Uma restrição de precedência, representada no modelo de objeto pela classe <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint>, estabelece a ordem na qual objetos <xref:Microsoft.SqlServer.Dts.Runtime.Executable> são executados em um pacote. A restrição de precedência permite que a execução dos contêineres e tarefas de um pacote dependam do resultado da execução de uma tarefa ou contêiner anterior. Restrições de precedência são estabelecidas entre pares de objetos <xref:Microsoft.SqlServer.Dts.Runtime.Executable> através da chamada ao método <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraints.Add%2A> da coleção <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraints> no objeto contêiner. Depois de criar uma restrição entre dois objetos executáveis, defina a propriedade <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.Value%2A> para estabelecer os critérios para executar o segundo executável definido na restrição.  
  
 Você pode usar uma restrição e uma expressão em uma única restrição de precedência, dependendo do valor especificado para a propriedade <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.EvalOp%2A>, conforme descrito na seguinte tabela:  
  
|Valor da propriedade EvalOp|Descrição|  
|----------------------------------|-----------------|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DTSPrecedenceEvalOp.Constraint>|Especifica que o resultado de execução determina se o contêiner ou tarefa restrita é executada. Defina a propriedade <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.Value%2A> do <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint> com o valor desejado da enumeração <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult>.|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DTSPrecedenceEvalOp.Expression>|Especifica que o valor de uma expressão determina se o contêiner ou tarefa restrita é executada. Defina a propriedade <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.Expression%2A> do <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint>.|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DTSPrecedenceEvalOp.ExpressionAndConstraint>|Especifica que o resultado de restrição deve ocorrer e que a expressão deve ser avaliada para determinar se o contêiner ou tarefa restrita deve ser executada. Defina ambas as propriedades <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.Value%2A> e <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.Expression%2A> do <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint> e defina sua propriedade <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.LogicalAnd%2A> como **true**.|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DTSPrecedenceEvalOp.ExpressionOrConstraint>|Especifica que o resultado de restrição deve ocorrer, ou que a expressão deve ser avaliada, para determinar se o contêiner ou tarefa restrita deve ser executada. Defina ambas as propriedades <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.Value%2A> e <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.Expression%2A> do <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint> e defina sua propriedade <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.LogicalAnd%2A> como **false**.|  
  
 O exemplo de código a seguir demonstra a adição de duas tarefas a um pacote. Um <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint> é criado entre elas, impedindo a execução da segunda tarefa antes do término da primeira.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package p = new Package();  
  
      // Add a File System task.  
      Executable eFileTask1 = p.Executables.Add("STOCK:FileSystemTask");  
      TaskHost thFileHost1 = eFileTask1 as TaskHost;  
  
      // Add a second File System task.  
      Executable eFileTask2 = p.Executables.Add("STOCK:FileSystemTask");  
      TaskHost thFileHost2 = eFileTask2 as TaskHost;  
  
      // Put a precedence constraint between the tasks.  
      // Set the constraint to specify that the second File System task cannot run  
      // until the first File System task finishes.  
      PrecedenceConstraint pcFileTasks =   
        p.PrecedenceConstraints.Add((Executable)thFileHost1, (Executable)thFileHost2);  
      pcFileTasks.Value = DTSExecResult.Completion;  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim p As Package = New Package()  
    ' Add a File System task.  
    Dim eFileTask1 As Executable = p.Executables.Add("STOCK:FileSystemTask")  
    Dim thFileHost1 As TaskHost = CType(eFileTask1, TaskHost)  
  
    ' Add a second File System task.  
    Dim eFileTask2 As Executable = p.Executables.Add("STOCK:FileSystemTask")  
    Dim thFileHost2 As TaskHost = CType(eFileTask2, TaskHost)  
  
    ' Put a precedence constraint between the tasks.  
    ' Set the constraint to specify that the second File System task cannot run  
    ' until the first File System task finishes.  
    Dim pcFileTasks As PrecedenceConstraint = _  
      p.PrecedenceConstraints.Add(CType(thFileHost1, Executable), CType(thFileHost2, Executable))  
    pcFileTasks.Value = DTSExecResult.Completion  
  
  End Sub  
  
End Module  
```
  
## <a name="see-also"></a>Consulte Também  
 [Adicionando a tarefa Fluxo de Dados programaticamente](../../integration-services/building-packages-programmatically/adding-the-data-flow-task-programmatically.md)  
  
  
