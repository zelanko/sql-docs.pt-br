---
title: Especificando eixos em consultas XPath (SQLXML)
description: Saiba como especificar eixos nas consultas XPath do SQLXML 4,0.
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], axes
- context node [SQLXML]
- attribute axis [SQLXML]
- axis [SQLXML]
- child axis
- parent axis
- axes [SQLXML]
ms.assetid: d17b8278-da58-4576-95b4-7a92772566d8
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 81bbefa0969cd4408ed0fbb21a2a035ddde5508e
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97413615"
---
# <a name="specifying-axes-in-xpath-queries-sqlxml-40"></a>Especificando eixos em consultas XPath (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  Os seguintes exemplos mostram como os eixos são especificados em consultas XPath.  
  
 As consultas XPath nesses exemplos são especificadas com relação ao esquema de mapeamento contido em SampleSchema1.xml. Para obter informações sobre este esquema de exemplo, consulte [exemplo de esquema XSD anotado para exemplos de XPath &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-retrieve-child-elements-of-the-context-node"></a>a. Recuperar elementos filho do nó de contexto  
 A consulta XPath a seguir seleciona todos os **\<Contact>** elementos filho do nó de contexto:  
  
```  
/child::Contact  
```  
  
 Na consulta, `child` é o eixo e `Contact` é o teste de nó (verdadeiro se `Contact` for um **\<element>** nó, porque \<element> é o tipo de nó primário associado ao `child` eixo).  
  
 O eixo `child` é o padrão. Portanto, a consulta pode ser escrita da seguinte forma:  
  
```  
/Contact  
```  
  
##### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>Para testar a consulta XPath com relação ao esquema de mapeamento  
  
1.  Copie o [código do esquema de exemplo](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md) e cole-o em um arquivo de texto. Salve o arquivo como SampleSchema1.xml.  
  
2.  Crie o seguinte modelo (XPathAxesSampleA.xml) e salve-o no diretório onde SampleSchema1.xml foi salvo.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        /Contact  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     O caminho do diretório especificado para o esquema de mapeamento (SampleSchema1.xml) é relativo ao diretório em que o modelo foi salvo. Também é possível especificar um caminho absoluto, por exemplo:  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  Crie e use o script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o modelo.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4,0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Aqui está o conjunto de resultados parcial da execução do modelo:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
  <Contact ContactID="1" LastName="Achong" FirstName="Gustavo" Title="Mr." />   
  <Contact ContactID="2" LastName="Abel" FirstName="Catherine" Title="Ms." />   
  <Contact ContactID="3" LastName="Abercrombie" FirstName="Kim" Title="Ms." />   
  <Contact ContactID="4" LastName="Acevedo" FirstName="Humberto" Title="Sr." />  
  ...  
</ROOT>  
```  
  
### <a name="b-retrieve-grandchildren-of-the-context-node"></a>B. Recuperar os netos do nó de contexto  
 A consulta XPath a seguir seleciona todos os **\<Order>** elementos filho do **\<Customer>** elemento filho do nó de contexto:  
  
```  
/child::Customer/child::Order  
```  
  
 Na consulta, `child` é o eixo e `Customer` e `Order` são os testes de nó (esses testes de nó serão verdadeiros se o cliente e a ordem forem **\<element>** nós, porque o **\<element>** nó é o nó primário do eixo **filho** ). Para cada nó correspondente **\<Customer>** , os nós correspondentes **\<Orders>** são adicionados ao resultado. Somente **\<Order>** é retornado no conjunto de resultados.  
  
 O eixo **filho** é o padrão. Assim, a consulta pode ser especificada como:  
  
```  
/Customer/Order  
```  
  
##### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>Para testar a consulta XPath com relação ao esquema de mapeamento  
  
1.  Copie o [código do esquema de exemplo](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md) e cole-o em um arquivo de texto. Salve o arquivo como SampleSchema1.xml.  
  
2.  Crie o seguinte modelo (XPathAxesSampleB.xml) e salve-o no diretório onde:  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        /Customer/Order  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     O caminho do diretório especificado para o esquema de mapeamento (SampleSchema1.xml) é relativo ao diretório em que o modelo foi salvo. Também é possível especificar um caminho absoluto, por exemplo:  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  Crie e use o script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o modelo.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4,0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Aqui está o conjunto de resultados parcial da execução do modelo:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Order SalesOrderID="Ord-43860" SalesPersonID="280"   
         OrderDate="2001-08-01T00:00:00"   
         DueDate="2001-08-13T00:00:00"   
         ShipDate="2001-08-08T00:00:00">  
  <OrderDetail ProductID="Prod-729" UnitPrice="226.8571"   
               OrderQty="1" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-732" UnitPrice="440.1742"   
               OrderQty="1" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-738" UnitPrice="220.2496"   
               OrderQty="1" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-753" UnitPrice="2576.3544"   
               OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-756" UnitPrice="1049.7528"   
               OrderQty="1" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-758" UnitPrice="1049.7528"   
               OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-761" UnitPrice="503.3507"   
               OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-762" UnitPrice="503.3507"   
               OrderQty="1" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-763" UnitPrice="503.3507"   
               OrderQty="1" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-765" UnitPrice="503.3507"   
               OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-768" UnitPrice="503.3507"   
               OrderQty="1" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-770" UnitPrice="503.3507"   
               OrderQty="1" UnitPriceDiscount="0" />   
  </Order>  
   ...  
</ROOT>  
```  
  
 Se a consulta XPath for especificada como `Customer/Order/OrderDetail` , de cada nó correspondente à **\<Customer>** consulta navegará para seus **\<Order>** elementos. E para cada nó correspondente **\<Order>** , a consulta adiciona os nós **\<OrderDetail>** ao resultado. Somente **\<OrderDetail>** é retornado no conjunto de resultados.  
  
### <a name="c-use--to-specify-the-parent-axis"></a>C. Usar . para especificar o eixo pai  
 A consulta a seguir recupera todos os **\<Order>** elementos com um **\<Customer>** elemento pai com um valor de atributo **CustomerID** de 1. A consulta usa o eixo **filho** no predicado para localizar o pai do **\<Order>** elemento.  
  
```  
/child::Customer/child::Order[../@CustomerID="1"]  
```  
  
 O eixo **filho** é o eixo padrão. Assim, a consulta pode ser especificada como:  
  
```  
/Customer/Order[../@CustomerID="1"]  
```  
  
 A consulta XPath é equivalente a:  
  
```  
/Customer[@CustomerID="1"]/Order.  
```  
  
> [!NOTE]  
>  A consulta XPath `/Order[../@CustomerID="1"]` retornará um erro, pois não há nenhum pai de **\<Order>** . Embora possa haver elementos no esquema de mapeamento que contêm **\<Order>** , o XPath não começou em nenhum deles; consequentemente, **\<Order>** é considerado um tipo de elemento de nível superior no documento.  
  
##### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>Para testar a consulta XPath com relação ao esquema de mapeamento  
  
1.  Copie o [código do esquema de exemplo](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md) e cole-o em um arquivo de texto. Salve o arquivo como SampleSchema1.xml.  
  
2.  Crie o seguinte modelo (XPathAxesSampleC.xml) e salve-o no diretório onde:  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        /Customer/Order[../@CustomerID="1"]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     O caminho do diretório especificado para o esquema de mapeamento (SampleSchema1.xml) é relativo ao diretório em que o modelo foi salvo. Também é possível especificar um caminho absoluto, por exemplo:  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  Crie e use o script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o modelo.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4,0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Aqui está o conjunto de resultados parcial da execução do modelo:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Order SalesOrderID="Ord-43860" SalesPersonID="280"   
         OrderDate="2001-08-01T00:00:00"   
         DueDate="2001-08-13T00:00:00"   
         ShipDate="2001-08-08T00:00:00">  
  <OrderDetail ProductID="Prod-729" UnitPrice="226.8571"   
               OrderQty="1" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-732" UnitPrice="440.1742"   
               OrderQty="1" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-738" UnitPrice="220.2496"   
               OrderQty="1" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-753" UnitPrice="2576.3544"   
               OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-756" UnitPrice="1049.7528"   
               OrderQty="1" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-758" UnitPrice="1049.7528"   
               OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-761" UnitPrice="503.3507"   
               OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-762" UnitPrice="503.3507"   
               OrderQty="1" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-763" UnitPrice="503.3507"   
               OrderQty="1" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-765" UnitPrice="503.3507"   
               OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-768" UnitPrice="503.3507"   
               OrderQty="1" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-770" UnitPrice="503.3507"   
               OrderQty="1" UnitPriceDiscount="0" />   
  </Order>  
   ...  
</Order>  
</ROOT>  
```  
  
### <a name="d-specify-the-attribute-axis"></a>D. Especificar o eixo de atributo  
 A consulta XPath a seguir seleciona todos os **\<Customer>** elementos filho do nó de contexto com um valor de atributo **CustomerID** de 1:  
  
```  
/child::Customer[attribute::CustomerID="1"]  
```  
  
 No predicado `attribute::CustomerID` , `attribute` é o eixo e `CustomerID` é o teste do nó (se `CustomerID` for um atributo, o teste do nó será verdadeiro, pois o **\<attribute>** nó é o nó primário do `attribute` eixo).  
  
 Um atalho para o eixo `attribute` (@) pode ser especificado e, como o eixo `child` é o padrão, ele pode ser omitido da consulta:  
  
```  
/Customer[@CustomerID="1"]  
```  
  
##### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>Para testar a consulta XPath com relação ao esquema de mapeamento  
  
1.  Copie o [código do esquema de exemplo](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md) e cole-o em um arquivo de texto. Salve o arquivo como SampleSchema1.xml.  
  
2.  Crie seguinte o modelo (XPathAxesSampleD.xml) e salve-o no diretório onde SampleSchema1.xml foi salvo.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        child::Customer[attribute::CustomerID="1"]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     O caminho do diretório especificado para o esquema de mapeamento (SampleSchema1.xml) é relativo ao diretório em que o modelo foi salvo. Também é possível especificar um caminho absoluto, por exemplo:  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  Crie e use o script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o modelo.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4,0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Aqui está o conjunto de resultados parcial da execução do modelo:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Customer CustomerID="1" SalesPersonID="280"   
            TerritoryID="1" AccountNumber="1"   
            CustomerType="S" Orders="Ord-43860 Ord-44501 Ord-45283 Ord-46042">  
    <Order SalesOrderID="Ord-43860" SalesPersonID="280"   
           OrderDate="2001-08-01T00:00:00"   
           DueDate="2001-08-13T00:00:00"   
           ShipDate="2001-08-08T00:00:00">  
       <OrderDetail ProductID="Prod-729" UnitPrice="226.8571"   
                    OrderQty="1" UnitPriceDiscount="0" />   
       <OrderDetail ProductID="Prod-732" UnitPrice="440.1742"   
                    OrderQty="1" UnitPriceDiscount="0" />   
       <OrderDetail ProductID="Prod-738" UnitPrice="220.2496"   
                    OrderQty="1" UnitPriceDiscount="0" />   
      ...   
    </Order>  
   ...  
  </Customer>  
</ROOT>  
```  
  
  
