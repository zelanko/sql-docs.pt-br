---
title: Desconectando de uma instância do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, disconnecting
- SMO [SQL Server], disconnecting
- instances of SQL Server, disconnecting
- disconnecting [SMO]
ms.assetid: 4ca7f7eb-6b3f-4c73-ac63-88afa8570b61
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: de53acd4ef3d9feb6ed1a5026d8890f83e88d557
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "70148731"
---
# <a name="disconnecting-from-an-instance-of-sql-server"></a>Desconectando de uma instância do SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  O fechamento e a desconexão manuais do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] SMO (SQL Management Objects) não são necessários. As conexões são abertas e fechadas, conforme o necessário.  
  
## <a name="connection-pooling"></a>Pool de conexões  
 Quando o método [Connect](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionmanager.connect) é chamado, a conexão não é liberada automaticamente. O método de [desconexão](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionmanager.disconnect) deve ser chamado explicitamente para liberar a conexão com o pool de conexões. Você também pode solicitar uma conexão não inserida no pool. Você faz isso definindo a propriedade [NonPooledConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionsettings.nonpooledconnection) da <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> propriedade que faz referência ao objeto [ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx) .  
  
## <a name="disconnecting-from-an-instance-of-sql-server-for-rmo"></a>Desconectando de uma instância do SQL Server para RMO  
 O fechamento de conexões de servidor quando você está programando com RMO é um pouco diferente do que quando a programação é feita com SMO.  
  
 Como a conexão do servidor para um objeto RMO é mantida pelo objeto [ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx) , esse objeto também é usado ao desconectar-se de uma instância [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] do quando você programa usando o RMO. Para fechar uma conexão usando o objeto [ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx) , chame o método [Disconnect](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionmanager.disconnect) do objeto RMO. Depois que a conexão tiver sido fechada, os objetos RMO não poderão ser usados.  
  
## <a name="example"></a>Exemplo  
Para usar qualquer exemplo de código fornecido, será necessário escolher o ambiente de programação, o modelo de programação e a linguagem de programação para criar o aplicativo. Para obter mais informações, consulte [criar um projeto do Visual C&#35; Smo no Visual Studio .net](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
 
  
## <a name="closing-and-disconnecting-an-smo-object-in-visual-basic"></a>Fechando e desconectando um objeto SMO no Visual Basic  
 Este exemplo de código mostra como solicitar uma conexão não agrupada definindo a propriedade [NonPooledConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionsettings.nonpooledconnection) da propriedade <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> Object.  
  
```VBNET
Dim srv As Server
srv = New Server
'Disable automatic disconnection.
srv.ConnectionContext.AutoDisconnectMode = AutoDisconnectMode.NoAutoDisconnect
'Connect to the local, default instance of SQL Server.
srv.ConnectionContext.Connect()
'The actual connection is made when a property is retrieved.
Console.WriteLine(srv.Information.Version)
'Disconnect explicitly.
srv.ConnectionContext.Disconnect()
```
  
## <a name="closing-and-disconnecting-an-smo-object-in-visual-c"></a>Fechando e desconectando um objeto SMO no Visual C#  
 Este exemplo de código mostra como solicitar uma conexão não agrupada definindo a propriedade [NonPooledConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionsettings.nonpooledconnection) da propriedade <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> Object.  
  
```csharp  
{   
Server srv;   
srv = new Server();   
//Disable automatic disconnection.   
srv.ConnectionContext.AutoDisconnectMode = AutoDisconnectMode.NoAutoDisconnect;   
//Connect to the local, default instance of SQL Server.   
srv.ConnectionContext.Connect();   
//The actual connection is made when a property is retrieved.   
Console.WriteLine(srv.Information.Version);   
//Disconnect explicitly.   
srv.ConnectionContext.Disconnect();  
}  
```  
  
## <a name="see-also"></a>Consulte Também  
 <xref:Microsoft.SqlServer.Management.Smo.Server>   
 [ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx)  
  
  
