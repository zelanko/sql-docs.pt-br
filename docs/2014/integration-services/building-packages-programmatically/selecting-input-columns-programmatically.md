---
title: Selecionar colunas de entrada programaticamente | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- input column mapping
- data flow task [Integration Services], components
- data flow task [Integration Services], column mapping
- mapping input columns [Integration Services]
- column mapping [Integration Services]
- data flow [Integration Services], column mapping
- data flow [Integration Services], components
ms.assetid: b53b110a-dcf4-4464-ae98-81e892ab74c3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d7c1592058776246ad3df657c3340303a60df296
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62771742"
---
# <a name="selecting-input-columns-programmatically"></a>Selecionando colunas de entrada programaticamente
  Depois de ter conectado componentes programaticamente, selecione as colunas dos componentes upstream que você transformará ou passará para os componentes downstream. Se você não selecionar colunas de entrada para seu componente, o componente não receberá nenhuma linha da tarefa de fluxo de dados.  
  
## <a name="selecting-columns"></a>Selecionando colunas  
 Chame o método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100.GetVirtualInput%2A> para recuperar a lista de colunas disponíveis de um componente upstream, e chame o método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapperClass.SetUsageType%2A> da instância do componente de tempo de design para selecionar colunas da coleção de colunas de entrada virtual. Quando você chama esse método, o componente cria uma nova coluna de entrada em sua coleção de colunas de entrada com a mesma ID de linhagem da coluna correspondente da coleção de saída do componente upstream.  
  
 Não selecione colunas chamando o método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSVirtualInput100.SetUsageType%2A> do objeto de entrada virtual diretamente, pois ele ignora a capacidade do componente de rejeitar colunas com base em tipos de dados inadequados ou outras propriedades.  
  
## <a name="sample"></a>Amostra  
 O exemplo de código seguinte mostra como usar a instância de tempo de design de um componente para selecionar as colunas para um componente.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      // Create a package and add a Data Flow task.  
      Package package = new Package();  
      Executable e = package.Executables.Add("STOCK:PipelineTask");  
      TaskHost thMainPipe = e as TaskHost;  
      MainPipe dataFlowTask = thMainPipe.InnerObject as MainPipe;  
  
      // Add an OLE DB connection manager to the package.  
      ConnectionManager conMgr = package.Connections.Add("OLEDB");  
      conMgr.ConnectionString = "Provider=SQLOLEDB.1;" +  
        "Data Source=<servername>;Initial Catalog=AdventureWorks;" +  
        "Integrated Security=SSPI;";  
      conMgr.Name = "SSIS Connection Manager for OLE DB";  
      conMgr.Description = "OLE DB connection to the AdventureWorks database.";  
  
      // Create and configure an OLE DB source component.    
      IDTSComponentMetaData100 source =  
        dataFlowTask.ComponentMetaDataCollection.New();  
      source.ComponentClassID = "DTSAdapter.OleDbSource";  
      // Create the design-time instance of the source.  
      CManagedComponentWrapper srcDesignTime = source.Instantiate();  
      // The ProvideComponentProperties method creates a default output.  
      srcDesignTime.ProvideComponentProperties();  
      // Assign the connection manager.  
      source.RuntimeConnectionCollection[0].ConnectionManager =  
        DtsConvert.GetExtendedInterface(conMgr);  
      // Set the custom properties of the source.  
      srcDesignTime.SetComponentProperty("AccessMode", 2);  
      srcDesignTime.SetComponentProperty("SqlCommand",  
        "Select * from Production.Product");  
  
      // Connect to the data source,  
      //  and then update the metadata for the source.  
      srcDesignTime.AcquireConnections(null);  
      srcDesignTime.ReinitializeMetaData();  
      srcDesignTime.ReleaseConnections();  
  
      // Create and configure an OLE DB destination.  
      IDTSComponentMetaData100 destination =  
        dataFlowTask.ComponentMetaDataCollection.New();  
      destination.ComponentClassID = "DTSAdapter.OleDbDestination";  
      // Create the design-time instance of the destination.  
      CManagedComponentWrapper destDesignTime = destination.Instantiate();  
      // The ProvideComponentProperties method creates a default input.  
      destDesignTime.ProvideComponentProperties();  
  
      // Create the path from source to destination.  
      IDTSPath100 path = dataFlowTask.PathCollection.New();  
      path.AttachPathAndPropagateNotifications(source.OutputCollection[0],  
        destination.InputCollection[0]);  
  
      // Get the destination's default input and virtual input.  
      IDTSInput100 input = destination.InputCollection[0];  
      IDTSVirtualInput100 vInput = input.GetVirtualInput();  
  
      // Iterate through the virtual input column collection.  
      foreach (IDTSVirtualInputColumn100 vColumn in vInput.VirtualInputColumnCollection)  
      {  
        // Call the SetUsageType method of the destination  
        //  to add each available virtual input column as an input column.  
        destDesignTime.SetUsageType(  
           input.ID, vInput, vColumn.LineageID, DTSUsageType.UT_READONLY);  
      }  
  
      // Verify that the columns have been added to the input.  
      foreach (IDTSInputColumn100 inputColumn in destination.InputCollection[0].InputColumnCollection)  
        Console.WriteLine(inputColumn.Name);  
      Console.Read();  
  
      // Add other components to the data flow and connect them.  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports Microsoft.SqlServer.Dts.Pipeline  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
  
Module Module1  
  
  Sub Main()  
  
    ' Create a package and add a Data Flow task.  
    Dim package As Microsoft.SqlServer.Dts.Runtime.Package = _  
      New Microsoft.SqlServer.Dts.Runtime.Package()  
    Dim e As Executable = package.Executables.Add("STOCK:PipelineTask")  
    Dim thMainPipe As Microsoft.SqlServer.Dts.Runtime.TaskHost = _  
      CType(e, Microsoft.SqlServer.Dts.Runtime.TaskHost)  
    Dim dataFlowTask As MainPipe = CType(thMainPipe.InnerObject, MainPipe)  
  
    ' Add an OLE DB connection manager to the package.  
    Dim conMgr As ConnectionManager = package.Connections.Add("OLEDB")  
    conMgr.ConnectionString = "Provider=SQLOLEDB.1;" & _  
      "Data Source=<servername>;Initial Catalog=AdventureWorks;" & _  
      "Integrated Security=SSPI;"  
    conMgr.Name = "SSIS Connection Manager for OLE DB"  
    conMgr.Description = "OLE DB connection to the AdventureWorks database."  
  
    ' Create and configure an OLE DB source component.    
    Dim source As IDTSComponentMetaData100 = _  
      dataFlowTask.ComponentMetaDataCollection.New  
    source.ComponentClassID = "DTSAdapter.OleDbSource"  
    ' Create the design-time instance of the source.  
    Dim srcDesignTime As CManagedComponentWrapper = source.Instantiate  
    ' The ProvideComponentProperties method creates a default output.  
    srcDesignTime.ProvideComponentProperties()  
    ' Assign the connection manager.  
    source.RuntimeConnectionCollection(0).ConnectionManager = _  
      DtsConvert.GetExtendedInterface(conMgr)  
    ' Set the custom properties of the source.  
    srcDesignTime.SetComponentProperty("AccessMode", 2)  
    srcDesignTime.SetComponentProperty("SqlCommand", _  
      "Select * from Production.Product")  
  
    ' Connect to the data source,  
    '  and then update the metadata for the source.  
    srcDesignTime.AcquireConnections(Nothing)  
    srcDesignTime.ReinitializeMetaData()  
    srcDesignTime.ReleaseConnections()  
  
    ' Create and configure an OLE DB destination.  
    Dim destination As IDTSComponentMetaData100 = _  
      dataFlowTask.ComponentMetaDataCollection.New  
    destination.ComponentClassID = "DTSAdapter.OleDbDestination"  
    ' Create the design-time instance of the destination.  
    Dim destDesignTime As CManagedComponentWrapper = destination.Instantiate  
    ' The ProvideComponentProperties method creates a default input.  
    destDesignTime.ProvideComponentProperties()  
  
    ' Create the path from source to destination.  
    Dim path As IDTSPath100 = dataFlowTask.PathCollection.New  
    path.AttachPathAndPropagateNotifications(source.OutputCollection(0), _  
      destination.InputCollection(0))  
  
    ' Get the destination's default input and virtual input.  
    Dim input As IDTSInput100 = destination.InputCollection(0)  
    Dim vInput As IDTSVirtualInput100 = input.GetVirtualInput  
  
    ' Iterate through the virtual input column collection.  
    For Each vColumn As IDTSVirtualInputColumn100 In vInput.VirtualInputColumnCollection  
      ' Call the SetUsageType method of the destination  
      '  to add each available virtual input column as an input column.  
      destDesignTime.SetUsageType(input.ID, vInput, vColumn.LineageID, DTSUsageType.UT_READONLY)  
    Next  
  
    ' Verify that the columns have been added to the input.  
    For Each inputColumn As IDTSInputColumn100 In destination.InputCollection(0).InputColumnCollection  
      Console.WriteLine(inputColumn.Name)  
    Next  
    Console.Read()  
  
    ' Add other components to the data flow and connect them.  
  
  End Sub  
  
End Module  
```  
  
![Ícone do Integration Services (pequeno)](../media/dts-16.gif "ícone do Integration Services (pequeno)")**mantenha-se para cima até o momento com o Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte também  
 [Salvar um pacote programaticamente](../building-packages-programmatically/saving-a-package-programmatically.md)  
  
  
