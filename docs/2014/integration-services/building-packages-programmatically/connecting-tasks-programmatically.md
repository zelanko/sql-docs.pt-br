---
title: Conectar tarefas programaticamente | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 93c50b2947e3a5174c19555dad903b34a7bea184
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84924874"
---
# <a name="connecting-tasks-programmatically"></a>Conectando tarefas programaticamente
  Uma restrição de precedência, representada no modelo de objeto pela classe <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint>, estabelece a ordem na qual objetos <xref:Microsoft.SqlServer.Dts.Runtime.Executable> são executados em um pacote. A restrição de precedência permite que a execução dos contêineres e tarefas de um pacote dependam do resultado da execução de uma tarefa ou contêiner anterior. Restrições de precedência são estabelecidas entre pares de objetos <xref:Microsoft.SqlServer.Dts.Runtime.Executable> através da chamada ao método <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraints.Add%2A> da coleção <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraints> no objeto contêiner. Depois de criar uma restrição entre dois objetos executáveis, defina a propriedade <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.Value%2A> para estabelecer os critérios para executar o segundo executável definido na restrição.  
  
 Você pode usar uma restrição e uma expressão em uma única restrição de precedência, dependendo do valor especificado para a propriedade <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.EvalOp%2A>, conforme descrito na seguinte tabela:  
  
|Valor da propriedade EvalOp|DESCRIÇÃO|  
|----------------------------------|-----------------|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DTSPrecedenceEvalOp.Constraint>|Especifica que o resultado de execução determina se o contêiner ou tarefa restrita é executada. Defina a propriedade <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.Value%2A> do <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint> com o valor desejado da enumeração <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult>.|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DTSPrecedenceEvalOp.Expression>|Especifica que o valor de uma expressão determina se o contêiner ou tarefa restrita é executada. Defina a propriedade <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.Expression%2A> do <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint>.|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DTSPrecedenceEvalOp.ExpressionAndConstraint>|Especifica que o resultado de restrição deve ocorrer e que a expressão deve ser avaliada para determinar se o contêiner ou tarefa restrita deve ser executada. Defina as propriedades <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.Value%2A> e <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.Expression%2A> do <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint>, e defina sua propriedade <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.LogicalAnd%2A> como `true`.|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DTSPrecedenceEvalOp.ExpressionOrConstraint>|Especifica que o resultado de restrição deve ocorrer, ou que a expressão deve ser avaliada, para determinar se o contêiner ou tarefa restrita deve ser executada. Defina as propriedades <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.Value%2A> e <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.Expression%2A> do <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint>, e defina sua propriedade <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.LogicalAnd%2A> como `false`.|  
  
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
  
![Ícone de Integration Services (pequeno)](../media/dts-16.gif "Ícone do Integration Services (pequeno)")  **Mantenha-se atualizado com Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte Também  
 [Adicionando a tarefa Fluxo de Dados programaticamente](../building-packages-programmatically/adding-the-data-flow-task-programmatically.md)  
  
  
