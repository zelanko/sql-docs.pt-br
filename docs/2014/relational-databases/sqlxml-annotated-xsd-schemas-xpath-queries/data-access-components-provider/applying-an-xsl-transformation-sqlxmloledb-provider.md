---
title: Aplicando um XSL Transformation (provedor SQLXMLOLEDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXMLOLEDB Provider, applying XSL transformations
- applying XSL transformations [SQLXML]
- xsl property
- Base Path property
- XSL Transformations [SQLXML]
ms.assetid: cb5e41ab-dd20-4873-af20-f417bd1bbf6d
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 016ea0dd6e5352a0b45147a5ea4cea3764abb305
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82703267"
---
# <a name="applying-an-xsl-transformation-sqlxmloledb-provider"></a>Aplicando um XSL Transformation (provedor SQLXMLOLEDB)
  Neste exemplo de aplicativo ADO, uma consulta SQL é executada e uma transformação em XSL é aplicada ao resultado. Definir a propriedade ClientSideXML como true impõe o processamento do conjunto de linhas no lado do cliente. O dialeto do comando é definido como {5d531cb2-e6ed-11d2-b252-00c04f681b71}, porque a consulta SQL é especificada em um modelo e esse dialeto precisa ser especificado ao executar um modelo. A propriedade XSL especifica o arquivo XSL a ser usado para aplicar a transformação. O valor da propriedade caminho base é usado para pesquisar o arquivo XSL. Se você especificar um caminho no valor da propriedade XSL, o caminho será relativo ao caminho especificado na propriedade caminho base.  
  
 Este exemplo mostra como usar as propriedades específicas do Provedor SQLXMLOLEDB a seguir:  
  
-   ClientSideXML  
  
-   xsl  
  
 Nesse aplicativo de exemplo de ADO do lado cliente, um modelo XML que consiste em uma consulta SQL é executado no servidor.  
  
 Como a propriedade ClientSideXML é definida como true, a instrução SELECT sem a cláusula FOR XML é enviada ao servidor. O servidor executa a consulta e retorna um conjunto de linhas para o cliente. O cliente aplica a transformação de FOR XML ao conjunto de linhas e produz o documento XML.  
  
 A propriedade XSL é especificada no aplicativo; Portanto, a transformação XSL é aplicada ao documento XML gerado no cliente e o resultado é uma tabela de duas colunas.  
  
 Para executar o comando de modelo, o modelo XML dialeto-{5d531cb2-e6ed-11d2-b252-00c04f681b71}-deve ser especificado.  
  
> [!NOTE]  
>  No código, é necessário fornecer o nome da instância do Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] na cadeia de conexão. Além disso, este exemplo especifica o uso do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client para o provedor de dados, o que requer a instalação de software cliente de rede adicional. Para obter mais informações, consulte [requisitos do sistema para SQL Server Native Client](../../native-client/system-requirements-for-sql-server-native-client.md).  
  
```  
Option Explicit  
Sub main()  
Dim oTestStream As New ADODB.Stream  
Dim oTestConnection As New ADODB.Connection  
Dim oTestCommand As New ADODB.Command  
oTestConnection.Open "provider=SQLXMLOLEDB.4.0;data provider=SQLNCLI11;data source=SqlServerName;initial catalog=AdventureWorks;Integrated Security=SSPI;"  
Set oTestCommand.ActiveConnection = oTestConnection  
oTestCommand.Properties("ClientSideXML") = True  
oTestCommand.CommandText = _  
        "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql' >" & _  
       " <sql:query> " & _  
        "   SELECT TOP 25 FirstName, LastName FROM Person.Contact FOR XML AUTO " & _  
        "   </sql:query> " & _  
        " </ROOT> "  
oTestStream.Open  
' You need the dialect if you are executing a template.  
oTestCommand.Dialect = "{5d531cb2-e6ed-11d2-b252-00c04f681b71}"  
oTestCommand.Properties("Output Stream").Value = oTestStream  
oTestCommand.Properties("Base Path").Value = "c:\Schemas\SQLXML4\ExecuteTemplateWithXSL\"  
oTestCommand.Properties("xsl").Value = "myxsl.xsl"  
oTestCommand.Execute , , adExecuteStream  
  
oTestStream.Position = 0  
oTestStream.Charset = "utf-8"  
Debug.Print oTestStream.ReadText(adReadAll)  
End Sub  
Sub Form_Load()  
 main  
End Sub  
```  
  
 A seguir está o modelo XSL. O resultado da aplicação desse modelo XSL é uma tabela de duas colunas.  
  
```  
<?xml version='1.0' encoding='UTF-8'?>            
 <xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" version="1.0">   
  
    <xsl:template match = 'Person.Contact'>  
       <TR>  
         <TD><xsl:value-of select = '@FirstName' /></TD>  
         <TD><B><xsl:value-of select = '@LastName' /></B></TD>  
       </TR>  
    </xsl:template>  
    <xsl:template match = '/'>  
      <HTML>  
        <HEAD>  
           <STYLE>th { background-color: #CCCCCC }</STYLE>  
        </HEAD>  
        <BODY>  
         <TABLE border='1' style='width:300;'>  
           <TR><TH colspan='2'>Contacts</TH></TR>  
           <TR>  
              <TH >First name</TH>  
              <TH>Last name</TH>  
           </TR>  
           <xsl:apply-templates select = 'ROOT' />  
         </TABLE>  
        </BODY>  
      </HTML>  
    </xsl:template>  
</xsl:stylesheet>  
```  
  
  
