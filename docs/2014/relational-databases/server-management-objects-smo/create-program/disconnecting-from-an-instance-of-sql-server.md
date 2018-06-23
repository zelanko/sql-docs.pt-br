---
title: Desconectando de uma instância do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, disconnecting
- SMO [SQL Server], disconnecting
- instances of SQL Server, disconnecting
- disconnecting [SMO]
ms.assetid: 4ca7f7eb-6b3f-4c73-ac63-88afa8570b61
caps.latest.revision: 43
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 1f2ce4ae7ce42df42be9b6bc68c3d13acf949dba
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117109"
---
# <a name="disconnecting-from-an-instance-of-sql-server"></a>Desconectando de uma instância do SQL Server
  Fechando e desconectando manualmente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] objetos Management Objects (SMO) não é necessária. As conexões são abertas e fechadas, conforme o necessário.  
  
## <a name="connection-pooling"></a>Pool de conexões  
 Quando o <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Connect%2A> método é chamado, a conexão não é liberada automaticamente. O método <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Disconnect%2A> deve ser chamado explicitamente para liberar a conexão com o pool de conexões. Você também pode solicitar uma conexão não inserida no pool. Para isso, defina a propriedade <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.NonPooledConnection%2A> da propriedade <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> que faz referência ao objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>.  
  
## <a name="disconnecting-from-an-instance-of-sql-server-for-rmo"></a>Desconectando de uma instância do SQL Server para RMO  
 O fechamento de conexões de servidor quando você está programando com RMO é um pouco diferente do que quando a programação é feita com SMO.  
  
 Como a conexão de servidor para um objeto RMO é mantida pelo <xref:Microsoft.SqlServer.Management.Common.ServerConnection> do objeto, esse objeto também é usado durante a desconexão de uma instância de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] quando você programa usando RMO. Para fechar uma conexão usando o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> de objeto, chame o <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Disconnect%2A> método do objeto RMO. Depois que a conexão tiver sido fechada, os objetos RMO não poderão ser usados.  
  
## <a name="example"></a>Exemplo  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="closing-and-disconnecting-an-smo-object-in-visual-basic"></a>Fechando e desconectando um objeto SMO no Visual Basic  
 Este exemplo de código mostra como solicitar uma conexão sem pool definindo a <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.NonPooledConnection%2A> propriedade o <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> propriedade de objeto.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VB4](SMO How to#SMO_VB4)]  -->  
  
## <a name="closing-and-disconnecting-an-smo-object-in-visual-c"></a>Fechando e desconectando um objeto SMO no Visual C#  
 Este exemplo de código mostra como solicitar uma conexão sem pool definindo a <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.NonPooledConnection%2A> propriedade o <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> propriedade de objeto.  
  
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
  
  