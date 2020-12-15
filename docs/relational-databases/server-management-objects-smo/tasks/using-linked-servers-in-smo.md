---
description: Usando servidores vinculados no SMO
title: Usando servidores vinculados em SMO | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- linked servers [SQL Server], SMO
ms.assetid: 0ea8837b-2596-4df1-b065-3bb717c9f22c
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8f6d7474189e618e6d8afb9c9fe5541b98d962a8
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97473217"
---
# <a name="using-linked-servers-in-smo"></a>Usando servidores vinculados no SMO
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  Um servidor vinculado representa uma fonte de dados OLE DB em um servidor remoto. Fontes de dados remotas OLE DB são vinculadas à instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando o objeto <xref:Microsoft.SqlServer.Management.Smo.LinkedServer>.  
  
 Os servidores de banco de dados remotos podem ser vinculados à instância atual do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando um provedor de OLE DB. No SMO, servidores vinculados são representados pelo objeto <xref:Microsoft.SqlServer.Management.Smo.LinkedServer>. A propriedade <xref:Microsoft.SqlServer.Management.Smo.LinkedServer.LinkedServerLogins%2A> referencia uma coleção de objetos <xref:Microsoft.SqlServer.Management.Smo.LinkedServerLogin>. Aqui são armazenadas as credenciais de logon que são necessárias para estabelecer uma conexão com o servidor vinculado.  
  
## <a name="ole-db-providers"></a>Provedores OLE DB  
 No SMO, provedores OLE DB instalados são representados por uma coleção de objetos <xref:Microsoft.SqlServer.Management.Smo.OleDbProviderSettings>.  
  
## <a name="example"></a>Exemplo  
 Para os exemplos de código a seguir, selecione o ambiente de programação, o modelo de programação e a linguagem de programação para criar seu aplicativo. Para obter mais informações, consulte [criar um projeto do Visual C&#35; Smo no Visual Studio .net](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-a-link-to-an-ole-db-provider-server-in-visual-c"></a>Criando um link com um servidor de provedor OLE DB no Visual C#  
 O exemplo de código mostra como criar um vínculo para uma fonte de dados heterogêneos OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], usando o objeto <xref:Microsoft.SqlServer.Management.Smo.LinkedServer>. Especificando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como o nome do produto, os dados são acessados no servidor vinculado usando o Provedor OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Client, que é o provedor OLE DB oficial do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
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
 O exemplo de código mostra como criar um vínculo para uma fonte de dados heterogêneos OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], usando o objeto <xref:Microsoft.SqlServer.Management.Smo.LinkedServer>. Especificando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como o nome do produto, os dados são acessados no servidor vinculado usando o Provedor OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Client, que é o provedor OLE DB oficial do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
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
  
  
