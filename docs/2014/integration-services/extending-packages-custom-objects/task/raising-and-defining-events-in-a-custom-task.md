---
title: Acionar e definir eventos em uma tarefa personalizada | Microsoft Docs
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
- SSIS events, custom
- status information [SQL Server], task events
- custom tasks [Integration Services], events
- SSIS custom tasks, events
- IDTSComponentEvents interface
- events [Integration Services], custom
- events [Integration Services], runtime
- custom events [Integration Services]
- SSIS events, runtime
- IDTSEvents interface
ms.assetid: e0898aa1-e90c-4c4e-99d4-708a76efddfd
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: af647a446366ea03063ea0deb84603a3f8f90dd8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62896124"
---
# <a name="raising-and-defining-events-in-a-custom-task"></a>Gerando e definindo eventos em uma tarefa personalizada
  O mecanismo de tempo de execução do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] fornece uma coleção de eventos que fornecem o status do progresso de uma tarefa enquanto a tarefa é validada e executada. A interface do <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents> define esses eventos e é fornecida a tarefas como um parâmetro para os métodos <xref:Microsoft.SqlServer.Dts.Runtime.Executable.Validate%2A> e <xref:Microsoft.SqlServer.Dts.Runtime.Executable.Execute%2A>.  
  
 Há outro conjunto de eventos, definidos na interface do <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents>, que são gerados em nome da tarefa pelo <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>. O <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> gera eventos que ocorrem antes e depois da validação e da execução, enquanto a tarefa gera os eventos que ocorrem durante a execução e a validação.  
  
## <a name="creating-custom-events"></a>Criando eventos personalizados  
 Os desenvolvedores de tarefas personalizadas podem definir eventos novos e personalizados criando um novo <xref:Microsoft.SqlServer.Dts.Runtime.EventInfo> em sua implementação substituída do método <xref:Microsoft.SqlServer.Dts.Runtime.Task.InitializeTask%2A>. Depois que o <xref:Microsoft.SqlServer.Dts.Runtime.EventInfo> é criado, é acrescentado à coleção `EventInfos` usando o método <xref:Microsoft.SqlServer.Dts.Runtime.EventInfos.Add%2A>. A assinatura do método <xref:Microsoft.SqlServer.Dts.Runtime.EventInfos.Add%2A> é como segue:  
  
 `public void Add(string eventName, string description, bool allowEventHandlers, string[] parameterNames, TypeCode[] parameterTypes, string[] parameterDescriptions);`  
  
 O exemplo de código seguinte mostra o método `InitializeTask` de uma tarefa personalizada, em que são criados dois eventos personalizados e definidas suas propriedades. Os eventos novos são adicionados à coleção <xref:Microsoft.SqlServer.Dts.Runtime.EventInfos>.  
  
 O primeiro evento personalizado tem um *eventName* de "**OnBeforeIncrement**" e *descrição* de "**Aciona depois que o valor inicial é atualizado.**" O próximo parâmetro, o valor `true`, indica que este evento deve permitir que um contêiner de manipulador de eventos seja criado para tratar o evento. O manipulador de eventos é um contêiner que fornece estrutura em um pacote e serviços para tarefas, como outros contêineres, como pacote, Sequência, ForLoop e ForEachLoop. Quando o *allowEventHandlers* parâmetro é `true`, <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> objetos são criados para o evento. Qualquer parâmetro definido para o evento está agora disponível para o <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> na coleção de variáveis do <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler>.  
  
```csharp  
public override void InitializeTask(Connections connections,  
   VariableDispenser variables, IDTSInfoEvents events,  
   IDTSLogging log, EventInfos eventInfos,  
   LogEntryInfos logEntryInfos, ObjectReferenceTracker refTracker)  
{  
    this.eventInfos = eventInfos;  
    string[] paramNames = new string[1];  
    TypeCode[] paramTypes = new TypeCode[1]{TypeCode.Int32};  
    string[] paramDescriptions = new string[1];  
  
    paramNames[0] = "InitialValue";  
    paramDescriptions[0] = "The value before it is incremented.";  
  
    this.eventInfos.Add("OnBeforeIncrement",   
      "Fires before the task increments the value.",  
      true,paramNames,paramTypes,paramDescriptions);  
    this.onBeforeIncrement = this.eventInfos["OnBeforeIncrement"];  
  
    paramDescriptions[0] = "The value after it has been incremented.";  
    this.eventInfos.Add("OnAfterIncrement",  
      "Fires after the initial value is updated.",  
      true,paramNames, paramTypes,paramDescriptions);  
    this.onAfterIncrement = this.eventInfos["OnAfterIncrement"];  
}  
```  
  
```vb  
Public Overrides Sub InitializeTask(ByVal connections As Connections, _  
ByVal variables As VariableDispenser, ByVal events As IDTSInfoEvents, _  
ByVal log As IDTSLogging, ByVal eventInfos As EventInfos, _  
ByVal logEntryInfos As LogEntryInfos, ByVal refTracker As ObjectReferenceTracker)   
  
    Dim paramNames(0) As String  
    Dim paramTypes(0) As TypeCode = {TypeCode.Int32}  
    Dim paramDescriptions(0) As String  
  
    Me.eventInfos = eventInfos  
  
    paramNames(0) = "InitialValue"  
    paramDescriptions(0) = "The value before it is incremented."  
  
    Me.eventInfos.Add("OnBeforeIncrement", _  
      "Fires before the task increments the value.", _  
      True, paramNames, paramTypes, paramDescriptions)  
    Me.onBeforeIncrement = Me.eventInfos("OnBeforeIncrement")  
  
    paramDescriptions(0) = "The value after it has been incremented."  
    Me.eventInfos.Add("OnAfterIncrement", _  
      "Fires after the initial value is updated.", True, _  
      paramNames, paramTypes, paramDescriptions)  
    Me.onAfterIncrement = Me.eventInfos("OnAfterIncrement")  
  
End Sub  
```  
  
## <a name="raising-custom-events"></a>Gerando eventos personalizados  
 Eventos personalizados são gerados chamando-se o método <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireCustomEvent%2A>. A linha de código seguinte gera um evento personalizado.  
  
```csharp  
componentEvents.FireCustomEvent(this.onBeforeIncrement.Name,  
   this.onBeforeIncrement.Description, ref arguments,  
   null, ref bFireOnBeforeIncrement);  
```  
  
```vb  
componentEvents.FireCustomEvent(Me.onBeforeIncrement.Name, _  
Me.onBeforeIncrement.Description, arguments, _  
Nothing,  bFireOnBeforeIncrement)  
```  
  
## <a name="sample"></a>Amostra  
 O exemplo seguinte mostra uma tarefa que define um evento personalizado no método `InitializeTask`, adiciona o evento personalizado à coleção <xref:Microsoft.SqlServer.Dts.Runtime.EventInfos> e gera o evento personalizado durante seu método `Execute` chamando o método <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireCustomEvent%2A>.  
  
```csharp  
[DtsTask(DisplayName = "CustomEventTask")]  
    public class CustomEventTask : Task  
    {  
        public override DTSExecResult Execute(Connections connections,   
          VariableDispenser variableDispenser, IDTSComponentEvents componentEvents,  
           IDTSLogging log, object transaction)  
        {  
            bool fireAgain;  
            object[] args = new object[1] { "The value of the parameter." };  
            componentEvents.FireCustomEvent( "MyCustomEvent",   
              "Firing the custom event.", ref args,  
              "CustomEventTask" , ref fireAgain );  
            return DTSExecResult.Success;  
        }  
  
        public override void InitializeTask(Connections connections,  
          VariableDispenser variableDispenser, IDTSInfoEvents events,  
          IDTSLogging log, EventInfos eventInfos,  
          LogEntryInfos logEntryInfos, ObjectReferenceTracker refTracker)  
        {  
            string[] names = new string[1] {"Parameter1"};  
            TypeCode[] types = new TypeCode[1] {TypeCode.String};  
            string[] descriptions = new string[1] {"Parameter description." };  
  
            eventInfos.Add("MyCustomEvent",  
             "Fires when my interesting event happens.",  
             true, names, types, descriptions);  
  
        }  
   }  
```  
  
```vb  
<DtsTask(DisplayName = "CustomEventTask")> _   
    Public Class CustomEventTask  
     Inherits Task  
        Public Overrides Function Execute(ByVal connections As Connections, _  
          ByVal variableDispenser As VariableDispenser, _  
          ByVal componentEvents As IDTSComponentEvents, _  
          ByVal log As IDTSLogging, ByVal transaction As Object) _  
          As DTSExecResult  
  
            Dim fireAgain As Boolean  
            Dim args() As Object =  New Object(1) {"The value of the parameter."}  
  
            componentEvents.FireCustomEvent("MyCustomEvent", _  
              "Firing the custom event.", args, _  
              "CustomEventTask" ,  fireAgain)  
            Return DTSExecResult.Success  
        End Function  
  
        Public Overrides  Sub InitializeTask(ByVal connections As Connections, _  
          ByVal variableDispenser As VariableDispenser,  
          ByVal events As IDTSInfoEvents,  
          ByVal log As IDTSLogging, ByVal eventInfos As EventInfos, ByVal logEnTryInfos As LogEnTryInfos, ByVal refTracker As ObjectReferenceTracker)  
  
            Dim names() As String =  New String(1) {"Parameter1"}  
            Dim types() As TypeCode =  New TypeCode(1) {TypeCode.String}  
            Dim descriptions() As String =  New String(1) {"Parameter description."}  
  
            eventInfos.Add("MyCustomEvent", _  
              "Fires when my interesting event happens.", _  
              True, names, types, descriptions)  
  
        End Sub  
  
    End Class  
```  
  
![Ícone do Integration Services (pequeno)](../../media/dts-16.gif "ícone do Integration Services (pequeno)")**mantenha-se para cima até o momento com o Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte também  
 [Manipuladores de eventos do SSIS &#40;Integration Services&#41;](../../integration-services-ssis-event-handlers.md)   
 [Adicionar um manipulador de eventos a um pacote](../../add-an-event-handler-to-a-package.md)  
  
  
