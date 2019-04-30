---
title: Fluxos e persistência | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- persisted streams [ADO]
- streams [ADO], persistence
ms.assetid: ad5bf52c-fd10-4cfa-bf7d-fcedcaa41eea
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 80f81dcff4f6220257e1210f5bc9dad7baca0b03
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63062624"
---
# <a name="streams-and-persistence"></a>Fluxos e persistência
O [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto [salve](../../../ado/reference/ado-api/save-method.md) armazenamentos de método, ou *persistir*, um **Recordset** em um arquivo e o [abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md)restaurações de método de **Recordset** desse arquivo.  
  
 Com o ADO 2.7 ou posterior, o **salvar** e **abra** métodos podem persistir um **conjunto de registros** para um [Stream](../../../ado/reference/ado-api/stream-object-ado.md) objeto também. Esse recurso é especialmente útil ao trabalhar com o serviço de dados remota (RDS) e o Active Server Pages (ASP).  
  
 Para obter mais informações sobre como persistência pode ser usada por si só em páginas ASP, consulte a documentação atual do ASP.  
  
 A seguir está alguns cenários que mostram como **Stream** objetos e persistência podem ser usados.  
  
## <a name="scenario-1"></a>Cenário 1  
 Neste cenário simplesmente salva uma **conjunto de registros** para um arquivo e, em seguida, para um **Stream**. Ele é aberto o fluxo persistido em outro **conjunto de registros**.  
  
```  
Dim rs1 As ADODB.Recordset  
Dim rs2 As ADODB.Recordset  
Dim stm As ADODB.Stream  
  
Set rs1 = New ADODB.Recordset  
Set rs2 = New ADODB.Recordset  
Set stm = New ADODB.Stream  
  
rs1.Open   "SELECT * FROM Customers", "Provider=sqloledb;" & _  
        "Data Source=MyServer;Initial Catalog=Northwind;" & _  
        "Integrated Security=SSPI;""", adopenStatic, adLockReadOnly, adCmdText  
rs1.Save "c:\myfolder\mysubfolder\myrs.xml", adPersistXML  
rs1.Save stm, adPersistXML  
rs2.Open stm  
```  
  
## <a name="scenario-2"></a>Cenário 2  
 Esse cenário persiste um **conjunto de registros** em um **Stream** em formato XML. Em seguida, ele lê a **Stream** em uma cadeia de caracteres que você pode examinar, manipular ou exibir.  
  
```  
Dim rs As ADODB.Recordset  
Dim stm As ADODB.Stream  
Dim strRst As String  
  
Set rs = New ADODB.Recordset  
Set stm = New ADODB.Stream  
  
' Open, save, and close the recordset.   
rs.Open "SELECT * FROM Customers", "Provider=sqloledb;" & _  
        "Data Source=MyServer;Initial Catalog=Northwind;" & _  
        "Integrated Security=SSPI;"""  
rs.Save stm, adPersistXML  
rs.Close  
Set rs = nothing  
  
' Put saved Recordset into a string variable.  
strRst = stm.ReadText(adReadAll)  
  
' Examine, manipulate, or display the XML data.  
...  
```  
  
## <a name="scenario-3"></a>Cenário 3  
 Esse código de exemplo mostra a persistência de código ASP uma **conjunto de registros** como XML diretamente para o **resposta** objeto:  
  
```  
...  
<%  
response.ContentType = "text/xml"  
  
' Create and open a Recordset.  
Set rs = Server.CreateObject("ADODB.Recordset")  
rs.Open "select * from Customers", "Provider=sqloledb;" & _  
        "Data Source=MyServer;Initial Catalog=Northwind;" & _  
        "Integrated Security=SSPI;"""  
  
' Save Recordset directly into output stream.  
rs.Save Response, adPersistXML   
  
' Close Recordset.  
rs.Close  
Set rs = nothing  
%>  
...  
```  
  
## <a name="scenario-4"></a>Cenário 4  
 Nesse cenário, o código ASP grava o conteúdo a **Recordset** no formato ADTG ao cliente. O [Microsoft Cursor Service para OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) pode usar esses dados para criar um desconectado **conjunto de registros**.  
  
 Uma nova propriedade no RDS [DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md), [URL](../../../ado/reference/rds-api/url-property-rds.md), aponta para a página. ASP que gera a **conjunto de registros**. Isso significa que um **conjunto de registros** objeto pode ser obtido sem RDS usando o lado do servidor [DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) objeto ou o usuário escrever um objeto comercial. Isso simplifica o modelo de programação do RDS significativamente.  
  
 Código do lado do servidor, chamado de https://server/directory/recordset.asp:  
  
```  
<%  
Dim rs   
Set rs = Server.CreateObject("ADODB.Recordset")  
rs.Open "select au_fname, au_lname, phone from Authors", ""& _  
        "Provider=sqloledb;Data Source=MyServer;" & _  
        "Initial Catalog=Pubs;Integrated Security=SSPI;"  
response.ContentType = "multipart/mixed"  
rs.Save response, adPersistADTG  
%>  
```  
  
 Código do lado do cliente:  
  
```  
<HTML>  
<HEAD>  
<TITLE>RDS Query Page</TITLE>  
</HEAD>  
<body>  
<CENTER>  
<H1>Remote Data Service 2.5</H1>  
<TABLE DATASRC="#DC1">  
   <TR>   
      <TD><SPAN DATAFLD="au_fname"></SPAN></TD>  
      <TD><SPAN DATAFLD="au_lname"></SPAN></TD>  
      <TD><SPAN DATAFLD="phone"></SPAN></TD>  
   </TR>  
</TABLE>  
<BR>  
  
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"  
    ID=DC1 HEIGHT=1 WIDTH = 1>  
    <PARAM NAME="URL" VALUE="https://server/directory/recordset.asp">  
</OBJECT>  
  
</SCRIPT>  
</BODY>  
</HTML>  
```  
  
 Os desenvolvedores também têm a opção de usar um **Recordset** objeto no cliente:  
  
```  
...  
function GetRs()   
    {  
    rs = CreateObject("ADODB.Recordset");  
    rs.Open "https://server/directory/recordset.asp"  
    DC1.SourceRecordset = rs;  
    }  
...  
```  
  
## <a name="see-also"></a>Consulte também  
 [Método Open (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Método Save](../../../ado/reference/ado-api/save-method.md)
