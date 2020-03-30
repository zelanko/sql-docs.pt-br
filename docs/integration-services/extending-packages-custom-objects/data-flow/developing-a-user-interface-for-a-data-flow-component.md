---
title: Desenvolvendo uma interface do usuário para um componente de fluxo de dados | Microsoft Docs
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
- data flow components [Integration Services], custom editors
- user interfaces [Integration Services]
- custom data flow components [Integration Services], custom editors
- custom component editors [Integration Services]
- IDtsComponentUI interface
- UITypeName property
- custom user interface [Integration Services], custom data flow component
- editors [Integration Services]
ms.assetid: 10b829a1-609b-42e3-9070-cfe5a2bb698c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 21bc28f99768c7b31d6ba5b18170140a23400853
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71287774"
---
# <a name="developing-a-user-interface-for-a-data-flow-component"></a>Desenvolvendo uma interface do usuário para um componente de fluxo de dados

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Os desenvolvedores de componentes podem fornecer uma interface de usuário personalizada para um componente, que é exibida no [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] quando o componente é editado. A implementação de uma interface de usuário personalizada fornece a você uma notificação quando o componente é adicionado a ou excluído de uma tarefa de fluxo de dados, e quando é solicitada ajuda para o componente.  
  
 Se você não fornecer uma interface de usuário personalizada para seu componente, os usuários ainda poderão configurar o componente e suas propriedades personalizadas utilizando o Editor Avançado. Para certificar-se de que o Editor Avançado permita aos usuários editar valores de propriedade personalizados adequadamente, utilize as propriedades <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100.TypeConverter%2A> e <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100.UITypeEditor%2A> do <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100> quando apropriado. Para obter mais informações, consulte "Criando propriedades personalizadas" em [Métodos de tempo de design de um componente de fluxo de dados](../../../integration-services/extending-packages-custom-objects/data-flow/design-time-methods-of-a-data-flow-component.md).  
  
## <a name="setting-the-uitypename-property"></a>Definindo a propriedade UITypeName  
 Para fornecer uma interface de usuário personalizada, o desenvolvedor deve definir a propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.UITypeName%2A> do <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> como o nome de uma classe que implementa a interface <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI>. Quando essa propriedade é definida pelo componente, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] carrega e chama a interface do usuário personalizada quando o componente é editado no Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)].  
  
 A propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.UITypeName%2A> é uma cadeia de caracteres delimitada por vírgulas que identifica o nome totalmente qualificado do tipo. A lista a seguir mostra, em ordem, os elementos que identificam o tipo:  
  
-   Nome do tipo  
  
-   Nome do assembly  
  
-   Versão do arquivo  
  
-   Cultura  
  
-   Token de chave pública  
  
 O exemplo de código a seguir mostra uma classe que deriva da classe base <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> e especifica a propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.UITypeName%2A>.  
  
```csharp  
[DtsPipelineComponent(  
DisplayName="SampleComponent",  
UITypeName="MyNamespace.MyComponentUIClassName,MyAssemblyName,Version=1.0.0.0,Culture=neutral,PublicKeyToken=abcd...",  
ComponentType = ComponentType.Transform)]  
public class SampleComponent : PipelineComponent  
{  
//TODO: Implement the component here.  
}  
```  
  
```vb  
<DtsPipelineComponent(DisplayName="SampleComponent", _  
UITypeName="MyNamespace.MyComponentUIClassName,MyAssemblyName,Version=1.0.0.0,Culture=neutral,PublicKeyToken=abcd...", ComponentType=ComponentType.Transform)> _   
Public Class SampleComponent   
 Inherits PipelineComponent   
End Class  
```  
  
## <a name="implementing-the-idtscomponentui-interface"></a>Implementando a interface IDtsComponentUI  
 A interface <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI> contém métodos que o Designer [!INCLUDE[ssIS](../../../includes/ssis-md.md)] chama quando um componente é adicionado, excluído e editado. Desenvolvedores de componente podem fornecer código na sua implementação desses métodos para interagir com usuários do componente.  
  
 Essa classe costuma ser implementada em um assembly separado do próprio componente. Embora o uso de um assembly separado não seja exigido, isso permite ao desenvolvedor criar e empregar o componente e a interface de usuário separadamente, e mantém a superfície binária do componente pequena.  
  
 A implementação de uma interface de usuário personalizada dá ao desenvolvedor de componente mais controle sobre o componente pois ele é editado no Designer [!INCLUDE[ssIS](../../../includes/ssis-md.md)]. Por exemplo, um componente pode adicionar código ao método <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI.New%2A>, que é chamado quando um componente é inicialmente adicionado a uma tarefa de fluxo de dados, e exibir um assistente que orienta o usuário na configuração inicial do componente.  
  
 Após criar uma classe que implementa a interface <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI>, adicione código para responder à interação do usuário com o componente. O método <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI.Initialize%2A> fornece a interface <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> do componente e é chamado antes dos métodos <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI.New%2A> e <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI.Edit%2A>. Essa referência deve ser armazenada em uma variável de membro particular e usada para modificar metadados do componente depois disso.  
  
## <a name="modifying-a-component-and-persisting-changes"></a>Modificando um componente e mantendo alterações  
 A interface <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> é fornecida como um parâmetro ao método <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI.Initialize%2A>. Essa referência deve ser armazenada em cache em uma variável de membro pelo código de interface de usuário e, depois, usada para modificar o componente em resposta à interação do usuário com a interface de usuário.  
  
 Embora você possa modificar o componente diretamente através da interface <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100>, é melhor criar uma instância do <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapper> utilizando o método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.Instantiate%2A>. Quando você edita o componente diretamente através da interface, ignora as garantias de validação dele. A vantagem de utilizar a instância de tempo de design do componente através do <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapper> é que você garante o controle pelo componente das alterações feitas nele.  
  
 O valor de retorno do método <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI.Edit%2A> determina se alterações feitas em um componente são mantidas ou descartadas. Quando esse método retorna **false**, todas as alterações são descartadas; **true** mantém as alterações no componente e marca o pacote que deve ser salvo.  
  
### <a name="using-the-services-of-the-ssis-designer"></a>Usando os serviços do Designer SSIS  
 O parâmetro **IServiceProvider** do método <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI.Initialize%2A> fornece acesso aos seguintes serviços do Designer [!INCLUDE[ssIS](../../../includes/ssis-md.md)]:  
  
|Serviço|DESCRIÇÃO|  
|-------------|-----------------|  
|<xref:Microsoft.SqlServer.Dts.Design.IDtsClipboardService>|Usado para determinar se o componente foi gerado como parte de uma operação copiar/colar ou recortar/colar.|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionService>|Usado acessar conexões existentes ou criar novas conexões no pacote.|  
|<xref:Microsoft.SqlServer.Dts.Design.IErrorCollectionService>|Usado para capturar eventos de componentes de fluxo de dados quando você precisa capturar todos os erros e avisos levantados pelo componente, em vez de receber apenas o último erro ou aviso.|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsVariableService>|Usado para acessar variáveis existentes ou criar novas variáveis no pacote.|  
|<xref:Microsoft.SqlServer.Dts.Design.IDtsPipelineEnvironmentService>|Usado por componentes de fluxo de dados para acessar a tarefa Fluxo de Dados pai e outros componentes no fluxo de dados. Esse recurso pode ser usado para desenvolver um componente como o Assistente para Dimensões de Alteração Lenta, que cria e conecta componentes de fluxo de dados adicionais, conforme necessário.|  
  
 Esses serviços oferecem aos desenvolvedores de componente a capacidade de acessar e criar objetos no pacote no qual o componente é carregado.  
  
## <a name="sample"></a>Amostra  
 O exemplo de código a seguir mostra a integração de uma classe de interface do usuário personalizada que implementa a interface <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI>, e um formulário do Windows que serve como o editor de um componente.  
  
### <a name="custom-user-interface-class"></a>Classe de interface do usuário personalizada  
 O código a seguir mostra a classe que implementa a interface <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI>. O método <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI.Edit%2A> cria o editor de componente e, depois, exibe o formulário. O valor de retorno do formulário determina se as alterações do componente são mantidas.  
  
```csharp  
using System;  
using System.Windows.Forms;  
using Microsoft.SqlServer.Dts.Runtime;  
using Microsoft.SqlServer.Dts.Pipeline.Design;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
  
namespace Microsoft.Samples.SqlServer.Dts  
{  
    public class SampleComponentUI : IDtsComponentUI  
    {  
        IDTSComponentMetaData100 md;  
        IServiceProvider sp;  
  
        public void Help(System.Windows.Forms.IWin32Window parentWindow)  
        {  
        }  
        public void New(System.Windows.Forms.IWin32Window parentWindow)  
        {  
        }  
        public void Delete(System.Windows.Forms.IWin32Window parentWindow)  
        {  
        }  
        public bool Edit(System.Windows.Forms.IWin32Window parentWindow, Variables vars, Connections cons)  
        {  
            // Create and display the form for the user interface.  
            SampleComponentUIForm componentEditor = new SampleComponentUIForm(cons, vars, md);  
  
            DialogResult result  = componentEditor.ShowDialog(parentWindow);  
  
            if (result == DialogResult.OK)  
                return true;  
  
            return false;  
        }  
        public void Initialize(IDTSComponentMetaData100 dtsComponentMetadata, IServiceProvider serviceProvider)  
        {  
            // Store the component metadata.  
            this.md = dtsComponentMetadata;  
        }  
    }  
}  
```  
  
```vb  
Imports System   
Imports System.Windows.Forms   
Imports Microsoft.SqlServer.Dts.Runtime   
Imports Microsoft.SqlServer.Dts.Pipeline.Design   
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper   
  
Namespace Microsoft.Samples.SqlServer.Dts   
  
 Public Class SampleComponentUI   
 Implements IDtsComponentUI   
   Private md As IDTSComponentMetaData100   
   Private sp As IServiceProvider   
  
   Public Sub Help(ByVal parentWindow As System.Windows.Forms.IWin32Window)   
   End Sub   
  
   Public Sub New(ByVal parentWindow As System.Windows.Forms.IWin32Window)   
   End Sub   
  
   Public Sub Delete(ByVal parentWindow As System.Windows.Forms.IWin32Window)   
   End Sub   
  
   Public Function Edit(ByVal parentWindow As System.Windows.Forms.IWin32Window, ByVal vars As Variables, ByVal cons As Connections) As Boolean   
     ' Create and display the form for the user interface.  
     Dim componentEditor As SampleComponentUIForm = New SampleComponentUIForm(cons, vars, md)   
     Dim result As DialogResult = componentEditor.ShowDialog(parentWindow)   
     If result = DialogResult.OK Then   
       Return True   
     End If   
     Return False   
   End Function   
  
   Public Sub Initialize(ByVal dtsComponentMetadata As IDTSComponentMetaData100, ByVal serviceProvider As IServiceProvider)   
     Me.md = dtsComponentMetadata   
   End Sub   
 End Class   
  
End Namespace  
```  
  
### <a name="custom-editor"></a>Editor personalizado  
 O código a seguir mostra a implementação do formulário do Windows que é mostrado durante a chamada ao método <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI.Edit%2A>.  
  
```csharp  
using System;  
using System.Drawing;  
using System.Collections;  
using System.ComponentModel;  
using System.Windows.Forms;  
using System.Data;  
  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.Samples.SqlServer.Dts  
{  
    public partial class SampleComponentUIForm : System.Windows.Forms.Form  
    {  
        private Connections connections;  
        private Variables variables;  
        private IDTSComponentMetaData100 metaData;  
        private CManagedComponentWrapper designTimeInstance;  
        private System.ComponentModel.IContainer components = null;  
  
        public SampleComponentUIForm( Connections cons, Variables vars, IDTSComponentMetaData100 md)  
        {  
            variables = vars;  
            connections = cons;  
            metaData = md;  
        }  
  
        private void btnOk_Click(object sender, System.EventArgs e)  
        {  
            if (designTimeInstance == null)  
                designTimeInstance = metaData.Instantiate();  
  
            designTimeInstance.SetComponentProperty( "CustomProperty", txtCustomPropertyValue.Text);  
  
            this.Close();  
        }  
  
        private void btnCancel_Click(object sender, System.EventArgs e)  
        {  
            this.Close();  
        }  
    }  
}  
```  
  
```vb  
Imports System   
Imports System.Drawing   
Imports System.Collections   
Imports System.ComponentModel   
Imports System.Windows.Forms   
Imports System.Data   
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper   
Imports Microsoft.SqlServer.Dts.Runtime   
  
Namespace Microsoft.Samples.SqlServer.Dts   
  
 Public Partial Class SampleComponentUIForm   
  Inherits System.Windows.Forms.Form   
   Private connections As Connections   
   Private variables As Variables   
   Private metaData As IDTSComponentMetaData100   
   Private designTimeInstance As CManagedComponentWrapper   
   Private components As System.ComponentModel.IContainer = Nothing   
  
   Public Sub New(ByVal cons As Connections, ByVal vars As Variables, ByVal md As IDTSComponentMetaData100)   
     variables = vars   
     connections = cons   
     metaData = md   
   End Sub   
  
   Private Sub btnOk_Click(ByVal sender As Object, ByVal e As System.EventArgs)   
     If designTimeInstance Is Nothing Then   
       designTimeInstance = metaData.Instantiate   
     End If   
     designTimeInstance.SetComponentProperty("CustomProperty", txtCustomPropertyValue.Text)   
     Me.Close   
   End Sub   
  
   Private Sub btnCancel_Click(ByVal sender As Object, ByVal e As System.EventArgs)   
     Me.Close   
   End Sub   
 End Class   
  
End Namespace  
```
  
## <a name="see-also"></a>Consulte Também  
 [Criar um componente de fluxo de dados personalizado](../../../integration-services/extending-packages-custom-objects/data-flow/creating-a-custom-data-flow-component.md)  
  
  
