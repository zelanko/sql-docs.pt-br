---
description: Conectando-se a uma instância do SQL Server
title: Conectando-se a uma instância do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, connections
- connections [SMO]
- instances of SQL Server, connections
- SMO [SQL Server], connections
ms.assetid: ad3cf354-b2e3-468b-b986-1232e375fd84
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 32e004da26b8cba5df8b44e4fbef3fd90967cdfc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88490442"
---
# <a name="connecting-to-an-instance-of-sql-server"></a>Conectando-se a uma instância do SQL Server
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  A primeira etapa de programação em um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] aplicativo Smo (Management Objects) é criar uma instância do <xref:Microsoft.SqlServer.Management.Smo.Server> objeto e estabelecer sua conexão com uma instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 Você pode criar uma instância do objeto <xref:Microsoft.SqlServer.Management.Smo.Server> e estabelecer uma conexão com a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de três maneiras. A primeira é usar uma variável do objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> para fornecer as informações de conexão. A segunda é fornecer as informações de conexão definindo explicitamente as propriedades do objeto <xref:Microsoft.SqlServer.Management.Smo.Server>. A terceira é transmitir o nome da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no construtor do objeto <xref:Microsoft.SqlServer.Management.Smo.Server>. 
  
 **Usando um objeto ServerConnection**  
  
 A vantagem de usar a variável do objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> é que as informações de conexão podem ser reutilizadas. Declare uma variável do objeto <xref:Microsoft.SqlServer.Management.Smo.Server>. Declare um objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> e defina as propriedades com informações de conexão como o nome da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]e o modo de autenticação. Passe a variável do objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> como parâmetro para o construtor do objeto <xref:Microsoft.SqlServer.Management.Smo.Server>. Não é recomendável compartilhar conexões entre diferentes objetos de servidor simultaneamente. Use o método <xref:Microsoft.SqlServer.Management.Common.ServerConnection.Copy%2A> para obter uma cópia das configurações de conexão existentes.  
  
 **Definindo explicitamente as propriedades do objeto Server**  
  
 Como alternativa, você pode declarar a variável do objeto <xref:Microsoft.SqlServer.Management.Smo.Server> e chamar o construtor padrão. Dessa maneira, o objeto <xref:Microsoft.SqlServer.Management.Smo.Server> tenta se conectar à instância padrão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] com todas as configurações de conexão padrão.  
  
 **Fornecendo o nome de instância do SQL Server no construtor do objeto Server**  
  
 Declare a variável do objeto <xref:Microsoft.SqlServer.Management.Smo.Server> e passe o nome da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como parâmetro de cadeia de caracteres no construtor. O objeto <xref:Microsoft.SqlServer.Management.Smo.Server> estabelece uma conexão com a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] com as configurações de conexão padrão.  
  
## <a name="connection-pooling"></a>Pool de conexões  
 Normalmente não é necessário chamar o método <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Connect%2A> do objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>. O SMO estabelecerá automaticamente uma conexão quando for necessário e liberará a conexão com o pool de conexão após concluir as operações. Quando o método <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Connect%2A> é chamado, a conexão não é liberada para o pool. Uma chamada explícita do método <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Disconnect%2A> é necessária para liberar a conexão com o pool. Além disso, você pode solicitar uma conexão sem pool definindo a propriedade <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.NonPooledConnection%2A> do objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>.  
  
## <a name="multithreaded-applications"></a>Aplicativos multi-threaded  
 Para aplicativos multithreaded, um objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> separado deveria ser usado em cada thread.  
  
## <a name="connecting-to-an-instance-of-sql-server-for-rmo"></a>Conectando-se a uma instância do SQL Server para RMO  
 O RMO (Replication Management Objects) usa um método ligeiramente diferente do SMO para conexão a um servidor de replicação.  
  
 Os objetos de programação RMO exigem que uma conexão com uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] seja feita usando o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> objeto implementado pelo namespace **Microsoft. SqlServer. Management. Common** . Essa conexão com o servidor é feita independentemente de um objeto de programação de RMO. Então, ela é passada para o objeto RMO, seja durante a criação da instância, seja por atribuição à propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> do objeto. Dessa maneira, um objeto de programação de RMO e as instâncias de objeto de conexão podem ser criados e gerenciados separadamente, e um único objeto de conexão pode ser reutilizado com vários objetos de programação de RMO. As regras a seguir se aplicam a conexões com um servidor de replicação:  
  
-   São definidas todas as propriedades da conexão para um objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> especificado.  
  
-   Cada conexão com uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] precisa ter seu próprio objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>.  
  
-   Todas as informações sobre autenticação para estabelecer com êxito a conexão e o logon no servidor são fornecidas no objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>.  
  
-   Por padrão, as conexões são feitas usando a Autenticação do Microsoft Windows. Para usar a Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.LoginSecure%2A> precisa ser definido como False, e <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.Login%2A> e <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.Password%2A> precisam ser definidos com um logon e senha válidos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Credenciais de segurança sempre precisam ser armazenados e manipulados de maneira segura, além de fornecidos em tempo de execução quando possível.  
  
-   O método <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Connect%2A> precisa ser chamado antes de passar a conexão com qualquer objeto de programação de RMO.  
  
## <a name="examples"></a>Exemplos  
Para usar qualquer exemplo de código fornecido, será necessário escolher o ambiente de programação, o modelo de programação e a linguagem de programação para criar o aplicativo. Para obter mais informações, consulte  [criar um projeto do Visual C&#35; Smo no Visual Studio .net](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="connecting-to-the-local-instance-of-sql-server-by-using-windows-authentication-in-visual-basic"></a>Conectando-se à instância local do SQL Server usando a Autenticação do Windows no Visual Basic  
 A conexão com a instância local do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não exige muito código. Em vez disso, ela depende das configurações padrão para o servidor e o método de autenticação. A primeira operação que exige a recuperação dos dados faz com que uma conexão seja criada.  
 
Este exemplo é Visual Basic código .NET que se conecta à instância local do SQL Server usando a autenticação do Windows. 

```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'The connection is established when a property is requested.
Console.WriteLine(srv.Information.Version)
'The connection is automatically disconnected when the Server variable goes out of scope.
```
  
## <a name="connecting-to-the-local-instance-of-sql-server-by-using-windows-authentication-in-visual-c"></a>Conectando-se à instância local do SQL Server usando a Autenticação do Windows no Visual C#  
 A conexão com a instância local do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não exige muito código. Em vez disso, ela depende das configurações padrão para o servidor e o método de autenticação. A primeira operação que exige a recuperação dos dados faz com que uma conexão seja criada.  
  
 Este exemplo é o código Visual C# .NET que se conecta à instância local do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando a Autenticação do Windows.  
  
```csharp  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//The connection is established when a property is requested.   
Console.WriteLine(srv.Information.Version);   
}   
//The connection is automatically disconnected when the Server variable goes out of scope.  
```  
  
## <a name="connecting-to-a-remote-instance-of-sql-server-by-using-windows-authentication-in-visual-basic"></a>Conectando-se a uma instância remota do SQL Server usando a Autenticação do Windows no Visual Basic  
 Ao se conectar a uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando a Autenticação do Windows, você não precisa especificar o tipo de autenticação. A Autenticação do Windows é o padrão.  
  
 Este exemplo é um [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] código .NET que se conecta à instância remota do usando a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] autenticação do Windows. A variável de cadeia de caracteres *strServer* contém o nome da instância remota.  
  
```VBNET   
'Connect to a remote instance of SQL Server.
Dim srv As Server
'The strServer string variable contains the name of a remote instance of SQL Server.
srv = New Server(strServer)
'The actual connection is made when a property is retrieved. 
Console.WriteLine(srv.Information.Version)
'The connection is automatically disconnected when the Server variable goes out of scope.
```
  
## <a name="connecting-to-a-remote-instance-of-sql-server-by-using-windows-authentication-in-visual-c"></a>Conectando-se a uma instância remota do SQL Server usando a Autenticação do Windows no Visual C#  
 Ao se conectar a uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando a Autenticação do Windows, você não precisa especificar o tipo de autenticação. A Autenticação do Windows é o padrão.  
  
 Este exemplo é o código Visual C# .NET que se conecta à instância remota do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando a Autenticação do Windows. A variável de cadeia de caracteres *strServer* contém o nome da instância remota.  
  
```csharp  
{   
//Connect to a remote instance of SQL Server.   
Server srv;   
//The strServer string variable contains the name of a remote instance of SQL Server.   
srv = new Server(strServer);   
//The actual connection is made when a property is retrieved.   
Console.WriteLine(srv.Information.Version);   
}   
//The connection is automatically disconnected when the Server variable goes out of scope.  
```  
  
## <a name="connecting-to-an-instance-of-sql-server-by-using-sql-server-authentication-in-visual-basic"></a>Conectando-se a uma instância do SQL Server usando a Autenticação do SQL Server no Visual Basic  
 Ao conectar-se a uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando a Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], você deve especificar o tipo de autenticação. Este exemplo demonstra o método alternativo de declarar uma variável do objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>, que habilita as informações de conexão a serem reutilizadas.  
  
 O exemplo é um [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] código .NET que demonstra como se conectar ao remoto e *vPassword* contém o logon e a senha.  
  
```VBNET  
' compile with:   
' /r:Microsoft.SqlServer.Smo.dll  
' /r:Microsoft.SqlServer.ConnectionInfo.dll  
' /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll   
  
Imports Microsoft.SqlServer.Management.Smo  
Imports Microsoft.SqlServer.Management.Common  
  
Public Class A  
   Public Shared Sub Main()  
      Dim sqlServerLogin As [String] = "user_id"  
      Dim password As [String] = "pwd"  
      Dim instanceName As [String] = "instance_name"  
      Dim remoteSvrName As [String] = "remote_server_name"  
  
      ' Connecting to an instance of SQL Server using SQL Server Authentication  
      Dim srv1 As New Server()   ' connects to default instance  
      srv1.ConnectionContext.LoginSecure = False   ' set to true for Windows Authentication  
      srv1.ConnectionContext.Login = sqlServerLogin  
      srv1.ConnectionContext.Password = password  
      Console.WriteLine(srv1.Information.Version)   ' connection is established  
  
      ' Connecting to a named instance of SQL Server with SQL Server Authentication using ServerConnection  
      Dim srvConn As New ServerConnection()  
      srvConn.ServerInstance = ".\" & instanceName   ' connects to named instance  
      srvConn.LoginSecure = False   ' set to true for Windows Authentication  
      srvConn.Login = sqlServerLogin  
      srvConn.Password = password  
      Dim srv2 As New Server(srvConn)  
      Console.WriteLine(srv2.Information.Version)   ' connection is established  
  
      ' For remote connection, remote server name / ServerInstance needs to be specified  
      Dim srvConn2 As New ServerConnection(remoteSvrName)  
      srvConn2.LoginSecure = False  
      srvConn2.Login = sqlServerLogin  
      srvConn2.Password = password  
      Dim srv3 As New Server(srvConn2)  
      Console.WriteLine(srv3.Information.Version)   ' connection is established  
   End Sub  
End Class  
```  
  
## <a name="connecting-to-an-instance-of-sql-server-by-using-sql-server-authentication-in-visual-c"></a>Conectando-se a uma instância do SQL Server usando a Autenticação do SQL Server no Visual C#  
 Ao conectar-se a uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando a Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], você deve especificar o tipo de autenticação. Este exemplo demonstra o método alternativo de declarar uma variável do objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>, que habilita as informações de conexão a serem reutilizadas.  
  
 O exemplo é o código do Visual C# .NET que demonstra como se conectar ao remoto e *vPassword* contêm o logon e a senha.  
  
```csharp  
// compile with:   
// /r:Microsoft.SqlServer.Smo.dll  
// /r:Microsoft.SqlServer.ConnectionInfo.dll  
// /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll   
  
using System;  
using Microsoft.SqlServer.Management.Smo;  
using Microsoft.SqlServer.Management.Common;  
  
public class A {  
   public static void Main() {   
      String sqlServerLogin = "user_id";  
      String password = "pwd";  
      String instanceName = "instance_name";  
      String remoteSvrName = "remote_server_name";  
  
      // Connecting to an instance of SQL Server using SQL Server Authentication  
      Server srv1 = new Server();   // connects to default instance  
      srv1.ConnectionContext.LoginSecure = false;   // set to true for Windows Authentication  
      srv1.ConnectionContext.Login = sqlServerLogin;  
      srv1.ConnectionContext.Password = password;  
      Console.WriteLine(srv1.Information.Version);   // connection is established  
  
      // Connecting to a named instance of SQL Server with SQL Server Authentication using ServerConnection  
      ServerConnection srvConn = new ServerConnection();  
      srvConn.ServerInstance = @".\" + instanceName;   // connects to named instance  
      srvConn.LoginSecure = false;   // set to true for Windows Authentication  
      srvConn.Login = sqlServerLogin;  
      srvConn.Password = password;  
      Server srv2 = new Server(srvConn);  
      Console.WriteLine(srv2.Information.Version);   // connection is established  
  
      // For remote connection, remote server name / ServerInstance needs to be specified  
      ServerConnection srvConn2 = new ServerConnection(remoteSvrName);  
      srvConn2.LoginSecure = false;  
      srvConn2.Login = sqlServerLogin;  
      srvConn2.Password = password;  
      Server srv3 = new Server(srvConn2);  
      Console.WriteLine(srv3.Information.Version);   // connection is established  
   }  
}  
```  
  
## <a name="see-also"></a>Consulte Também  
 <xref:Microsoft.SqlServer.Management.Smo.Server>   
 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>  
  
  
