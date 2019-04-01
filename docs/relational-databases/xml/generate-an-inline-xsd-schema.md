---
title: Gerar um esquema XSD embutido | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- XSD schemas [SQL Server]
- XMLSCHEMA option
- schemas [SQL Server], XML
- XDR schemas
- FOR XML clause, inline XSD schema generation
- inline XSD schema generation [SQL Server]
- XMLDATA option
ms.assetid: 04b35145-1cca-45f4-9eb7-990abf2e647d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 386540c5f11561a8d576de045fd151531877b063
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58512433"
---
# <a name="generate-an-inline-xsd-schema"></a>Gerar um esquema XSD embutido
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Em uma cláusula FOR XML, é possível solicitar que a consulta retorne um esquema embutido junto com os resultados da consulta. Para obter um esquema XDR, use a palavra-chave XMLDATA na cláusula FOR XML. Para obter um esquema XSD, use a palavra-chave XMLSCHEMA.  
  
 Este tópico descreve a palavra-chave XMLSCHEMA e explica a estrutura do esquema XSD embutido resultante. As limitações a seguir estão presentes quando você está solicitando esquemas embutidos:  
  
-   É possível especificar XMLSCHEMA em modo RAW e AUTO, não em modo EXPLICIT.  
  
-   Se uma consulta FOR XML especificar a diretiva TYPE, o resultado da consulta será de tipo **xml** e esse resultado será tratado como uma instância dos dados XML sem-tipo. Para obter mais informações, veja [Dados XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md).  
  
 Quando você especifica XMLSCHEMA em uma consulta FOR XML, recebe um esquema e dados XML, o resultado da consulta. Cada elemento de alto nível dos dados faz referência ao esquema anterior usando uma declaração de namespace padrão que, por sua vez, faz referência ao namespace de destino do esquema embutido.  
  
 Por exemplo:  
  
```  
<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:schema="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="https://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">  
  <xsd:import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes" schemaLocation="https://schemas.microsoft.com/sqlserver/2004/sqltypes/sqltypes.xsd" />  
  <xsd:element name="Production.ProductModel">  
    <xsd:complexType>  
      <xsd:attribute name="ProductModelID" type="sqltypes:int" use="required" />  
      <xsd:attribute name="Name" use="required">  
        <xsd:simpleType sqltypes:sqlTypeAlias="[AdventureWorks2012].[dbo].[Name]">  
          <xsd:restriction base="sqltypes:nvarchar" sqltypes:localeId="1033" sqltypes:sqlCompareOptions="IgnoreCase IgnoreKanaType IgnoreWidth" sqltypes:sqlSortId="52">  
            <xsd:maxLength value="50" />  
          </xsd:restriction>  
        </xsd:simpleType>  
      </xsd:attribute>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
<Production.ProductModel xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1" ProductModelID="1" Name="Classic Vest" />  
```  
  
 O resultado inclui o esquema XML e o resultado do XML. O elemento de alto nível <`ProductModel`> no resultado faz referência ao esquema usando a declaração de namespace padrão, xmlns = "urn:schemas-microsoft-com:sql:SqlRowSet 1."  
  
 A parte de esquema do resultado pode conter vários documentos de esquema que descrevem vários namespaces. Como um mínimo, os seguintes dois documentos de esquema são retornados:  
  
-   Um documento de esquema para o namespace **Sqltypes** e para o qual os tipos básicos de SQL estão sendo retornados.  
  
-   Outro documento de esquema que descreve a forma do resultado da consulta FOR XML.  
  
 Além disso, se quaisquer tipos de dados **xml** com tipo estiverem incluídos no resultado da consulta, os esquemas associados a esses tipos de dados **xml** com tipo serão incluídos.  
  
 O namespace de destino do documento de esquema que descreve a forma do resultado de FOR XML contém uma parte fixa e uma parte numérica que é incrementada automaticamente. O formato desse namespace é mostrado no exemplo a seguir em que *n* é um inteiro positivo. Por exemplo, na consulta anterior, urn:schemas-microsoft-com:sql:SqlRowSet 1 é o namespace de destino.  
  
```  
urn:schemas-microsoft-com:sql:SqlRowSetn  
```  
  
 A alteração nos namespaces de destino no resultado que ocorreu de uma execução para outra pode não ser desejável. Por exemplo, se você consultar o XML resultante, a alteração no namespace de destino precisará que a consulta seja atualizada. Opcionalmente, é possível especificar um namespace de destino quando a opção XMLSCHEMA é adicionada à cláusula FOR XML. O XML resultante incluirá o namespace fornecido e permanecerá igual, independentemente de quantas vezes você executou a consulta.  
  
```  
SELECT ProductModelID, Name  
FROM   Production.ProductModel  
WHERE ProductModelID=1  
FOR XML AUTO, XMLSCHEMA ('MyURI')  
```  
  
## <a name="entity-elements"></a>Elementos de entidade  
 Para discutir os detalhes da estrutura do esquema XSD gerada para o resultado da consulta, é necessário primeiro descrever o elemento  
  
 Um elemento de entidade nos dados XML retornados pela consulta FOR XML é um elemento gerado a partir de uma tabela e não de uma coluna. Por exemplo, a consulta FOR XML a seguir retorna informações de contato da tabela `Person` no banco de dados `AdventureWorks2012` .  
  
```  
SELECT BusinessEntityID, FirstName  
FROM Person.Person  
WHERE BusinessEntityID = 1  
FOR XML AUTO, ELEMENTS  
```  
  
 Este é o resultado:  
  
 `<Person>`  
  
 `<BusinessEntityID>1</BusinessEntityID>`  
  
 `<FirstName>Ken</FirstName>`  
  
 `</Person>`  
  
 Nesse resultado, <`Person`> é o elemento de entidade. Pode haver vários elementos de entidade no resultado XML e cada um deles tem uma declaração global no esquema XSD embutido. Por exemplo, a consulta a seguir recupera o cabeçalho do pedido de vendas e informações detalhadas de um pedido específico.  
  
```  
SELECT  SalesOrderHeader.SalesOrderID, ProductID, OrderQty  
FROM    Sales.SalesOrderHeader, Sales.SalesOrderDetail  
WHERE   SalesOrderHeader.SalesOrderID = SalesOrderDetail.SalesOrderID  
AND     SalesOrderHeader.SalesOrderID=5001  
FOR XML AUTO, ELEMENTS, XMLSCHEMA  
```  
  
 Como a consulta especifica a diretiva ELEMENTS, o XML resultante é centrado em elemento. A consulta também especifica a diretiva XMLSCHEMA. Portanto, um esquema XSD embutido é retornado. Este é o resultado:  
  
 `<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:schema="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="https://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">`  
  
 `<xsd:import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes" schemaLocation="https://schemas.microsoft.com/sqlserver/2004/sqltypes/sqltypes.xsd" />`  
  
 `<xsd:element name="Sales.SalesOrderHeader">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="SalesOrderID" type="sqltypes:int" />`  
  
 `<xsd:element ref="schema:Sales.SalesOrderDetail" minOccurs="0" maxOccurs="unbounded" />`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `<xsd:element name="Sales.SalesOrderDetail">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="ProductID" type="sqltypes:int" />`  
  
 `<xsd:element name="OrderQty" type="sqltypes:smallint" />`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `</xsd:schema>`  
  
 Observe o seguinte na consulta anterior:  
  
-   No resultado, <`SalesOrderHeader`> e <`SalesOrderDetail`> são elementos de entidade. Por isso, eles são declarados globalmente no esquema. Isto é, a declaração é exibida no nível superior dentro do elemento <`Schema`>.  
  
-   O <`SalesOrderID`>, <`ProductID`>e <`OrderQty`> não são elementos de entidade porque são mapeados para colunas. Os dados de coluna são retornados como elementos no XML por causa da diretiva ELEMENTS. Estes são mapeados para elementos locais do tipo complexo do elemento de entidade. Observe que, se a diretiva ELEMENTS não for especificada, os valores de `SalesOrderID`, `ProductID` e `OrderQty` serão mapeados para atributos locais do tipo complexo do elemento de entidade correspondente.  
  
## <a name="attribute-name-clashes"></a>Conflitos de nomes de atributos  
 A discussão a seguir baseia-se nas tabelas `CustOrder` e `CustOrderDetail` . Para testar os exemplos a seguir, crie essas tabelas e adicione seus próprios dados de exemplo:  
  
```  
CREATE TABLE CustOrder (OrderID int primary key, CustomerID int)  
GO  
CREATE TABLE CustOrderDetail (OrderID int, ProductID int, Qty int)  
GO  
```  
  
 No FOR XML, algumas vezes, o mesmo nome é usado para indicar propriedades e atributos diferentes. Por exemplo, a seguinte consulta em modo RAW centrada em atributo gera dois atributos que têm o mesmo nome, OrderID. Isso gera um erro.  
  
```  
SELECT CustOrder.OrderID,   
       CustOrderDetail.ProductID,   
       CustOrderDetail.OrderID  
FROM   dbo.CustOrder, dbo.CustOrderDetail  
WHERE  CustOrder.OrderID = CustOrderDetail.OrderID  
FOR XML RAW, XMLSCHEMA  
```  
  
 No entanto, como é aceitável ter dois elementos com o mesmo nome, é possível eliminar o problema adicionando a diretiva ELEMENTS:  
  
```  
SELECT CustOrder.OrderID,  
       CustOrderDetail.ProductID,   
       CustOrderDetail.OrderID  
from   dbo.CustOrder, dbo.CustOrderDetail  
where  CustOrder.OrderID = CustOrderDetail.OrderID  
FOR XML RAW, XMLSCHEMA, ELEMENTS  
```  
  
 Este é o resultado. Observe que no esquema XSD embutido, o elemento OrderID está definido duas vezes. Uma das declarações tem minOccurs definido como 0, que corresponde ao OrderID da tabela CustOrderDetail, e a segunda é mapeada para a coluna de chave primária OrderID da tabela `CustOrder` , na qual, por padrão, minOccurs é 1.  
  
 `<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="https://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">`  
  
 `<xsd:import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes" schemaLocation="https://schemas.microsoft.com/sqlserver/2004/sqltypes/sqltypes.xsd" />`  
  
 `<xsd:element name="row">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="OrderID" type="sqltypes:int" />`  
  
 `<xsd:element name="ProductID" type="sqltypes:int" minOccurs="0" />`  
  
 `<xsd:element name="OrderID" type="sqltypes:int" minOccurs="0" />`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `</xsd:schema>`  
  
## <a name="element-name-clashes"></a>Conflitos de nomes de elementos  
 Em FOR XML, o mesmo nome pode ser usado para indicar dois subelementos. Por exemplo, a consulta a seguir recupera valores de ListPrice e DealerPrice de produtos, mas a consulta especifica o mesmo alias, Price, para essas duas colunas. Portanto o conjunto de linhas resultante terá duas colunas com o mesmo nome.  
  
### <a name="case-1-both-subelements-are-nonkey-columns-of-the-same-type-and-can-be-null"></a>Caso 1: Os dois subelementos são colunas não chave do mesmo tipo e podem ser NULL  
 Na consulta seguinte, os dois subelementos são colunas não chave do mesmo tipo e podem ser NULL.  
  
```  
DROP TABLE T  
go  
CREATE TABLE T (ProductID int primary key, ListPrice money, DealerPrice money)  
go  
INSERT INTO T values (1, 1.25, null)  
go  
  
SELECT ProductID, ListPrice Price, DealerPrice Price  
FROM   T  
for    XML RAW, ELEMENTS, XMLSCHEMA  
```  
  
 Este é o XML correspondente gerado. Apenas uma fração do XSD embutido é mostrada:  
  
 `...`  
  
 `<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="https://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">`  
  
 `<xsd:import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes" />`  
  
 `<xsd:element name="row">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="ProductID" type="sqltypes:int" />`  
  
 `<xsd:element name="Price" type="sqltypes:money" minOccurs="0" maxOccurs="2" />`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `</xsd:schema>`  
  
 `<row xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1">`  
  
 `<ProductID>1</ProductID>`  
  
 `<Price>1.2500</Price>`  
  
 `</row>`  
  
 Observe o seguinte no esquema XSD embutido:  
  
-   ListPrice e DealerPrice são do mesmo tipo, `money`, e ambos podem ser NULL na tabela. Portanto, como eles podem não ser retornados no XML resultante, há apenas um elemento filho <`Price`> na declaração de tipo complexo do elemento <`row`> que tem minOccurs=0 e maxOccurs=2.  
  
-   No resultado, como o valor de `DealerPrice` é NULL na tabela, apenas `ListPrice` é retornado como um elemento <`Price`>. Se adicionar o parâmetro `XSINIL` à diretiva ELEMENTS, você receberá os dois elementos que têm o valor de `xsi:nil` definido como TRUE para o elemento<`Price`> correspondente a DealerPrice. Também receberá dois elementos filho <`Price`> na definição de tipo complexo <`row`> no esquema XSD embutido com o atributo `nillable` definido como TRUE para ambos. Este fragmento é um resultado parcial:  
  
 `...`  
  
 `<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="https://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">`  
  
 `<xsd:import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes" />`  
  
 `<xsd:element name="row">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="ProductID" type="sqltypes:int" nillable="1" />`  
  
 `<xsd:element name="Price" type="sqltypes:money" nillable="1" />`  
  
 `<xsd:element name="Price" type="sqltypes:money" nillable="1" />`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `</xsd:schema>`  
  
 `<row xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`  
  
 `<ProductID>1</ProductID>`  
  
 `<Price>1.2500</Price>`  
  
 `<Price xsi:nil="true" />`  
  
 `</row>`  
  
### <a name="case-2-one-key-and-one-nonkey-column-of-the-same-type"></a>Caso 2: Uma coluna de chave e uma de não chave do mesmo tipo  
 A consulta a seguir ilustra uma coluna de chave e uma de não chave do mesmo tipo.  
  
```  
CREATE TABLE T (Col1 int primary key, Col2 int, Col3 nvarchar(20))  
go  
INSERT INTO T VALUES (1, 1, 'test')  
go   
```  
  
 A seguinte consulta na tabela **T** especifica o mesmo alias para Col1 e Col2, em que Col1 é uma chave primária e não pode ser nula e Col2 pode ser nula. Isso gera dois elementos irmãos que são filhos do elemento <`row`>.  
  
```  
SELECT Col1 as Col, Col2 as Col, Col3  
FROM T  
FOR XML RAW, ELEMENTS, XMLSCHEMA  
```  
  
 Este é o resultado. Apenas um fragmento do esquema XSD embutido é mostrado.  
  
 `...`  
  
 `<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="https://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">`  
  
 `<xsd:import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes" />`  
  
 `<xsd:element name="row">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="Col" type="sqltypes:int" />`  
  
 `<xsd:element name="Col" type="sqltypes:int" minOccurs="0" />`  
  
 `<xsd:element name="Col3" minOccurs="0">`  
  
 `<xsd:simpleType>`  
  
 `<xsd:restriction base="sqltypes:nvarchar"`  
  
 `sqltypes:localeId="1033"`  
  
 `sqltypes:sqlCompareOptions="IgnoreCase`  
  
 `IgnoreKanaType IgnoreWidth"`  
  
 `sqltypes:sqlSortId="52">`  
  
 `<xsd:maxLength value="20" />`  
  
 `</xsd:restriction>`  
  
 `</xsd:simpleType>`  
  
 `</xsd:element>`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `</xsd:schema>`  
  
 `<row xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1">`  
  
 `<Col>1</Col>`  
  
 `<Col>1</Col>`  
  
 `<Col3>test</Col3>`  
  
 `</row>`  
  
 Observe que, no esquema XSD embutido, o elemento <`Col`> correspondente a Col2 tem minOccurs definido como 0.  
  
### <a name="case-3-both-elements-of-different-types-and-corresponding-columns-can-be-null"></a>Caso 3: Os dois elementos de tipos diferentes e colunas correspondentes podem ser NULL  
 A consulta seguinte é especificada para a tabela de exemplo mostrada no caso 2:  
  
```  
SELECT Col1, Col2 as Col, Col3 as Col  
FROM T  
FOR XML RAW, ELEMENTS, XMLSCHEMA  
```  
  
 Na consulta a seguir, Col2 e Col3 recebem os mesmos alias. Isso gera dois elementos irmãos que têm o mesmo nome e que são filhos do elemento <`raw`> no resultado. Essas duas colunas são de tipos diferentes e podem ser NULL. Este é o resultado. Apenas um esquema XSD embutido parcial é mostrado.  
  
 `...`  
  
 `<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="https://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">`  
  
 `<xsd:import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes" />`  
  
 `<xsd:simpleType name="Col1">`  
  
 `<xsd:restriction base="sqltypes:int" />`  
  
 `</xsd:simpleType>`  
  
 `<xsd:simpleType name="Col2">`  
  
 `<xsd:restriction base="sqltypes:nvarchar" sqltypes:localeId="1033"`  
  
 `sqltypes:sqlCompareOptions="IgnoreCase`  
  
 `IgnoreKanaType IgnoreWidth" sqltypes:sqlSortId="52">`  
  
 `<xsd:maxLength value="20" />`  
  
 `</xsd:restriction>`  
  
 `</xsd:simpleType>`  
  
 `<xsd:element name="row">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="Col1" type="sqltypes:int" />`  
  
 `<xsd:element name="Col" minOccurs="0" maxOccurs="2" type="xsd:anySimpleType" />`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `</xsd:schema>`  
  
 `<row xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1">`  
  
 `<Col1>1</Col1>`  
  
 `<Col xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"`  
  
 `xsi:type="Col1">1</Col>`  
  
 `<Col xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"`  
  
 `xsi:type="Col2">test</Col>`  
  
 `</row>`  
  
 Observe o seguinte no esquema XSD embutido:  
  
-   Como Col2 e Col3 podem ser NULL, a declaração do elemento <`Col`> especifica minOccurs como 0 e maxOccurs como 2.  
  
-   Como os dois elementos <`Col`> são irmãos, há uma declaração de elemento no esquema. Além disso, como os dois elementos também são de tipos diferentes, embora ambos sejam de tipos simples, o tipo do elemento no esquema é `xsd:anySimpleType`. No resultado, cada tipo de instância é identificado pelo atributo `xsi:type`.  
  
-   No resultado, cada instância do elemento <`Col`> faz referência ao seu tipo de instância usando o atributo `xsi:type`.  
  
  
