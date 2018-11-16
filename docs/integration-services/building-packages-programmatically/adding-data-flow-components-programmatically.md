---
title: Adicionar componentes de fluxo de dados programaticamente | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.technology: integration-services
ms.reviewer: ''
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow task [Integration Services], components
- components [Integration Services], data flow
- data flow [Integration Services], components
ms.assetid: c06065cf-43e5-4b6b-9824-7309d7f5e35e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ee94fa73cbc7c148574c15ae136e9efaeea1e740
ms.sourcegitcommit: 0638b228980998de9056b177c83ed14494b9ad74
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/14/2018
ms.locfileid: "51639514"
---
# <a name="adding-data-flow-components-programmatically"></a>Adicionando componentes de fluxo de dados programaticamente
  Ao compilar um fluxo de dados, comece adicionando componentes. Em seguida, configure esses componentes e os conecte para estabelecer o fluxo de dados em tempo de execução. Esta seção descreve como adicionar um componente à tarefa de fluxo de dados, criar a instância tempo de design do componente e configurar o componente. Para obter informaçõessobre como conectar componentes, consulte [Conectar componentes do fluxo de dados programaticamente](../../integration-services/building-packages-programmatically/connecting-data-flow-components-programmatically.md).  
  
## <a name="adding-a-component"></a>Adicionando um componente  
 Chame o método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaDataCollection100.New%2A> da coleção <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.MainPipeClass.ComponentMetaDataCollection%2A> para criar um componente novo e adicioná-lo à tarefa de fluxo de dados. Este método retorna a interface <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> do componente. Contudo, neste momento, o <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> não contém informações específicas de nenhum componente. Defina a propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ComponentClassID%2A> para identificar o tipo de componente. A tarefa de fluxo de dados usa o valor dessa propriedade para criar uma instância do componente em tempo de execução.  
  
 O valor especificado na propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ComponentClassID%2A> pode ser o CLSID, o PROGID ou a propriedade <xref:Microsoft.SqlServer.Dts.Runtime.PipelineComponentInfo.CreationName%2A> do componente. O CLSID é exibido normalmente na janela Propriedades como o valor da propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ComponentClassID%2A> do componente. Para obter informações sobre como obter essa propriedade e outras propriedades de componentes disponíveis, consulte [Descobrir componentes de fluxo de dados programaticamente](../../integration-services/building-packages-programmatically/discovering-data-flow-components-programmatically.md).  
  
## <a name="adding-a-managed-component"></a>Adicionando um componente gerenciado  
 Não é possível usar o CLSID ou o PROGID para adicionar um dos componentes de fluxo de dados gerenciados ao fluxo de dados, pois esses valores apontam para um wrapper e não para o componente em si. Em vez disso, você pode usar a propriedade **CreationName** ou a propriedade **AssemblyQualifiedName** conforme mostrado no exemplo a seguir.  
  
 Se você pretende usar a propriedade **AssemblyQualifiedName**, você deve adicionar uma referência em seu projeto [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ao assembly que contém o componente gerenciado. Esses assemblies não são listados na guia .NET da caixa de diálogo **Adicionar Referência**. Normalmente, você deve navegar para localizar o assembly na pasta **C:\Program Files\Microsoft SQL Server\100\DTS\PipelineComponents**.  
  
 Os componentes de fluxo de dados gerenciados embutidos incluem:  
  
-   [!INCLUDE[vstecado](../../includes/vstecado-md.md)] Origem  
  
-   Origem XML  
  
-   Destino DataReader  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Destino Compact  
  
-   Componente Script  
  
 O exemplo de código seguinte mostra ambos os modos de adicionar um componente gerenciado ao fluxo de dados:  
  
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
      Microsoft.SqlServer.Dts.Runtime.Package package = new Microsoft.SqlServer.Dts.Runtime.Package();  
      Executable e = package.Executables.Add("STOCK:PipelineTask");  
      Microsoft.SqlServer.Dts.Runtime.TaskHost thMainPipe = (Microsoft.SqlServer.Dts.Runtime.TaskHost)e;  
      MainPipe dataFlowTask = (MainPipe)thMainPipe.InnerObject;  
  
      // The Application object will be used to obtain the CreationName  
      //  of a PipelineComponentInfo from its PipelineComponentInfos collection.  
      Application app = new Application();  
  
      // Add a first ADO NET source to the data flow.  
      //  The CreationName property requires an Application instance.  
      IDTSComponentMetaData100 component1 = dataFlowTask.ComponentMetaDataCollection.New();  
      component1.Name = "DataReader Source";  
      component1.ComponentClassID = app.PipelineComponentInfos["DataReader Source"].CreationName;  
  
      // Add a second ADO NET source to the data flow.  
      //  The AssemblyQualifiedName property requires a reference to the assembly.  
      IDTSComponentMetaData100 component2 = dataFlowTask.ComponentMetaDataCollection.New();  
      component2.Name = "DataReader Source";  
      component2.ComponentClassID = typeof(Microsoft.SqlServer.Dts.Pipeline.DataReaderSourceAdapter).AssemblyQualifiedName;  
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
  
    Dim package As Microsoft.SqlServer.Dts.Runtime.Package = _  
      New Microsoft.SqlServer.Dts.Runtime.Package()  
    Dim e As Executable = package.Executables.Add("STOCK:PipelineTask")  
    Dim thMainPipe As Microsoft.SqlServer.Dts.Runtime.TaskHost = _  
      CType(e, Microsoft.SqlServer.Dts.Runtime.TaskHost)  
    Dim dataFlowTask As MainPipe = CType(thMainPipe.InnerObject, MainPipe)  
  
    ' The Application object will be used to obtain the CreationName  
    '  of a PipelineComponentInfo from its PipelineComponentInfos collection.  
    Dim app As New Application()  
  
    ' Add a first ADO NET source to the data flow.  
    '  The CreationName property requires an Application instance.  
    Dim component1 As IDTSComponentMetaData100 = _  
      dataFlowTask.ComponentMetaDataCollection.New()  
    component1.Name = "DataReader Source"  
    component1.ComponentClassID = app.PipelineComponentInfos("DataReader Source").CreationName  
  
    ' Add a second ADO NET source to the data flow.  
    '  The AssemblyQualifiedName property requires a reference to the assembly.  
    Dim component2 As IDTSComponentMetaData100 = _  
      dataFlowTask.ComponentMetaDataCollection.New()  
    component2.Name = "DataReader Source"  
    component2.ComponentClassID = _  
      GetType(Microsoft.SqlServer.Dts.Pipeline.DataReaderSourceAdapter).AssemblyQualifiedName  
  
  End Sub  
  
End Module  
```  
  
## <a name="creating-the-design-time-instance-of-the-component"></a>Criando a instância tempo de design do componente  
 Chame o método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.Instantiate%2A> para criar a instância tempo de design do componente identificada pela propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ComponentClassID%2A>. Esse método retorna o objeto <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapper>, que é o wrapper gerenciado para a interface <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSDesigntimeComponent100>.  
  
 Sempre que possível, você deve modificar um componente usando os métodos da instância tempo de design em vez de modificar os metadados do componente diretamente. Embora existam itens nos metadados que você deve definir diretamente, como as conexões, em geral não se aconselha modificar os metadados diretamente, pois assim você ignora a capacidade do componente de monitorar e validar alterações.  
  
## <a name="assigning-connections"></a>Atribuindo conexões  
 Alguns componentes, como o componente Origem OLE DB, requerem uma conexão com dados externos e usam um objeto <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> existente no pacote para esse propósito. A propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeConnectionCollection100.Count%2A> da coleção <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.RuntimeConnectionCollection%2A> indica o número de objetos <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> em tempo de execução requeridos pelo componente. Se a contagem for maior que zero, o componente precisará de uma conexão. Atribua um gerenciador de conexões do pacote para o componente especificando as propriedades <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeConnection100.ConnectionManager%2A> e <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeConnection100.Name%2A> da primeira conexão no <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.RuntimeConnectionCollection%2A>. Observe que o nome do gerenciador de conexões na coleção de conexões em tempo de execução deve corresponder ao nome do gerenciador de conexões referenciado do pacote.  
  
## <a name="setting-the-values-of-custom-properties"></a>Definindo os valores de propriedades personalizadas  
 Depois de criar a instância tempo de design do componente, chame o método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapperClass.ProvideComponentProperties%2A>. Esse método é similar a um construtor por que ele inicializa um componente recém-criado criando suas propriedades personalizadas e seus objetos de entrada e saída. Não chame <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapperClass.ProvideComponentProperties%2A> mais de uma vez em um componente, pois o componente pode se redefinir e perder qualquer modificação feita em seus metadados anteriormente.  
  
 O <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.CustomPropertyCollection%2A> do componente contém uma coleção de objetos <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100> específicos ao componente. Ao contrário de outros modelos de programação, em que as propriedades de um objeto são sempre visíveis no objeto, os componentes preenchem somente suas coleções de propriedades personalizadas quando você chama o método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapperClass.ProvideComponentProperties%2A>. Depois de chamar o método, use o método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapperClass.SetComponentProperty%2A> da instância tempo de design do componente para atribuir valores a suas propriedades personalizadas. Esse método aceita um par nome/valor que identifica a propriedade personalizada e fornece seu valor novo.  
  
## <a name="initializing-output-columns"></a>Inicializando colunas de saída  
 Depois de adicionar um componente à tarefa e configurá-lo, inicialize a coleção de colunas no <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100> do objeto. Essa etapa é especialmente relevante para componentes de origem, mas não pode inicializar as colunas para componentes de transformação e destino, pois geralmente eles dependem das colunas que recebem dos componentes upstream.  
  
 Chame o método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapperClass.ReinitializeMetaData%2A> para inicializar as colunas nas saídas de um componente de origem. Como os componentes não se conectam automaticamente a fontes de dados externas, chame o método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapperClass.AcquireConnections%2A> antes de chamar <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapperClass.ReinitializeMetaData%2A> para fornecer ao componente acesso a sua fonte de dados externa e a capacidade de preencher os metadados da sua coluna. Finalmente, chame o método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapperClass.ReleaseConnections%2A> para liberar a conexão.  
  
## <a name="next-step"></a>Próxima etapa  
 Depois de adicionar e configurar o componente, a próxima etapa é criar caminhos entre componentes, que é discutido no tópico [Criando um caminho entre dois componentes](../../integration-services/building-packages-programmatically/connecting-data-flow-components-programmatically.md).  
  
## <a name="sample"></a>Amostra  
 O exemplo de código a seguir adiciona o componente Origem OLE DB a uma tarefa de fluxo de dados, cria uma instância tempo de design do componente e configura as propriedades do componente. Esse exemplo requer uma referência adicional ao assembly Microsoft.SqlServer.DTSRuntimeWrap.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
using Microsoft.SqlServer.Dts.Runtime.Wrapper;  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Runtime.Package package = new Runtime.Package();  
      Executable e = package.Executables.Add("STOCK:PipelineTask");  
      Runtime.TaskHost thMainPipe = e as Runtime.TaskHost;  
      MainPipe dataFlowTask = thMainPipe.InnerObject as MainPipe;  
  
      // Add an OLEDB connection manager to the package.  
      ConnectionManager cm = package.Connections.Add("OLEDB");  
      cm.Name = "OLEDB ConnectionManager";  
      cm.ConnectionString = "Data Source=(local);" +   
        "Initial Catalog=AdventureWorks;Provider=SQLOLEDB.1;" +   
        "Integrated Security=SSPI;"  
  
      // Add an OLE DB source to the data flow.  
      IDTSComponentMetaData100 component =   
        dataFlowTask.ComponentMetaDataCollection.New();  
      component.Name = "OLEDBSource";  
      component.ComponentClassID = "DTSAdapter.OleDbSource.1";  
      // You can also use the CLSID of the component instead of the PROGID.  
      //component.ComponentClassID = "{2C0A8BE5-1EDC-4353-A0EF-B778599C65A0}";  
  
      // Get the design time instance of the component.  
      CManagedComponentWrapper instance = component.Instantiate();  
  
      // Initialize the component  
      instance.ProvideComponentProperties();  
  
      // Specify the connection manager.  
      if (component.RuntimeConnectionCollection.Count > 0)  
      {  
        component.RuntimeConnectionCollection[0].ConnectionManager =   
          DtsConvert.GetExtendedInterface(package.Connections[0]);  
        component.RuntimeConnectionCollection[0].ConnectionManagerID =   
          package.Connections[0].ID;      }  
  
      // Set the custom properties.  
      instance.SetComponentProperty("AccessMode", 2);  
      instance.SetComponentProperty("SqlCommand",   
        "Select * from Production.Product");  
  
      // Reinitialize the metadata.  
      instance.AcquireConnections(null);  
      instance.ReinitializeMetaData();  
      instance.ReleaseConnections();  
  
      // Add other components to the data flow and connect them.  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports Microsoft.SqlServer.Dts.Runtime.Wrapper  
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
  
    ' Add an OLEDB connection manager to the package.  
    Dim cm As ConnectionManager = package.Connections.Add("OLEDB")  
    cm.Name = "OLEDB ConnectionManager"  
    cm.ConnectionString = "Data Source=(local);" & _  
      "Initial Catalog=AdventureWorks;Provider=SQLOLEDB.1;" & _  
      "Integrated Security=SSPI;"  
  
    ' Add an OLE DB source to the data flow.  
    Dim component As IDTSComponentMetaData100 = _  
      dataFlowTask.ComponentMetaDataCollection.New()  
    component.Name = "OLEDBSource"  
    component.ComponentClassID = "DTSAdapter.OleDbSource.1"  
    ' You can also use the CLSID of the component instead of the PROGID.  
    'component.ComponentClassID = "{2C0A8BE5-1EDC-4353-A0EF-B778599C65A0}";  
  
    ' Get the design time instance of the component.  
    Dim instance As CManagedComponentWrapper = component.Instantiate()  
  
    ' Initialize the component.  
    instance.ProvideComponentProperties()  
  
    ' Specify the connection manager.  
    If component.RuntimeConnectionCollection.Count > 0 Then  
      component.RuntimeConnectionCollection(0).ConnectionManager = _  
        DtsConvert.GetExtendedInterface(package.Connections(0))  
      component.RuntimeConnectionCollection(0).ConnectionManagerID = _  
        package.Connections(0).ID  
    End If  
  
    ' Set the custom properties.  
    instance.SetComponentProperty("AccessMode", 2)  
    instance.SetComponentProperty("SqlCommand", _  
      "Select * from Production.Product")  
  
    ' Reinitialize the metadata.  
    instance.AcquireConnections(vbNull)  
    instance.ReinitializeMetaData()  
    instance.ReleaseConnections()  
  
    ' Add other components to the data flow and connect them.  
  
  End Sub  
  
End Module  
```  
  
## <a name="external-resources"></a>Recursos externos  
 Entrada de blog, [EzAPI – Atualizado para SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=243223) em blogs.msdn.com.  

## <a name="see-also"></a>Consulte Também  
 [Conectar componentes de fluxo de dados programaticamente](../../integration-services/building-packages-programmatically/connecting-data-flow-components-programmatically.md)  
  
  
