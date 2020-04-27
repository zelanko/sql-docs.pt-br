---
title: Executando consultas XPath (provedor SQLXMLOLEDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXMLOLEDB Provider, executing XPath queries
- queries [SQLXML], SQLXMLOLEDB Provider
- Base Path property
- XPath queries [SQLXML], SQLXMLOLEDB Provider
- Mapping Schema property
ms.assetid: 19063222-dc9c-48ae-a55f-778103674a9e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 10539c4eb4a8953a968ea4a6acff1e25e0298aae
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66013103"
---
# <a name="executing-xpath-queries-sqlxmloledb-provider"></a>Executando consultas XPath (provedor SQLXMLOLEDB)
  Este exemplo ilustra o uso das seguintes propriedades específicas de provedor SQLXMLOLEDB:  
  
-   `ClientSideXML`  
  
-   `Base Path`  
  
-   `Mapping Schema`  
  
 Neste aplicativo de exemplo do ADO, uma consulta XPath (raiz) é especificada em um esquema de mapeamento XSD (MySchema.xml). O esquema tem um ** \<elemento Contacts>** com os atributos **ContactID**, **FirstName**e **LastName** . No esquema, ocorre o mapeamento padrão: um nome de elemento é mapeado para a tabela com o mesmo nome, e os atributos do tipo simples, para as colunas com os mesmos nomes.  
  
```  
<xsd:schema xmlns:xsd='http://www.w3.org/2001/XMLSchema'  
   xmlns:sql='urn:schemas-microsoft-com:mapping-schema'>  
 <xsd:element name= 'root' sql:is-constant='1'>   
    <xsd:complexType>  
       <xsd:sequence>  
         <xsd:element ref = 'Contacts'/>  
       </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
  <xsd:element name='Contacts' sql:relation='Person.Contact'>   
     <xsd:complexType>  
          <xsd:attribute name='ContactID' type='xsd:integer' />  
          <xsd:attribute name='FirstName' type='xsd:string'/>   
          <xsd:attribute name='LastName' type='xsd:string' />   
     </xsd:complexType>  
   </xsd:element>  
</xsd:schema>  
```  
  
 A propriedade esquema de mapeamento fornece o esquema de mapeamento no qual a consulta XPath é executada. O esquema de mapeamento pode ser um esquema XSD ou XDR. A propriedade caminho base fornece o caminho do arquivo para o esquema de mapeamento.  
  
 A propriedade ClientSideXML é definida como true. Assim, o documento XML é gerado no cliente.  
  
 No aplicativo, uma consulta XPath é especificada diretamente. Por isso, o dialeto XPath {ec2a4293-e898-11d2-b1b7-00c04f680c56} deve ser incluído.  
  
> [!NOTE]  
>  No código, é necessário fornecer o nome da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] na cadeia de conexão. Além disso, este exemplo especifica o uso do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cliente nativo (SQLNCLI11) para o provedor de dados que requer a instalação de um software cliente de rede adicional. Para obter mais informações, consulte [requisitos do sistema para SQL Server Native Client](../../native-client/system-requirements-for-sql-server-native-client.md).  
  
```  
Option Explicit  
Sub main()  
Dim oTestStream As New ADODB.Stream  
Dim oTestConnection As New ADODB.Connection  
Dim oTestCommand As New ADODB.Command  
  
oTestConnection.Open "provider=SQLXMLOLEDB.4.0;data provider=SQLNCLI11;data source=SqlServerName;initial catalog=AdventureWorks;Integrated Security= SSPI;"  
  
oTestCommand.ActiveConnection = oTestConnection  
oTestCommand.Properties("ClientSideXML") = True  
  
oTestCommand.CommandText = "root"  
oTestStream.Open  
oTestCommand.Dialect = "{ec2a4293-e898-11d2-b1b7-00c04f680c56}"  
oTestCommand.Properties("Output Stream").Value = oTestStream  
oTestCommand.Properties("Base Path").Value = "c:\Schemas\SQLXML4\XPathDirect\"  
oTestCommand.Properties("Mapping Schema").Value = "mySchema.xml"  
oTestCommand.Properties("Output Encoding") = "utf-8"  
oTestCommand.Execute , , adExecuteStream  
oTestStream.Position = 0  
oTestStream.Charset = "utf-8"  
Debug.Print oTestStream.ReadText(adReadAll)  
  
End Sub  
Sub Form_Load()  
 main  
End Sub  
```  
  
  
