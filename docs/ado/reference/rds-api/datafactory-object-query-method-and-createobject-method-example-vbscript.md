---
title: Criar objeto RDSServer. datafactory usando CreateObject (VBScript) | Microsoft Docs
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
- DataFactory object [ADO], VBScript example
- CreateObject method [ADO], VBScript example
- Query method [ADO], VBScript example
ms.assetid: b4e2844a-120a-4513-860b-f1b6e4b5dda4
author: rothja
ms.author: jroth
ms.openlocfilehash: fa54e59af5187bf9b4daaa898bbaabfa614a4286
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82752644"
---
# <a name="datafactory-object-query-method-and-createobject-method-example-vbscript"></a>Exemplo do método CreateObject, do método Query e objeto DataFactory (VBScript)
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Este exemplo cria um objeto [RDSServer. datafactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) usando o método [CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md) do [RDS. Objeto DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) . Para testar este exemplo, recorte e cole esse código entre o \< corpo> e \< /Body> marcas em um documento HTML normal e nomeie-o **DataFactoryVBS. asp**. O script ASP identificará seu servidor.  
  
```  
<!-- BeginDataFactoryVBS -->  
<HTML>  
<HEAD>  
<!--use the following META tag instead of adovbs.inc-->  
<!--METADATA TYPE="typelib" uuid="00000205-0000-0010-8000-00AA006D2EA4" -->  
<META name="VI60_DefaultClientScript" Content="VBScript">  
  
<META NAME="GENERATOR" Content="Microsoft Visual Studio 6.0">  
<TITLE>DataFactory Object, Query Method, and   
CreateObject Method Example (VBScript)</TITLE>  
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
</HEAD>  
<BODY>  
<h1>DataFactory Object, Query Method, and   
CreateObject Method Example (VBScript)</h1>  
<H2>RDS API Code Examples</H2>  
<HR>  
<H3>Using Query Method of RDSServer.DataFactory</H3>  
  
<!-- RDS.DataSpace  ID RDS1-->  
<OBJECT ID="RDS1" WIDTH=1 HEIGHT=1  
CLASSID="CLSID:BD96C556-65A3-11D0-983A-00C04FC29E36">  
</OBJECT>  
  
<!-- RDS.DataControl with parameters   
set at run time -->  
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"  
   ID=RDS WIDTH=1 HEIGHT=1>  
</OBJECT>  
  
<TABLE DATASRC=#RDS>  
<TBODY>  
  <TR>  
    <TD><SPAN DATAFLD="FirstName"></SPAN></TD>  
    <TD><SPAN DATAFLD="LastName"></SPAN></TD>  
  </TR>  
</TBODY>      
</TABLE>  
  
<HR>  
<INPUT TYPE=BUTTON NAME="Run" VALUE="Run">  
<BR>  
<H4>Click Run -    
The <i>CreateObject</i> Method of the RDS.DataSpace Object Creates   
an instance of the RDSServer.DataFactory;   
The <i>Query</i> Method of the RDSServer.DataFactory is used  
to bring back a Recordset. </H4>  
  
<Script Language="VBScript">  
  
    Dim rdsDF  
    Dim strServer  
    Dim strCnxn  
    Dim strSQL  
  
    strServer = "https://<%=Request.ServerVariables("SERVER_NAME")%>"  
    strCnxn = "Provider='sqloledb';Integrated Security='SSPI';Initial Catalog='Northwind';"  
    strSQL = "Select FirstName, LastName from Employees"  
  
    Sub Run_OnClick()  
  
        ' Create RDSServer.DataFactory Object  
        Dim rs  
        ' Get Recordset  
        Set DF = RDS1.CreateObject("RDSServer.DataFactory", strServer)  
        Set rs = DF.Query(strCnxn, strSQL)  
        ' Set parameters of RDS.DataControl at Run Time  
        RDS.Server = strServer  
        RDS.SQL = strSQL  
        RDS.Connect = strCnxn  
        RDS.Refresh  
  
    End Sub  
</Script>  
  
</BODY>  
</HTML>  
<!-- EndDataFactoryVBS -->  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Método CreateObject (RDS)](../../../ado/reference/rds-api/createobject-method-rds.md)   
 [Objeto datafactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)   
 [Objeto DataSpace (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)   
 [Método Query (RDS)](../../../ado/reference/rds-api/query-method-rds.md)


