---
title: Descobrir componentes de fluxo de dados programaticamente | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: building-packages-programmatically
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- PipelineComponentInfos collection
- data flow task [Integration Services], components
- discovering data flow components
- components [Integration Services], data flow
- data flow [Integration Services], components
ms.assetid: ff92a96a-8af6-4532-82cc-c0bbff92401b
caps.latest.revision: "44"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ad91fc10f1799978de74207f8b3bfae79c4d22b1
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="discovering-data-flow-components-programmatically"></a>Descobrindo componentes de fluxo de dados programaticamente
  Depois de adicionar uma tarefa de fluxo de dados a um pacote, sua próxima etapa será determinar os componentes de fluxo de dados que estarão disponíveis para uso. Você pode descobrir programaticamente as fontes de fluxo de dados, as transformações e os destinos instalados e disponíveis no computador local. Para obter informações sobre como adicionar uma tarefa de fluxo de dados ao pacote, consulte [Adicionar a tarefa de fluxo de dados programaticamente](../../integration-services/building-packages-programmatically/adding-the-data-flow-task-programmatically.md).  
  
## <a name="discovering-components"></a>Descobrindo componentes  
 A classe <xref:Microsoft.SqlServer.Dts.Runtime.Application> fornece a coleção <xref:Microsoft.SqlServer.Dts.Runtime.Application.PipelineComponentInfos%2A> que contém um objeto <xref:Microsoft.SqlServer.Dts.Runtime.PipelineComponentInfo> para cada componente corretamente instalado no computador local. Cada <xref:Microsoft.SqlServer.Dts.Runtime.PipelineComponentInfo> contém informações sobre um componente, como seu nome, sua descrição e seu nome de criação. É possível usar o valor retornado na propriedade <xref:Microsoft.SqlServer.Dts.Runtime.PipelineComponentInfo.CreationName%2A> para definir a propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ComponentClassID%2A> do <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> quando um componente for adicionado a um pacote.  
  
## <a name="next-step"></a>Próxima etapa  
 Depois de descobrir quais são os componentes disponíveis, a próxima etapa será adicionar e configurá-los, assunto que será discutido no próximo tópico, [Adicionar a tarefa de fluxo de dados programaticamente](../../integration-services/building-packages-programmatically/adding-data-flow-components-programmatically.md).  
  
## <a name="sample"></a>Amostra  
 O exemplo de código a seguir mostra como enumerar a coleção <xref:Microsoft.SqlServer.Dts.Runtime.PipelineComponentInfos> do objeto <xref:Microsoft.SqlServer.Dts.Runtime.Application> para descobrir programaticamente os componentes de fluxo de dados disponíveis no computador local. Esse exemplo precisa de uma referência ao assembly Microsoft.SqlServer.ManagedDTS.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Application application = new Application();  
      PipelineComponentInfos componentInfos = application.PipelineComponentInfos;  
  
      foreach (PipelineComponentInfo componentInfo in componentInfos)  
      {  
        Console.WriteLine("Name: " + componentInfo.Name + "\n" +  
          " CreationName: " + componentInfo.CreationName + "\n");  
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
  
    Dim application As Application = New Application()  
  
    Dim componentInfos As PipelineComponentInfos = application.PipelineComponentInfos  
  
    For Each componentInfo As PipelineComponentInfo In componentInfos  
      Console.WriteLine("Name: " & componentInfo.Name & vbCrLf & _  
        " CreationName: " & componentInfo.CreationName & vbCrLf)  
    Next  
  
    Console.Read()  
  
  End Sub  
  
End Module  
```
  
## <a name="see-also"></a>Consulte também  
 [Adicionar componentes de fluxo de dados programaticamente](../../integration-services/building-packages-programmatically/adding-data-flow-components-programmatically.md)  
  
  
