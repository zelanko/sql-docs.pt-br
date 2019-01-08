---
title: Desconectando de uma instância do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, disconnecting
- SMO [SQL Server], disconnecting
- instances of SQL Server, disconnecting
- disconnecting [SMO]
ms.assetid: 4ca7f7eb-6b3f-4c73-ac63-88afa8570b61
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7783fa93912c305403cc34ad6e52668123d164ed
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52781448"
---
# <a name="disconnecting-from-an-instance-of-sql-server"></a>Desconectando de uma instância do SQL Server
  O fechamento e a desconexão manuais do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] SMO (SQL Management Objects) não são necessários. As conexões são abertas e fechadas, conforme o necessário.  
  
## <a name="connection-pooling"></a>Pool de conexões  
 Quando o método <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Connect%2A> é chamado, a conexão não é liberada automaticamente. O método <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Disconnect%2A> deve ser chamado explicitamente para liberar a conexão com o pool de conexões. Você também pode solicitar uma conexão não inserida no pool. Para isso, defina a propriedade <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.NonPooledConnection%2A> da propriedade <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> que faz referência ao objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>.  
  
## <a name="disconnecting-from-an-instance-of-sql-server-for-rmo"></a>Desconectando de uma instância do SQL Server para RMO  
 O fechamento de conexões de servidor quando você está programando com RMO é um pouco diferente do que quando a programação é feita com SMO.  
  
 Como a conexão de servidor para um objeto RMO é mantida pela <xref:Microsoft.SqlServer.Management.Common.ServerConnection> do objeto, esse objeto também é usado durante a desconexão de uma instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] quando você programa usando RMO. Para fechar uma conexão usando o objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>, chame o método <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Disconnect%2A> do objeto RMO. Depois que a conexão tiver sido fechada, os objetos RMO não poderão ser usados.  
  
## <a name="example"></a>Exemplo  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="closing-and-disconnecting-an-smo-object-in-visual-basic"></a>Fechando e desconectando um objeto SMO no Visual Basic  
 Este exemplo de código mostra como solicitar uma conexão não agrupada definindo a propriedade <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.NonPooledConnection%2A> da propriedade de objeto <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A>.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VB4](SMO How to#SMO_VB4)]  -->  
  
## <a name="closing-and-disconnecting-an-smo-object-in-visual-c"></a>Fechando e desconectando um objeto SMO no Visual C#  
 Este exemplo de código mostra como solicitar uma conexão não agrupada definindo a propriedade <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.NonPooledConnection%2A> da propriedade de objeto <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A>.  
  
```  
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
 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>  
  
  
