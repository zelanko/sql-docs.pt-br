---
title: 'Criando atributos de tipo ID, IDREF e IDREFS válidos usando SQL: prefix (SQLXML 4,0) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- IDREFS relationships [SQLXML]
- annotated XSD schemas, ID type attribute
- IDREF type attribute [SQLXML]
- annotated XSD schemas, IDREFS type attribute
- ID type attribute [SQLXML]
- sql:prefix
- prefix annotation
- IDREF relationships [SQLXML]
- IDREFS type attribute [SQLXML]
- annotated XSD schemas, IDREF type attribute
- ID relationships [SQLXML]
ms.assetid: 1c7f77d3-81f3-4820-bb63-c4aaa4ea9aa1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 48ae7034ec0c133c1140e4c581794302ca8bad77
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66013917"
---
# <a name="creating-valid-id-idref-and-idrefs-type-attributes-using-sqlprefix-sqlxml-40"></a>Criando atributos de tipo ID, IDREF e IDREFS válidos usando sql:prefix (SQLXML 4.0)
  Um atributo pode ser especificado como um atributo de tipo ID. Atributos especificados como IDREF ou IDREFS poderão, então, ser usados para fazer referência aos atributos de tipo ID, permitindo vínculos entre documentos.  
  
 ID, IDREF e IDREFS correspondem a relações CP/FK (chave primária/chave estrangeira) no banco de dados, com poucas diferenças. Em um documento XML, os valores de atributos de tipo ID devem ser distintos. Se os atributos **CustomerID** e **OrderID** forem especificados como tipo de ID em um documento XML, esses valores deverão ser distintos. No entanto, em um banco de dados, as colunas CustomerID e OrderID podem ter os mesmos valores. (Por exemplo, CustomerID = 1 e OrderID = 1 são válidos no banco de dados.)  
  
 Para que os atributos ID, IDREF e IDREFS sejam válidos:  
  
-   O valor de ID deve ser exclusivo dentro do documento XML.  
  
-   Para todos os atributos IDREF e IDREFS, os valores de ID referenciados devem estar no documento XML.  
  
-   O valor de um atributo ID, IDREF e IDREFS deve ser um token nomeado. (Por exemplo, o valor inteiro 101 não pode ser um valor de ID.)  
  
-   Os atributos de tipo ID, IDREF e IDREFS não podem ser mapeados para colunas do tipo `text`, `ntext` ou `image`, nem para qualquer outro tipo de dados binários (por exemplo, `timestamp`).  
  
 Se um documento XML contiver várias IDs, use a anotação `sql:prefix` para garantir que os valores sejam exclusivos.  
  
 Observe que a anotação `sql:prefix` não pode ser usada com atributo fixo XSD.  
  
## <a name="examples"></a>Exemplos  
 Para criar exemplos de funcionamento usando os exemplos a seguir, é necessário atender a determinados requisitos. Para obter mais informações, consulte [Requirements for running SQLXML examples](../sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-id-and-idrefs-types"></a>a. Especificando os tipos ID e IDREFS  
 No esquema a seguir, o ** \<elemento>do cliente** consiste no ** \<elemento filho Order>** . O ** \<elemento Order>** também tem um elemento filho, o ** \<OrderDetail>** elemento.  
  
 O atributo **OrderIDList** de ** \<>do cliente** é um atributo de tipo IDREFS que se refere ao atributo **OrderID** do elemento ** \<Order>** .  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustOrders"  
                 parent="Sales.Customer"  
                 parent-key="CustomerID"  
                 child="Sales.SalesOrderHeader"  
                 child-key="CustomerID" />  
    <sql:relationship name="OrderOrderDetail"  
                 parent="Sales.SalesOrderHeader"  
                 parent-key="SalesOrderID"  
                 child="Sales.SalesOrderDetail"  
                 child-key="SalesOrderID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  <xsd:element name="Customer" sql:relation="Sales.Customer" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader"    
               sql:relationship="CustOrders" maxOccurs="unbounded" >  
          <xsd:complexType>  
              <xsd:sequence>  
                <xsd:element name="OrderDetail"   
                             sql:relation="Sales.SalesOrderDetail"   
                   sql:relationship="OrderOrderDetail"   
                   maxOccurs="unbounded" >  
                  <xsd:complexType>  
                   <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
                   <xsd:attribute name="ProductID" type="xsd:string" />  
                   <xsd:attribute name="OrderQty" type="xsd:integer" />  
                  </xsd:complexType>  
               </xsd:element>  
             </xsd:sequence>  
             <xsd:attribute name="SalesOrderID"   
                            type="xsd:ID" sql:prefix="ord-" />  
             <xsd:attribute name="OrderDate" type="xsd:date" />  
             <xsd:attribute name="CustomerID" type="xsd:string" />  
          </xsd:complexType>  
      </xsd:element>  
    </xsd:sequence>  
    <xsd:attribute name="CustomerID" type="xsd:string" />  
    <xsd:attribute name="OrderIDList" type="xsd:IDREFS"   
                   sql:relation="Sales.SalesOrderHeader" sql:field="SalesOrderID"  
                   sql:relationship="CustOrders" sql:prefix="ord-">  
    </xsd:attribute>  
  </xsd:complexType>  
</xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Para testar uma consulta XPath de exemplo com relação ao esquema  
  
1.  Copie o código de esquema acima e cole-o em um arquivo de texto. Salve o arquivo como sqlPrefix.xml.  
  
2.  Copie o modelo a seguir e cole-o em um arquivo de texto. Salve o arquivo como sqlPrefixT.xml no mesmo diretório onde você salvou sqlPrefix.xml.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="sqlPrefix.xml">  
        /Customer[@CustomerID=1]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     O caminho de diretório especificado para o esquema de mapeamento (sqlPrefix.xml) é relativo ao diretório onde o modelo está salvo. Também é possível especificar um caminho absoluto, por exemplo:  
  
    ```  
    mapping-schema="C:\SqlXmlTest\sqlPrefix.xml"  
    ```  
  
3.  Crie e use o script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o modelo.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Este é o resultado parcial:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Customer CustomerID="1" OrderIDList="ord-43860 ord-44501 ord-45283 ord-46042">  
    <Order SalesOrderID="ord-43860" OrderDate="2001-08-01" CustomerID="1">  
      <OrderDetail SalesOrderID="43860" ProductID="729" OrderQty="1" />   
      <OrderDetail SalesOrderID="43860" ProductID="732" OrderQty="1" />   
      <OrderDetail SalesOrderID="43860" ProductID="738" OrderQty="1" />   
      <OrderDetail SalesOrderID="43860" ProductID="753" OrderQty="2" />   
      ...  
    </Order>  
    ...  
 </Customer>  
</ROOT>  
```  
  
  
