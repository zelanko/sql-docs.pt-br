---
title: Criar um componente de fluxo de dados personalizado | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- design-time component interface [Integration Services]
- custom data flow components [Integration Services], about data flow components
- custom data flow components [Integration Services]
- data flow components [Integration Services]
- data flow components [Integration Services], developing
ms.assetid: 9d96bcf5-eba8-44bd-b113-ed51ad0d0521
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f7acd3f9c218a068f5af09da21ec21b1fcf6e065
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86921252"
---
# <a name="creating-a-custom-data-flow-component"></a>Criando um componente de fluxo de dados personalizado

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  No [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], a tarefa de fluxo de dados expõe um modelo de objeto que permite que os desenvolvedores criem componentes de fluxo de dados personalizados, como fontes, transformações e destinos, usando o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] e o código gerenciado.  
  
 Uma tarefa de fluxo de dados consiste em componentes que contêm uma interface <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> e uma coleção de objetos <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100> que definem o movimento dos dados entre os componentes.  
  
> [!NOTE]  
>  Quando você cria um provedor personalizado, precisa atualizar o arquivo ProviderDescriptors.xml com os valores de coluna de metadados.  
  
## <a name="design-time-and-run-time"></a>Tempo de design e tempo de execução  
 Antes da execução, diz-se que a tarefa de fluxo de dados está em um estado de tempo de design, quando sofre alterações incrementais. As alterações podem incluir a adição ou remoção de componentes, a adição ou remoção dos objetos do caminho que conectam componentes e as alterações nos metadados dos componentes. Quando ocorrem alterações em metadados, o componente pode monitorar e reagir às alterações. Por exemplo, um componente pode desabilitar certas alterações ou fazer alterações adicionais em resposta a uma alteração. Em tempo de design, o designer interage com um componente através da interface <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSDesigntimeComponent100> em tempo de design.  
  
 No tempo de execução, a tarefa de fluxo de dados examina a sequência de componentes, prepara um plano de execução e gerencia um pool de threads de trabalho que executa o plano de trabalho. Embora cada thread de trabalho desempenhe algum trabalho interno à tarefa de fluxo de dados, a principal tarefa do thread de trabalho é chamar os métodos do componente através da interface <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeComponent100> em tempo de execução.  
  
## <a name="creating-a-component"></a>Criando um componente  
 Para criar um componente de fluxo de dados, você deve derivar uma classe da classe base <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>, aplicar a classe <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> e substituir os métodos apropriados da classe base. O <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> implementa as interfaces <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSDesigntimeComponent100> e <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeComponent100> e expõe os métodos para você substituir em seu componente.  
  
 Dependendo dos objetos usados pelo seu componente, seu projeto precisará de referências a alguns ou todos os assemblies seguintes:  
  
|Recurso|Assembly para referência|Namespace para importar|  
|-------------|---------------------------|-------------------------|  
|Fluxo de dados|Microsoft.SqlServer.PipelineHost|<xref:Microsoft.SqlServer.Dts.Pipeline>|  
|Wrapper de fluxo de dados|Microsoft.SqlServer.DTSPipelineWrap|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper>|  
|Runtime|Microsoft.SQLServer.ManagedDTS|<xref:Microsoft.SqlServer.Dts.Runtime>|  
|Wrapper de runtime|Microsoft.SqlServer.DTSRuntimeWrap|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper>|  
  
 O exemplo de código a seguir mostra um componente simples que deriva da classe base e aplica o <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute>. Você precisa adicionar uma referência ao assembly Microsoft.SqlServer.DTSPipelineWrap.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
  
namespace Microsoft.Samples.SqlServer.Dts  
{  
    [DtsPipelineComponent(DisplayName = "SampleComponent", ComponentType = ComponentType.Transform )]  
    public class BasicComponent: PipelineComponent  
    {  
        // TODO: Override the base class methods.  
    }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Pipeline  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
  
<DtsPipelineComponent(DisplayName:="SampleComponent", ComponentType:=ComponentType.Transform)> _  
Public Class BasicComponent  
  
    Inherits PipelineComponent  
  
    ' TODO: Override the base class methods.  
  
End Class  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Desenvolvendo uma interface do usuário para um componente de fluxo de dados](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-user-interface-for-a-data-flow-component.md)  
  
  
