---
title: Executar modelos com consultas SQL (SQLXMLOLEDB)
description: Exiba um exemplo de um aplicativo ADO do lado do cliente usando o provedor SQLXMLOLEDB para executar um modelo XML do lado do servidor que contém uma consulta SQL.
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- templates [SQLXML]
- SQLXMLOLEDB Provider, executing template files
- templates [SQLXML], SQL queries
- XML templates [SQLXML]
- SQL queries [SQLXML]
ms.assetid: ff2bc36f-e3fb-4d8f-8e3a-2680a39eda11
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7c97dd6675b13d5f47298f3791f8f47da793a9a8
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85650391"
---
# <a name="executing-templates-that-contain-sql-queries-sqlxmloledb-provider"></a>Executando modelos que contêm consultas SQL (provedor SQLXMLOLEDB)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  Este exemplo ilustra o uso da propriedade ClientSideXML específica do provedor SQLXMLOLEDB. Nesse aplicativo de exemplo de ADO do lado cliente, um modelo XML que consiste em uma consulta SQL é executado no servidor.  
  
 Como a propriedade ClientSideXML é definida como true, a instrução SELECT sem a cláusula FOR XML é enviada ao servidor. O servidor executa a consulta e retorna um conjunto de linhas para o cliente. O cliente aplica a transformação de FOR XML ao conjunto de linhas e produz um documento XML.  
  
 O modelo XML fornece um único elemento raiz de nível superior ( \<ROOT> ) para o documento XML que é gerado; portanto, a propriedade raiz XML não é fornecida.  
  
 Para executar modelos de XML, o dialeto {5d531cb2-e6ed-11d2-b252-00c04f681b71} deve ser especificado.  
  
> [!NOTE]  
>  No código, é necessário fornecer o nome da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] na cadeia de conexão. Além disso, este exemplo especifica o uso do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cliente nativo (SQLNCLI11) para o provedor de dados que requer a instalação de um software cliente de rede adicional. Para obter mais informações, consulte [requisitos do sistema para SQL Server Native Client](../../../relational-databases/native-client/system-requirements-for-sql-server-native-client.md).  
  
```  
Option Explicit  
  
Sub Main()  
  Dim oTestStream As New ADODB.Stream  
  Dim oTestConnection As New ADODB.Connection  
  Dim oTestCommand As New ADODB.Command  
  oTestConnection.Open "Provider=SQLXMLOLEDB.4.0;Data Provider=SQLNCLI11;Data Source=SqlServerName;Initial Catalog=AdventureWorks;Integrated Security=SSPI;"  
  
  Set oTestCommand.ActiveConnection = oTestConnection  
  oTestCommand.Properties("ClientSideXML") = True  
  oTestCommand.CommandText = "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'> " & _  
        " <sql:query> " & _  
        "   SELECT TOP 10 FirstName, LastName FROM Person.Contact FOR XML AUTO " & _  
        "   </sql:query> " & _  
        " </ROOT> "  
  oTestStream.Open  
  ' You need the dialect if you are executing   
  ' XML templates (not for SQL queries).  
  oTestCommand.Dialect = "{5d531cb2-e6ed-11d2-b252-00c04f681b71}"  
  oTestCommand.Properties("Output Stream").Value = oTestStream  
  oTestCommand.Execute , , adExecuteStream  
  
  oTestStream.Position = 0  
  oTestStream.Charset = "utf-8"  
  Debug.Print oTestStream.ReadText(adReadAll)  
End Sub  
  
Sub Form_Load()  
  Main  
End Sub  
```  
  
  
