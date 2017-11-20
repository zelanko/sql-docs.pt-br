---
title: Gerando e definindo eventos em dados de um componente de fluxo | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-custom-objects
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow components [Integration Services], events
- events [Integration Services], custom
- custom events [Integration Services]
- custom data flow components [Integration Services], events
- events [Integration Services], raising
- predefined events [Integration Services]
ms.assetid: 1d8c5358-9384-47a8-b7cb-7b0650384119
caps.latest.revision: 51
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: a900b27c9056d95fb2284d8ba9d6b09d9c6635b5
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="raising-and-defining-events-in-a-data-flow-component"></a>Gerando e definindo eventos em um componente de fluxo de dados
  Desenvolvedores de componente podem gerar um subconjunto dos eventos definidos na interface <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents> por meio de chamada dos métodos expostos na propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ComponentMetaData%2A>. Você também pode definir eventos personalizados usando a coleção <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.EventInfos%2A> e gerá-los durante a execução usando o método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireCustomEvent%2A>. Esta seção descreve como criar e gerar um evento, e fornece diretrizes sobre quando você deve gerar eventos em tempo de design.  
  
## <a name="raising-events"></a>Gerando eventos  
 Componentes geram eventos usando o **incêndio\<X >** métodos do <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> interface. Você pode gerar eventos durante o design e a execução do componente. Em geral, durante o design do componente, os métodos <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireError%2A> e <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireWarning%2A> são chamados durante a validação. Esses eventos exibem mensagens no **lista de erros** painel de [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] e fornecer comentários para usuários do componente quando um componente é configurado incorretamente.  
  
 Os componentes também podem gerar eventos a qualquer momento durante a execução. Eventos permitem aos desenvolvedores de componentes fornecer comentários a usuários do componente durante sua execução. É provável que a chamada do método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireError%2A> durante a execução leve à falha do pacote.  
  
## <a name="defining-and-raising-custom-events"></a>Definindo e gerando eventos personalizados  
  
### <a name="defining-a-custom-event"></a>Definindo um evento personalizado  
 Eventos personalizados são criados chamando o método <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.IDTSEventInfos100.Add%2A> da coleção <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.EventInfos%2A>. Esta coleção é definida pela tarefa de fluxo de dados e fornecida como uma propriedade para o desenvolvedor de componente através da classe base <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>. Esta classe contém eventos personalizados definidos pela tarefa de fluxo de dados e eventos personalizados definidos pelo componente durante o método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.RegisterEvents%2A>.  
  
 Os eventos personalizados de um componente não persistem no pacote XML. Portanto, o método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.RegisterEvents%2A> é chamado durante o design e a execução para permitir que o componente defina os eventos gerados por ele.  
  
 O *allowEventHandlers* parâmetro o <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.IDTSEventInfos100.Add%2A> método Especifica se o componente permite <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> objetos a serem criados para o evento. Observe que <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandlers> são síncronos. Portanto, o componente não retomará a execução até que um <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> anexado ao evento personalizado termine a execução. Se o *allowEventHandlers* parâmetro é **true**, cada parâmetro do evento se torna automaticamente disponível para qualquer <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> objetos por meio de variáveis que são criadas e preenchidas automaticamente pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] tempo de execução.  
  
### <a name="raising-a-custom-event"></a>Gerando um evento personalizado  
 Componentes geram eventos personalizados chamando o método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireCustomEvent%2A> e fornecendo o nome, texto e parâmetros do evento. Se o *allowEventHandlers* parâmetro é **true**, qualquer <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandlers> que são criados para o evento personalizado são executados pelo [!INCLUDE[ssIS](../../../includes/ssis-md.md)] mecanismo de tempo de execução.  
  
### <a name="custom-event-sample"></a>Exemplo de evento personalizado  
 O exemplo de código a seguir mostra um componente que define um texto personalizado durante o método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.RegisterEvents%2A> e, depois, gera o evento em tempo de execução chamando o método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireCustomEvent%2A>.  
  
```csharp  
public override void RegisterEvents()  
{  
    string [] parameterNames = new string[2]{"RowCount", "StartTime"};  
    ushort [] parameterTypes = new ushort[2]{ DtsConvert.VarTypeFromTypeCode(TypeCode.Int32), DtsConvert.VarTypeFromTypeCode(TypeCode.DateTime)};  
    string [] parameterDescriptions = new string[2]{"The number of rows to sort.", "The start time of the Sort operation."};  
    EventInfos.Add("StartingSort","Fires when the component begins sorting the rows.",false,ref parameterNames, ref paramterTypes, ref parameterDescriptions);  
}  
public override void ProcessInput(int inputID, PipelineBuffer buffer)  
{  
    while (buffer.NextRow())  
    {  
       // Process buffer rows.  
    }  
  
    IDTSEventInfo100 eventInfo = EventInfos["StartingSort"];  
    object []arguments = new object[2]{buffer.RowCount, DateTime.Now };  
    ComponentMetaData.FireCustomEvent("StartingSort", "Beginning sort operation.", ref arguments, ComponentMetaData.Name, ref FireSortEventAgain);  
}  
```  
  
```vb  
Public  Overrides Sub RegisterEvents()   
  Dim parameterNames As String() = New String(2) {"RowCount", "StartTime"}   
  Dim parameterTypes As System.UInt16() = New System.UInt16(2) {DtsConvert.VarTypeFromTypeCode(TypeCode.Int32), DtsConvert.VarTypeFromTypeCode(TypeCode.DateTime)}   
  Dim parameterDescriptions As String() = New String(2) {"The number of rows to sort.", "The start time of the Sort operation."}   
  EventInfos.Add("StartingSort", "Fires when the component begins sorting the rows.", False, parameterNames, paramterTypes, parameterDescriptions)   
End Sub   
  
Public  Overrides Sub ProcessInput(ByVal inputID As Integer, ByVal buffer As PipelineBuffer)   
  While buffer.NextRow   
  End While   
  Dim eventInfo As IDTSEventInfo100 = EventInfos("StartingSort")   
  Dim arguments As Object() = New Object(2) {buffer.RowCount, DateTime.Now}   
  ComponentMetaData.FireCustomEvent("StartingSort", _  
    "Beginning sort operation.", arguments, _  
    ComponentMetaData.Name, FireSortEventAgain)   
End Sub  
```  

## <a name="see-also"></a>Consulte também  
 [Integration Services &#40; SSIS &#41; Manipuladores de eventos](../../../integration-services/integration-services-ssis-event-handlers.md)   
 [Adicionar um manipulador de eventos a um pacote](http://msdn.microsoft.com/library/5e56885d-8658-480a-bed9-3f2f8003fd78)  
  
  

