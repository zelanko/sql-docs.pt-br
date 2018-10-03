---
title: Conectar componentes de fluxo de dados programaticamente | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow task [Integration Services], components
- paths [Integration Services], components
- components [Integration Services], data flow
- data flow [Integration Services], components
ms.assetid: 404ecab7-7698-447b-93d6-dd256beb11ff
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8074535e3361e8f4694877ab09dcacb940cb8a84
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47748044"
---
# <a name="connecting-data-flow-components-programmatically"></a>Conectando componentes de fluxo de dados programaticamente
  Depois de adicionar componentes à tarefa de fluxo de dados, conecte-os para criar uma árvore de execução que represente o fluxo de dados das origens às transformações nos destinos. Você usa objetos <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100> para conectar os componentes no fluxo de dados.  
  
## <a name="creating-a-path"></a>Criando um caminho  
 Chame o método New da propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.MainPipeClass.PathCollection%2A> da interface <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.MainPipe> para criar um caminho novo e adicioná-lo à coleção de caminhos na tarefa de fluxo de dados. Esse método retorna um objeto <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100> novo, desconectado a ser usado para conectar dois componentes.  
  
 Chame o método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100.AttachPathAndPropagateNotifications%2A> para conectar o caminho e notificar os componentes que participam do caminho de que eles foram conectados. Esse método aceita um <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100> do componente upstream e um <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100> do componente downstream como parâmetros. Por padrão, a chamada ao método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A> do componente cria uma única entrada para componentes que têm entradas e uma única saída para componentes que têm saídas. O exemplo a seguir usa essa saída padrão da origem e a entrada do destino.  
  
## <a name="next-step"></a>Próxima etapa  
 Depois de estabelecer um caminho entre dois componentes, a próxima etapa é mapear colunas de entrada no componente downstream, discutida no próximo tópico, [Selecionar colunas de entrada programaticamente](../../integration-services/building-packages-programmatically/selecting-input-columns-programmatically.md).  
  
## <a name="sample"></a>Amostra  
 O exemplo de código a seguir mostra como estabelecer um caminho entre dois componentes.  
  
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
      Package package = new Package();  
      Executable e = package.Executables.Add("STOCK:PipelineTask");  
      TaskHost thMainPipe = e as TaskHost;  
      MainPipe dataFlowTask = thMainPipe.InnerObject as MainPipe;  
  
      // Create the source component.    
      IDTSComponentMetaData100 source =  
        dataFlowTask.ComponentMetaDataCollection.New();  
      source.ComponentClassID = "DTSAdapter.OleDbSource";  
      CManagedComponentWrapper srcDesignTime = source.Instantiate();  
      srcDesignTime.ProvideComponentProperties();  
  
      // Create the destination component.  
      IDTSComponentMetaData100 destination =  
        dataFlowTask.ComponentMetaDataCollection.New();  
      destination.ComponentClassID = "DTSAdapter.OleDbDestination";  
      CManagedComponentWrapper destDesignTime = destination.Instantiate();  
      destDesignTime.ProvideComponentProperties();  
  
      // Create the path.  
      IDTSPath100 path = dataFlowTask.PathCollection.New();  
      path.AttachPathAndPropagateNotifications(source.OutputCollection[0],  
        destination.InputCollection[0]);  
    }  
  }  
```  
  
 }  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports Microsoft.SqlServer.Dts.Pipeline  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
  
Module Module1  
  
  Sub Main()  
  
    Dim package As Microsoft.SqlServer.Dts.Runtime.Package = _  
      New Microsoft.SqlServer.Dts.Runtime.Package()  
    Dim e As Executable = package.Executables.Add("STOCK:PipelineTask")  
    Dim thMainPipe As Microsoft.SqlServer.Dts.Runtime.TaskHost = _  
      CType(e, Microsoft.SqlServer.Dts.Runtime.TaskHost)  
    Dim dataFlowTask As MainPipe = CType(thMainPipe.InnerObject, MainPipe)  
  
    ' Create the source component.    
    Dim source As IDTSComponentMetaData100 = _  
      dataFlowTask.ComponentMetaDataCollection.New()  
    source.ComponentClassID = "DTSAdapter.OleDbSource"  
    Dim srcDesignTime As CManagedComponentWrapper = source.Instantiate()  
    srcDesignTime.ProvideComponentProperties()  
  
    ' Create the destination component.  
    Dim destination As IDTSComponentMetaData100 = _  
      dataFlowTask.ComponentMetaDataCollection.New()  
    destination.ComponentClassID = "DTSAdapter.OleDbDestination"  
    Dim destDesignTime As CManagedComponentWrapper = destination.Instantiate()  
    destDesignTime.ProvideComponentProperties()  
  
    ' Create the path.  
    Dim path As IDTSPath100 = dataFlowTask.PathCollection.New()  
    path.AttachPathAndPropagateNotifications(source.OutputCollection(0), _  
      destination.InputCollection(0))  
  
  End Sub  
  
End Module  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Selecionar colunas de entrada programaticamente](../../integration-services/building-packages-programmatically/selecting-input-columns-programmatically.md)  
  
  
