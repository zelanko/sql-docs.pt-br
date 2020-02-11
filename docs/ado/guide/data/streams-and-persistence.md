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
ms.openlocfilehash: 22fbf503196c467a7816bf4e9c76151276cc6d4a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67924025"
---
# <a name="streams-and-persistence"></a>Fluxos e persistência
O método [Save](../../../ado/reference/ado-api/save-method.md) do objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) armazena, ou *persiste*, um **conjunto de registros** em um arquivo e o método [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) restaura o **conjunto de registros** desse arquivo.  
  
 Com o ADO 2,7 ou posterior, os métodos **Save** e **Open** também podem persistir um **conjunto de registros** em um objeto [Stream](../../../ado/reference/ado-api/stream-object-ado.md) . Esse recurso é especialmente útil ao trabalhar com o serviço de dados remoto (RDS) e páginas de Active Server (ASP).  
  
 Para obter mais informações sobre como a persistência pode ser usada por si só em páginas ASP, consulte a documentação ASP atual.  
  
 Veja a seguir alguns cenários que mostram como os objetos de **fluxo** e a persistência podem ser usados.  
  
## <a name="scenario-1"></a>Cenário 1  
 Esse cenário simplesmente salva um **conjunto de registros** em um arquivo e depois em um **fluxo**. Em seguida, ele abre o fluxo persistente em outro **conjunto de registros**.  
  
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
 Esse cenário persiste um **conjunto de registros** em um **fluxo** em formato XML. Em seguida, ele lê o **fluxo** em uma cadeia de caracteres que você pode examinar, manipular ou exibir.  
  
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
 Este código de exemplo mostra o código ASP que mantém um **conjunto de registros** como XML diretamente para o objeto de **resposta** :  
  
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
 Nesse cenário, o código ASP grava o conteúdo do **conjunto de registros** no formato ADTG para o cliente. O [serviço de cursor da Microsoft para OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) pode usar esses dados para criar um **conjunto de registros**desconectado.  
  
 Uma nova propriedade na [URL](../../../ado/reference/rds-api/url-property-rds.md)do [controle de origem](../../../ado/reference/rds-api/datacontrol-object-rds.md)de RDS, aponta para a página. asp que gera o **conjunto de registros**. Isso significa que um objeto **Recordset** pode ser obtido sem RDS usando o objeto [DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) do lado do servidor ou o usuário que está gravando um objeto comercial. Isso simplifica significativamente o modelo de programação do RDS.  
  
 Código do lado do servidor, chamadohttps://server/directory/recordset.asp:  
  
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
  
 Os desenvolvedores também têm a opção de usar um objeto **Recordset** no cliente:  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Método Open (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Método Save](../../../ado/reference/ado-api/save-method.md)
