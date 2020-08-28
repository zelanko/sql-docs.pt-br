---
description: Exemplo do método SubmitChanges (VBScript)
title: Exemplo do método SubmitChanges (VBScript) | Microsoft Docs
ms.prod: sql
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- SubmitChanges method [ADO], VBScript example
ms.assetid: 619bc7fd-ad0a-44ea-9678-ad40a662c258
author: rothja
ms.author: jroth
ms.openlocfilehash: 7de649459a7b31d4d30230d8a4e7878c6938bf13
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88981087"
---
# <a name="submitchanges-method-example-vbscript"></a>Exemplo do método SubmitChanges (VBScript)
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 O fragmento de código a seguir mostra como usar o método [SubmitChanges](./submitchanges-method-rds.md) com um [RDS. Objeto DataControl](./datacontrol-object-rds.md) .  
  
 Para testar este exemplo, recorte e cole esse código em um documento ASP normal e nomeie-o **SubmitChangesCtrlVBS. asp**. O script ASP identificará seu servidor.  
  
```  
<!-- BeginCancelUpdateVBS -->  
<%@Language=VBScript%>  
  
<%'Option Explicit%>  
<% 'use the following META tag instead of adovbs.inc%>  
<!--METADATA TYPE="typelib" uuid="00000205-0000-0010-8000-00AA006D2EA4" -->  
<HTML>  
<HEAD>  
<META NAME="GENERATOR" Content="Microsoft Visual Studio 6.0">  
<TITLE></TITLE>  
</HEAD>  
<BODY>  
<CENTER>  
<H1>Remote Data Service</H1>  
<H2>SubmitChanges and CancelUpdate Methods</H2>  
  
<%  ' to integrate/test this code replace the Server property value and   
    ' the Data Source value in the Connect property with identical values%>  
  
<HR>  
<OBJECT id="RDS" classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" HEIGHT="1" WIDTH="1"></OBJECT>  
<SCRIPT Language="VBScript">  
  
     'set RDS properties for control just created  
    RDS.Server = "https://<%=Request.ServerVariables("SERVER_NAME")%>"  
    RDS.Connect = "Provider='sqloledb';Integrated Security='SSPI';Initial Catalog='Northwind';"  
    RDS.SQL = "Select * from Employees"  
    RDS.Refresh  
</SCRIPT>  
  
<TABLE DATASRC="#RDS">  
<THEAD>  
<TR ID="ColHeaders">  
   <TH>ID</TH>  
   <TH>FName</TH>  
   <TH>LName</TH>  
   <TH>Title</TH>  
   <TH>Hire Date</TH>  
   <TH>Birth Date</TH>  
   <TH>Extension</TH>  
   <TH>Home Phone</TH>  
</TR>  
</THEAD>  
<TBODY>  
<TR>  
   <TD> <INPUT DATAFLD="EmployeeID" size=4 id=text1 name=text1> </TD>  
   <TD> <INPUT DATAFLD="FirstName" size=10 id=text2 name=text2> </TD>  
   <TD> <INPUT DATAFLD="LastName" size=10 id=text3 name=text3> </TD>  
   <TD> <INPUT DATAFLD="Title" size=10 id=text4 name=text4> </TD>  
   <TD> <INPUT DATAFLD="HireDate" size=10 id=text5 name=text5> </TD>  
   <TD> <INPUT DATAFLD="BirthDate" size=10 id=text6 name=text6> </TD>  
   <TD> <INPUT DATAFLD="Extension" size=10 id=text7 name=text7> </TD>  
   <TD> <INPUT DATAFLD="HomePhone" size=8 id=text8 name=text8> </TD>  
</TR>  
</TBODY>  
</TABLE>  
<HR>  
<INPUT TYPE=button NAME="SubmitChange" VALUE="Submit Changes">  
<INPUT TYPE=button NAME="CancelChange" VALUE="Cancel Update">  
<BR>  
<H4>Alter a current entry on the grid. Move off that Row. <BR>  
Submit the Changes to your DBMS or cancel the updates. </H4>  
</CENTER>  
<SCRIPT Language="VBScript">  
  
Sub SubmitChange_OnClick  
  
    msgbox "Changes will be made"  
    RDS.SubmitChanges     
    RDS.Refresh  
  
End Sub  
  
Sub CancelChange_OnClick  
  
    msgbox "Changes will be cancelled"  
    RDS.CancelUpdate  
    RDS.Refresh  
  
End Sub  
</SCRIPT>  
  
</BODY>  
</HTML>  
<!-- EndCancelUpdateVBS -->  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto DataControl (RDS)](./datacontrol-object-rds.md)   
 [Método SubmitChanges (RDS)](./submitchanges-method-rds.md)