---
title: Executando consultas SQL (provedor SQLXMLOLEDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- queries [SQLXML], SQLXMLOLEDB Provider
- xml root property [SQLXML]
- SQLXMLOLEDB Provider, executing SQL queries
- SQL queries [SQLXML]
ms.assetid: 50334cf5-9c87-4c00-9beb-e08577c4fa82
author: rothja
ms.author: jroth
ms.openlocfilehash: f8410a4a0ecc8d522a38e22315746cb45295e6bb
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85015819"
---
# <a name="executing-sql-queries-sqlxmloledb-provider"></a>Executando consultas SQL (provedor SQLXMLOLEDB)
  Este exemplo ilustra o uso das seguintes propriedades específicas de provedor SQLXMLOLEDB:  
  
-   ClientSideXML  
  
-   xml root  
  
 Neste aplicativo de exemplo ADO do lado do cliente, uma consulta SQL simples é executada no cliente. Como a propriedade ClientSideXML é definida como true, a instrução SELECT sem a cláusula FOR XML é enviada ao servidor. O servidor executa a consulta e retorna um conjunto de linhas para o cliente. O cliente aplica a transformação de FOR XML ao conjunto de linhas e produz um documento XML.  
  
 A propriedade raiz XML fornece o único elemento raiz de nível superior para o documento XML gerado.  
  
> [!NOTE]  
>  No código, é necessário fornecer o nome da instância do Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] na cadeia de conexão. Este exemplo também especifica o uso do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (SQLNCLI11) para o provedor de dados, o que requer a instalação adicional do software cliente da rede. Para obter mais informações, consulte [requisitos do sistema para SQL Server Native Client](../../native-client/system-requirements-for-sql-server-native-client.md).  
  
```  
Option Explicit  
Sub main()  
Dim oTestStream As New ADODB.Stream  
Dim oTestConnection As New ADODB.Connection  
Dim oTestCommand As New ADODB.Command  
  
oTestConnection.Open "provider=SQLXMLOLEDB.4.0;data provider=SQLNCLI11;data source=SqlServerName;initial catalog=AdventureWorks;Integrated Security=SSPI ;"  
oTestCommand.ActiveConnection = oTestConnection  
oTestCommand.Properties("ClientSideXML") = True  
oTestCommand.CommandText = "SELECT TOP 10 FirstName, LastName FROM Person.Contact FOR XML AUTO"  
oTestStream.Open  
oTestCommand.Properties("Output Stream").Value = oTestStream  
oTestCommand.Properties("xml root") = "root"  
oTestCommand.Execute , , adExecuteStream  
  
oTestStream.Position = 0  
oTestStream.Charset = "utf-8"  
Debug.Print oTestStream.ReadText(adReadAll)  
End Sub  
Sub Form_Load()  
 main  
End Sub  
```  
  
  
