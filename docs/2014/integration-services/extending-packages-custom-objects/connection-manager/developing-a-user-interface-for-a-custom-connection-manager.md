---
title: Desenvolver uma interface do usuário para um gerenciador de conexões personalizado | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- custom connection managers [Integration Services], developing user interface
- custom user interface [Integration Services], custom connection manager
ms.assetid: 908bf2ac-fc84-4af8-a869-1cb43573d2df
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 54ec4cc92383d0b8e423aabd19c0aeee9226d71f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62896036"
---
# <a name="developing-a-user-interface-for-a-custom-connection-manager"></a>Desenvolvendo uma interface do usuário para um gerenciador de conexões personalizado
  Depois de ter substituído a implementação das propriedades e dos métodos da classe de base para fornecer sua funcionalidade personalizada, talvez você queira criar uma interface do usuário personalizada para seu gerenciador de conexões. Se você não criar uma interface de usuário personalizada, os usuários poderão configurar seu gerenciador de conexões somente utilizando a janela Propriedades.  
  
 Em um projeto ou assembly de interface do usuário personalizado, você normalmente tem duas classes – uma classe que implementa <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI> e o formulário do Windows exibido para reunir informações do usuário.  
  
> [!IMPORTANT]  
>  Depois de assinar e criar sua interface do usuário personalizada e instalá-la no cache de assembly global, conforme descrito em [Codificar um gerenciador de conexões personalizado](../building-deploying-and-debugging-custom-objects.md), lembre-se de fornecer o nome totalmente qualificado desta classe na propriedade <xref:Microsoft.SqlServer.Dts.Runtime.DtsConnectionAttribute.UITypeName%2A> do <xref:Microsoft.SqlServer.Dts.Runtime.DtsConnectionAttribute>.  
  
> [!NOTE]  
>  A maioria das tarefas, fontes e destinos incluídos no [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] funcionam somente com tipos específicos de gerenciadores de conexões internos. Portanto, esses exemplos não podem ser testados com as tarefas e componentes internos.  
  
## <a name="coding-the-user-interface-class"></a>Codificando a classe de interface do usuário  
 A interface <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI> tem quatro métodos: <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI.Initialize%2A>, <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI.New%2A>, <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI.Edit%2A> e <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI.Delete%2A>. As seções seguintes descrevem esses quatro métodos.  
  
> [!NOTE]  
>  Talvez não seja necessário gravar nenhum código para o método <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI.Delete%2A>, se nenhuma limpeza for exigida quando o usuário excluir uma instância do gerenciador de conexões.  
  
### <a name="initializing-the-user-interface"></a>Inicializando a interface do usuário   
 No método <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI.Initialize%2A>, o designer fornece uma referência para o gerenciador de conexões que está sendo configurado, dessa forma a classe de interface do usuário pode modificar as propriedades do gerenciador de conexões. Conforme mostrado no código a seguir, seu código precisa armazenar em cache a referência ao gerenciador de conexões para uso futuro.  
  
```vb  
Public Sub Initialize(ByVal connectionManager As Microsoft.SqlServer.Dts.Runtime.ConnectionManager, ByVal serviceProvider As System.IServiceProvider) Implements Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI.Initialize  
  
    _connectionManager = connectionManager  
    _serviceProvider = serviceProvider  
  
  End Sub  
```  
  
```csharp  
public void Initialize(Microsoft.SqlServer.Dts.Runtime.ConnectionManager connectionManager, System.IServiceProvider serviceProvider)  
{  
  
  _connectionManager = connectionManager;  
  _serviceProvider = serviceProvider;  
  
}  
```  
  
### <a name="creating-a-new-instance-of-the-user-interface"></a>Criando uma nova instância da interface do usuário  
 O método <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI.New%2A>, que não é um construtor, é chamado após o método <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI.Initialize%2A> quando o usuário cria uma nova instância do gerenciador de conexões. No método <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI.New%2A>, você normalmente quer exibir o formulário para editar, a menos que o usuário tivesse copiado e colado um gerenciador de conexões existente. O código seguinte mostra uma implementação desse método.  
  
```vb  
Public Function [New](ByVal parentWindow As System.Windows.Forms.IWin32Window, ByVal connections As Microsoft.SqlServer.Dts.Runtime.Connections, ByVal connectionUIArgs As Microsoft.SqlServer.Dts.Runtime.Design.ConnectionManagerUIArgs) As Boolean Implements Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI.New  
  
  Dim clipboardService As IDtsClipboardService  
  
  clipboardService = _  
    DirectCast(_serviceProvider.GetService(GetType(IDtsClipboardService)), IDtsClipboardService)  
  If Not clipboardService Is Nothing Then  
    ' If the connection manager has been copied and pasted, take no action.  
    If clipboardService.IsPasteActive Then  
      Return True  
    End If  
  End If  
  
  Return EditSqlConnection(parentWindow)  
  
End Function  
```  
  
```csharp  
public bool New(System.Windows.Forms.IWin32Window parentWindow, Microsoft.SqlServer.Dts.Runtime.Connections connections, Microsoft.SqlServer.Dts.Runtime.Design.ConnectionManagerUIArgs connectionUIArgs)  
  {  
    IDtsClipboardService clipboardService;  
  
    clipboardService = (IDtsClipboardService)_serviceProvider.GetService(typeof(IDtsClipboardService));  
    if (clipboardService != null)  
    // If connection manager has been copied and pasted, take no action.  
    {  
      if (clipboardService.IsPasteActive)  
      {  
        return true;  
      }  
    }  
  
    return EditSqlConnection(parentWindow);  
  }  
```  
  
### <a name="editing-the-connection-manager"></a>Editando o gerenciador de conexões  
 Como o formulário para edição é chamado por meio dos métodos <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI.New%2A> e <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI.Edit%2A>, é conveniente utilizar uma função auxiliar para encapsular o código que exibe o formulário. O código seguinte mostra uma implementação dessa função auxiliar.  
  
```vb  
Private Function EditSqlConnection(ByVal parentWindow As IWin32Window) As Boolean  
  
  Dim sqlCMUIForm As New SqlConnMgrUIFormVB  
  
  sqlCMUIForm.Initialize(_connectionManager, _serviceProvider)  
  If sqlCMUIForm.ShowDialog(parentWindow) = DialogResult.OK Then  
    Return True  
  Else  
    Return False  
  End If  
  
End Function  
```  
  
```csharp  
private bool EditSqlConnection(IWin32Window parentWindow)  
 {  
  
   SqlConnMgrUIFormCS sqlCMUIForm = new SqlConnMgrUIFormCS();  
  
   sqlCMUIForm.Initialize(_connectionManager, _serviceProvider);  
   if (sqlCMUIForm.ShowDialog(parentWindow) == DialogResult.OK)  
   {  
     return true;  
   }  
   else  
   {  
     return false;  
   }  
  
 }  
```  
  
 No método <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI.Edit%2A>, você tem que simplesmente exibir o formulário para editar. O código seguinte mostra uma implementação do método <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI.Edit%2A> que usa uma função auxiliar para encapsular o código para o formulário.  
  
```vb  
Public Function Edit(ByVal parentWindow As System.Windows.Forms.IWin32Window, ByVal connections As Microsoft.SqlServer.Dts.Runtime.Connections, ByVal connectionUIArg As Microsoft.SqlServer.Dts.Runtime.Design.ConnectionManagerUIArgs) As Boolean Implements Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI.Edit  
  
  Return EditSqlConnection(parentWindow)  
  
End Function  
```  
  
```csharp  
public bool Edit(System.Windows.Forms.IWin32Window parentWindow, Microsoft.SqlServer.Dts.Runtime.Connections connections, Microsoft.SqlServer.Dts.Runtime.Design.ConnectionManagerUIArgs connectionUIArg)  
{  
  
  return EditSqlConnection(parentWindow);  
  
}  
```  
  
## <a name="coding-the-user-interface-form"></a>Codificando o formulário de interface do usuário  
 Depois de criar a classe de interface do usuário que implementa os métodos da interface <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI>, você deverá criar um formulário do Windows onde o usuário possa configurar as propriedades do gerenciador de conexões.  
  
### <a name="initializing-the-user-interface-form"></a>Inicializando o formulário de interface do usuário   
 Quando você exibir seu formulário personalizado para editar, poderá transmitir uma referência ao gerenciador de conexões que está sendo editado. Você pode transmitir essa referência utilizando um construtor personalizado para a classe de formulário ou criando seu próprio método `Initialize`, conforme mostrado aqui.  
  
```vb  
Public Sub Initialize(ByVal connectionManager As ConnectionManager, ByVal serviceProvider As IServiceProvider)  
  
  _connectionManager = connectionManager  
  _serviceProvider = serviceProvider  
  ConfigureControlsFromConnectionManager()  
  EnableControls()  
  
End Sub  
```  
  
```csharp  
public void Initialize(ConnectionManager connectionManager, IServiceProvider serviceProvider)  
 {  
  
   _connectionManager = connectionManager;  
   _serviceProvider = serviceProvider;  
   ConfigureControlsFromConnectionManager();  
   EnableControls();  
  
 }  
```  
  
### <a name="setting-properties-on-the-user-interface-form"></a>Definindo propriedades no formulário de interface do usuário  
 Finalmente, sua classe de formulário precisa de uma função auxiliar que preencha os controles no formulário quando ele for primeiramente carregado com os valores existentes ou padrão das propriedades do gerenciador de conexões. Sua classe de formulário também precisa de uma função similar que defina os valores das propriedades para os valores inseridos pelo usuário quando o usuário clicar em OK e fechar o formulário.  
  
```vb  
Private Const CONNECTIONNAME_BASE As String = "SqlConnectionManager"  
  
Private Sub ConfigureControlsFromConnectionManager()  
  
  Dim tempName As String  
  Dim tempServerName As String  
  Dim tempDatabaseName As String  
  
  With _connectionManager  
  
    tempName = .Properties("Name").GetValue(_connectionManager).ToString  
    If Not String.IsNullOrEmpty(tempName) Then  
      _connectionName = tempName  
    Else  
      _connectionName = CONNECTIONNAME_BASE  
    End If  
  
    tempServerName = .Properties("ServerName").GetValue(_connectionManager).ToString  
    If Not String.IsNullOrEmpty(tempServerName) Then  
      _serverName = tempServerName  
      txtServerName.Text = _serverName  
    End If  
  
    tempDatabaseName = .Properties("DatabaseName").GetValue(_connectionManager).ToString  
    If Not String.IsNullOrEmpty(tempDatabaseName) Then  
      _databaseName = tempDatabaseName  
      txtDatabaseName.Text = _databaseName  
    End If  
  
  End With  
  
End Sub  
  
Private Sub ConfigureConnectionManagerFromControls()  
  
  With _connectionManager  
    .Properties("Name").SetValue(_connectionManager, _connectionName)  
    .Properties("ServerName").SetValue(_connectionManager, _serverName)  
    .Properties("DatabaseName").SetValue(_connectionManager, _databaseName)  
  End With  
  
End Sub  
```  
  
```csharp  
private const string CONNECTIONNAME_BASE = "SqlConnectionManager";  
  
private void ConfigureControlsFromConnectionManager()  
 {  
  
   string tempName;  
   string tempServerName;  
   string tempDatabaseName;  
  
   {  
     tempName = _connectionManager.Properties["Name"].GetValue(_connectionManager).ToString();  
     if (!String.IsNullOrEmpty(tempName))  
     {  
       _connectionName = tempName;  
     }  
     else  
     {  
       _connectionName = CONNECTIONNAME_BASE;  
     }  
  
     tempServerName = _connectionManager.Properties["ServerName"].GetValue(_connectionManager).ToString();  
     if (!String.IsNullOrEmpty(tempServerName))  
     {  
       _serverName = tempServerName;  
       txtServerName.Text = _serverName;  
     }  
  
     tempDatabaseName = _connectionManager.Properties["DatabaseName"].GetValue(_connectionManager).ToString();  
     if (!String.IsNullOrEmpty(tempDatabaseName))  
     {  
       _databaseName = tempDatabaseName;  
       txtDatabaseName.Text = _databaseName;  
     }  
  
   }  
  
 }  
  
 private void ConfigureConnectionManagerFromControls()  
 {  
  
   {  
     _connectionManager.Properties["Name"].SetValue(_connectionManager, _connectionName);  
     _connectionManager.Properties["ServerName"].SetValue(_connectionManager, _serverName);  
     _connectionManager.Properties["DatabaseName"].SetValue(_connectionManager, _databaseName);  
   }  
  
 }  
```  
  
![Ícone do Integration Services (pequeno)](../../media/dts-16.gif "ícone do Integration Services (pequeno)")**mantenha-se para cima até o momento com o Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte também  
 [Criar um gerenciador de conexões personalizado](creating-a-custom-connection-manager.md)   
 [Codificar um gerenciador de conexões personalizado](coding-a-custom-connection-manager.md)  
  
  
