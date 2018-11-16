---
title: Executando modelos que contêm consultas XPath (provedor SQLXMLOLEDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXMLOLEDB Provider, executing template files
- Base Path property
- templates [SQLXML], XPath queries
- XPath queries [SQLXML], templates
- XPath queries [SQLXML], SQLXMLOLEDB Provider
- Mapping Schema property
- XML templates [SQLXML]
ms.assetid: 7368c188-607e-459e-8254-8f23352dfa01
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9f8ed1e6fb9df209203c210cb09aa97deff9de05
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51673955"
---
# <a name="executing-templates-that-contain-xpath-queries-sqlxmloledb-provider"></a>Executando modelos que contêm consultas XPath (provedor SQLXMLOLEDB)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Este exemplo mostra como usar as propriedades específicas do Provedor SQLXMLOLEDB a seguir:  
  
-   ClientSideXML  
  
-   Caminho base  
  
-   Esquema de mapeamento  
  
 Neste aplicativo ADO de exemplo, um modelo XML que consiste em uma consulta XPath (raiz) é especificado no esquema de mapeamento XSD (MySchema. xml) que é descrito em [executar consultas de XPath &#40;provedor SQLXMLOLEDB&#41; ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-xpath-queries-sqlxmloledb-provider.md).  
  
 A propriedade de esquema de mapeamento fornece o esquema de mapeamento XSD com relação à qual a consulta XPath é executada. A propriedade de caminho de Base fornece o caminho do arquivo para o esquema de mapeamento.  
  
 A propriedade ClientSideXML é definida como True. Assim, o documento XML é gerado no cliente.  
  
 No aplicativo, uma consulta XPath é especificada diretamente. Portanto, o dialeto {5d531cb2-e6ed-11d2-b252-00c04f681b71} deve ser incluído.  
  
> [!NOTE]  
>  No código, é necessário fornecer o nome da instância do Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] na cadeia de conexão. Além disso, este exemplo especifica o uso do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (SQLNCLI11) para o provedor de dados que requer o software de cliente de rede adicionais a serem instalados. Para obter mais informações, consulte [requisitos de sistema do SQL Server Native Client](../../../relational-databases/native-client/system-requirements-for-sql-server-native-client.md).  
  
```  
Option Explicit  
Sub Main()  
  
   Dim oTestStream As New ADODB.Stream  
   Dim oTestConnection As New ADODB.Connection  
   Dim oTestCommand As New ADODB.Command  
  
   oTestConnection.Open "provider=SQLXMLOLEDB.4.0;data provider=SQLNCLI11;data source=SqlServerName;initial catalog=AdventureWorks;Integrated Security=SSPI;"  
  
   oTestCommand.ActiveConnection = oTestConnection  
   oTestCommand.Properties("ClientSideXML") = "False"  
  
   oTestCommand.CommandText = "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'> " & _  
        " <sql:xpath-query mapping-schema='mySchema.xml' > " & _  
        "   root " & _  
        "   </sql:xpath-query> " & _  
        " </ROOT> "  
   oTestStream.Open  
   ' You need the dialect if you are executing a template.  
   oTestCommand.Dialect = "{5d531cb2-e6ed-11d2-b252-00c04f681b71}"  
   oTestCommand.Properties("Output Stream").Value = oTestStream  
   oTestCommand.Properties("Base Path").Value = "c:\Schemas\SQLXML4\TemplateWithXPath\"  
   oTestCommand.Properties("Mapping Schema").Value = "mySchema.xml"  
   oTestCommand.Properties("Output Encoding") = "utf-8"  
   oTestCommand.Execute , , adExecuteStream  
   oTestStream.Position = 0  
   oTestStream.Charset = "utf-8"  
   Debug.Print oTestStream.ReadText(adReadAll)  
  
End Sub  
  
Sub Form_Load()  
   Main  
End Sub  
```  
  
 Este é o esquema:  
  
```  
<xsd:schema xmlns:xsd='https://www.w3.org/2001/XMLSchema'  
   xmlns:sql='urn:schemas-microsoft-com:mapping-schema'>  
 <xsd:element name= 'root' sql:is-constant='1'>   
    <xsd:complexType>  
       <xsd:sequence>  
         <xsd:element ref = 'Contact'/>  
       </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
  
  <xsd:element name='Contact' sql:relation='Person.Contact'>  
     <xsd:complexType>  
          <xsd:attribute name='ContactID' type='xsd:integer' />  
          <xsd:attribute name='FirstName' type='xsd:string'/>   
          <xsd:attribute name='LastName' type='xsd:string' />   
     </xsd:complexType>  
   </xsd:element>  
</xsd:schema>  
```  
  
  
