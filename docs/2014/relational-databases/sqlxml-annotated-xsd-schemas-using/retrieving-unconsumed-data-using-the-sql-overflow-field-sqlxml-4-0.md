---
title: 'Recuperando dados não consumidos usando SQL: overflow-field (SQLXML 4.0) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- unconsumed data
- storing unconsumed data
- retrieving unconsumed data
- annotated XSD schemas, unconsumed data
- overflow data [SQLXML]
- sql:overflow-field
ms.assetid: 8526998d-b47d-4a32-8dc2-7f50a8d11097
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: d0787be7f62ae4a3fc593d750bb6fc6f2b949cc6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36119477"
---
# <a name="retrieving-unconsumed-data-using-the-sqloverflow-field-sqlxml-40"></a>Recuperando dados não consumidos usando sql:overflow-field (SQLXML 4.0)
  Quando forem inseridos registros em um banco de dados a partir de um documento XML usando a função OPENXML do [!INCLUDE[tsql](../../includes/tsql-md.md)], todos os dados não consumidos no documento XML de origem poderão ser armazenados em uma coluna. Ao recuperar os dados de um banco de dados usando esquemas anotados, o atributo `sql:overflow-field` pode ser especificado para identificar a coluna da tabela na qual os dados de estouro estão armazenados. O `sql:overflow-field` atributo pode ser especificado em  **\<elemento >**.  
  
 Em seguida, esses dados são recuperados destas formas:  
  
-   Os atributos armazenados na coluna de estouro são adicionados ao elemento que contém a anotação `sql:overflow-field`.  
  
-   Os elementos filhos e seus descendentes, armazenados na coluna de estouro do banco de dados, são adicionados como elementos filhos, após o conteúdo que é especificado explicitamente no esquema. (Nenhuma ordem é preservada.)  
  
## <a name="examples"></a>Exemplos  
 Para criar exemplos de funcionamento usando os exemplos a seguir, é necessário atender a determinados requisitos. Para obter mais informações, consulte [requisitos para executar exemplos do SQLXML](../sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-sqloverflow-field-for-an-element"></a>A. Especificando sql:overflow-field para um elemento  
 Este exemplo presume que o seguinte script foi executado de forma que existe uma tabela chamada Customers2 no banco de dados tempdb:  
  
```  
USE tempdb  
CREATE TABLE Customers2 (  
CustomerID       VARCHAR(10),   
ContactName    VARCHAR(30),   
AddressOverflow    NVARCHAR(500))  
  
GO  
INSERT INTO Customers2 VALUES (  
'ALFKI',   
'Joe',  
'<Address>  
  <Address1>Maple St.</Address1>  
  <Address2>Apt. E105</Address2>  
  <City>Seattle</City>  
  <State>WA</State>  
  <Zip>98147</Zip>  
 </Address>')  
GO  
```  
  
 Além disso, você deve criar um diretório virtual para o banco de dados tempdb e um nome virtual de modelo do tipo `template` chamado "template".  
  
 No exemplo a seguir, o esquema de mapeamento recupera os dados não consumidos que são armazenados na coluna AddressOverflow tabela Customers2:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  
  <xsd:element name="Customers2" sql:overflow-field="AddressOverflow" >  
    <xsd:complexType>  
      <xsd:attribute name="CustomerID"  type="xsd:integer"/>  
      <xsd:attribute name="ContactName"  type="xsd:string" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Para testar uma consulta XPath de exemplo com relação ao esquema  
  
1.  Copie o código de esquema acima e cole-o em um arquivo de texto. Salve o arquivo como Overflow.xml.  
  
2.  Copie o modelo a seguir e cole-o em um arquivo de texto. Salve o arquivo como OverflowT.xml no mesmo diretório em que você salvou Overflow.xml. A consulta no modelo seleciona os registros na tabela Customer2.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="Overflow.xml">  
            /Customers2  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     O caminho de diretório especificado para o esquema de mapeamento (Overflow.xml) é relativo ao diretório no qual o modelo foi salvo. Também é possível especificar um caminho absoluto, por exemplo:  
  
    ```  
    mapping-schema="C:\SqlXmlTest\Overflow.xml"  
    ```  
  
3.  Crie e use o script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o modelo.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4.0](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Este é o conjunto de resultados:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Customers2 CustomerID="ALFKI" ContactName="Joe">  
    <Address1>Maple St.</Address1>   
    <Address2>Apt. E105</Address2>   
    <City>Seattle</City>   
    <State>WA</State>   
    <Zip>98147</Zip>   
  </Customers2>  
</ROOT>  
```  
  
  