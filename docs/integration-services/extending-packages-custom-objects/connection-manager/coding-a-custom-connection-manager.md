---
title: "Codificar um gerenciador de conexões personalizado | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-custom-objects
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom connection managers [Integration Services], coding
ms.assetid: b12b6778-1f01-4a7d-984d-73f2f7630aa5
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fe3f9823cfb1b84c0ea3d80a5f2917632b2829f8
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="coding-a-custom-connection-manager"></a>Codificando um gerenciador de conexões personalizado
  Depois de criar uma classe que herda da classe base <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase> e aplicar o atributo <xref:Microsoft.SqlServer.Dts.Runtime.DtsConnectionAttribute> a essa classe, você deve substituir a implementação das propriedades e dos métodos da classe base para fornecer sua funcionalidade personalizada.  
  
 Para obter exemplos de gerenciadores de conexão personalizados, consulte [Desenvolver uma interface do usuário para um gerenciador de conexões personalizado](../../../integration-services/extending-packages-custom-objects/connection-manager/developing-a-user-interface-for-a-custom-connection-manager.md). Os exemplos de código mostrados neste tópico foram extraídos do exemplo do Gerenciador de Conexões Personalizado do SQL Server.  
  
> [!NOTE]  
>  A maioria das tarefas, fontes e destinos incluídos no [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] funcionam somente com tipos específicos de gerenciadores de conexões internos. Portanto, esses exemplos não podem ser testados com as tarefas e componentes internos.  
  
## <a name="configuring-the-connection-manager"></a>Configurando o gerenciador de conexões  
  
### <a name="setting-the-connectionstring-property"></a>Definindo a propriedade ConnectionString  
 A propriedade <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.ConnectionString%2A> é uma propriedade importante e a única propriedade exclusiva para um gerenciador de conexões personalizado. O gerenciador de conexões usa o valor dessa propriedade para se conectar à fonte de dados externa. Se você estiver combinando várias outras propriedades, como nome de servidor e nome de banco de dados, para criar a cadeia de conexão você pode usar uma função auxiliar para montar a cadeia, substituindo alguns valores de um modelo de cadeia de conexão pelo novo valor fornecido pelo usuário. O exemplo de código seguinte mostra uma implementação da propriedade <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.ConnectionString%2A> que confia em uma função auxiliar para montar a cadeia.  
  
```vb  
' Default values.  
Private _serverName As String = "(local)"  
Private _databaseName As String = "AdventureWorks"  
Private _connectionString As String = String.Empty  
  
Private Const CONNECTIONSTRING_TEMPLATE As String = _  
  "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=SSPI"  
  
Public Property ServerName() As String  
  Get  
    Return _serverName  
  End Get  
  Set(ByVal value As String)  
    _serverName = value  
  End Set  
End Property  
  
Public Property DatabaseName() As String  
  Get  
    Return _databaseName  
  End Get  
  Set(ByVal value As String)  
    _databaseName = value  
  End Set  
End Property  
  
Public Overrides Property ConnectionString() As String  
  Get  
    UpdateConnectionString()  
    Return _connectionString  
  End Get  
  Set(ByVal value As String)  
    _connectionString = value  
  End Set  
End Property  
  
Private Sub UpdateConnectionString()  
  
  Dim temporaryString As String = CONNECTIONSTRING_TEMPLATE  
  
  If Not String.IsNullOrEmpty(_serverName) Then  
    temporaryString = temporaryString.Replace("<servername>", _serverName)  
  End If  
  If Not String.IsNullOrEmpty(_databaseName) Then  
    temporaryString = temporaryString.Replace("<databasename>", _databaseName)  
  End If  
  
  _connectionString = temporaryString  
  
End Sub  
```  
  
```csharp  
// Default values.  
private string _serverName = "(local)";  
private string _databaseName = "AdventureWorks";  
private string _connectionString = String.Empty;  
  
private const string CONNECTIONSTRING_TEMPLATE = "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=SSPI";  
  
public string ServerName  
{  
  get  
  {  
    return _serverName;  
  }  
  set  
  {  
    _serverName = value;  
  }  
}  
  
public string DatabaseName  
{  
  get  
  {  
    return _databaseName;  
  }  
  set  
  {  
    _databaseName = value;  
  }  
}  
  
public override string ConnectionString  
{  
  get  
  {  
    UpdateConnectionString();  
    return _connectionString;  
  }  
  set  
  {  
    _connectionString = value;  
  }  
}  
  
private void UpdateConnectionString()  
{  
  
  string temporaryString = CONNECTIONSTRING_TEMPLATE;  
  
  if (!String.IsNullOrEmpty(_serverName))  
  {  
    temporaryString = temporaryString.Replace("<servername>", _serverName);  
  }  
  
  if (!String.IsNullOrEmpty(_databaseName))  
  {  
    temporaryString = temporaryString.Replace("<databasename>", _databaseName);  
  }  
  
  _connectionString = temporaryString;  
  
}  
```  
  
### <a name="validating-the-connection-manager"></a>Validando o gerenciador de conexões  
 Você anula o método <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.Validate%2A> para ter certeza de que o gerenciador de conexões foi configurado corretamente. No mínimo, você deve validar o formato da cadeia de conexão e se certificar de que foram fornecidos valores para todos os argumentos. A execução não pode continuar até que o gerenciador de conexões retorne <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult.Success> do método <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.Validate%2A>.  
  
 O exemplo de código seguinte mostra uma implementação de <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.Validate%2A> que assegura que o usuário especificou um nome de servidor para a conexão.  
  
```vb  
Public Overrides Function Validate(ByVal infoEvents As Microsoft.SqlServer.Dts.Runtime.IDTSInfoEvents) As Microsoft.SqlServer.Dts.Runtime.DTSExecResult  
  
  If String.IsNullOrEmpty(_serverName) Then  
    infoEvents.FireError(0, "SqlConnectionManager", "No server name specified", String.Empty, 0)  
    Return DTSExecResult.Failure  
  Else  
    Return DTSExecResult.Success  
  End If  
  
End Function  
```  
  
```csharp  
public override Microsoft.SqlServer.Dts.Runtime.DTSExecResult Validate(Microsoft.SqlServer.Dts.Runtime.IDTSInfoEvents infoEvents)  
{  
  
  if (String.IsNullOrEmpty(_serverName))  
  {  
    infoEvents.FireError(0, "SqlConnectionManager", "No server name specified", String.Empty, 0);  
    return DTSExecResult.Failure;  
  }  
  else  
  {  
    return DTSExecResult.Success;  
  }  
  
}  
```  
  
### <a name="persisting-the-connection-manager"></a>Persistindo o gerenciador de conexões  
 Normalmente, você não tem que implementar a persistência personalizada em um gerenciador de conexões. A persistência personalizada é necessária somente quando as propriedades de um objeto usam tipos de dados complexos. Para obter mais informações, consulte [Desenvolvendo objetos personalizados para o Integration Services](../../../integration-services/extending-packages-custom-objects/developing-custom-objects-for-integration-services.md).  
  
## <a name="working-with-the-external-data-source"></a>Trabalhando com a fonte de dados externa  
 Os métodos que suportam a conexão a uma fonte de dados externa são os métodos mais importantes de um gerenciador de conexões personalizado. Os métodos <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.AcquireConnection%2A> e <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.ReleaseConnection%2A> são chamados em vários momentos durante o tempo de design e o tempo de execução.  
  
### <a name="acquiring-the-connection"></a>Adquirindo a conexão  
 Você precisa decidir que tipo de objeto é apropriado para o método <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.AcquireConnection%2A> para voltar de seu gerenciador de conexões personalizado. Por exemplo, um gerenciador de conexões de Arquivo retorna somente uma cadeia que contém um caminho e um nome de arquivo, enquanto o gerenciador de conexões ADO.NET retorna um objeto de conexão gerenciado que já está aberto. Um gerenciador de conexões OLE DB retorna um objeto de conexão do OLE DB nativo que não pode ser usado a partir do código gerenciado. O gerenciador de conexões do SQL Server personalizado, do qual são tirados os trechos de códigos deste tópico, retorna um objeto **SqlConnection** aberto.  
  
 Os usuários do seu gerenciador de conexões precisam saber antecipadamente que tipo de objeto devem esperar, assim podem converter o objeto retornado para o tipo apropriado e acessar seus métodos e propriedades.  
  
```vb  
Public Overrides Function AcquireConnection(ByVal txn As Object) As Object  
  
  Dim sqlConnection As New SqlConnection  
  
  UpdateConnectionString()  
  
  With sqlConnection  
    .ConnectionString = _connectionString  
    .Open()  
  End With  
  
  Return sqlConnection  
  
End Function  
```  
  
```csharp  
public override object AcquireConnection(object txn)  
{  
  
  SqlConnection sqlConnection = new SqlConnection();  
  
  UpdateConnectionString();  
  
  {  
    sqlConnection.ConnectionString = _connectionString;  
    sqlConnection.Open();  
  }  
  
  return sqlConnection;  
  
}  
```  
  
### <a name="releasing-the-connection"></a>Liberando a conexão  
 A ação adotada no método <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.ReleaseConnection%2A> depende do tipo de objeto que você retornou do método <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.AcquireConnection%2A>. Se houver um objeto de conexão aberto, você deve fechá-lo e liberar qualquer recurso que esteja usando. Se <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.AcquireConnection%2A> retornou só um valor da cadeia de caracteres, nenhuma ação precisa ser tomada.  
  
```vb  
Public Overrides Sub ReleaseConnection(ByVal connection As Object)  
  
  Dim sqlConnection As SqlConnection  
  
  sqlConnection = DirectCast(connection, SqlConnection)  
  
  If sqlConnection.State <> ConnectionState.Closed Then  
    sqlConnection.Close()  
  End If  
  
End Sub  
```  
  
```csharp  
public override void ReleaseConnection(object connection)  
{  
  SqlConnection sqlConnection;  
  sqlConnection = (SqlConnection)connection;  
  if (sqlConnection.State != ConnectionState.Closed)  
    sqlConnection.Close();  
}  
```  
 
## <a name="see-also"></a>Consulte Também  
 [Criar um gerenciador de conexões personalizado](../../../integration-services/extending-packages-custom-objects/connection-manager/creating-a-custom-connection-manager.md)   
 [Desenvolver uma interface do usuário para um gerenciador de conexões personalizado](../../../integration-services/extending-packages-custom-objects/connection-manager/developing-a-user-interface-for-a-custom-connection-manager.md)  
  
  
