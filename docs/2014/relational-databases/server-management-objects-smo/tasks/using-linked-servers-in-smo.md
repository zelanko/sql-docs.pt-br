---
title: Usando servidores vinculados no SMO | Microsoft Docs
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
- linked servers [SQL Server], SMO
ms.assetid: 0ea8837b-2596-4df1-b065-3bb717c9f22c
caps.latest.revision: 34
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7ae91209d5786ed976e1c29ed9b51d7d52e0070a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36012019"
---
# <a name="using-linked-servers-in-smo"></a>Usando servidores vinculados no SMO
  Um servidor vinculado representa uma fonte de dados OLE DB em um servidor remoto. Fontes de dados OLE DB remotas estão vinculadas à instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando o <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> objeto.  
  
 Servidores de banco de dados remoto podem ser vinculados à instância atual do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando um provedor OLE DB. No SMO, servidores vinculados são representados pelo <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> objeto. O <xref:Microsoft.SqlServer.Management.Smo.LinkedServer.LinkedServerLogins%2A> propriedade referencia uma coleção de <xref:Microsoft.SqlServer.Management.Smo.LinkedServerLogin> objetos. Aqui são armazenadas as credenciais de logon que são necessárias para estabelecer uma conexão com o servidor vinculado.  
  
## <a name="ole-db-providers"></a>Provedores OLE DB  
 No SMO, provedores OLE DB instalados são representados por uma coleção de objetos <xref:Microsoft.SqlServer.Management.Smo.OleDbProviderSettings>.  
  
## <a name="example"></a>Exemplo  
 Para o exemplo de código a seguir, selecione o ambiente de programação, o modelo de programação e a linguagem de programação para criar seu aplicativo. Para obter mais informações, consulte [criar um projeto Visual Basic SMO no Visual Studio .NET](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) e [criar um Visual C&#35; projeto SMO no Visual Studio .NET](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-a-link-to-an-ole-db-provider-server-in-visual-basic"></a>Criando um vínculo com um servidor de provedor OLE DB no Visual Basic  
 O exemplo de código mostra como criar um link para um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] OLE DB, origem de dados heterogêneos usando o <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> objeto. Especificando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como o nome do produto, os dados são acessados no servidor vinculado usando o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cliente OLE DB Provider, que é o provedor OLE DB oficial para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBLinkedServers1](SMO How to#SMO_VBLinkedServers1)]  -->  
  
## <a name="creating-a-link-to-an-ole-db-provider-server-in-visual-c"></a>Criando um link com um servidor de provedor OLE DB no Visual C#  
 O exemplo de código mostra como criar um link para um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] OLE DB, origem de dados heterogêneos usando o <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> objeto. Especificando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como o nome do produto, os dados são acessados no servidor vinculado usando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cliente OLE DB Provider, que é o provedor OLE DB oficial para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
```  
//Connect to the local, default instance of SQL Server.   
{   
   Server srv = new Server();   
   //Create a linked server.   
   LinkedServer lsrv = default(LinkedServer);   
   lsrv = new LinkedServer(srv, "OLEDBSRV");   
   //When the product name is SQL Server the remaining properties are   
   //not required to be set.   
   lsrv.ProductName = "SQL Server";   
   lsrv.Create();   
}   
```  
  
## <a name="creating-a-link-to-an-ole-db-provider-server-in-powershell"></a>Criando um link para um servidor de provedor OLE DB no PowerShell  
 O exemplo de código mostra como criar um link para um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] OLE DB, origem de dados heterogêneos usando o <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> objeto. Especificando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como o nome do produto, os dados são acessados no servidor vinculado usando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cliente OLE DB Provider, que é o provedor OLE DB oficial para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
```  
#Get a server object which corresponds to the default instance  
$svr = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#Create a linked server object which corresponds to an OLEDB type of SQL server product  
$lsvr = New-Object -TypeName Microsoft.SqlServer.Management.SMO.LinkedServer -argumentlist $svr,"OLEDBSRV"  
  
#When the product name is SQL Server the remaining properties are not required to be set.   
$lsvr.ProductName = "SQL Server"  
  
#Create the Database Object  
$lsvr.Create()   
```  
  
  