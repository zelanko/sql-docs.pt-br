---
description: Adicionando a tarefa Fluxo de Dados programaticamente
title: Adicionar a tarefa de Fluxo de Dados programaticamente | Microsoft Docs
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
- adding Data Flow task
- SSIS data flow
- data flow task [Integration Services], adding
- MainPipe object
ms.assetid: 0ca03712-a82e-4aa7-949b-f869a8936ddf
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c5090cbe224a9ac3f94bff828189d3517c1dd376
ms.sourcegitcommit: 827ad02375793090fa8fee63cc372d130f11393f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2020
ms.locfileid: "89480770"
---
# <a name="adding-the-data-flow-task-programmatically"></a>Adicionando a tarefa Fluxo de Dados programaticamente

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  O [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] inclui uma tarefa chamada Fluxo de Dados, que é representada pelo namespace <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper> no modelo de objeto. A tarefa Fluxo de Dados é uma tarefa especializada, de alto desempenho, dedicada a transformar e mover dados durante a execução de pacotes. Assim como outras tarefas, a tarefa Fluxo de Dados é encapsulada pelo objeto <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> e, na perspectiva do mecanismo de tempo de execução, essa é apenas mais uma tarefa do pacote. Porém, o fluxo de dados contém objetos adicionais chamados de componentes de fluxo de dados. Esses são os componentes que fazem com que os dados se movam de uma origem para um destino, às vezes por uma transformação. Os componentes definem a direção do movimento e como os dados são transformados. A configuração da tarefa Fluxo de Dados envolve a adição de componentes à tarefa e, em seguida, a conexão desses componentes para estabelecer o fluxo de dados e conseguir a transformação pretendida.  
  
 Há três tipos de componentes em uma tarefa Fluxo de Dados: **Origens de Fluxo de Dados**, **Transformações de Fluxo de Dados** e **Destinos de Fluxo de Dados**, mostrados nesta ordem dentro da caixa de ferramentas do Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)]. Estes tipos também são referenciados simplesmente como origens, transformações ou destinos. Como os próprios nomes indicam, há um fluxo de dados de uma origem para uma transformação e, depois, para um destino. Esta é uma descrição simplificada do fluxo de dados para ilustrar o conceito, mas a tarefa Fluxo de Dados é flexível e eficiente o bastante para lidar com várias origens e conectar diversas transformações que enviam a saída a vários destinos.  
  
 A tarefa Fluxo de Dados é adicionada a um pacote da mesma forma que são adicionadas outras tarefas. Após a adição da tarefa, ela é configurada através da adição de componentes à tarefa de fluxo de dados, e da configuração e conexão de componentes na tarefa.  
  
## <a name="sample"></a>Amostra  
 O exemplo de código a seguir mostra como adicionar uma tarefa Fluxo de Dados a um pacote. Este exemplo exige uma referência aos assemblies Microsoft.SqlServer.PipelineHost, Microsoft.SqlServer.DTSPipelineWrap e Microsoft.SqlServer.ManagedDTS.  
  
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
      Package p = new Package();  
      Executable e = p.Executables.Add("STOCK:PipelineTask");  
      TaskHost thMainPipe = e as TaskHost;  
      MainPipe dataFlowTask = thMainPipe.InnerObject as MainPipe;   
    }  
  }  
}  
```  
  
```vb  
Imports System.IO  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports Microsoft.SqlServer.Dts.Pipeline  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
  
Module Module1  
  
  Sub Main()  
  
    Dim p As Package = New Package()  
    Dim e As Executable = p.Executables.Add("STOCK:PipelineTask")  
    Dim thMainPipe As TaskHost = CType(e, TaskHost)  
    Dim dataFlowTask As MainPipe = CType(thMainPipe.InnerObject, MainPipe)  
  
  End Sub  
  
End Module  
```  
  
## <a name="external-resources"></a>Recursos externos  
 Entrada no blog, [EzAPI – Updated for SQL Server 2012](https://techcommunity.microsoft.com/t5/sql-server-integration-services/ezapi-updated-for-sql-server-2012/ba-p/388042) (EzAPI – atualizado para o SQL Server 2012) em blogs.msdn.com.  
  
## <a name="see-also"></a>Consulte Também  
 [Descobrindo componentes de fluxo de dados programaticamente](../../integration-services/building-packages-programmatically/discovering-data-flow-components-programmatically.md)  
  
  
