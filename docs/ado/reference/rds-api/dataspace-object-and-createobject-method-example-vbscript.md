---
title: "Objeto de espaço de dados e de exemplo do método CreateObject (VBScript) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: VB
helpviewer_keywords:
- DataSpace object [RDS], VBScript example
- CreateObject method [ADO], VBScript example
ms.assetid: 12b0e160-5e5c-441f-bed7-ac0bd061e003
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ed789c409619c2ef7d1de934ad8eeed106f80032
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="dataspace-object-and-createobject-method-example-vbscript"></a>Exemplo de método CreateObject (VBScript) e o objeto de espaço de dados
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 O exemplo a seguir mostra como usar o [CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md) método o [RDS. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) com o objeto de negócios padrão [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md). Para testar este exemplo, recorte e cole este código entre as \<corpo > e \</Body > marcas em uma HTML normal de documento e nomeie-o **DataSpaceVBS.asp**. Script ASP identificará o seu servidor.  
  
```  
<!-- BeginDataSpaceVBS -->  
<html>  
<head>  
<!--use the following META tag instead of adovbs.inc-->  
<!--METADATA TYPE="typelib" uuid="00000205-0000-0010-8000-00AA006D2EA4" -->  
    <meta name="VI60_DefaultClientScript"  content=VBScript>  
    <meta name="GENERATOR" content="Microsoft Visual Studio 6.0">  
    <title>DataSpace Object and CreateObject Method Example (VBScript)</title>  
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
  
<body>  
<h1>DataSpace Object and CreateObject Method Example (VBScript)</h1>  
  
<H2>RDS API Code Examples</H2>  
<HR>  
<H3>Using Query Method of RDSServer.DataFactory</H3>  
  
<!-- RDS.DataSpace  ID rdsDS-->  
<OBJECT ID="rdsDS" WIDTH=1 HEIGHT=1  
CLASSID="CLSID:BD96C556-65A3-11D0-983A-00C04FC29E36">  
</OBJECT>  
  
<!-- RDS.DataControl with parameters set at run time -->  
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
  
<H4>Click Run -  
The <i>CreateObject</i> Method of the RDS.DataSpace Object Creates an instance of the RDSServer.DataFactory.  
The <i>Query</i> Method of the RDSServer.DataFactory is used to bring back a Recordset.</H4>  
  
<Script Language="VBScript">  
  
    Dim rdsDF  
    Dim strServer  
    Dim strCnxn  
    Dim strSQL  
  
    strServer = "http://<%=Request.ServerVariables("SERVER_NAME")%>"  
    strCnxn = "Provider='sqloledb';Data Source=" & _  
            "<%=Request.ServerVariables("SERVER_NAME")%>" & ";" & _  
            "Integrated Security='SSPI';Initial Catalog='Northwind';"  
    strSQL = "Select FirstName, LastName from Employees"  
  
    Sub Run_OnClick()  
  
       Dim rs        
        ' Create Data Factory  
       Set rdsDF = rdsDS.CreateObject("RDSServer.DataFactory", strServer)  
        'Get Recordset    
       Set rs = rdsDF.Query(strCnxn, strSQL)     
       ' Use  RDS.DataControl to bind Recordset to data-aware Table above  
       RDS.SourceRecordset = rs  
  
    End Sub  
</Script>  
  
</body>  
</html>  
<!-- EndDataSpaceVBS -->  
```  
  
 O exemplo a seguir mostra como usar o **CreateObject** método para criar uma instância de um objeto de negócios personalizada, VbBusObj.VbBusObjCls. Ele também usa o Active Server Pages script para identificar o nome do servidor Web.  
  
 Para ver o exemplo completo, abra o seletor de aplicativos de exemplo. No **da camada do cliente** coluna, selecione **VBScript no Internet Explorer**. No **camada intermediária** coluna, selecione **objeto de negócios do Visual Basic personalizado**.  
  
> [!NOTE]
>  Se você estiver se conectando a um provedor de fonte de dados que oferece suporte à autenticação do Windows, você deve especificar **Trusted_Connection = yes** ou **segurança integrada = SSPI** em vez de ID de usuário e senha informações na cadeia de conexão.  
  
```  
Sub Window_OnLoad()  
   strServer = "http://<%=Request.ServerVariables("SERVER_NAME")%>"  
   Set BO = ADS1.CreateObject("VbBusObj.VbBusObjCls", strServer)  
   txtConnect.Value = "dsn=Pubs;uid=MyUserID;pwd=MyPassword;"  
   txtGetRecordset.Value = "Select * From authors for Browse"  
End Sub  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Método CreateObject (RDS)](../../../ado/reference/rds-api/createobject-method-rds.md)   
 [Objeto DataSpace (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)


