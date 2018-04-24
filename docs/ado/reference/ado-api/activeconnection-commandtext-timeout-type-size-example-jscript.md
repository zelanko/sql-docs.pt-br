---
title: Armazenado exemplo de propriedades de procedimento (JScript) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- JScript
helpviewer_keywords:
- ActiveConnection property [ADO], JScript example
- CommandText property [ADO], JScript example
- Size property [ADO], JScript example
- Direction property [ADO], JScript example
- CommandTimeout property [ADO], JScript example
ms.assetid: ea74e2a3-c965-43aa-9076-26a084b48ad8
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 06479e3fc2e3db026994f5a929e8dcf02f90fbe1
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="activeconnection-commandtext-commandtimeout-commandtype-size-and-direction-properties-example-jscript"></a>ActiveConnection CommandText, CommandTimeout, CommandType, tamanho e exemplo de propriedades de direção (JScript)
Este exemplo usa o [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md), [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md), [CommandTimeout](../../../ado/reference/ado-api/commandtimeout-property-ado.md), [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md), [tamanho](../../../ado/reference/ado-api/size-property-ado-parameter.md), e [direção](../../../ado/reference/ado-api/direction-property.md) propriedades para executar um procedimento armazenado. Recorte e cole o seguinte código ao bloco de notas ou outro editor de texto e salve-o como **ActiveConnectionJS.asp**.  
  
```  
<!-- BeginActiveConnectionJS -->  
<%@LANGUAGE="JScript"%>  
<%// use this meta tag instead of adojavas.inc%>  
<!--METADATA TYPE="typelib" uuid="00000205-0000-0010-8000-00AA006D2EA4" -->  
  
<html>  
<head>  
    <title>ActiveConnection, CommandText, CommandTimeout, CommandType, Size, and Direction Properties</title>  
<style>  
<!--  
BODY {  
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
  
<body bgcolor="White">  
  
<%  
    var iRoyalty = parseInt(Request.Form("RoyaltyValue"));  
    // check user input  
  
    if (iRoyalty > -1)  
    {  
            // connection and recordset variables  
        var Cnxn = Server.CreateObject("ADODB.Connection")  
        var strCnxn = "Provider='sqloledb';Data Source=" + Request.ServerVariables("SERVER_NAME") + ";" +  
            "Initial Catalog='pubs';Integrated Security='SSPI';";  
        var cmdByRoyalty = Server.CreateObject("ADODB.Command");  
        var rsByRoyalty = Server.CreateObject("ADODB.Recordset");  
        var rsAuthor = Server.CreateObject("ADODB.Recordset");  
        // display variables  
        var filter, strMessage;          
  
        try  
        {  
            // open connection  
            Cnxn.Open(strCnxn);  
  
            cmdByRoyalty.CommandText = "byroyalty";  
            cmdByRoyalty.CommandType = adCmdStoredProc;  
            cmdByRoyalty.CommandTimeOut = 15;  
  
            // The stored procedure called above is as follows:  
                //    CREATE PROCEDURE byroyalty  
                //  @percentage int  
                //    AS  
                //  SELECT au_id from titleauthor  
                //  WHERE titleauthor.royaltyper = @percentage  
                //  GO  
  
            prmByRoyalty = Server.CreateObject("ADODB.Parameter");  
            prmByRoyalty.Type = adInteger;  
            prmByRoyalty.Size = 3;  
            prmByRoyalty.Direction = adParamInput;  
            prmByRoyalty.Value = iRoyalty;  
            cmdByRoyalty.Parameters.Append(prmByRoyalty);  
  
            cmdByRoyalty.ActiveConnection = Cnxn;  
  
            // recordset by Command - Execute  
            rsByRoyalty = cmdByRoyalty.Execute();  
  
            // recordset by Recordset - Open  
            rsAuthor.Open("Authors", Cnxn);  
  
            while (!rsByRoyalty.EOF)  
            {  
                // set filter  
                filter = "au_id='" + rsByRoyalty("au_id")  
                rsAuthor.Filter = filter + "'";  
  
                // start new line  
                strMessage = "<P>";  
  
                // get data  
                strMessage += rsAuthor("au_fname") + " ";   
                strMessage += rsAuthor("au_lname") + " ";  
  
                // end line  
                strMessage += "</P>";  
  
                // show data  
                Response.Write(strMessage);  
  
                // get next record  
                rsByRoyalty.MoveNext;  
            }  
        }  
        catch (e)  
        {  
            Response.Write(e.message);  
        }  
        finally  
        {  
            // clean up  
            if (rsByRoyalty.State == adStateOpen)  
                rsByRoyalty.Close;  
            if (rsAuthor.State == adStateOpen)  
                rsAuthor.Close;  
            if (Cnxn.State == adStateOpen)  
                Cnxn.Close;  
            rsByRoyalty = null;  
            rsAuthor = null;  
            Cnxn = null;  
        }  
    }  
%>  
  
<hr>  
  
<form method="POST" action="ActiveConnectionJS.asp">  
  <p align="left">Enter royalty percentage to find (e.g., 40): <input type="text" name="RoyaltyValue" size="5"></p>  
  <p align="left"><input type="submit" value="Submit" name="B1"><input type="reset" value="Reset" name="B2"></p>  
</form>  
  
</body>  
  
</html>  
<!-- EndActiveConnectionJS -->  
```  
  
## <a name="see-also"></a>Consulte também  
 [Propriedade ActiveCommand (ADO)](../../../ado/reference/ado-api/activecommand-property-ado.md)   
 [Objeto de comando (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [Propriedade CommandText (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [Propriedade CommandTimeout (ADO)](../../../ado/reference/ado-api/commandtimeout-property-ado.md)   
 [Propriedade CommandType (ADO)](../../../ado/reference/ado-api/commandtype-property-ado.md)   
 [Objeto de Conexão (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Propriedade de direção](../../../ado/reference/ado-api/direction-property.md)   
 [Objeto de parâmetro](../../../ado/reference/ado-api/parameter-object.md)   
 [Objeto de registro (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Propriedade Size (Parâmetro ADO)](../../../ado/reference/ado-api/size-property-ado-parameter.md)
