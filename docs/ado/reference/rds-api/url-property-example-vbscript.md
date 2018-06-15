---
title: Exemplo de propriedade de URL (VBScript) | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: sql
ms.prod_service: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- URL property [ADO], VBScript example
ms.assetid: 6ae5ac50-c88c-4262-b7ab-f2b3de382a0b
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 233d7ab118a25725deca1cb5c6d90396b4dd0dea
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35288855"
---
# <a name="url-property-example-vbscript"></a>Exemplo de propriedade de URL (VBScript)
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 O código a seguir demonstra como definir a **URL** propriedade no lado do cliente para especificar um arquivo. ASP que por sua vez, controla o envio de alterações para a fonte de dados.  
  
```  
<!-- BeginURLClientVBS -->  
<%@ Language=VBScript %>  
<html>  
<head>  
    <meta name="VI60_DefaultClientScript"  content=VBScript>  
    <meta name="GENERATOR" content="Microsoft Visual Studio 6.0">  
    <title>URL Property Example (VBScript)</title>  
<style>  
<!--  
body {  
   font-family: 'Verdana','Arial','Helvetica',sans-serif;  
   BACKGROUND-COLOR:white;  
   COLOR:black;  
    }  
.thead {  
   background-color: #008080;   
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
   color: white;  
   }  
.thead2 {  
   background-color: #800000;   
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
   color: white;  
   }  
.tbody {   
   text-align: center;  
   background-color: #f7efde;  
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
    }  
-->  
</style>  
</head>  
  
<body onload=Getdata()>  
<h1>URL Property Example (VBScript)</h1>  
<OBJECT classid=clsid:BD96C556-65A3-11D0-983A-00C04FC29E33 height=1 id=ADC width=1>  
</OBJECT>  
  
<table datasrc="#ADC" align="center">  
<thead>  
<tr id="ColHeaders" class="thead2">  
   <th>FirstName</th>  
   <th>LastName</th>  
   <th>Extension</th>  
</tr>  
</thead>  
<tbody class="tbody">  
<tr>  
   <td><input datafld="FirstName" size=15> </td>  
   <td><input datafld="LastName" size=25> </td>  
   <td><input datafld="Extension" size=15> </td>  
</tr>  
</tbody>  
</table>  
  
<script Language="VBScript">  
Sub Getdata()  
  
      ADC.URL = "http://MyServer/URLServerVBS.asp"  
      ADC.Refresh  
End Sub  
  
</script>  
  
</body>  
</html>  
<!-- EndURLClientVBS -->  
```  
  
 O código do lado do servidor que existe no **URLServerVBS.asp** envia a atualização **registros** à fonte de dados.  
  
```  
<!-- BeginURLServerVBS -->  
<%@ Language=VBScript %>  
<%  
  
        ' XML output req's  
    Response.ContentType = "text/xml"  
    const adPersistXML  = 1  
  
        ' recordset vars  
    Dim strSQL, rsEmployees   
    Dim strCnxn, Cnxn  
  
    strCnxn = "Provider='sqloledb';Data Source=" & _  
            Request.ServerVariables("SERVER_NAME") & ";" & _  
            "Integrated Security='SSPI';Initial Catalog='Northwind';"  
    Set Cnxn = Server.CreateObject("ADODB.Connection")  
    Set rsEmployees = Server.CreateObject("ADODB.Recordset")  
  
    strSQL = "SELECT FirstName, LastName, Extension FROM Employees"  
  
    Cnxn.Open strCnxn  
    rsEmployees.Open strSQL, Cnxn  
  
        ' output as XML  
    rsEmployees.Save Response, adPersistXML  
  
        ' Clean up  
    rsEmployees.Close  
    Cnxn.Close  
    Set rsEmployees = Nothing  
    Set Cnxn = Nothing  
%>  
<!-- EndURLServerVBS -->  
```  
  
## <a name="see-also"></a>Consulte também  
 [Propriedade URL (RDS)](../../../ado/reference/rds-api/url-property-rds.md)


