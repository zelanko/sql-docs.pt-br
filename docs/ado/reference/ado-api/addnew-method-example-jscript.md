---
title: Exemplo do método AddNew (JScript) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- JScript
helpviewer_keywords:
- AddNew method [ADO], JScript example
ms.assetid: eabdd278-6576-4be7-9315-fb79cb8ef678
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 13e0fc40945e6cd8c68591a8f94cd9a052cda76e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47631244"
---
# <a name="addnew-method-example-jscript"></a>Exemplo do método AddNew (JScript)
Este exemplo usa o [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) método para criar um novo registro com o nome especificado. Recortar e colar o seguinte código ao bloco de notas ou outro editor de texto e salve-o como **AddNewJS.asp**.  
  
```  
<!-- BeginAddNewJS -->  
<%@LANGUAGE="JScript" %>  
<!-- Include file for JScript ADO Constants -->  
<%// use this meta tag instead of adojavas.inc%>  
<!--METADATA TYPE="typelib" uuid="00000205-0000-0010-8000-00AA006D2EA4" -->  
  
<html>  
  
<head>  
    <title>Add New Method Example (JScript)</title>  
<style>  
<!--  
body {  
   font-family: 'Verdana','Arial','Helvetica',sans-serif;  
   BACKGROUND-COLOR:white;  
   COLOR:black;  
    }  
-->  
</style>  
</head>  
  
<body>  
<h1>AddNew Method Example (JScript)</h1>  
  
<%  
    if (Request.Form("Addit") == "AddNew")  
    {  
        // connection and recordset variables  
        var Cnxn = Server.CreateObject("ADODB.Connection")  
        var strCnxn = "Provider='sqloledb';Data Source=" + Request.ServerVariables("SERVER_NAME") + ";" +  
            "Initial Catalog='Northwind';Integrated Security='SSPI';";  
        var rsEmployee = Server.CreateObject("ADODB.Recordset");  
        //record variables  
        var FName = String(Request.Form("FirstName"));  
        var LName = String(Request.Form("LastName"));  
  
        try  
        {  
            // open connection  
            Cnxn.Open(strCnxn)  
  
            // open Employee recordset using client-side cursor  
            rsEmployee.CursorLocation = adUseClient;  
            rsEmployee.Open("Employees", strCnxn, adOpenKeyset, adLockOptimistic, adCmdTable);  
  
            rsEmployee.AddNew();  
            rsEmployee("FirstName") = FName;  
            rsEmployee("LastName") = LName;  
            rsEmployee.Update;  
  
            // of course, you would normally do error handling here  
            Response.Write("New record added.")  
        }  
        catch (e)  
        {  
            Response.Write(e.message);  
        }  
        finally  
        {  
            // clean up  
            if (rsEmployee.State == adStateOpen)  
                rsEmployee.Close;  
            if (Cnxn.State == adStateOpen)  
                Cnxn.Close;  
            rsEmployee = null;  
            Cnxn = null;  
        }  
    }  
%>  
  
<form method="post" action="AddNewJS.asp" id=form1 name=form1>  
<table>  
<tr>  
    <td colspan="2">  
    <h4>Please enter the record to add:</h4>  
    </td>  
</tr>  
<tr>  
    <td>  
        First Name:  
    </td>  
    <td>  
        <input name="FirstName" maxLength=20>  
    </td>  
</tr>  
<tr>  
    <td>  
        Last Name:  
    </td>  
    <td>  
        <input name="LastName" size="30" maxLength=30>  
    </td>  
</tr>  
<tr>  
    <td align="right">  
        <input type="submit" value="Submit" name="Submit">  
    </td>  
    <TD align="left">  
        <INPUT type="reset" value="Reset" name="Reset">  
    </TD>  
</tr>  
</table>  
<INPUT type="hidden" value="AddNew" name="Addit">  
</form>  
</body>  
</HTML>  
<!-- EndAddNewJS -->  
```  
  
## <a name="see-also"></a>Consulte também  
 [Método AddNew (ADO)](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
