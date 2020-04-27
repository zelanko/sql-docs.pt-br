---
title: Adicionar tarefas programaticamente | Microsoft Docs
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
- tasks [Integration Services], packages
- adding package tasks
ms.assetid: 5d4652d5-228c-4238-905c-346dd8503fdf
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: da9a2e5bf8338b8188f00f3c340d50ef32f1204f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62771832"
---
# <a name="adding-tasks-programmatically"></a>Adicionando tarefas programaticamente
  As tarefas podem ser adicionadas aos seguintes tipos de objetos no mecanismo de tempo de execução:  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.Package>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.Sequence>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.ForLoop>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler>  
  
 Essas classes são consideradas contêineres e todas herdam a propriedade <xref:Microsoft.SqlServer.Dts.Runtime.IDTSSequence.Executables%2A>. Os contêineres podem conter uma coleção de tarefas, que são objetos executáveis processados pelo runtime durante a execução do contêiner. A ordem de execução dos objetos na coleção é determinada em qualquer conjunto <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint> em cada tarefa dos contêineres. Restrições de precedência habilitam a ramificação da execução com base no êxito, falha ou conclusão de um <xref:Microsoft.SqlServer.Dts.Runtime.Executable> na coleção.  
  
 Cada contêiner tem uma coleção <xref:Microsoft.SqlServer.Dts.Runtime.Executables> que contém os objetos individuais <xref:Microsoft.SqlServer.Dts.Runtime.Executable>. Cada tarefa executável herda e implementa os métodos <xref:Microsoft.SqlServer.Dts.Runtime.Executable.Execute%2A> e <xref:Microsoft.SqlServer.Dts.Runtime.Executable.Validate%2A>. Esses dois métodos são chamados pelo mecanismo de tempo de execução para processar cada <xref:Microsoft.SqlServer.Dts.Runtime.Executable>.  
  
 Para adicionar uma tarefa a um pacote, você precisa de um contêiner com uma coleção existente <xref:Microsoft.SqlServer.Dts.Runtime.Executables>. Em geral, a tarefa a ser adicionada à coleção é um pacote. Para adicionar o executável da nova tarefa na coleção para esse contêiner, chame o método <xref:Microsoft.SqlServer.Dts.Runtime.Executables.Add%2A>. O método possui um único parâmetro, uma cadeia de caracteres, que contém CLSID, PROGID, o moniker STOCK ou o <xref:Microsoft.SqlServer.Dts.Runtime.TaskInfo.CreationName%2A> da tarefa você está adicionando.  
  
## <a name="task-names"></a>Nomes de tarefas  
 Embora você possa especificar uma tarefa pelo nome ou pela ID, o moniker `STOCK` é o parâmetro mais usado no método <xref:Microsoft.SqlServer.Dts.Runtime.Executables.Add%2A>. Para adicionar uma tarefa a um executável identificado pelo moniker `STOCK`, use a seguinte sintaxe:  
  
```csharp  
Executable exec = package.Executables.Add("STOCK:BulkInsertTask");  
  
```  
  
```vb  
Dim exec As Executable = package.Executables.Add("STOCK:BulkInsertTask")  
  
```  
  
 A lista a seguir mostra os nomes de cada tarefa que são usados depois do moniker `STOCK`.  
  
-   ActiveXScriptTask  
  
-   BulkInsertTask  
  
-   ExecuteProcessTask  
  
-   ExecutePackageTask  
  
-   Exec80PackageTask  
  
-   FileSystemTask  
  
-   FTPTask  
  
-   MSMQTask  
  
-   PipelineTask  
  
-   ScriptTask  
  
-   SendMailTask  
  
-   SQLTask  
  
-   TransferStoredProceduresTask  
  
-   TransferLoginsTask  
  
-   TransferErrorMessagesTask  
  
-   TransferJobsTask  
  
-   TransferObjectsTask  
  
-   TransferDatabaseTask  
  
-   WebServiceTask  
  
-   WmiDataReaderTask  
  
-   WmiEventWatcherTask  
  
-   XMLTask  
  
 Se preferir uma sintaxe mais explícita ou se a tarefa a ser adicionada não possuir um moniker STOCK, você poderá adicionar a tarefa ao executável usando o nome longo. Essa sintaxe requer que você também especifique o número da versão da tarefa.  
  
```csharp  
Executable exec = package.Executables.Add(  
  "Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask, " +  
  "Microsoft.SqlServer.ScriptTask, Version=10.0.000.0, " +  
  "Culture=neutral, PublicKeyToken=89845dcd8080cc91");  
```  
  
```vb  
Dim exec As Executable = package.Executables.Add( _  
  "Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask, " & _  
  "Microsoft.SqlServer.ScriptTask, Version=10.0.000.0, " & _  
  "Culture=neutral, PublicKeyToken=89845dcd8080cc91")  
```  
  
 Você pode obter o nome longo para a tarefa programaticamente, sem precisar especificar a versão da tarefa, usando a propriedade **AssemblyQualifiedName** da classe, conforme mostrado no exemplo a seguir. Esse exemplo precisa de uma referência ao assembly Microsoft.SqlServer.SQLTask.  
  
```csharp  
using Microsoft.SqlServer.Dts.Tasks.ExecuteSQLTask;  
...  
      Executable exec = package.Executables.Add(  
        typeof(Microsoft.SqlServer.Dts.Tasks.ExecuteSQLTask.ExecuteSQLTask).AssemblyQualifiedName);  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Tasks.ExecuteSQLTask  
...  
    Dim exec As Executable = package.Executables.Add( _  
      GetType(Microsoft.SqlServer.Dts.Tasks.ExecuteSQLTask.ExecuteSQLTask).AssemblyQualifiedName)  
```  
  
 O exemplo de código a seguir mostra como criar uma coleção <xref:Microsoft.SqlServer.Dts.Runtime.Executables> a partir de um novo pacote e, depois, adicionar uma tarefa Sistema de Arquivos e uma tarefa Inserção em Massa à coleção, através de seus monikers `STOCK`. Esse exemplo precisa de uma referência aos assemblies Microsoft.SqlServer.FileSystemTask e Microsoft.SqlServer.BulkInsertTask.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
using Microsoft.SqlServer.Dts.Tasks.FileSystemTask;  
using Microsoft.SqlServer.Dts.Tasks.BulkInsertTask;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package p = new Package();  
      // Add a File System task to the package.  
      Executable exec1 = p.Executables.Add("STOCK:FileSystemTask");  
      TaskHost thFileSystemTask = exec1 as TaskHost;  
      // Add a Bulk Insert task to the package.  
      Executable exec2 = p.Executables.Add("STOCK:BulkInsertTask");  
      TaskHost thBulkInsertTask = exec2 as TaskHost;  
  
      // Iterate through the package Executables collection.  
      Executables pExecs = p.Executables;  
      foreach (Executable pExec in pExecs)  
      {  
        TaskHost taskHost = (TaskHost)pExec;  
        Console.WriteLine("Type {0}", taskHost.InnerObject.ToString());  
      }  
      Console.Read();  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports Microsoft.SqlServer.Dts.Tasks.FileSystemTask  
Imports Microsoft.SqlServer.Dts.Tasks.BulkInsertTask  
  
Module Module1  
  
  Sub Main()  
  
    Dim p As Package = New Package()  
    ' Add a File System task to the package.  
    Dim exec1 As Executable = p.Executables.Add("STOCK:FileSystemTask")  
    Dim thFileSystemTask As TaskHost = CType(exec1, TaskHost)  
    ' Add a Bulk Insert task to the package.  
    Dim exec2 As Executable = p.Executables.Add("STOCK:BulkInsertTask")  
    Dim thBulkInsertTask As TaskHost = CType(exec2, TaskHost)  
  
    ' Iterate through the package Executables collection.  
    Dim pExecs As Executables = p.Executables  
    Dim pExec As Executable  
    For Each pExec In pExecs  
      Dim taskHost As TaskHost = CType(pExec, TaskHost)  
      Console.WriteLine("Type {0}", taskHost.InnerObject.ToString())  
    Next  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
 **Saída de exemplo:**  
  
 `Type Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask`  
  
 `Type Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask`  
  
## <a name="taskhost-container"></a>Contêiner TaskHost  
 A classe <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> é um contêiner que não aparece na interface gráfica do usuário, mas é muito importante na programação. Essa classe é um wrapper de cada tarefa. As tarefas que são adicionadas ao pacote através do método <xref:Microsoft.SqlServer.Dts.Runtime.Executables.Add%2A> como um objeto <xref:Microsoft.SqlServer.Dts.Runtime.Executable> podem ser convertidas um objeto <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>. Quando uma tarefa é convertida como um <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>, você pode usar propriedades e métodos adicionais na tarefa. Além disso, a própria tarefa pode ser acessada através da propriedade <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.InnerObject%2A> do <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>. Dependendo das suas necessidades, você pode optar por manter a tarefa como um objeto <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> para poder usar as propriedades da tarefa através da coleção <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.Properties%2A>. A vantagem de usar o <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.Properties%2A> é que você pode escrever mais códigos genéricos. Se precisar de código muito específico para uma tarefa, converta a tarefa para seu objeto apropriado.  
  
 O exemplo de código a seguir mostra como converter um <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>, thBulkInsertTask, que contém um <xref:Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask>em um objeto <xref:Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask>.  
  
```csharp  
BulkInsertTask myTask = thBulkInsertTask.InnerObject as BulkInsertTask;  
```  
  
```vb  
Dim myTask As BulkInsertTask = CType(thBulkInsertTask.InnerObject, BulkInsertTask)  
```  
  
 O exemplo de código a seguir mostra como converter o executável em um <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>, e depois usar a propriedade <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.InnerObject%2A> para determinar que tipo de executável está contido no host.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
using Microsoft.SqlServer.Dts.Tasks.FileSystemTask;  
using Microsoft.SqlServer.Dts.Tasks.BulkInsertTask;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package p = new Package();  
      // Add a File System task to the package.  
      Executable exec1 = p.Executables.Add("STOCK:FileSystemTask");  
      TaskHost thFileSystemTask1 = exec1 as TaskHost;  
      // Add a Bulk Insert task to the package.  
      Executable exec2 = p.Executables.Add("STOCK:BulkInsertTask");  
      TaskHost thFileSystemTask2 = exec2 as TaskHost;  
  
      // Iterate through the package Executables collection.  
      Executables pExecs = p.Executables;  
      foreach (Executable pExec in pExecs)  
      {  
        TaskHost taskHost = (TaskHost)pExec;  
        if (taskHost.InnerObject is Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask)  
        {  
          // Do work with FileSystemTask here.  
          Console.WriteLine("Found task of type {0}", taskHost.InnerObject.ToString());  
        }  
        else if (taskHost.InnerObject is Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask)  
        {  
          // Do work with BulkInsertTask here.  
          Console.WriteLine("Found task of type {0}", taskHost.InnerObject.ToString());  
        }  
        // Add additional statements to check InnerObject, if desired.  
      }  
      Console.Read();  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports Microsoft.SqlServer.Dts.Tasks.FileSystemTask  
Imports Microsoft.SqlServer.Dts.Tasks.BulkInsertTask  
  
Module Module1  
  
  Sub Main()  
  
    Dim p As Package = New Package()  
    ' Add a File System task to the package.  
    Dim exec1 As Executable = p.Executables.Add("STOCK:FileSystemTask")  
    Dim thFileSystemTask1 As TaskHost = CType(exec1, TaskHost)  
    ' Add a Bulk Insert task to the package.  
    Dim exec2 As Executable = p.Executables.Add("STOCK:BulkInsertTask")  
    Dim thFileSystemTask2 As TaskHost = CType(exec2, TaskHost)  
  
    ' Iterate through the package Executables collection.  
    Dim pExecs As Executables = p.Executables  
    Dim pExec As Executable  
    For Each pExec In pExecs  
      Dim taskHost As TaskHost = CType(pExec, TaskHost)  
      If TypeOf taskHost.InnerObject Is Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask Then  
        ' Do work with FileSystemTask here.  
        Console.WriteLine("Found task of type {0}", taskHost.InnerObject.ToString())  
      ElseIf TypeOf taskHost.InnerObject Is Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask Then  
        ' Do work with BulkInsertTask here.  
        Console.WriteLine("Found task of type {0}", taskHost.InnerObject.ToString())  
      End If  
      ' Add additional statements to check InnerObject, if desired.  
    Next  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
 **Saída de exemplo:**  
  
 `Found task of type Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask`  
  
 `Found task of type Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask`  
  
 A instrução <xref:Microsoft.SqlServer.Dts.Runtime.Executables.Add%2A> retorna um executável que é convertido em um objeto <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> do objeto <xref:Microsoft.SqlServer.Dts.Runtime.Executable> recém-criado.  
  
 Para definir propriedades ou chamar métodos no objeto novo, você tem duas opções:  
  
1.  Use a coleção <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.Properties%2A> do <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>. Por exemplo, para obter uma propriedade do objeto, use `th.Properties["propertyname"].GetValue(th))`. Para definir uma propriedade, use `th.Properties["propertyname"].SetValue(th, <value>);`.  
  
2.  Converta o <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.InnerObject%2A> do <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> na classe de tarefa. Por exemplo, para converter a tarefa Inserção em Massa em um <xref:Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask> depois de sua adição a um pacote como um <xref:Microsoft.SqlServer.Dts.Runtime.Executable> e, subsequentemente, converter em um <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>, use `BulkInsertTask myTask = th.InnerObject as BulkInsertTask;`.  
  
 O uso da classe <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> em código, em vez de sua conversão na classe específica da tarefa apresenta as seguintes vantagens:  
  
-   O provedor <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost><xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.Properties%2A> não precisa de uma referência ao assembly no código.  
  
-   Você pode criar rotinas com código genérico que funcionam para qualquer tarefa, pois você não precisa saber o nome da tarefa no momento de compilação. Tais rotinas genéricas incluem métodos onde você transmite o nome da tarefa para o método; o código do método funciona para todas as tarefas. Esse é um método bom para escrever código de teste.  
  
 A conversão do <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> na classe específica de tarefa apresenta as seguintes vantagens:  
  
-   O projeto do Visual Studio oferece conclusão de instrução (IntelliSense).  
  
-   O código pode ser executado mais rápido.  
  
-   Objetos específicos da tarefa permitem associação inicial e as otimizações resultantes. Para obter mais informações sobre associações iniciais e tardias, consulte o tópico "Early and Late Binding" no Visual Basic Language Concepts.  
  
 O exemplo de código a seguir expande o conceito de reutilização do código de tarefa. Em vez de converter tarefas nos equivalentes de sua classe específica, o exemplo de código mostra como converter o executável em um <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>, e depois usa o <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.Properties%2A> para escrever o código genérico em relação a todas as tarefas.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package package = new Package();  
  
      string[] tasks = { "STOCK:SQLTask", "STOCK:ScriptTask",   
        "STOCK:ExecuteProcessTask", "STOCK:PipelineTask",   
        "STOCK:FTPTask", "STOCK:SendMailTask", "STOCK:MSMQTask" };  
  
      foreach (string s in tasks)  
      {  
        TaskHost taskhost = package.Executables.Add(s) as TaskHost;  
        DtsProperties props = taskhost.Properties;  
        Console.WriteLine("Enumerating properties on " + taskhost.Name);  
        Console.WriteLine(" TaskHost.InnerObject is " + taskhost.InnerObject.ToString());  
        Console.WriteLine();  
  
        foreach (DtsProperty prop in props)  
        {  
          Console.WriteLine("Properties for " + prop.Name);  
          Console.WriteLine("Name : " + prop.Name);  
          Console.WriteLine("Type : " + prop.Type.ToString());  
          Console.WriteLine("Readable : " + prop.Get.ToString());  
          Console.WriteLine("Writable : " + prop.Set.ToString());  
          Console.WriteLine();  
        }  
      }  
      Console.Read();  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim package As Package = New Package()  
  
    Dim tasks() As String = New String() {"STOCK:SQLTask", "STOCK:ScriptTask", _  
              "STOCK:ExecuteProcessTask", "STOCK:PipelineTask", _  
              "STOCK:FTPTask", "STOCK:SendMailTask", "STOCK:MSMQTask"}  
  
    For Each s As String In tasks  
  
      Dim taskhost As TaskHost = CType(package.Executables.Add(s), TaskHost)  
      Dim props As DtsProperties = taskhost.Properties  
      Console.WriteLine("Enumerating properties on " & taskhost.Name)  
      Console.WriteLine(" TaskHost.InnerObject is " & taskhost.InnerObject.ToString())  
      Console.WriteLine()  
  
      For Each prop As DtsProperty In props  
        Console.WriteLine("Properties for " + prop.Name)  
        Console.WriteLine(" Name : " + prop.Name)  
        Console.WriteLine(" Type : " + prop.Type.ToString())  
        Console.WriteLine(" Readable : " + prop.Get.ToString())  
        Console.WriteLine(" Writable : " + prop.Set.ToString())  
        Console.WriteLine()  
      Next  
  
    Next  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
## <a name="external-resources"></a>Recursos externos  
 Entrada no blog, [EzAPI – Updated for SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=243223) (EzAPI – atualizado para o SQL Server 2012) em blogs.msdn.com.  
  
![Ícone de Integration Services (pequeno)](../media/dts-16.gif "Ícone do Integration Services (pequeno)")  **Mantenha-se atualizado com Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte Também  
 [Conectando tarefas programaticamente](../building-packages-programmatically/connecting-tasks-programmatically.md)  
  
  
