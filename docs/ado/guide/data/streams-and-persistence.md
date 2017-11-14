---
title: "Fluxos e persistência | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- persisted streams [ADO]
- streams [ADO], persistence
ms.assetid: ad5bf52c-fd10-4cfa-bf7d-fcedcaa41eea
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: af1ecf7ed9f4702d986d6f1881b3264ab8171c87
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="streams-and-persistence"></a>Fluxos e persistência
O [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto [salvar](../../../ado/reference/ado-api/save-method.md) repositórios de método ou *persistir*, um **registros** em um arquivo e o [abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md)método restaura o **registros** desse arquivo.  
  
 Com o ADO 2.7 ou posterior, o **salvar** e **abrir** métodos podem persistir um **Recordset** para um [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) objeto também. Esse recurso é especialmente útil ao trabalhar com o Remote Data Service (RDS) e o Active Server Pages (ASP).  
  
 Para obter mais informações sobre como persistência pode ser usada por si só nas páginas ASP, consulte a documentação atual do ASP.  
  
 Estes são alguns cenários que mostram como **fluxo** objetos e persistência podem ser usados.  
  
## <a name="scenario-1"></a>Cenário 1  
 Neste cenário simplesmente salva um **registros** para um arquivo e, em seguida, um **fluxo**. Ele é aberto o fluxo persistente em outro **registros**.  
  
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
 Essa situação persiste um **registros** em uma **fluxo** em formato XML. Ele lê o **fluxo** em uma cadeia de caracteres que você pode examinar, manipular ou exibir.  
  
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
 Este exemplo de código mostra a persistência de código ASP um **registros** como XML diretamente para o **resposta** objeto:  
  
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
 Nesse cenário, o código ASP grava o conteúdo do **registros** no formato ADTG ao cliente. O [do serviço Microsoft Cursor do OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) pode usar esses dados para criar um desconectada **registros**.  
  
 Uma nova propriedade no RDS [DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md), [URL](../../../ado/reference/rds-api/url-property-rds.md), aponta para a página. ASP que gera a **registros**. Isso significa um **registros** objeto pode ser obtido sem RDS usando o lado do servidor [DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) objeto ou o usuário gravar um objeto comercial. Isso simplifica o modelo de programação de RDS significativamente.  
  
 Código do lado do servidor, denominado http://server/directory/recordset.asp:  
  
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
    <PARAM NAME="URL" VALUE="http://server/directory/recordset.asp">  
</OBJECT>  
  
</SCRIPT>  
</BODY>  
</HTML>  
```  
  
 Os desenvolvedores também tem a opção de usar um **registros** objeto no cliente:  
  
```  
...  
function GetRs()   
    {  
    rs = CreateObject("ADODB.Recordset");  
    rs.Open "http://server/directory/recordset.asp"  
    DC1.SourceRecordset = rs;  
    }  
...  
```  
  
## <a name="see-also"></a>Consulte também  
 [Método Open (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Objeto de registro (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Método Save](../../../ado/reference/ado-api/save-method.md)

