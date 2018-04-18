---
title: Usando servidores vinculados no SMO | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: smo
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- linked servers [SQL Server], SMO
ms.assetid: 0ea8837b-2596-4df1-b065-3bb717c9f22c
caps.latest.revision: 36
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 5e14e7516cbf5998c89165efe6b55775d8da9ecb
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="using-linked-servers-in-smo"></a>Usando servidores vinculados no SMO
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  Um servidor vinculado representa uma fonte de dados OLE DB em um servidor remoto. Fontes de dados OLE DB remotas estão vinculadas à instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando o <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> objeto.  
  
 Servidores de banco de dados remoto podem ser vinculados à instância atual do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando um provedor OLE DB. No SMO, servidores vinculados são representados pelo <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> objeto. O <xref:Microsoft.SqlServer.Management.Smo.LinkedServer.LinkedServerLogins%2A> propriedade referencia uma coleção de <xref:Microsoft.SqlServer.Management.Smo.LinkedServerLogin> objetos. Aqui são armazenadas as credenciais de logon que são necessárias para estabelecer uma conexão com o servidor vinculado.  
  
## <a name="ole-db-providers"></a>Provedores OLE DB  
 No SMO, provedores OLE DB instalados são representados por uma coleção de objetos <xref:Microsoft.SqlServer.Management.Smo.OleDbProviderSettings>.  
  
## <a name="example"></a>Exemplo  
 Para os exemplos de código a seguir, selecione o ambiente de programação, o modelo de programação e a linguagem de programação para criar seu aplicativo. Para obter mais informações, consulte [criar um Visual C&#35; projeto SMO no Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-a-link-to-an-ole-db-provider-server-in-visual-c"></a>Criando um link com um servidor de provedor OLE DB no Visual C#  
 O exemplo de código mostra como criar um link para um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] OLE DB, origem de dados heterogêneos usando o <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> objeto. Especificando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como o nome do produto, os dados são acessados no servidor vinculado usando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cliente OLE DB Provider, que é o provedor OLE DB oficial para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
```csharp  
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
  
```powershell  
#Get a server object which corresponds to the default instance  
$svr = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#Create a linked server object which corresponds to an OLEDB type of SQL server product  
$lsvr = New-Object -TypeName Microsoft.SqlServer.Management.SMO.LinkedServer -argumentlist $svr,"OLEDBSRV"  
  
#When the product name is SQL Server the remaining properties are not required to be set.   
$lsvr.ProductName = "SQL Server"  
  
#Create the Database Object  
$lsvr.Create()   
```  
  
  
