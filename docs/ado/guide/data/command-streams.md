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
manager: craigg
ms.openlocfilehash: e6a5e9581a2a236eab869e74825ee97e7e289d44
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62472692"
---
# <a name="command-streams"></a>Fluxos de comando
ADO sempre tem suporte para entrada de comando no formato de cadeia de caracteres especificado pelo **CommandText** propriedade. Como alternativa, com o ADO 2.7 ou posterior, você também pode usar um fluxo de informações para a entrada de comando, atribuindo o fluxo para o **CommandStream** propriedade. Você pode atribuir ADO **Stream** ou qualquer objeto que dá suporte a COM **IStream** interface.  
  
 O conteúdo do fluxo de comando é passado simplesmente do ADO para seu provedor, para que seu provedor deve oferecer suporte a entrada de comando por fluxo para esse recurso funcione. Por exemplo, o SQL Server dá suporte a consultas na forma de modelos XML ou OpenXML extensões para Transact-SQL.  
  
 Como os detalhes do fluxo devem ser interpretados pelo provedor, você deve especificar o dialeto do comando, definindo o **dialeto** propriedade. O valor de **dialeto** é uma cadeia de caracteres que contém um GUID, que é definido por seu provedor. Para obter informações sobre valores válidos para **dialeto** com suporte pelo seu provedor, consulte a documentação do provedor.  
  
## <a name="xml-template-query-example"></a>Exemplo de consulta de modelo XML  
 O exemplo a seguir é escrito em VBScript para o banco de dados Northwind.  
  
 Primeiro, inicializar e abrir o **Stream** objeto que será usado para conter o fluxo de consulta:  
  
```  
Dim adoStreamQuery  
Set adoStreamQuery = Server.CreateObject("ADODB.Stream")  
adoStreamQuery.Open  
```  
  
 O conteúdo do fluxo de consulta será uma consulta de modelo XML.  
  
 A consulta do modelo requer uma referência ao namespace XML identificada pelo sql: prefixo do \<sql:query > marca. Uma instrução SQL SELECT é incluída como o conteúdo do modelo XML e atribuída a uma variável de cadeia de caracteres da seguinte maneira:  
  
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
  
 Atribuir adoStreamQuery para o **CommandStream** propriedade do ADO **comando** objeto:  
  
```  
Dim adoCmd  
Set adoCmd  = Server.CreateObject("ADODB.Command"")  
adoCmd.CommandStream = adoStreamQuery  
```  
  
 Especifique a linguagem de comandos **dialeto**, que indica como o SQL Server OLE DB Provider deve interpretar o fluxo de comando. O dialeto especificado por um GUID específico do provedor:  
  
```  
adoCmd.Dialect = "{5D531CB2-E6Ed-11D2-B252-00C04F681B71}"  
```  
  
 Por fim, execute a consulta e retornam os resultados para um **Recordset** objeto:  
  
```  
Set objRS = adoCmd.Execute  
```
