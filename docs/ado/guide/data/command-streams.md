---
title: Fluxos de comando | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- command streams [ADO]
- streams [ADO], command
ms.assetid: 0ac09dbe-2665-411e-8fbb-d1efe6c777be
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fd0c2273739a3651c7fdd4c424ce0cb47d39dd5b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67925841"
---
# <a name="command-streams"></a>Fluxos de comando
O ADO sempre tem suporte para entrada de comando no formato de cadeia de caracteres especificado pela propriedade **CommandText** . Como alternativa, com o ADO 2,7 ou posterior, você também pode usar um fluxo de informações para entrada de comando atribuindo o fluxo à propriedade **CommandStream** . Você pode atribuir um objeto de **fluxo** ADO ou qualquer objeto que ofereça suporte à interface com **IStream** .  
  
 O conteúdo do fluxo de comando é simplesmente passado do ADO para seu provedor, de modo que seu provedor deve dar suporte à entrada de comando por fluxo para que esse recurso funcione. Por exemplo, SQL Server dá suporte a consultas na forma de modelos XML ou extensões OpenXML para Transact-SQL.  
  
 Como os detalhes do fluxo devem ser interpretados pelo provedor, você deve especificar o dialeto de comando definindo a propriedade **dialeto** . O valor de **dialeto** é uma cadeia de caracteres que contém um GUID, que é definido pelo seu provedor. Para obter informações sobre valores válidos para **dialeto** com suporte no seu provedor, consulte a documentação do provedor.  
  
## <a name="xml-template-query-example"></a>Exemplo de consulta de modelo XML  
 O exemplo a seguir é escrito em VBScript para o banco de dados Northwind.  
  
 Primeiro, inicialize e abra o objeto de **fluxo** que será usado para conter o fluxo de consulta:  
  
```  
Dim adoStreamQuery  
Set adoStreamQuery = Server.CreateObject("ADODB.Stream")  
adoStreamQuery.Open  
```  
  
 O conteúdo do fluxo de consulta será uma consulta de modelo XML.  
  
 A consulta de modelo requer uma referência ao namespace de XML identificado pelo prefixo SQL: da marca \<SQL: Query>. Uma instrução SQL SELECT é incluída como o conteúdo do modelo XML e atribuída a uma variável de cadeia de caracteres da seguinte maneira:  
  
```  
sQuery = "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'>  
<sql:query> SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME </sql:query>  
</ROOT>"  
```  
  
 Em seguida, grave a cadeia de caracteres no fluxo:  
  
```  
adoStreamQuery.WriteText sQuery, adWriteChar  
adoStreamQuery.Position = 0  
```  
  
 Atribua adoStreamQuery à propriedade **CommandStream** de um objeto de **comando** ADO:  
  
```  
Dim adoCmd  
Set adoCmd  = Server.CreateObject("ADODB.Command"")  
adoCmd.CommandStream = adoStreamQuery  
```  
  
 Especifique o **dialeto**do idioma do comando, que indica como o provedor de OLE DB de SQL Server deve interpretar o fluxo de comando. O dialeto especificado por um GUID específico do provedor:  
  
```  
adoCmd.Dialect = "{5D531CB2-E6Ed-11D2-B252-00C04F681B71}"  
```  
  
 Por fim, execute a consulta e retorne os resultados para um objeto **Recordset** :  
  
```  
Set objRS = adoCmd.Execute  
```
