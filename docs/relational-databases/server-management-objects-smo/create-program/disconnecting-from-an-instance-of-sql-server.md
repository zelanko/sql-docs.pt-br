---
title: Desconectando de uma instância do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: smo
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, disconnecting
- SMO [SQL Server], disconnecting
- instances of SQL Server, disconnecting
- disconnecting [SMO]
ms.assetid: 4ca7f7eb-6b3f-4c73-ac63-88afa8570b61
caps.latest.revision: 45
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e8a99d5b82f8901d66c1ad25de5de03694e5b3e1
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43109004"
---
# <a name="disconnecting-from-an-instance-of-sql-server"></a>Desconectando de uma instância do SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  Manualmente, fechando e desconectando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] objetos Management Objects (SMO) não é necessária. As conexões são abertas e fechadas, conforme o necessário.  
  
## <a name="connection-pooling"></a>Pool de conexões  
 Quando o [Connect](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionmanager.connect) método é chamado, a conexão não é liberada automaticamente. O [desconectar](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionmanager.disconnect) método deve ser chamado explicitamente para liberar a conexão ao pool de conexão. Você também pode solicitar uma conexão não inserida no pool. Você pode fazer isso definindo a [NonPooledConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionsettings.nonpooledconnection) propriedade da <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> propriedade que faz referência a [ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx) objeto.  
  
## <a name="disconnecting-from-an-instance-of-sql-server-for-rmo"></a>Desconectando de uma instância do SQL Server para RMO  
 O fechamento de conexões de servidor quando você está programando com RMO é um pouco diferente do que quando a programação é feita com SMO.  
  
 Como a conexão de servidor para um objeto RMO é mantida pela [ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx) do objeto, esse objeto também é usado durante a desconexão de uma instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] quando você programa usando RMO. Para fechar uma conexão usando o [ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx) do objeto, chame o [Disconnect](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionmanager.disconnect) método do objeto RMO. Depois que a conexão tiver sido fechada, os objetos RMO não poderão ser usados.  
  
## <a name="example"></a>Exemplo  
Para usar qualquer exemplo de código fornecido, será necessário escolher o ambiente de programação, o modelo de programação e a linguagem de programação para criar o aplicativo. Para obter mais informações, consulte [criar um Visual C&#35; projeto do SMO no Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
 
  
## <a name="closing-and-disconnecting-an-smo-object-in-visual-basic"></a>Fechando e desconectando um objeto SMO no Visual Basic  
 Este exemplo de código mostra como solicitar uma conexão não agrupada definindo a [NonPooledConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionsettings.nonpooledconnection) propriedade do <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> propriedade de objeto.  
  
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
 Este exemplo de código mostra como solicitar uma conexão não agrupada definindo a [NonPooledConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionsettings.nonpooledconnection) propriedade do <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> propriedade de objeto.  
  
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
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.SqlServer.Management.Smo.Server>   
 [ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx)  
  
  
