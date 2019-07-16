---
title: Exemplo do método ConvertToString (VBScript) | Microsoft Docs
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
- ConvertToString method [ADO], VBScript example
ms.assetid: edd0a01c-1a1b-4b91-9966-2529e244abae
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1feada03927b1c2359babf7d68d6c9a8ffcba2b6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67964553"
---
# <a name="converttostring-method-example-vbscript"></a>Exemplo do método ConvertToString (VBScript)
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 O exemplo a seguir mostra como converter um **conjunto de registros** em uma cadeia de caracteres codificado em MIME que usa o **RDSServer.DataFactory ConvertToString** método. Em seguida, mostra como a cadeia de caracteres pode ser convertida de volta em uma **conjunto de registros**. Recortar e colar o seguinte código ao bloco de notas ou outro editor de texto e salve-o como **ConvertToString.htm**.  
  
```  
<!-- BeginConvertToStringVBS -->  
<HTML>  
<HEAD><TITLE>ConvertToString Example</TITLE><HEAD>  
<BODY>  
  
<SCRIPT LANGUAGE=VBSCRIPT>  
Sub ConvertToStringX()  
    Dim objRs, objDF, strServer, vString  
    Const adcExecSync = 1  
    Const adcFetchUpFront = 1  
  
    ' Replace value below with your server name to use without ASP.  
    strServer = "https://<%=Request.ServerVariables("SERVER_NAME")%>">  
  
    Set objDF = RDS1.CreateObject("RDSServer.DataFactory", strServer)  
    Set objRs = objDF.Query(txtConnect.Value,txtQueryRecordset.Value)  
  
    ' convert Recordset to MIME encoded string  
    vString = objDF.ConvertToString(objRs)  
  
    ' display MIME string for demo purposes  
    txtRS.value = vString  
  
    ' convert MIME string back to useable ADO Recordset   
    ' using RDS.DataControl  
    RDC1.SQL = vString  
  
    RDC1.ExecuteOptions = adcExecSync  
    RDC1.FetchOptions = adcFetchUpFront  
    RDC1.Refresh  
  
    MsgBox "RecordCount = " & RDC1.Recordset.RecordCount  
End Sub   
</SCRIPT>  
  
Connect String:   
 <INPUT TYPE=Text NAME=txtConnect SIZE=50   
    VALUE="Provider=sqloledb;Initial Catalog=pubs;Integrated Security='SSPI';">   
 <BR>  
  
Query:   
 <INPUT TYPE=Text NAME=txtQueryRecordset SIZE=50   
    VALUE="select * from authors">   
 <BR>  
  
 <INPUT TYPE=Button VALUE="ConvertToString" OnClick="ConvertToStringX()">  
 <BR>  
  
MIME Encoded RS: <BR>  
 <TEXTAREA NAME=txtRS ROWS=15 COLS=50 WRAP=virtual></TEXTAREA>  
  
<!-- RDS.DataSpace  ID RDS1 -->  
 <OBJECT ID="RDS1" WIDTH=1 HEIGHT=1  
     CLASSID="CLSID:BD96C556-65A3-11D0-983A-00C04FC29E36">  
 </OBJECT>  
  
<!-- RDS.DataControl ID RDC1 -->  
 <OBJECT ID="RDC1" WIDTH=1 HEIGHT=1   
     CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33">  
 </OBJECT>  
</BODY>  
</HTML>  
<!-- EndConvertToStringVBS -->  
```  
  
## <a name="see-also"></a>Consulte também  
 [Método ConvertToString (RDS)](../../../ado/reference/rds-api/converttostring-method-rds.md)   
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)




