---
title: Executando consultas XPath (provedor SQLXMLOLEDB)
description: Saiba como usar propriedades específicas do provedor SQLXMLOLEDB ao executar consultas XPath.
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d5a337408ef4cf1a2e4b72cbb20f9c64681efd0c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85650318"
---
# <a name="executing-xpath-queries-sqlxmloledb-provider"></a>Executando consultas XPath (provedor SQLXMLOLEDB)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  Este exemplo ilustra o uso das seguintes propriedades específicas de provedor SQLXMLOLEDB:  
  
-   **ClientSideXML**  
  
-   **Caminho base**  
  
-   **Esquema de mapeamento**  
  
 Neste aplicativo de exemplo do ADO, uma consulta XPath (raiz) é especificada em um esquema de mapeamento XSD (MySchema.xml). O esquema tem um **\<Contacts>** elemento com os atributos **ContactID**, **FirstName**e **LastName** . No esquema, ocorre o mapeamento padrão: um nome de elemento é mapeado para a tabela com o mesmo nome, e os atributos do tipo simples, para as colunas com os mesmos nomes.  
  
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
>  No código, é necessário fornecer o nome da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] na cadeia de conexão. Além disso, este exemplo especifica o uso do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cliente nativo (SQLNCLI11) para o provedor de dados que requer a instalação de um software cliente de rede adicional. Para obter mais informações, consulte [requisitos do sistema para SQL Server Native Client](../../../relational-databases/native-client/system-requirements-for-sql-server-native-client.md).  
  
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
  
  
