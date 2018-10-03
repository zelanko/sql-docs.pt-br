---
title: Recuperando conjuntos de resultados em fluxos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- streams [ADO], retrieving query results
- query results into stream [ADO]
- retrieving results into stream [ADO]
ms.assetid: 996c1321-c926-4f57-8297-85c8c20de974
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 45ba231b1523a74ac8b2c09f55e19c3dc287ef20
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47734954"
---
# <a name="retrieving-resultsets-into-streams"></a>Recuperar conjuntos de resultados em fluxos
Em vez de receber os resultados em tradicional **Recordset** objeto ADO em vez disso, pode recuperar os resultados da consulta em um fluxo. O ADO **Stream** objeto (ou outros objetos que dão suporte a COM **IStream** interface, como o ASP **solicitar** e **resposta** objetos ) pode ser usado para conter esses resultados. Um uso para esse recurso é para recuperar os resultados em formato XML. Com o SQL Server, por exemplo, resultados XML podem ser retornados de várias maneiras, como usar a cláusula FOR XML com uma consulta SQL SELECT ou usando uma consulta XPath.  
  
 Para receber os resultados da consulta em formato de fluxo em vez de usar um **conjunto de registros**, você deve especificar o **adExecuteStream** constante do **ExecuteOptionEnum** como um parâmetro das **Execute** método de um **comando** objeto. Se seu provedor oferecer suporte a esse recurso, os resultados serão retornados em um fluxo após a execução. Talvez seja necessário especificar propriedades adicionais do provedor específico antes do código é executado. Por exemplo, com o Microsoft OLE DB Provider para SQL Server, propriedades, como **saída Stream** na **propriedades** coleção dos **comando** objeto deve ser especificado. Para obter mais informações sobre propriedades dinâmicas específicas do SQL Server, relacionado a esse recurso, consulte XML-Related propriedades no SQL Server Books Online.  
  
## <a name="for-xml-query-example"></a>Por exemplo de consulta XML  
 O exemplo a seguir é gravado em VBScript para o banco de dados Northwind:  
  
```  
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
  
 A cláusula FOR XML instrui o SQL Server para retornar dados na forma de um documento XML.  
  
### <a name="for-xml-syntax"></a>Para obter a sintaxe XML  
  
```  
FOR XML [RAW|AUTO|EXPLICIT]  
```  
  
 PARA XML brutos gera elementos de linha genéricos que têm valores de coluna como atributos. FOR XML AUTO usa heurística para gerar uma árvore hierárquica com nomes de elementos com base em nomes de tabela. FOR XML EXPLICIT gera uma tabela universal com relações totalmente descritas por metadados.  
  
 Segue um exemplo de instrução SQL SELECT FOR XML:  
  
```  
SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME FOR XML AUTO  
```  
  
 O comando pode ser especificado em uma cadeia de caracteres, conforme mostrado anteriormente, atribuído a **CommandText**, ou na forma de uma consulta de modelo XML atribuída a **CommandStream**. Para obter mais informações sobre consultas de modelo XML, consulte [fluxos de comando](../../../ado/guide/data/command-streams.md) no ADO ou usando fluxos de entrada de comando no SQL Server Books Online.  
  
 Como uma consulta de modelo XML, a consulta FOR XML aparece da seguinte maneira:  
  
```  
<sql:query> SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME FOR XML AUTO </sql:query>  
```  
  
 Este exemplo especifica que o ASP **resposta** do objeto para o **saída Stream** propriedade:  
  
```  
adoCmd.Properties("Output Stream") = Response  
```  
  
 Em seguida, especifique **adExecuteStream** parâmetro do **Execute**. Este exemplo envolve o fluxo de marcas XML para criar uma ilha de dados XML:  
  
```  
Response.write "<XML ID=MyDataIsle>"  
adoCmd.Execute , , adExecuteStream  
Response.write "</XML>"  
```  
  
### <a name="remarks"></a>Comentários  
 Neste ponto, XML que está sendo transmitida ao navegador do cliente e está pronta para ser exibido. Isso é feito usando o VBScript do lado do cliente para associar o documento XML a uma instância do DOM e executando um loop em cada nó filho para criar uma lista de produtos em HTML.
