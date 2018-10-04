---
title: 'Especificando relações usando SQL: Relationship (SQLXML 4.0) | Microsoft Docs'
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- IDREFS relationships [SQLXML]
- parent attribute [SQLXML]
- element relationships [SQLXML]
- multiple element relationships
- attribute relationships [SQLXML]
- sql:relationship
- relationship chains [SQLXML]
- IDREF relationships [SQLXML]
- parent-child relationships [SQLXML]
- relationship annotation
- XSD schemas [SQLXML], relationships
- annotated XSD schemas, relationships
- relationships [SQLXML], specifying
- unnamed relationships
- ID relationships [SQLXML]
- hierarchical relationships [SQLXML]
- named relationships [SQLXML]
ms.assetid: 98820afa-74e1-4e62-b336-6111a3dede4c
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7578df8d31dadba739bb2de58a8568f6ba55d7e4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47661954"
---
# <a name="specifying-relationships-using-sqlrelationship-sqlxml-40"></a>Especificando relações usando sql:relationship (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Os elementos em um documento XML podem ser relacionados. Eles podem ser aninhados hierarquicamente e as relações ID, IDREF ou IDREFS entre os elementos podem ser especificadas.  
  
 Por exemplo, em um esquema XSD, uma  **\<cliente >** elemento contém  **\<Order >** elementos filho. Quando o esquema é mapeado para o banco de dados AdventureWorks, o  **\<cliente >** elemento é mapeado para a tabela Sales. Customer e o  **\<Order >** elemento é mapeado para o Tabela Sales. SalesOrderHeader. Essas tabelas subjacentes, Sales. Customer e Sales. SalesOrderHeader, estão relacionadas porque os clientes fazem pedidos. O elemento CustomerID na tabela Sales.SalesOrderHeader é uma chave estrangeira que se refere à chave primária CustomerID na tabela Sales.Customer. Você pode estabelecer estas relações entre elementos de esquema de mapeamento usando o **SQL: Relationship** anotação.  
  
 No esquema XSD anotado, o **SQL: Relationship** anotação é usada para aninhar os elementos de esquema hierarquicamente, com base na chave primária e chave estrangeira entre as tabelas subjacentes para o qual os elementos do mapa. Especificar o **SQL: Relationship** anotação, você deve identificar o seguinte:  
  
-   A tabela pai (Sales.Customer) e a tabela filha (Sales.SalesOrderHeader).  
  
-   A coluna ou as colunas que compõem a relação entre as tabelas pai e filha. Por exemplo, a coluna CustomerID que aparece nas tabelas pai e filha.  
  
 Estas informações são usadas para gerar a hierarquia adequada.  
  
 Para fornecer os nomes de tabela e as informações de junção necessárias, os seguintes atributos são especificados na **SQL: Relationship** anotação. Esses atributos são válidos somente com o  **\<SQL: Relationship >** elemento:  
  
 **Nome**  
 Especifica o nome exclusivo da relação.  
  
 **Parent**  
 Especifica a relação pai (tabela). Este é um atributo opcional. Se o atributo não for especificado, o nome da tabela pai será obtido das informações na hierarquia filha no documento. Se o esquema especificar duas hierarquias pai-filho que usam os mesmos  **\<SQL: Relationship >** mas elementos pai diferente, você não especificar o atributo pai em  **\<sql: relação >**. Essas informações são obtidas da hierarquia no esquema.  
  
 **parent-key**  
 Especifica a chave pai do pai. Se a chave pai for composta por várias colunas, os valores serão especificados com um espaço entre eles. Há um mapeamento posicional entre os valores que são especificados para a chave de várias colunas e para a chave filha correspondente.  
  
 **filho**  
 Especifica a relação de filho (tabela).  
  
 **child-key**  
 Especifica a chave filha no filho que se refere à parent-key no pai. Se a chave filha for composta por vários atributos (colunas), os valores de child-key serão especificados com um espaço entre eles. Há um mapeamento posicional entre os valores que são especificados para a chave de várias colunas e para a chave pai correspondente.  
  
 **Inverso**  
 Este atributo especificado em  **\<SQL: Relationship >** é usado por diagramas de atualização. Para obter mais informações, consulte [especificando o atributo SQL: Inverse em SQL: Relationship](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-the-sql-inverse-attribute-on-sql-relationship-sqlxml-4-0.md).  
  
 O **SQL: Key-campos** anotação deve ser especificada em um elemento que contém um elemento filho, que tem um  **\<SQL: Relationship >** definida entre o elemento e o filho, e ele faz Forneça a chave primária da tabela especificada no elemento pai. Mesmo se o esquema não especificar  **\<SQL: Relationship >**, você deve especificar **SQL: Key-campos** para gerar a hierarquia adequada. Para obter mais informações, consulte [Identifying Key Columns by Using SQL: Key-campos](../../relational-databases/sqlxml-annotated-xsd-schemas-using/identifying-key-columns-using-sql-key-fields-sqlxml-4-0.md).  
  
 Para produzir o aninhamento adequado no resultado, é recomendável que **SQL: Key-campos** são especificados em todos os esquemas.  
  
## <a name="examples"></a>Exemplos  
 Para criar exemplos de funcionamento usando os exemplos a seguir, é necessário atender a determinados requisitos. Para obter mais informações, consulte [requisitos para executar exemplos do SQLXML](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-the-sqlrelationship-annotation-on-an-element"></a>A. Especificando uma anotação sql:relationship em um elemento  
 Inclui o seguinte esquema XSD anotado  **\<cliente >** e  **\<Order >** elementos. O  **\<ordem >** é um elemento filho do  **\<cliente >** elemento.  
  
 No esquema, o **SQL: Relationship** anotação é especificada na  **\<ordem >** elemento filho. A própria relação é definida na  **\<xsd:appinfo >** elemento.  
  
 O  **\<relação >** elemento identifica CustomerID na tabela Sales. SalesOrderHeader como uma chave estrangeira que faz referência à chave primária CustomerID na tabela Sales. Customer. Portanto, os pedidos que pertencem a um cliente aparecem como um elemento filho do que  **\<cliente >** elemento.  
  
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
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customer" sql:relation="Sales.Customer" type="CustomerType" />  
   <xsd:complexType name="CustomerType" >  
     <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Sales.SalesOrderHeader"  
                    sql:relationship="CustOrders" >  
           <xsd:complexType>  
              <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
              <xsd:attribute name="CustomerID" type="xsd:string" />  
           </xsd:complexType>  
        </xsd:element>  
     </xsd:sequence>  
        <xsd:attribute name="CustomerID"   type="xsd:string" />   
    </xsd:complexType>  
  
</xsd:schema>  
```  
  
 O esquema anterior usa uma relação nomeada. Você pode também especificar uma relação sem-nome. Os resultados são os mesmos.  
  
 Este é o esquema revisado no qual uma relação sem-nome é especificada:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  
  <xsd:element name="Customer" sql:relation="Sales.Customer"  type="CustomerType" />  
   <xsd:complexType name="CustomerType" >  
     <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Sales.SalesOrderHeader">  
           <xsd:annotation>  
            <xsd:appinfo>  
              <sql:relationship   
                parent="Sales.Customer"  
                parent-key="CustomerID"  
                child="Sales.SalesOrderHeader"  
                child-key="CustomerID" />  
            </xsd:appinfo>  
           </xsd:annotation>  
           <xsd:complexType>  
              <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
              <xsd:attribute name="CustomerID" type="xsd:string" />  
           </xsd:complexType>  
        </xsd:element>  
     </xsd:sequence>  
        <xsd:attribute name="CustomerID"   type="xsd:string" />   
    </xsd:complexType>  
  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Para testar uma consulta XPath de exemplo com relação ao esquema  
  
1.  Copie o código de esquema acima e cole-o em um arquivo de texto. Salve o arquivo como sql-relationship.xml.  
  
2.  Copie o seguinte modelo abaixo e cole-o em um arquivo de texto. Salve o arquivo como sql-relationshipT.xml no mesmo diretório em que você salvou sql-relationship.xml.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="sql-relationship.xml">  
            /Customer[@CustomerID=1]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     O caminho de diretório especificado para o esquema de mapeamento (sql-relationship.xml) é relativo ao diretório onde o modelo é salvo. Também é possível especificar um caminho absoluto, por exemplo:  
  
    ```  
    mapping-schema="C:\MyDir\sql-relationship.xml"  
    ```  
  
3.  Crie e use o script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o modelo.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas SQLXML](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Este é o conjunto de resultados:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
  <Customer CustomerID="1">   
    <Order OrderID="43860" CustomerID="1" />   
    <Order OrderID="44501" CustomerID="1" />   
    <Order OrderID="45283" CustomerID="1" />   
    <Order OrderID="46042" CustomerID="1" />   
  </Customer>   
</ROOT>  
```  
  
### <a name="b-specifying-a-relationship-chain"></a>B. Especificando uma cadeia de relações  
 Para obter este exemplo, pressuponha que você deseja o seguinte documento XML que use dados obtidos do banco de dados AdventureWorks:  
  
```  
<Order SalesOrderID="43659">  
  <Product Name="Mountain Bike Socks, M"/>   
  <Product Name="Sport-100 Helmet, Blue"/>  
  ...  
</Order>  
...  
```  
  
 Para cada pedido na tabela Sales. SalesOrderHeader, o documento XML tem uma  **\<ordem >** elemento. E cada  **\<ordem >** elemento tem uma lista de  **\<produto >** elementos filho, um para cada produto solicitado no pedido.  
  
 Para especificar um esquema XSD que gerará esta hierarquia, você deve especificar duas relações: OrderOD e ODProduct. A relação OrderOD especifica a relação pai-filho entre as tabelas Sales.SalesOrderHeader e Sales.SalesOrderDetail. A relação ODProduct especifica a relação entre as tabelas Sales.SalesOrderDetail e Production.Product.  
  
 No esquema a seguir, o **msdata:relationship** anotação sob o  **\<produto >** elemento especifica dois valores: OrderOD e ODProduct. A ordem em que esses valores são especificados é importante.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:msdata="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <msdata:relationship name="OrderOD"  
          parent="Sales.SalesOrderHeader"  
          parent-key="SalesOrderID"  
          child="Sales.SalesOrderDetail"  
          child-key="SalesOrderID" />  
  
    <msdata:relationship name="ODProduct"  
          parent="Sales.SalesOrderDetail"  
          parent-key="ProductID"  
          child="Production.Product"  
          child-key="ProductID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Order" msdata:relation="Sales.SalesOrderHeader"   
               msdata:key-fields="SalesOrderID" type="OrderType" />  
   <xsd:complexType name="OrderType" >  
     <xsd:sequence>  
        <xsd:element name="Product" msdata:relation="Production.Product"   
                     msdata:key-fields="ProductID"  
                     msdata:relationship="OrderOD ODProduct">  
          <xsd:complexType>  
             <xsd:attribute name="Name" type="xsd:string" />  
          </xsd:complexType>  
        </xsd:element>  
     </xsd:sequence>  
        <xsd:attribute name="SalesOrderID"   type="xsd:integer" />   
    </xsd:complexType>  
</xsd:schema>  
```  
  
 Em vez de especificar uma relação nomeada, você pode especificar uma relação anônima. Nesse caso, todo o conteúdo do  **\<anotação >**...  **\</annotation >**, que descreve as duas relações, aparecem como um elemento filho do  **\<produto >**.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:msdata="urn:schemas-microsoft-com:mapping-schema">  
  
  <xsd:element name="Order" msdata:relation="Sales.SalesOrderHeader"   
               msdata:key-fields="SalesOrderID" type="OrderType" />  
  
   <xsd:complexType name="OrderType" >  
     <xsd:sequence>  
        <xsd:element name="Product" msdata:relation="Production.Product"   
                     msdata:key-fields="ProductID" >  
         <xsd:annotation>  
          <xsd:appinfo>  
           <msdata:relationship   
               parent="Sales.SalesOrderHeader"  
               parent-key="SalesOrderID"  
               child="Sales.SalesOrderDetail"  
               child-key="SalesOrderID" />  
  
           <msdata:relationship   
               parent="Sales.SalesOrderDetail"  
               parent-key="ProductID"  
               child="Production.Product"  
               child-key="ProductID" />  
         </xsd:appinfo>  
       </xsd:annotation>  
       <xsd:complexType>  
          <xsd:attribute name="Name" type="xsd:string" />  
       </xsd:complexType>  
     </xsd:element>  
   </xsd:sequence>  
   <xsd:attribute name="SalesOrderID"   type="xsd:integer" />   
  </xsd:complexType>  
 </xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Para testar uma consulta XPath de exemplo com relação ao esquema  
  
1.  Copie o código de esquema acima e cole-o em um arquivo de texto. Salve o arquivo como relationshipChain.xml.  
  
2.  Copie o seguinte modelo abaixo e cole-o em um arquivo de texto. Salve o arquivo como relationshipChainT.xml no mesmo diretório em que você salvou relationshipChain.xml.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="relationshipChain.xml">  
            /Order  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     O caminho de diretório especificado para o esquema de mapeamento (relationshipChain.xml) é relativo ao diretório onde o modelo é salvo. Também é possível especificar um caminho absoluto, por exemplo:  
  
    ```  
    mapping-schema="C:\MyDir\relationshipChain.xml"  
    ```  
  
3.  Crie e use o script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o modelo.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas SQLXML](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Este é o conjunto de resultados:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
  <Order SalesOrderID="43659">  
    <Product Name="Mountain Bike Socks, M" />   
    <Product Name="Sport-100 Helmet, Blue" />   
    <Product Name="AWC Logo Cap" />   
    <Product Name="Long-Sleeve Logo Jersey, M" />   
    <Product Name="Long-Sleeve Logo Jersey, XL" />   
    ...  
  </Order>  
  ...  
</ROOT>  
```  
  
### <a name="c-specifying-the-relationship-annotation-on-an-attribute"></a>C. Especificando a anotação de relação em um atributo  
 O esquema neste exemplo inclui um \<Customer > elemento com um \<CustomerID > elemento filho e um atributo OrderIDList do tipo IDREFS. O \<Customer > elemento é mapeado para a tabela Sales. Customer no banco de dados AdventureWorks. Por padrão, o escopo desse mapeamento se aplica a todos os elementos filho ou atributos, a menos que **Relation** é especificado no elemento filho ou atributo, caso em que a relação adequada de primary key/foreign key deve ser definido usando o \<relação > elemento. E o elemento filho ou atributo, que especifica a tabela diferente usando o **relação** anotação, deverá especificar também a **relação** anotação.  
  
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
     </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customer" sql:relation="Sales.Customer" type="CustomerType" />  
   <xsd:complexType name="CustomerType" >  
     <xsd:sequence>  
        <xsd:element name="CustomerID"   type="xsd:string" />   
     </xsd:sequence>  
     <xsd:attribute name="OrderIDList"   
                     type="xsd:IDREFS"   
                     sql:relation="Sales.SalesOrderHeader"   
                     sql:field="SalesOrderID"  
                     sql:relationship="CustOrders" >  
        </xsd:attribute>  
    </xsd:complexType>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Para testar uma consulta XPath de exemplo com relação ao esquema  
  
1.  Copie o código de esquema acima e cole-o em um arquivo de texto. Salve o arquivo como relationship-on-attribute.xml.  
  
2.  Copie o seguinte modelo e cole-o em um arquivo. Salve o arquivo como relationship-on-attributeT.xml no mesmo diretório onde você salvou relationship-on-attribute.xml. A consulta no modelo seleciona um cliente com o CustomerID 1.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="relationship-on-attribute.xml">  
        /Customer[CustomerID=1]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     O caminho de diretório especificado para o esquema de mapeamento (relationship-on-attribute.xml) é relativo ao diretório onde o modelo é salvo. Também é possível especificar um caminho absoluto, por exemplo:  
  
    ```  
    mapping-schema="C:\MyDir\relationship-on-attribute.xml"  
    ```  
  
3.  Crie e use o script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o modelo.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas SQLXML](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Este é o conjunto de resultados:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
  <Customer OrderIDList="43860 44501 45283 46042">  
    <CustomerID>1</CustomerID>   
  </Customer>  
</ROOT>  
```  
  
### <a name="d-specifying-sqlrelationship-on-multiple-elements"></a>D. Especificando sql:relationship em vários elementos  
 Neste exemplo, o esquema XSD anotado contém o  **\<cliente >**,  **\<Order >**, e  **\<OrderDetail >** elementos.  
  
 O  **\<ordem >** é um elemento filho do  **\<cliente >** elemento. **\<SQL: Relationship >** for especificado em de  **\<ordem >** elemento filho; portanto, os pedidos que pertencem a um cliente aparecem como elementos filho do  **\<cliente >**.  
  
 O  **\<ordem >** elemento inclui o  **\<OrderDetail >** elemento filho. **\<SQL: Relationship >** for especificado em  **\<OrderDetail >** elemento filho, portanto, os detalhes do pedido que pertençam a um pedido apareçam como elementos filho que **\<ordem >** elemento.  
  
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
              <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
              <xsd:attribute name="OrderDate" type="xsd:date" />  
              <xsd:attribute name="CustomerID" type="xsd:string" />  
          </xsd:complexType>  
        </xsd:element>  
      </xsd:sequence>  
      <xsd:attribute name="CustomerID" type="xsd:string" />  
     </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Para testar uma consulta XPath de exemplo com relação ao esquema  
  
1.  Copie o código de esquema acima e cole-o em um arquivo de texto. Salve o arquivo como relationship-multiple-elements.xml.  
  
2.  Copie o modelo a seguir e cole-o em um arquivo de texto. Salve o arquivo como relationship-multiple-elementsT.xml no mesmo diretório onde você salvou relationship-multiple-elements.xml. A consulta no modelo retorna informações de pedido por um cliente com o CustomerID de 1 e SalesOrderID de 43860.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="relationship-multiple-elements.xml">  
        /Customer[@CustomerID=1]/Order[@SalesOrderID=43860]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     O caminho de diretório especificado para o esquema de mapeamento (relationship-multiple-elements.xml) é relativo ao diretório onde o modelo é salvo. Também é possível especificar um caminho absoluto, por exemplo:  
  
    ```  
    mapping-schema="C:\MyDir\relationship-multiple-elements.xml"  
    ```  
  
3.  Crie e use o script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o modelo.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas SQLXML](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Este é o conjunto de resultados:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Order SalesOrderID="43860" OrderDate="2001-08-01" CustomerID="1">  
     <OrderDetail SalesOrderID="43860" ProductID="761" OrderQty="2" />   
     <OrderDetail SalesOrderID="43860" ProductID="770" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="758" OrderQty="2" />   
     <OrderDetail SalesOrderID="43860" ProductID="765" OrderQty="2" />   
     <OrderDetail SalesOrderID="43860" ProductID="732" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="762" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="738" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="768" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="753" OrderQty="2" />   
     <OrderDetail SalesOrderID="43860" ProductID="729" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="763" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="756" OrderQty="1" />   
  </Order>  
</ROOT>  
```  
  
### <a name="e-specifying-the-sqlrelationship-without-the-parent-attribute"></a>E. Especificando o \<SQL: Relationship > sem o atributo pai  
 Este exemplo ilustra especificando o  **\<SQL: Relationship >** sem a **pai** atributo. Por exemplo, pressuponha que você tenha as seguintes tabelas de funcionário:  
  
```  
Emp1(SalesPersonID, FirstName, LastName, ReportsTo)  
Emp2(SalesPersonID, FirstName, LastName, ReportsTo)  
```  
  
 A seguinte exibição XML tem o  **\<Emp1 >** e  **\<Emp2 >** elementos de mapeamento de tabelas do Sales.Emp1 e Sales.Emp2:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="EmpOrders"  
          parent-key="SalesPersonID"  
          child="Sales.SalesOrderHeader"  
          child-key="SalesPersonID" />  
     </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Emp1" sql:relation="Sales.Emp1" type="EmpType" />  
  <xsd:element name="Emp2" sql:relation="Sales.Emp2" type="EmpType" />  
   <xsd:complexType name="EmpType" >  
     <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Sales.SalesOrderHeader"   
                     sql:relationship="EmpOrders" >  
          <xsd:complexType>  
             <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
             <xsd:attribute name="CustomerID" type="xsd:string" />  
          </xsd:complexType>  
        </xsd:element>  
     </xsd:sequence>  
        <xsd:attribute name="SalesPersonID"   type="xsd:integer" />   
        <xsd:attribute name="LastName"   type="xsd:string" />   
    </xsd:complexType>  
  
</xsd:schema>  
```  
  
 No esquema, tanto a  **\<Emp1 >** elemento e  **\<Emp2 >** elemento são do tipo **EmpType**. O tipo **EmpType** descreve uma  **\<ordem >** elemento filho e correspondente  **\<SQL: Relationship >**. Nesse caso, não há nenhum pai único que pode ser identificado no  **\<SQL: Relationship >** usando o **pai** atributo. Nessa situação, você não especificar o **pai** atributo no  **\<SQL: Relationship >**; o **pai** informações de atributo são obtidas das hierarquia no esquema.  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Para testar uma consulta XPath de exemplo com relação ao esquema  
  
1.  Crie estas tabelas no banco de dados AdventureWorks:  
  
    ```  
    USE AdventureWorks  
    CREATE TABLE Sales.Emp1 (  
           SalesPersonID int primary key,   
           FirstName  varchar(20),   
           LastName   varchar(20),   
           ReportsTo int)  
    Go  
    CREATE TABLE Sales.Emp2 (  
           SalesPersonID int primary key,   
           FirstName  varchar(20),   
           LastName   varchar(20),   
           ReportsTo int)  
    Go  
    ```  
  
2.  Adicione estes dados de exemplo nas tabelas:  
  
    ```  
    INSERT INTO Sales.Emp1 values (279, 'Nancy', 'Devolio',NULL)  
    INSERT INTO Sales.Emp1 values (282, 'Andrew', 'Fuller',1)  
    INSERT INTO Sales.Emp1 values (276, 'Janet', 'Leverling',1)  
    INSERT INTO Sales.Emp2 values (277, 'Margaret', 'Peacock',3)  
    INSERT INTO Sales.Emp2 values (283, 'Steven', 'Devolio',4)  
    INSERT INTO Sales.Emp2 values (275, 'Nancy', 'Buchanan',5)  
    INSERT INTO Sales.Emp2 values (281, 'Michael', 'Suyama',6)  
    ```  
  
3.  Copie o código de esquema acima e cole-o em um arquivo de texto. Salve o arquivo como relationship-noparent.xml.  
  
4.  Copie o modelo a seguir e cole-o em um arquivo de texto. Salve o arquivo como relationship-noparentT.xml no mesmo diretório em que você salvou relationship-noparent.xml. A consulta no modelo seleciona todos os \<Emp1 > elementos (portanto, o pai é Emp1).  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="relationship-noparent.xml">  
            /Emp1  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     O caminho de diretório especificado para o esquema de mapeamento (relationship-noparent.xml) é relativo ao diretório onde o modelo é salvo. Também é possível especificar um caminho absoluto, por exemplo:  
  
    ```  
    mapping-schema="C:\MyDir\relationship-noparent.xml"  
    ```  
  
5.  Crie e use o script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o modelo.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas SQLXML](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Aqui está um conjunto de resultados parciais:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
<Emp1 SalesPersonID="276" LastName="Leverling">  
  <Order SalesOrderID="43663" CustomerID="510" />   
  <Order SalesOrderID="43666" CustomerID="511" />   
  <Order SalesOrderID="43859" CustomerID="259" />  
  ...  
</Emp1>  
```  
  
  
