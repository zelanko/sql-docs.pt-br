---
title: Manipular eventos programaticamente | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Integration Services packages, events
- SQL Server Integration Services packages, events
- SSIS events, programmatically handling
- packages [Integration Services], events
- DtsEventHandler object
- SSIS packages, events
- SSIS events
- events [Integration Services], programmatically
- tasks [Integration Services], events
- IDTSEvents interface
ms.assetid: 0f00bd66-efd5-4f12-9e1c-36195f739332
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8e0417ddf5c4c09cfffa07b7b76918a89622aec6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62771796"
---
# <a name="handling-events-programmatically"></a>Manipulando eventos programaticamente
  O tempo de execução [!INCLUDE[ssIS](../../includes/ssis-md.md)] fornece uma coleção de eventos que ocorrem antes, durante e depois da validação e execução de um pacote. Esses eventos podem ser capturados de duas formas. O primeiro método é através da implementação da interface <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents> em uma classe e do fornecimento da classe como um parâmetro para os métodos `Execute` e `Validate` do pacote. O segundo método é através da criação de objetos <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler>, que podem conter outros objetos [!INCLUDE[ssIS](../../includes/ssis-md.md)], tais como tarefas e loops, que são executados quando ocorre um evento em <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents>. Essa seção descreve esses dois métodos e fornece exemplos de código para demonstrar o seu uso.  
  
## <a name="receiving-idtsevents-callbacks"></a>Recebendo retornos de chamada de IDTSEvents  
 Desenvolvedores que criam e executam pacotes programaticamente podem receber notificações de eventos durante o processo de validação e execução através da interface <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents>. Isso é feito através da criação de uma classe que implementa a interface <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents> e do fornecimento dessa classe como um parâmetro para os métodos `Validate` e `Execute` de um pacote. Os métodos da classe são chamados, então, pelo mecanismo de tempo de execução quando os eventos ocorrem.  
  
 A classe <xref:Microsoft.SqlServer.Dts.Runtime.DefaultEvents> é uma classe que já implementa a interface <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents>; portanto, outro alternativa à implementação direta de <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents> é derivar de <xref:Microsoft.SqlServer.Dts.Runtime.DefaultEvents> e substituir os eventos específicos aos quais você deseja responder. Depois, você fornece sua classe como um parâmetro para os métodos `Validate` e `Execute` do <xref:Microsoft.SqlServer.Dts.Runtime.Package> para receber retornos de chamada de eventos.  
  
 O exemplo de código a seguir demonstra uma classe que deriva de <xref:Microsoft.SqlServer.Dts.Runtime.DefaultEvents>e substitui o método <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents.OnPreExecute%2A>. A classe é fornecida como portanto para o `Validate` e `Execute` métodos do pacote.  
  
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
      MyEventsClass eventsClass = new MyEventsClass();  
  
      p.Validate(null, null, eventsClass, null);  
      p.Execute(null, null, eventsClass, null, null);  
  
      Console.Read();  
    }  
  }  
  class MyEventsClass : DefaultEvents  
  {  
    public override void OnPreExecute(Executable exec, ref bool fireAgain)  
    {  
      // TODO: Add custom code to handle the event.  
      Console.WriteLine("The PreExecute event of the " +  
        exec.ToString() + " has been raised.");  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim p As Package = New Package()  
    Dim eventsClass As MyEventsClass = New MyEventsClass()  
  
    p.Validate(Nothing, Nothing, eventsClass, Nothing)  
    p.Execute(Nothing, Nothing, eventsClass, Nothing, Nothing)  
  
    Console.Read()  
  
  End Sub  
  
End Module  
  
Class MyEventsClass  
  Inherits DefaultEvents  
  
  Public Overrides Sub OnPreExecute(ByVal exec As Executable, ByRef fireAgain As Boolean)  
  
    ' TODO: Add custom code to handle the event.  
    Console.WriteLine("The PreExecute event of the " & _  
      exec.ToString() & " has been raised.")  
  
  End Sub  
  
End Class  
```  
  
## <a name="creating-dtseventhandler-objects"></a>Criando objetos DtsEventHandler  
 O mecanismo de tempo de execução fornece um sistema de tratamento e notificação de eventos robusto, altamente flexível através do objeto <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler>. Esses objetos permitem que você crie fluxos de trabalho inteiros dentro do manipulador de eventos, que só são executados quando ocorre o evento ao qual pertence o manipulador de eventos. O objeto <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> é um contêiner que é executado quando o evento correspondente de seu objeto pai dispara. Essa arquitetura permite criar fluxos de trabalho isolados que são executados em resposta a eventos que ocorrem em um contêiner. Como objetos <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> são síncronos, a execução só retoma quando os manipuladores de eventos anexados ao evento retornam.  
  
 O código a seguir demonstra como criar um objeto <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler>. O código adiciona um <xref:Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask> à coleção <xref:Microsoft.SqlServer.Dts.Runtime.Package.Executables%2A> do pacote e, depois, cria um objeto <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> para o evento <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents.OnError%2A> da tarefa. Um <xref:Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask> é adicionado ao manipulador de eventos, que é executado quando o evento <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents.OnError%2A> ocorre para o primeiro <xref:Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask>. Esse exemplo pressupõe que você tem um arquivo chamado C:\Windows\Temp\DemoFile.txt para teste. Na primeira execução do exemplo, o arquivo é copiado com êxito e o manipulador de eventos não é chamado. Na segunda execução do exemplo, o <xref:Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask> não consegue copiar o arquivo (pois o valor de <xref:Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask.OverwriteDestinationFile%2A> é `false`), o manipulador de eventos é chamado, o segundo <xref:Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask> exclui o arquivo de origem e o pacote relata falha em função do erro ocorrido.  
  
## <a name="example"></a>Exemplo  
  
```csharp  
using System;  
using System.IO;  
using Microsoft.SqlServer.Dts.Runtime;  
using Microsoft.SqlServer.Dts.Tasks.FileSystemTask;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      string f = "DemoFile.txt";  
      Executable e;  
      TaskHost th;  
      FileSystemTask fst;  
  
      Package p = new Package();  
  
      p.Variables.Add("sourceFile", true, String.Empty,  
        @"C:\Windows\Temp\" + f);  
      p.Variables.Add("destinationFile", true, String.Empty,  
        Path.Combine(Directory.GetCurrentDirectory(), f));  
  
      // Create a first File System task and add it to the package.  
      // This task tries to copy a file from one folder to another.  
      e = p.Executables.Add("STOCK:FileSystemTask");  
      th = e as TaskHost;  
      th.Name = "FileSystemTask1";  
      fst = th.InnerObject as FileSystemTask;  
  
      fst.Operation = DTSFileSystemOperation.CopyFile;  
      fst.OverwriteDestinationFile = false;  
      fst.Source = "sourceFile";  
      fst.IsSourcePathVariable = true;  
      fst.Destination = "destinationFile";  
      fst.IsDestinationPathVariable = true;  
  
      // Add an event handler for the FileSystemTask's OnError event.  
      DtsEventHandler ehOnError = (DtsEventHandler)th.EventHandlers.Add("OnError");  
  
      // Create a second File System task and add it to the event handler.  
      // This task deletes the source file if the event handler is called.  
      e = ehOnError.Executables.Add("STOCK:FileSystemTask");  
      th = e as TaskHost;  
      th.Name = "FileSystemTask2";  
      fst = th.InnerObject as FileSystemTask;  
  
      fst.Operation = DTSFileSystemOperation.DeleteFile;  
      fst.Source = "sourceFile";  
      fst.IsSourcePathVariable = true;  
  
      DTSExecResult vr = p.Validate(null, null, null, null);  
      Console.WriteLine("ValidationResult = " + vr.ToString());  
      if (vr == DTSExecResult.Success)  
      {  
        DTSExecResult er = p.Execute(null, null, null, null, null);  
        Console.WriteLine("ExecutionResult = " + er.ToString());  
        if (er == DTSExecResult.Failure)  
          if (!File.Exists(@"C:\Windows\Temp\" + f))  
            Console.WriteLine("Source file has been deleted by the event handler.");  
      }  
      Console.Read();  
    }  
  }  
}  
```  
  
```vb  
Imports System.IO  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports Microsoft.SqlServer.Dts.Tasks.FileSystemTask  
  
Module Module1  
  
  Sub Main()  
  
    Dim f As String = "DemoFile.txt"  
    Dim e As Executable  
    Dim th As TaskHost  
    Dim fst As FileSystemTask  
  
    Dim p As Package = New Package()  
  
    p.Variables.Add("sourceFile", True, String.Empty, _  
      "C:\Windows\Temp\" & f)  
    p.Variables.Add("destinationFile", True, String.Empty, _  
      Path.Combine(Directory.GetCurrentDirectory(), f))  
  
    ' Create a first File System task and add it to the package.  
    ' This task tries to copy a file from one folder to another.  
    e = p.Executables.Add("STOCK:FileSystemTask")  
    th = CType(e, TaskHost)  
    th.Name = "FileSystemTask1"  
    fst = CType(th.InnerObject, FileSystemTask)  
  
    fst.Operation = DTSFileSystemOperation.CopyFile  
    fst.OverwriteDestinationFile = False  
    fst.Source = "sourceFile"  
    fst.IsSourcePathVariable = True  
    fst.Destination = "destinationFile"  
    fst.IsDestinationPathVariable = True  
  
    ' Add an event handler for the FileSystemTask's OnError event.  
    Dim ehOnError As DtsEventHandler = CType(th.EventHandlers.Add("OnError"), DtsEventHandler)  
  
    ' Create a second File System task and add it to the event handler.  
    ' This task deletes the source file if the event handler is called.  
    e = ehOnError.Executables.Add("STOCK:FileSystemTask")  
    th = CType(e, TaskHost)  
    th.Name = "FileSystemTask1"  
    fst = CType(th.InnerObject, FileSystemTask)  
  
    fst.Operation = DTSFileSystemOperation.DeleteFile  
    fst.Source = "sourceFile"  
    fst.IsSourcePathVariable = True  
  
    Dim vr As DTSExecResult = p.Validate(Nothing, Nothing, Nothing, Nothing)  
    Console.WriteLine("ValidationResult = " + vr.ToString())  
    If vr = DTSExecResult.Success Then  
      Dim er As DTSExecResult = p.Execute(Nothing, Nothing, Nothing, Nothing, Nothing)  
      Console.WriteLine("ExecutionResult = " + er.ToString())  
      If er = DTSExecResult.Failure Then  
        If Not File.Exists("C:\Windows\Temp\" + f) Then  
          Console.WriteLine("Source file has been deleted by the event handler.")  
        End If  
      End If  
    End If  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
![Ícone do Integration Services (pequeno)](../media/dts-16.gif "ícone do Integration Services (pequeno)")**mantenha-se para cima até o momento com o Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte também  
 [Manipuladores de eventos do SSIS &#40;Integration Services&#41;](../integration-services-ssis-event-handlers.md)   
 [Adicionar um manipulador de eventos a um pacote](../add-an-event-handler-to-a-package.md)  
  
  
