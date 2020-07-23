---
title: Plano de execução e alocação de buffer | Microsoft Docs
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
- custom data flow components [Integration Services], buffer allocations
- custom data flow components [Integration Services], execution plans
- buffer allocations [Integration Services]
- data flow components [Integration Services], buffer allocations
- data flow components [Integration Services], execution plans
- execution plans [Integration Services]
ms.assetid: 679d9ff0-641e-47c3-abb8-d1a7dcb279dd
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 08a6b6b3e557b11cac28201b5dd246d296e6b15c
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86916152"
---
# <a name="execution-plan-and-buffer-allocation"></a>Plano de execução e alocação de buffer

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  Antes da execução, a tarefa de fluxo de dados examina seus componentes e gera um plano de execução para cada sequência de componentes. Essa seção fornece detalhes sobre o plano de execução, como visualizá-lo e como buffers de entrada e saída são alocados com base no plano de execução.  
  
## <a name="understanding-the-execution-plan"></a>Compreendendo o plano de execução  
 Um plano de execução contém threads de origem e threads de trabalho, e cada thread contém listas de trabalho que especificam listas de trabalho de saída para threads de origem ou listas de trabalho de entrada e saída para threads de trabalho. Os threads de origem em um plano de execução representam os componentes de origem no fluxo de dados e são identificados no plano de execução por *SourceThreadn*, em que *n* é o número com base em zero do thread de origem.  
  
 Cada thread de origem cria um buffer, define um ouvinte e chama o método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> no componente de origem. É nesse ponto que a execução é iniciada e dados são gerados, pois o componente de origem começa a adicionar linhas aos buffers de saída fornecidos pela tarefa de fluxo de dados. Depois do início da execução dos threads de origem, o balanço do trabalho é distribuído entre os threads de trabalho.  
  
 Um thread de trabalho pode conter listas de trabalho de entrada e saída e é identificado no plano de execução como *WorkThreadn*, em que *n* é o número com base em zero do thread de trabalho. Esses threads contêm listas de trabalho de saída quando o gráfico contém um componente com saídas assíncronas.  
  
 O exemplo de plano de execução a seguir representa um fluxo de dados que contém um componente de origem conectado a uma transformação com uma saída assíncrona conectada a um componente de destino. Nesse exemplo, o WorkThread0 contém uma lista de trabalho de saída porque o componente de transformação possui uma saída assíncrona.  
  
```  
SourceThread0   
    Influences: 72 158   
    Output Work List   
        CreatePrimeBuffer of type 1 for output id 10   
        SetBufferListener: "WorkThread0" for input ID 73   
        CallPrimeOutput on component "OLE DB Source" (1)   
    End Output Work List   
    This thread drives 0 distributors   
End SourceThread0   
WorkThread0   
    Influences: 72 158   
    Input Work list, input ID 73   
        CallProcessInput on input ID 73 on component "Sort" (72) for view type 2   
    End Input Work list for input 73   
    Output Work List   
        CreatePrimeBuffer of type 3 for output id 74   
        SetBufferListener: "WorkThread1" for input ID 171with internal handoff   
        CallPrimeOutput on component "Sort" (72)   
    End Output Work List   
    This thread drives 0 distributors   
End WorkThread0   
WorkThread1   
    Influences: 158   
    Input Work list, input ID 171  
        CallProcessInput on input ID 171 on component "OLE DB Destination" (158) for view type 4  
    End Input Work list for input 171   
    Output Work List   
    End Output Work List   
    This thread drives 0 distributors   
End WorkThread1  
```  
  
> [!NOTE]  
>  O plano de execução é gerado toda vez que um pacote é executado. Para capturá-lo, adicione um provedor de logs ao pacote, habilite o registro em log e selecione o evento **PipelineExecutionPlan**.  
  
## <a name="understanding-buffer-allocation"></a>Compreendendo a alocação de buffers  
 Com base no plano de execução, a tarefa de fluxo de dados cria buffers contendo as colunas definidas nas saídas dos componentes de fluxo de dados. O buffer é reutilizado como os fluxos de dados pela sequência de componentes, até ser encontrado um componente com saídas assíncronas. Portanto, é criado um buffer novo, que contém as colunas de saída da saída assíncrona e as colunas de saída de componentes downstream.  
  
 Durante a execução, componentes têm acesso ao buffer na origem atual ou thread de trabalho. O buffer é de entrada, fornecido pelo método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A>, ou de saída, fornecido pelo método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A>. A propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.Mode%2A> do <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer> também identifica cada buffer como um buffer de entrada ou de saída.  
  
 Os componentes de transformação com saídas assíncronas recebem o buffer de entrada existente do método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> e recebem o novo buffer de saída do método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A>. Um componente de transformação com saídas assíncronas é o único tipo de componente de fluxo de dados que recebe um buffer de entrada e saída.  
  
 Já que é provável que o buffer fornecido a um componente contenha mais colunas do que o componente tem em suas coleções de colunas de entrada ou saída, desenvolvedores de componentes podem chamar o método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSBufferManager100.FindColumnByLineageID%2A> para localizar uma coluna no buffer, especificando seu **LineageID**.  
  
