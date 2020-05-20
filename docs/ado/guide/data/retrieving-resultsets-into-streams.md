---
title: Recuperando conjuntos de resultados em fluxos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/20/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- streams [ADO], retrieving query results
- query results into stream [ADO]
- retrieving results into stream [ADO]
ms.assetid: 996c1321-c926-4f57-8297-85c8c20de974
author: rothja
ms.author: jroth
ms.openlocfilehash: b20363f3ffae96750046ab98bd623ea44d68a8e2
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760922"
---
# <a name="retrieving-resultsets-into-streams"></a>Recuperar conjuntos de resultados em fluxos
Em vez de receber resultados no objeto **Recordset** tradicional, o ADO pode, em vez disso, recuperar os resultados da consulta em um fluxo. O objeto de **fluxo** ADO (ou outros objetos que dão suporte à interface com **IStream** , como os objetos **Request** e **Response** do ASP) pode ser usado para conter esses resultados. Um uso para esse recurso é recuperar resultados em formato XML. Com SQL Server, por exemplo, os resultados de XML podem ser retornados de várias maneiras, como usar a cláusula FOR XML com uma consulta SQL SELECT ou usando uma consulta XPath.  
  
 Para receber resultados da consulta no formato de fluxo em vez de em um **conjunto de registros**, você deve especificar a constante **adExecuteStream** de **ExecuteOptionEnum** como um parâmetro do método **Execute** de um objeto **Command** . Se seu provedor oferecer suporte a esse recurso, os resultados serão retornados em um fluxo após a execução. Talvez seja necessário especificar propriedades específicas do provedor adicionais antes que o código seja executado. Por exemplo, com o provedor de OLE DB da Microsoft para SQL Server, as propriedades como **fluxo de saída** na coleção **Propriedades** do objeto de **comando** devem ser especificadas. Para obter mais informações sobre propriedades dinâmicas específicas de SQL Server relacionadas a esse recurso, consulte Propriedades relacionadas a XML no Manuais Online do SQL Server.  
  
## <a name="for-xml-query-example"></a>Exemplo de consulta FOR XML  
 O exemplo a seguir é escrito em VBScript para o banco de dados Northwind:  
  
```html
<!-- BeginRecordAndStreamVBS -->  
<%@ LANGUAGE = VBScript %>  
<%  Option Explicit      %>  
  
<HTML>  
<HEAD>  
<META NAME="GENERATOR" Content="Microsoft Developer Studio"/>  
<META HTTP-EQUIV="Content-Type" content="text/html"; charset="iso-8859-1">  
<TITLE>FOR XML Query Example</TITLE>  
  
<STYLE>  
   BODY  
   {  
      FONT-FAMILY: Tahoma;  
      FONT-SIZE: 8pt;  
      OVERFLOW: auto  
   }  
  
   H3  
   {  
      FONT-FAMILY: Tahoma;  
      FONT-SIZE: 8pt;  
      OVERFLOW: auto  
   }  
</STYLE>  
  
<!-- #include file="adovbs.inc" -->  
<%  
   Response.Write "<H3>Server-side processing</H3>"  
  
   Response.Write "Page Generated @ " & Now() & "<BR/>"  
  
   Dim adoConn  
   Set adoConn = Server.CreateObject("ADODB.Connection")  
  
   Dim sConn  
   sConn = "Provider=SQLOLEDB;Data Source=" & _  
      Request.ServerVariables("SERVER_NAME") & ";" & _  
      Initial Catalog=Northwind;Integrated Security=SSPI;"  
  
   Response.write "Connect String = " & sConn & "<BR/>"  
  
   adoConn.ConnectionString = sConn  
   adoConn.CursorLocation = adUseClient  
  
   adoConn.Open  
  
   Response.write "ADO Version = " & adoConn.Version & "<BR/>"  
   Response.write "adoConn.State = " & adoConn.State & "<BR/>"  
  
   Dim adoCmd  
   Set adoCmd = Server.CreateObject("ADODB.Command")  
   Set adoCmd.ActiveConnection = adoConn  
  
   Dim sQuery  
   sQuery = "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'><sql:query>SELECT * FROM PRODUCTS WHERE ProductName='Gumbr Gummibrchen' FOR XML AUTO</sql:query></ROOT>"  
  
   Response.write "Query String = " & sQuery & "<BR/>"  
  
   Dim adoStreamQuery  
   Set adoStreamQuery = Server.CreateObject("ADODB.Stream")  
   adoStreamQuery.Open  
   adoStreamQuery.WriteText sQuery, adWriteChar  
   adoStreamQuery.Position = 0  
  
   adoCmd.CommandStream = adoStreamQuery  
   adoCmd.Dialect = "{5D531CB2-E6Ed-11D2-B252-00C04F681B71}"  
  
   Response.write "Pushing XML to client for processing "  & "<BR/>"  
  
   adoCmd.Properties("Output Stream") = Response  
   Response.write "<XML ID='MyDataIsle'>"  
   adoCmd.Execute , , 1024  
   Response.write "</XML>"  
  
%>  
  
<SCRIPT language="VBScript" For="window" Event="onload">  
   Dim xmlDoc  
   Set xmlDoc = MyDataIsle.XMLDocument  
   xmlDoc.resolveExternals=false  
   xmlDoc.async=false  
  
   If xmlDoc.parseError.Reason <> "" then  
      Msgbox "parseError.Reason = " & xmlDoc.parseError.Reason  
   End If  
  
   Dim root, child  
   Set root = xmlDoc.documentElement  
   For each child in root.childNodes  
      dim OutputXML  
      OutputXML = document.all("log").innerHTML  
      document.all("log").innerHTML = OutputXML & "<LI>" & child.getAttribute("ProductName") & "</LI>"  
   Next  
</SCRIPT>  
  
</HEAD>  
  
<BODY>  
  
   <H3>Client-side processing of XML Document MyDataIsle</H3>  
   <UL id=log>  
   </UL>  
  
</BODY>  
</HTML>  
<!-- EndRecordAndStreamVBS -->  
  
```  
  
 A cláusula FOR XML instrui SQL Server retornar dados na forma de um documento XML.  
  
### <a name="for-xml-syntax"></a>Sintaxe de FOR XML  
  
```syntax
FOR XML [RAW|AUTO|EXPLICIT]  
```  
  
 FOR XML RAW gera elementos de linha genéricos que têm valores de coluna como atributos. FOR XML AUTO utiliza heurística para gerar uma árvore hierárquica com nomes de elementos com base em nomes de tabela. FOR XML EXPLICIT gera uma tabela universal com relações totalmente descritas pelos metadados.  
  
 Segue um exemplo de instrução SQL SELECT FOR XML:  
  
```sql
SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME FOR XML AUTO  
```  
  
 O comando pode ser especificado em uma cadeia de caracteres, conforme mostrado anteriormente, atribuído a **CommandText**ou na forma de uma consulta de modelo XML atribuída a **CommandStream**. Para obter mais informações sobre consultas de modelo XML, consulte [fluxos de comando](../../../ado/guide/data/command-streams.md) no ADO ou usando fluxos para entrada de comando no manuais online do SQL Server.  
  
 Como uma consulta de modelo XML, a consulta FOR XML aparece da seguinte maneira:  
  
```xml
<sql:query> SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME FOR XML AUTO </sql:query>  
```  
  
 Este exemplo especifica o objeto de **resposta** ASP para a propriedade de **fluxo de saída** :  
  
```vb
adoCmd.Properties("Output Stream") = Response  
```  
  
 Em seguida, especifique o parâmetro **adExecuteStream** de **Execute**. Este exemplo encapsula o fluxo em marcas XML para criar uma ilha de dados XML:  
  
```vb
Response.write "<XML ID=MyDataIsle>"  
adoCmd.Execute , , adExecuteStream  
Response.write "</XML>"  
```  
  
### <a name="remarks"></a>Comentários  
 Neste ponto, o XML foi transmitido para o navegador do cliente e está pronto para ser exibido. Isso é feito usando o VBScript do lado do cliente para associar o documento XML a uma instância do DOM e fazer o loop por meio de cada nó filho para criar uma lista de produtos em HTML.
