---
description: Exemplo dos métodos Execute, Requery e Clear (JScript)
title: Exemplo dos métodos Execute, Requery e Clear (JScript) | Microsoft Docs
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
- Requery method [ADO], JScript example
- Clear method [ADO], JScript example
- Execute method [ADO], JScript example
ms.assetid: 51a87e91-c9d9-4e49-af47-79cce2c4cfe0
author: rothja
ms.author: jroth
ms.openlocfilehash: f30dfef8bcfb769dd124f2501143eac6e619315c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443878"
---
# <a name="execute-requery-and-clear-methods-example-jscript"></a>Exemplo dos métodos Execute, Requery e Clear (JScript)
Este exemplo demonstra o método **Execute** quando executado a partir de um objeto [Command](../../../ado/reference/ado-api/command-object-ado.md) e um objeto [Connection](../../../ado/reference/ado-api/connection-object-ado.md) . Ele também usa o método [Requery](../../../ado/reference/ado-api/requery-method.md) para recuperar dados atuais em um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md)e o método [Clear](../../../ado/reference/ado-api/clear-method-ado.md) para limpar o conteúdo da coleção de [erros](../../../ado/reference/ado-api/errors-collection-ado.md) . (A coleção de **erros** é acessada por meio do objeto de **conexão** da propriedade [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) do [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).) Nomeie o arquivo **ExecuteJS. asp**.  
  
```  
<!-- BeginExecuteJS -->  
<%@LANGUAGE="JScript"%>  
<%// use this meta tag instead of adojavas.inc%>  
<!--METADATA TYPE="typelib" uuid="00000205-0000-0010-8000-00AA006D2EA4" -->  
  
<%  
    strLastName = new String(Request.Form("AuthorLName"));  
  
    if (strLastName.indexOf("undefined") > -1)  
        strLastName = "";  
%>  
  
<html>  
  
<head>  
<title>Execute, Requery and Clear Methods Example (JScript)</title>  
<style>  
<!--  
BODY {  
   font-family: 'Verdana','Arial','Helvetica',sans-serif;  
   BACKGROUND-COLOR:white;  
   COLOR:black;  
    }  
-->  
</style>  
</head>  
  
<body bgcolor="White">  
<h1>Execute, Requery and Clear Methods Example (JScript)</h1>  
<%  
    if (strLastName.length > 0)  
    {  
        // command and recordset variables  
        var Connect = "Provider='sqloledb';Data Source=" + Request.ServerVariables("SERVER_NAME") + ";" +  
            "Initial Catalog='pubs';Integrated Security='SSPI';";  
        var Cnxn = Server.CreateObject("ADODB.Connection");  
        var cmdAuthor = Server.CreateObject("ADODB.Command");  
        var rsAuthor = Server.CreateObject("ADODB.Recordset");  
        var rsAuthor2 = Server.CreateObject("ADODB.Recordset");  
        var SQLAuthor2, strMessage, strMessage2;  
        var Err, ErrCount;  
  
        try  
        {  
            // open connection  
            Cnxn.Open(Connect);  
  
            // command object parameters  
            cmdAuthor.CommandText = "SELECT * FROM Authors WHERE au_lname = ?";  
            cmdAuthor.Parameters.Append(cmdAuthor.CreateParameter("Last Name", adChar, adParamInput, 20, strLastName));  
            cmdAuthor.ActiveConnection = Cnxn;  
  
            // recordset from command.execute  
            rsAuthor = cmdAuthor.Execute();  
  
            // recordset from connection.execute  
            SQLAuthor2 = "SELECT * FROM Authors";  
            rsAuthor2 = Cnxn.Execute(SQLAuthor2);  
  
                // check for errors  
                ErrCount = Cnxn.errors.count;  
                if(ErrCount !== 0) //write the errors  
                {  
                    for(Err = 0; Err = ErrCount; Err++){  
                        Err = Cnxn.errors.item;  
                        Response.Write(Err);  
                    }  
                    // clean out any existing errors  
                    Cnxn.Errors.Clear;  
                }  
  
                // show the data      
            Response.Write("<HR><HR>");  
  
                // first recordset  
            Response.Write("<b>Command.Execute results</b>")  
            while (!rsAuthor.EOF)  
            {  
                // build output string by starting a new line  
                strMessage = "<P>";  
                strMessage += "<br>";  
  
                // recordset data   
                strMessage += rsAuthor("au_fname") + " ";   
                strMessage += rsAuthor("au_lname") + " ";  
  
                // end the line  
                strMessage += "</P>";  
  
                // show the results  
                Response.Write(strMessage);  
  
                // get next record  
                rsAuthor.MoveNext;  
            }  
  
            Response.Write("<HR><HR>");  
  
            // second recordset  
            Response.Write("<b>Connection.Execute results</b>")  
            while (!rsAuthor2.EOF)  
            {  
                // start a new line  
                strMessage2 = "<P>";  
  
                // first and last name are in first column  
                strMessage2 += rsAuthor2("au_fname") + " "   
                strMessage2 += rsAuthor2("au_lname") + " ";  
  
                // end the line  
                strMessage2 += "</P>";  
  
                // show results  
                Response.Write(strMessage2);  
  
                // get next record  
                rsAuthor2.MoveNext;  
            }  
        }  
        catch (e)  
        {  
            Response.Write(e.message);  
        }  
        finally  
        {  
            // clean up  
            if (rsAuthor.State == adStateOpen)  
                rsAuthor.Close;  
            if (rsAuthor2.State == adStateOpen)  
                rsAuthor2.Close;  
            if (Cnxn.State == adStateOpen)  
                Cnxn.Close;  
            rsAuthor1 = null;  
            rsAuthor2 = null;  
            Cnxn = null;  
        }  
    }  
%>  
  
<hr>  
  
<form method="POST" action="ExecuteJS.asp" id=form1 name=form1>  
  <p align="left">Enter last name of author to find (e.g., Ringer): <input type="text" name="AuthorLName" size="40"></p>  
  <p align="left"><input type="submit" value="Submit" name="B1"><input type="reset" value="Reset" name="B2"></p>  
</form>  
</body>  
  
</html>  
<!-- EndExecuteJS -->  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Método Clear (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [Objeto de conexão (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Objeto de erro](../../../ado/reference/ado-api/error-object.md)   
 [Método Execute (comando ADO)](../../../ado/reference/ado-api/execute-method-ado-command.md)   
 [Método Execute (conexão ADO)](../../../ado/reference/ado-api/execute-method-ado-connection.md)   
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Método Requery](../../../ado/reference/ado-api/requery-method.md)
