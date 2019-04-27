---
title: Desenvolver uma interface do usuário para uma tarefa personalizada | Microsoft Docs
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
- custom user interfaces [Integration Services]
- IDtsTaskUI interface
- DtsTaskAttribute attribute
- custom tasks [Integration Services], user interface
- custom user interface [Integration Services], custom tasks
- user interface [Integration Services]
- SSIS custom tasks, user interface
ms.assetid: 1e940cd1-c5f8-4527-b678-e89ba5dc398a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6268fe16c31c931dc71ad1a62bd72e08b1ecb537
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62768892"
---
# <a name="developing-a-user-interface-for-a-custom-task"></a>Desenvolvendo uma interface do usuário para uma tarefa personalizada
  O modelo de objeto do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] permite que desenvolvedores de tarefas personalizadas criem facilmente uma interface de usuário personalizada para uma tarefa que pode ser integrada e exibida no [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]. A interface de usuário pode fornecer informações úteis para o usuário no Designer [!INCLUDE[ssIS](../../../includes/ssis-md.md)], e orientar usuários na configuração correta das propriedades e definições da tarefa personalizada.  
  
 O desenvolvimento de uma interface de usuário personalizada para uma tarefa envolve o uso de duas classes importantes. A tabela a seguir descreve essas classes.  
  
|Classe|Descrição|  
|-----------|-----------------|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute>|Um atributo que identifica uma tarefa gerenciada e fornece informações em tempo de design através de suas propriedades para controlar como o Designer [!INCLUDE[ssIS](../../../includes/ssis-md.md)] exibe e interage com o objeto.|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI>|Uma interface usada pela tarefa para associar a tarefa com sua interface de usuário personalizada.|  
  
 Esta seção descreve a função do atributo <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute> e a interface <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI> quando você está desenvolvendo uma interface de usuário para uma tarefa personalizada e fornece detalhes sobre como criar, integrar, implantar e depurar a tarefa dentro do Designer [!INCLUDE[ssIS](../../../includes/ssis-md.md)].  
  
 O Designer [!INCLUDE[ssIS](../../../includes/ssis-md.md)] fornece vários pontos de entrada à interface do usuário para a tarefa: o usuário pode selecionar **Editar** no menu de atalho, clicar duas vezes na tarefa ou clicar no link **Mostrar Editor** no final da folha de propriedades. Quando o usuário acessa um desses pontos de entrada, o Designer [!INCLUDE[ssIS](../../../includes/ssis-md.md)] localiza e carrega o assembly que contém a interface de usuário para a tarefa. A interface de usuário para a tarefa é responsável pela criação da caixa de diálogo de propriedades que é exibida para o usuário no [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)].  
  
 Uma tarefa e sua interface de usuário são entidades separadas. Elas devem ser implementadas em assemblies separados para reduzir o trabalho de localização, implantação e manutenção. Em geral, a DLL da tarefa não carrega, chama ou contém conhecimento sobre sua interface de usuário, com exceção das informações contidas nos valores de atributo <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute> codificados na tarefa. Essa é a única forma de associação entre uma tarefa e sua interface de usuário.  
  
## <a name="the-dtstask-attribute"></a>O atributo DtsTask  
 O atributo <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute> é incluído no código da classe de tarefa para associar uma tarefa à sua interface de usuário. O Designer [!INCLUDE[ssIS](../../../includes/ssis-md.md)] usa as propriedades do atributo para determinar como exibir a tarefa no designer. Essas propriedades incluem o nome a ser exibido e o ícone, caso exista.  
  
 A tabela a seguir descreve as propriedades do atributo <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute>.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Localization.DtsLocalizableAttribute.DisplayName%2A>|Exibe o nome da tarefa na caixa de ferramentas Fluxo de Controle.|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Localization.DtsLocalizableAttribute.Description%2A>|A descrição da tarefa (herdada do <xref:Microsoft.SqlServer.Dts.Runtime.Localization.DtsLocalizableAttribute>). Essa propriedade é mostrada em Dicas de Ferramenta.|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute.IconResource%2A>|O ícone exibido no Designer [!INCLUDE[ssIS](../../../includes/ssis-md.md)].|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute.RequiredProductLevel%2A>|Se ele for usado, defina-o com um dos valores da enumeração <xref:Microsoft.SqlServer.Dts.Runtime.DTSProductLevel>. Por exemplo, `RequiredProductLevel = DTSProductLevel.None`.|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute.TaskContact%2A>|Mantém informações de contato para ocasiões em que a tarefa exige suporte técnico.|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute.TaskType%2A>|Atribui um tipo à tarefa.|  
|Attribute.TypeId|Quando implementado em uma classe derivada, obtém um identificador exclusivo para este Atributo. Para obter mais informações, consulte a propriedade `Attribute.TypeID` na biblioteca de classes .NET Framework.|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute.UITypeName%2A>|O nome de tipo do assembly que é usado pelo Designer [!INCLUDE[ssIS](../../../includes/ssis-md.md)] para carregar o assembly. Esta propriedade é usada para localizar o assembly de interface de usuário para a tarefa.|  
  
 O exemplo de código a seguir mostra a aparência do <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute>, codificado acima da definição de classe.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
namespace Microsoft.SSIS.Samples  
{  
  [DtsTask  
  (  
   DisplayName = "MyTask",  
   IconResource = "MyTask.MyTaskIcon.ico",  
   UITypeName = "My Custom Task," +  
   "Version=1.0.0.0," +  
   "Culture = Neutral," +  
   "PublicKeyToken = 12345abc6789de01",  
   TaskType = "PackageMaintenance",  
   TaskContact = "MyTask; company name; any other information",  
   RequiredProductLevel = DTSProductLevel.None  
   )]  
  public class MyTask : Task  
  {  
    // Your code here.  
  }  
}  
```  
  
```vb  
Imports System  
Imports Microsoft.SqlServer.Dts.Runtime  
  
<DtsTask(DisplayName:="MyTask", _  
 IconResource:="MyTask.MyTaskIcon.ico", _  
 UITypeName:="My Custom Task," & _  
 "Version=1.0.0.0,Culture=Neutral," & _  
 "PublicKeyToken=12345abc6789de01", _  
 TaskType:="PackageMaintenance", _  
 TaskContact:="MyTask; company name; any other information", _  
 RequiredProductLevel:=DTSProductLevel.None)> _  
Public Class MyTask  
  Inherits Task  
  
  ' Your code here.  
  
End Class 'MyTask  
```  
  
 O Designer [!INCLUDE[ssIS](../../../includes/ssis-md.md)] utiliza a propriedade <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute.UITypeName%2A> do atributo que inclui o nome do assembly, o nome do tipo, a versão, a cultura e o token de chave pública, para localizar o assembly no Cache de Assembly Global (GAC) e carregá-lo para ser usado pelo designer.  
  
 Depois de o assembly ser localizado, o Designer [!INCLUDE[ssIS](../../../includes/ssis-md.md)] utiliza as outras propriedades do atributo para exibir informações adicionais sobre a tarefa no Designer [!INCLUDE[ssIS](../../../includes/ssis-md.md)], tais como nome, ícone e descrição da tarefa.  
  
 As propriedades <xref:Microsoft.SqlServer.Dts.Runtime.Localization.DtsLocalizableAttribute.DisplayName%2A>, <xref:Microsoft.SqlServer.Dts.Runtime.Localization.DtsLocalizableAttribute.Description%2A>e <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute.IconResource%2A> especificam como a tarefa é apresentada ao usuário. A propriedade <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute.IconResource%2A> contém a ID do recurso do ícone inserida no assembly de interface do usuário. O designer carrega o recurso de ícone pelo ID do assembly e exibe-o ao lado do nome da tarefa na caixa de ferramentas e na superfície do designer quando a tarefa é adicionada a um pacote. Se uma tarefa não fornecer um recurso de ícone, o designer usará um ícone padrão para a tarefa.  
  
## <a name="the-idtstaskui-interface"></a>The IDTSTaskUI Interface  
 A interface <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI> define a coleção de métodos e propriedades chamados pelo Designer [!INCLUDE[ssIS](../../../includes/ssis-md.md)] para inicializar e exibir a interface de usuário associada à tarefa. Quando a interface de usuário para uma tarefa é invocada, o designer chama o método <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI.Initialize%2A>, implementado pela interface de usuário da tarefa quando você o escreveu, e depois fornece as coleções <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> e <xref:Microsoft.SqlServer.Dts.Runtime.Connections> da tarefa e pacote, respectivamente, como parâmetros. Essas coleções são armazenadas localmente e usadas subsequentemente no método <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI.GetView%2A>.  
  
 O designer chama o método <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI.GetView%2A> para solicitar a janela que é exibida no Designer [!INCLUDE[ssIS](../../../includes/ssis-md.md)]. A tarefa cria uma instância da janela que contém a interface de usuário para a tarefa e retorna a interface de usuário a ser exibida pelo designer. Normalmente, são fornecidos os objetos <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> e <xref:Microsoft.SqlServer.Dts.Runtime.Connections> para a janela através de um construtor sobrecarregado; assim, eles podem ser usados para configurar a tarefa.  
  
 O Designer [!INCLUDE[ssIS](../../../includes/ssis-md.md)] chama o método <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI.GetView%2A> da tarefa UI para exibir a interface de usuário para a tarefa. A interface de usuário da tarefa retorna o formulário Windows desse método e o Designer [!INCLUDE[ssIS](../../../includes/ssis-md.md)] mostra esse formulário como uma caixa de diálogo modal. Quando o formulário é fechado, o Designer [!INCLUDE[ssIS](../../../includes/ssis-md.md)] verifica o valor da propriedade `DialogResult` do formulário para determinar se a tarefa foi modificada e se essas modificações devem ser salvas. Se o valor da propriedade `DialogResult` for `OK`, o Designer [!INCLUDE[ssIS](../../../includes/ssis-md.md)] chamará os métodos de persistência da tarefa para salvar as alterações; caso contrário, as alterações serão descartadas.  
  
 O exemplo de código a seguir implementa a interface <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI> e pressupõe a existência de uma classe de formulário do Windows nomeada SampleTaskForm.  
  
```csharp  
using System;  
using System.Windows.Forms;  
using Microsoft.SqlServer.Dts.Runtime;  
using Microsoft.SqlServer.Dts.Runtime.Design;  
  
namespace Sample  
{  
   public class HelloWorldTaskUI : IDtsTaskUI  
   {  
      TaskHost   taskHost;  
      Connections connections;  
      public void Initialize(TaskHost taskHost, IServiceProvider serviceProvider)  
      {  
         this.taskHost = taskHost;  
         IDtsConnectionService cs = serviceProvider.GetService  
         ( typeof( IDtsConnectionService ) ) as   IDtsConnectionService;   
         this.connections = cs.GetConnections();  
      }  
      public ContainerControl GetView()  
      {  
        return new HelloWorldTaskForm(this.taskHost, this.connections);  
      }  
     public void Delete(IWin32Window parentWindow)  
     {  
     }  
     public void New(IWin32Window parentWindow)  
     {  
     }  
   }  
}  
```  
  
```vb  
Imports System  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports Microsoft.SqlServer.Dts.Runtime.Design  
Imports System.Windows.Forms  
  
Public Class HelloWorldTaskUI  
  Implements IDtsTaskUI  
  
  Dim taskHost As TaskHost  
  Dim connections As Connections  
  
  Public Sub Initialize(ByVal taskHost As TaskHost, ByVal serviceProvider As IServiceProvider) _  
    Implements IDtsTaskUI.Initialize  
  
    Dim cs As IDtsConnectionService  
  
    Me.taskHost = taskHost  
    cs = DirectCast(serviceProvider.GetService(GetType(IDtsConnectionService)), IDtsConnectionService)  
    Me.connections = cs.GetConnections()  
  
  End Sub  
  
  Public Function GetView() As ContainerControl _  
    Implements IDtsTaskUI.GetView  
  
    Return New HelloWorldTaskForm(Me.taskHost, Me.connections)  
  
  End Function  
  
  Public Sub Delete(ByVal parentWindow As IWin32Window) _  
    Implements IDtsTaskUI.Delete  
  
  End Sub  
  
  Public Sub [New](ByVal parentWindow As IWin32Window) _  
    Implements IDtsTaskUI.[New]  
  
  End Sub  
  
End Class  
```  
  
![Ícone do Integration Services (pequeno)](../../media/dts-16.gif "ícone do Integration Services (pequeno)")**mantenha-se para cima até o momento com o Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte também  
 [Criar uma tarefa personalizada](creating-a-custom-task.md)   
 [Codificar uma tarefa personalizada](coding-a-custom-task.md)   
 [Desenvolver uma interface do usuário para uma tarefa personalizada](developing-a-user-interface-for-a-custom-task.md)  
  
  
