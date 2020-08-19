---
description: Exemplo da propriedade Connect (VBScript)
title: Exemplo da propriedade Connect (VBScript) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Connect property [ADO], VBScript example
ms.assetid: 06297993-fe72-4446-aa76-3b8bc25444f6
author: rothja
ms.author: jroth
ms.openlocfilehash: f7b854f8d5b84883d28915af629c2af67036b718
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88439218"
---
# <a name="connect-property-example-vbscript"></a>Exemplo da propriedade Connect (VBScript)
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Este código mostra como definir a propriedade [Connect](../../../ado/reference/rds-api/connect-property-rds.md) em tempo de design:  
  
```  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="ADC1">  
.  
   <PARAM NAME="SQL" VALUE="Select * from Sales">  
   <PARAM NAME="CONNECT" VALUE="Provider=SQLOLEDB;Integrated Security=SSPI;Initial Catalog=Pubs">  
   <PARAM NAME="Server" VALUE="https://MyWebServer">  
.  
</OBJECT>  
```  
  
 O exemplo a seguir mostra como definir a propriedade **Connect** em tempo de execução no código VBScript.  
  
 Para testar este exemplo, recorte e cole o código entre \<Body> as \</Body> marcas e em um documento HTML normal e nomeie-o **ConnectVBS. asp**. O script ASP identificará seu servidor.  
  
```  
<!-- BeginConnectVBS -->  
<%@ Language=VBScript %>  
<HTML>  
<HEAD>  
<title>ADO Connect Property</title>  
  
    <%' local style sheet used for display%>  
<STYLE>  
<!--  
BODY {  
   font-family: 'Verdana','Arial','Helvetica',sans-serif;  
   BACKGROUND-COLOR:white;  
   COLOR:black;  
    }  
  
.tbody {   
   text-align: center;  
   background-color: #f7efde;  
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
    }  
-->  
</STYLE>  
</HEAD>  
  
<BODY>  
<h1>ADO Connect Property (RDS)</h1>  
  
<HR>  
<H3>Set Connect Property at Run Time</H3>  
  
<% ' RDS.DataControl with no parameters set at design time %>  
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID=RDS HEIGHT=1 WIDTH=1></OBJECT>  
<% ' Bind table to control for data display  %>  
<TABLE DATASRC=#RDS>  
<TBODY>  
  <TR class="tbody">  
    <TD><SPAN DATAFLD="FirstName"></SPAN></TD>  
    <TD><SPAN DATAFLD="LastName"></SPAN></TD>  
  </TR>  
</TBODY>  
</TABLE>  
<FORM name="frmInput">  
    SERVER: <INPUT Name="txtServer" Size="103" Value="https://<%=Request.ServerVariables("SERVER_NAME")%>"><BR>  
    DATA SOURCE: <INPUT Name="txtDataSource" Size="93" Value="<%=Request.ServerVariables("SERVER_NAME")%>"><BR>  
    CONNECT: <INPUT Name="txtConnect" Size="100"><BR>  
    SQL: <INPUT Name="txtSQL" Size="110" Value="Select FirstName, LastName from Employees">  
    <BR>  
    <INPUT TYPE=BUTTON NAME="Run" VALUE="Run">  
    <h4>  
    To make data grid appear, click 'Run' to see the connect string in text box above.  
    </h4>   
</FORM>  
<Script Language="VBScript">  
  
    ' Set parameters of RDS.DataControl at Run Time  
    Sub Run_OnClick  
  
        Dim Cnxn  
            ' build connection string  
        Cnxn = "Provider='sqloledb';"  
        Cnxn = Cnxn & "Data Source="  
        Cnxn = Cnxn & document.frmInput.txtDataSource.value & ";"  
        Cnxn = Cnxn & "Initial Catalog='Northwind';"  
        Cnxn = Cnxn & "Integrated Security='SSPI';"  
            ' assign the value  
        document.frmInput.txtConnect.value = Cnxn  
        MsgBox "Here we go!"  
            ' set RDS properties  
        RDS.Server = document.frmInput.txtServer.value  
        RDS.SQL = document.frmInput.txtSQL.value  
        RDS.Connect = document.frmInput.txtConnect.value  
        RDS.Refresh  
  
    End Sub  
  
</Script>  
  
</BODY>  
</HTML>  
<!-- EndConnectVBS -->  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedade Connect (RDS)](../../../ado/reference/rds-api/connect-property-rds.md)





















