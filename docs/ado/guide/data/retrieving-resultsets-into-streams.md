---
title: Recuperando conjuntos de resultados em fluxos | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- streams [ADO], retrieving query results
- query results into stream [ADO]
- retrieving results into stream [ADO]
ms.assetid: 996c1321-c926-4f57-8297-85c8c20de974
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9aadb2a81cc93effa0c280f5f74e6403c7403756
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="retrieving-resultsets-into-streams"></a>Recuperando conjuntos de resultados em fluxos
Em vez de receber os resultados nas tradicional **registros** objeto ADO em vez disso, pode recuperar os resultados da consulta em um fluxo. O ADO **fluxo** objeto (ou outros objetos que dão suporte a COM **IStream** interface, como o ASP **solicitação** e **resposta** objetos ) pode ser usado para conter os resultados. Um uso para esse recurso é para recuperar os resultados em formato XML. Com o SQL Server, por exemplo, resultados XML podem ser retornados de várias maneiras, como usando a cláusula FOR XML com uma consulta SQL SELECT ou uma consulta XPath.  
  
 Para receber os resultados da consulta em formato de fluxo em vez de usar um **Recordset**, você deve especificar o **adExecuteStream** constante de **ExecuteOptionEnum** como um parâmetro a **Execute** método de um **comando** objeto. Se o provedor oferece suporte a esse recurso, os resultados serão retornados em um fluxo na execução. Talvez seja necessário especificar as propriedades adicionais específicas do provedor antes do código é executado. Por exemplo, com o Microsoft OLE DB Provider para SQL Server, propriedades, como **fluxo de saída** no **propriedades** coleção do **comando** objeto deve ser especificado. Para obter mais informações sobre propriedades dinâmicas específicos do SQL Server, relacionado a esse recurso, consulte XML-Related propriedades no SQL Server Books Online.  
  
## <a name="for-xml-query-example"></a>Por exemplo de consulta XML  
 O exemplo a seguir é gravado no VBScript para o banco de dados Northwind:  
  
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
  
 FOR XML RAW gera elementos de linha genérica que têm valores de coluna como atributos. FOR XML AUTO usa heurística para gerar uma árvore hierárquica com nomes de elemento com base nos nomes de tabela. FOR XML EXPLICIT gera uma tabela universal com relações totalmente descritas por metadados.  
  
 Segue um exemplo de instrução SQL SELECT FOR XML:  
  
```  
SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME FOR XML AUTO  
```  
  
 O comando pode ser especificado em uma cadeia de caracteres, como mostrado anteriormente, atribuído a **CommandText**, ou na forma de uma consulta de modelo XML atribuída a **CommandStream**. Para obter mais informações sobre consultas de modelo XML, consulte [comando fluxos](../../../ado/guide/data/command-streams.md) no ADO ou usando fluxos de entrada de comando no SQL Server Books Online.  
  
 Como uma consulta de modelo XML, a consulta FOR XML aparece da seguinte maneira:  
  
```  
<sql:query> SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME FOR XML AUTO </sql:query>  
```  
  
 Este exemplo especifica que o ASP **resposta** de objeto para o **fluxo de saída** propriedade:  
  
```  
adoCmd.Properties("Output Stream") = Response  
```  
  
 Em seguida, especifique **adExecuteStream** parâmetro **Execute**. Este exemplo ajusta o fluxo de marcas XML para criar uma ilha de dados XML:  
  
```  
Response.write "<XML ID=MyDataIsle>"  
adoCmd.Execute , , adExecuteStream  
Response.write "</XML>"  
```  
  
### <a name="remarks"></a>Comentários  
 Neste ponto, XML tenha sido transmitido para o navegador do cliente e está pronto para ser exibido. Isso é feito usando o VBScript do lado do cliente para associar o documento XML a uma instância do DOM e loop através de cada nó filho para criar uma lista de produtos em HTML.

