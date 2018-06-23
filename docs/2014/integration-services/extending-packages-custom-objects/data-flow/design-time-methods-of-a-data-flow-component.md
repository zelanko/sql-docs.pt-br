---
title: Métodos de tempo de design de um componente de fluxo de dados | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- integration-services
ms.tgt_pltfrm: ''
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom data flow components [Integration Services], method execution sequence
- ProcessInput method
- method execution sequence [Integration Services]
- PrimeOutput method
- data flow components [Integration Services], method execution sequence
ms.assetid: b5a121a1-b87c-441b-a42c-2cec628dc81c
caps.latest.revision: 57
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: f2347e035bf6dd0cf78ebccfd61b19d9a6f2901e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36019846"
---
# <a name="design-time-methods-of-a-data-flow-component"></a>Métodos de tempo de design de um componente de fluxo de dados
  Antes da execução, diz-se que a tarefa de fluxo de dados está em um estado de tempo de design, quando sofre alterações incrementais. As alterações podem incluir a adição ou remoção de componentes, a adição ou remoção dos objetos do caminho que conectam componentes e as alterações nos metadados dos componentes. Quando ocorrem alterações em metadados, o componente pode monitorar e reagir às alterações. Por exemplo, um componente pode desabilitar certas alterações ou fazer alterações adicionais em resposta a uma alteração. Em tempo de design, o designer interage com um componente através da interface <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSDesigntimeComponent100> em tempo de design.  
  
## <a name="design-time-implementation"></a>Implementação de tempo de design  
 A interface tempo de design de um componente é descrita pela interface <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSDesigntimeComponent100>. Embora você não implemente essa interface explicitamente, uma familiaridade com os métodos definidos nessa interface ajuda você a entender quais métodos da classe base <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> correspondem à instância de tempo de design de um componente.  
  
 Quando um componente é carregado no [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], a instância de tempo de design do componente é instanciada e os métodos da interface <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSDesigntimeComponent100> são chamados à medida que o componente é editado. A implementação da classe base o deixa anular somente os métodos que seu componente requer. Em muitos casos, você pode anular esses métodos para impedir edições inadequadas a um componente. Por exemplo, para impedir os usuários de acrescentarem uma saída a um componente, anule o método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.InsertOutput%2A>. Caso contrário, quando a implementação desse método pela classe base for chamada, ela acrescentará uma saída ao componente.  
  
 Independentemente do propósito ou funcionalidade de seu componente, você deve anular os métodos <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A>, <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A> e <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReinitializeMetaData%2A>. Para obter mais informações sobre <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A> e <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReinitializeMetaData%2A>, consulte [Validar um componente de fluxo de dados](validating-a-data-flow-component.md).  
  
## <a name="providecomponentproperties-method"></a>Método ProvideComponentProperties  
 A inicialização de um componente ocorre no método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A>. Esse método é chamado pelo [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer quando um componente é acrescentado à tarefa de fluxo de dados, e é semelhante a um construtor de classe. Desenvolvedores de componente devem criar e inicializar suas entradas, saídas e propriedades personalizadas durante essa chamada de método. O método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A> difere de um construtor por que não é chamado toda vez que a instância de tempo de design ou a instância de tempo de execução do componente é instanciada.  
  
 A implementação da classe base do método acrescenta uma entrada e uma saída ao componente e atribui a ID da entrada à propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100.SynchronousInputID%2A>. Porém, no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], os objetos de entrada e saída adicionados pela classe base não são nomeados. Os pacotes que contêm um componente com objetos de entrada ou saída cuja propriedade Name não está definida não são carregados com êxito. Portanto, quando você usar a implementação de base, você deverá atribuir valores explicitamente à propriedade Name da entrada e saída padrão.  
  
```csharp  
public override void ProvideComponentProperties()  
{  
    /// TODO: Reset the component.  
    /// TODO: Add custom properties.  
    /// TODO: Add input objects.  
    /// TODO: Add output objects.  
}  
```  
  
```vb  
Public Overrides Sub ProvideComponentProperties()  
    ' TODO: Reset the component.  
    ' TODO: Add custom properties.  
    ' TODO: Add input objects.  
    ' TODO: Add output objects.  
End Sub  
```  
  
### <a name="creating-custom-properties"></a>Criando propriedades personalizadas  
 A chamada para o método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A> é onde os desenvolvedores de componente deveriam acrescentar propriedades personalizadas (<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100>) ao componente. Propriedades personalizadas não têm uma propriedade de tipo de dados. O tipo de dados de uma propriedade personalizada é definido pelo tipo de dados do valor que você atribui a sua propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100.Value%2A>. Porém, depois que você atribuir um valor inicial à propriedade personalizada, não poderá atribuir um valor com um tipo de dados diferente.  
  
> [!NOTE]  
>  A interface <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100> tem suporte limitado para valores de propriedade do tipo `Object`. O único objeto que você pode armazenar como valor de uma propriedade personalizada é uma matriz de tipos simples, como cadeias de caracteres ou inteiros.  
  
 Você pode indicar se sua propriedade personalizada suporta expressões de propriedade definindo o valor da sua propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100.ExpressionType%2A> para `CPET_NOTIFY` da enumeração <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSCustomPropertyExpressionType>, conforme demonstrado no exemplo seguinte. Você não tem que adicionar qualquer código para tratar ou validar a expressão de propriedade inserida pelo usuário. Você pode definir um valor padrão para a propriedade, validar seu valor e ler e usar esse valor normalmente.  
  
```csharp  
IDTSCustomProperty100 myCustomProperty;  
...  
myCustomProperty.ExpressionType = DTSCustomPropertyExpressionType.CPET_NOTIFY;  
```  
  
```vb  
Dim myCustomProperty As IDTSCustomProperty100  
...  
myCustomProperty.ExpressionType = DTSCustomPropertyExpressionType.CPET_NOTIFY  
```  
  
 Você pode limitar os usuários a selecionar um valor da propriedade personalizada de uma enumeração usando o <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100.TypeConverter%2A> propriedade, conforme mostrado no exemplo a seguir, que assume que você definiu uma enumeração pública chamada `MyValidValues`.  
  
```csharp  
IDTSCustomProperty100 customProperty = outputColumn.CustomPropertyCollection.New();  
customProperty.Name = "My Custom Property";  
// This line associates the type with the custom property.  
customProperty.TypeConverter = typeof(MyValidValues).AssemblyQualifiedName;  
// Now you can use the enumeration values directly.  
customProperty.Value = MyValidValues.ValueOne;    
```  
  
```vb  
Dim customProperty As IDTSCustomProperty100 = outputColumn.CustomPropertyCollection.New   
customProperty.Name = "My Custom Property"   
' This line associates the type with the custom property.  
customProperty.TypeConverter = GetType(MyValidValues).AssemblyQualifiedName   
' Now you can use the enumeration values directly.  
customProperty.Value = MyValidValues.ValueOne  
```  
  
 Para obter mais informações, consulte "Conversão do tipo generalizada" e "Implementando um conversor de tipo" na [Biblioteca MSDN](http://go.microsoft.com/fwlink/?LinkId=7022).  
  
 Você pode especificar uma caixa de diálogo do editor personalizado para o valor da sua propriedade personalizada usando a propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100.UITypeEditor%2A>, conforme demonstrado no exemplo a seguir. Em primeiro lugar, é preciso criar um editor do tipo personalizado que herde do `System.Drawing.Design.UITypeEditor`, caso você não consiga localizar uma classe de editor do tipo de interface do usuário existente adequada às suas necessidades.  
  
```csharp  
public class MyCustomTypeEditor : UITypeEditor  
{  
...  
}  
```  
  
```vb  
Public Class MyCustomTypeEditor  
  Inherits UITypeEditor   
  ...  
End Class  
```  
  
 Em seguida, especifique essa classe como o valor da propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100.UITypeEditor%2A> da sua propriedade personalizada.  
  
```csharp  
IDTSCustomProperty100 customProperty = outputColumn.CustomPropertyCollection.New();  
customProperty.Name = "My Custom Property";  
// This line associates the editor with the custom property.  
customProperty.UITypeEditor = typeof(MyCustomTypeEditor).AssemblyQualifiedName;  
```  
  
```vb  
Dim customProperty As IDTSCustomProperty100 = outputColumn.CustomPropertyCollection.New   
customProperty.Name = "My Custom Property"   
' This line associates the editor with the custom property.  
customProperty.UITypeEditor = GetType(MyCustomTypeEditor).AssemblyQualifiedName  
```  
  
 Para obter mais informações, consulte "Implementando um editor do tipo de interface do usuário" na [Biblioteca MSDN](http://go.microsoft.com/fwlink/?LinkId=7022).  
  
![Ícone do Integration Services (pequeno)](../../media/dts-16.gif "ícone do Integration Services (pequeno)")**permanecer acima para data com o Integration Services** <br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos de tempo de execução de um componente de fluxo de dados](run-time-methods-of-a-data-flow-component.md)  
  
  