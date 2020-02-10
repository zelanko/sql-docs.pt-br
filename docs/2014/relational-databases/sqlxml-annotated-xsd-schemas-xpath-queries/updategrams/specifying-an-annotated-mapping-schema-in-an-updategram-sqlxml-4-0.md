---
title: Especificando um esquema de mapeamento anotado em um updategram (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- annotated XSD schemas, updategrams
- data types [SQLXML], mapping schema in updategrams
- updategrams [SQLXML], annotated mapping schemas
- annotated XDR schemas, updategrams
- inverse attribute
- parent-child relationships [SQLXML]
- mapping-schema attribute
- mapping schema [SQLXML], updategrams
- sql:inverse
ms.assetid: 2e266ed9-4cfb-434a-af55-d0839f64bb9a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 627ab54ed35cbc0a43c5a0eac26a1397199edbd8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66014660"
---
# <a name="specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-40"></a>Especificando um esquema de mapeamento anotado em um diagrama de atualização (SQLXML 4.0)
  Este tópico explica como o esquema de mapeamento (XSD ou XDR), especificado em um diagrama de atualização, é usado para processar as atualizações. Em um updategram, você pode fornecer o nome de um esquema de mapeamento anotado a ser usado no mapeamento dos elementos e atributos no updategram para tabelas e colunas [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]no. Quando um esquema de mapeamento é especificado em um diagrama de atualização, os nomes de elementos e atributos especificados no diagrama deverão ser mapeados para os elementos e atributos do esquema de mapeamento.  
  
 Para especificar um esquema de mapeamento, use o `mapping-schema` atributo do elemento de ** \<>de sincronização** . Os exemplos a seguir mostram dois diagramas de atualização: um que usa um esquema de mapeamento simples e outro que usa um esquema mais complexo.  
  
> [!NOTE]  
>  Esta documentação parte do pressuposto de que você esteja familiarizado com suporte a modelos e ao esquema de mapeamento no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [introdução aos esquemas XSD anotados &#40;SQLXML 4,0&#41;](../../sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md). Para aplicativos herdados que usam XDR, consulte [esquemas XDR anotados &#40;preteridos no SQLXML 4,0&#41;](../../sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md).  
  
## <a name="dealing-with-data-types"></a>Lidando com tipos de dados  
 Se o esquema especificar o `image`tipo `binary`de dados `varbinary` [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , ou (usando `sql:datatype`) e não especificar um tipo de dados XML, o updategram assumirá que o tipo de dados XML `binary base 64`é. Se seus dados forem do tipo `bin.base`, você deverá especificar explicitamente o tipo (`dt:type=bin.base` ou `type="xsd:hexBinary"`).  
  
 Se o esquema especificar o tipo de dados XSD `dateTime`, `date` ou `time`, você também deverá especificar o tipo de dados [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] correspondente usando `sql:datatype="dateTime"`.  
  
 Ao manipular parâmetros do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] `money` tipo, você deve especificar `sql:datatype="money"` explicitamente no nó apropriado no esquema de mapeamento.  
  
## <a name="examples"></a>Exemplos  
 Para criar exemplos de trabalho usando os exemplos a seguir, você deve atender aos requisitos especificados em [requisitos para executar exemplos do SQLXML](../../sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-creating-an-updategram-with-a-simple-mapping-schema"></a>a. Criando um diagrama de atualização com um esquema de mapeamento simples  
 O esquema XSD a seguir (SampleSchema. xml) é um esquema de mapeamento que mapeia o elemento de ** \<>do cliente** para a tabela Sales. Customer:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Customer" sql:relation="Sales.Customer" >  
   <xsd:complexType>  
        <xsd:attribute name="CustID"    
                       sql:field="CustomerID"   
                       type="xsd:string" />  
        <xsd:attribute name="RegionID"    
                       sql:field="TerritoryID"    
                       type="xsd:string" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 O diagrama de atualização a seguir insere um registro na tabela Sales.Customer e usa o esquema de mapeamento anterior para mapear adequadamente esses dados para a tabela. Observe que o updategram usa o mesmo nome de elemento, ** \<>do cliente **, conforme definido no esquema. Isso é obrigatório porque o diagrama especifica um esquema específico.  
  
##### <a name="to-test-the-updategram"></a>Para testar o diagrama de atualização  
  
1.  Copie o código de esquema acima e cole-o em um arquivo de texto. Salve o arquivo como SampleUpdateSchema.xml.  
  
2.  Copie o modelo de diagrama abaixo e cole-o em um arquivo de texto. Salve o arquivo como SampleUpdategram.xml no mesmo diretório em que você salvou SampleUpdateSchema.xml.  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
      <updg:sync mapping-schema="SampleUpdateSchema.xml">  
        <updg:before>  
          <Customer CustID="1" RegionID="1"  />  
        </updg:before>  
        <updg:after>  
          <Customer CustID="1" RegionID="2" />  
        </updg:after>  
      </updg:sync>  
    </ROOT>  
    ```  
  
     O caminho de diretório especificado para o esquema de mapeamento (SampleUpdateSchema.xml) é relativo ao diretório onde o modelo foi salvo. Também é possível especificar um caminho absoluto, por exemplo:  
  
    ```  
    mapping-schema="C:\SqlXmlTest\SampleUpdateSchema.xml"  
    ```  
  
3.  Crie e use o script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o modelo.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4,0](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Este é o esquema XDR equivalente:  
  
```  
<?xml version="1.0" ?>  
   <Schema xmlns="urn:schemas-microsoft-com:xml-data"   
         xmlns:dt="urn:schemas-microsoft-com:datatypes"   
         xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
     <ElementType name="Customer" sql:relation="Sales.Customer" >  
       <AttributeType name="CustID" />  
       <AttributeType name="RegionID" />  
  
       <attribute type="CustID" sql:field="CustomerID" />  
       <attribute type="RegionID" sql:field="TerritoryID" />  
     </ElementType>  
   </Schema>   
```  
  
### <a name="b-inserting-a-record-by-using-the-parent-child-relationship-specified-in-the-mapping-schema"></a>B. Inserindo um registro usando a relação pai-filho especificada no esquema de mapeamento  
 Elementos de esquema podem ser relacionados. O ** \<elemento SQL: relationship>** especifica a relação pai-filho entre os elementos do esquema. Essas informações são usadas para atualizar as tabelas correspondentes que têm relação chave primária/chave estrangeira.  
  
 O esquema de mapeamento a seguir (SampleSchema. xml) consiste em dois elementos, ** \<Order>** e ** \<OD>**:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="OrderOD"  
          parent="Sales.SalesOrderHeader"  
          parent-key="SalesOrderID"  
          child="Sales.SalesOrderDetail"  
          child-key="SalesOrderID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="OD"   
                     sql:relation="Sales.SalesOrderDetail"  
                     sql:relationship="OrderOD" >  
           <xsd:complexType>  
              <xsd:attribute name="SalesOrderID"   type="xsd:integer" />  
              <xsd:attribute name="ProductID" type="xsd:integer" />  
             <xsd:attribute name="UnitPrice"  type="xsd:decimal" />  
             <xsd:attribute name="OrderQty"   type="xsd:integer" />  
             <xsd:attribute name="UnitPriceDiscount"   type="xsd:decimal" />  
  
           </xsd:complexType>  
        </xsd:element>  
     </xsd:sequence>  
        <xsd:attribute name="CustomerID"   type="xsd:string" />   
        <xsd:attribute name="SalesOrderID"  type="xsd:integer" />  
        <xsd:attribute name="OrderDate"  type="xsd:date" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 O updategram a seguir usa esse esquema XSD para adicionar um novo registro de detalhes do pedido (um ** \<elemento OD>** no bloco ** \<After>** ) para a ordem 43860. O atributo `mapping-schema` é usado para especificar o esquema de mapeamento no diagrama.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync mapping-schema="SampleUpdateSchema.xml" >  
    <updg:before>  
       <Order SalesOrderID="43860" />  
    </updg:before>  
    <updg:after>  
      <Order SalesOrderID="43860" >  
           <OD ProductID="753" UnitPrice="$10.00"  
               Quantity="5" Discount="0.0" />  
      </Order>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>Para testar o diagrama de atualização  
  
1.  Copie o código de esquema acima e cole-o em um arquivo de texto. Salve o arquivo como SampleUpdateSchema.xml.  
  
2.  Copie o modelo de diagrama de atualização acima e cole-o em um arquivo de texto. Salve o arquivo como SampleUpdategram.xml no mesmo diretório em que você salvou SampleUpdateSchema.xml.  
  
     O caminho de diretório especificado para o esquema de mapeamento (SampleUpdateSchema.xml) é relativo ao diretório onde o modelo foi salvo. Também é possível especificar um caminho absoluto, por exemplo:  
  
    ```  
    mapping-schema="C:\SqlXmlTest\SampleUpdateSchema.xml"  
    ```  
  
3.  Crie e use o script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o modelo.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4,0](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Este é o esquema XDR equivalente:  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"  
        xmlns:dt="urn:schemas-microsoft-com:datatypes"  
        xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  
<ElementType name="OD" sql:relation="Sales.SalesOrderDetail" >  
    <AttributeType name="SalesOrderID" />  
    <AttributeType name="ProductID" />  
    <AttributeType name="UnitPrice"  dt:type="fixed.14.4" />  
    <AttributeType name="OrderQty" />  
    <AttributeType name="UnitPriceDiscount" />  
  
    <attribute type="SalesOrderID" />  
    <attribute type="ProductID" />  
    <attribute type="UnitPrice" />  
    <attribute type="OrderQty" />  
    <attribute type="UnitPriceDiscount" />  
</ElementType>  
  
<ElementType name="Order" sql:relation="Sales.SalesOrderHeader" >  
    <AttributeType name="CustomerID" />  
    <AttributeType name="SalesOrderID" />  
    <AttributeType name="OrderDate" />  
  
    <attribute type="CustomerID" />  
    <attribute type="SalesOrderID" />  
    <attribute type="OrderDate" />  
    <element type="OD" >  
             <sql:relationship   
                   key-relation="Sales.SalesOrderHeader"  
                   key="SalesOrderID"  
                   foreign-key="SalesOrderID"  
                   foreign-relation="Sales.SalesOrderDetail" />  
    </element>  
</ElementType>  
</Schema>  
```  
  
### <a name="c-inserting-a-record-by-using-the-parent-child-relationship-and-inverse-annotation-specified-in-the-xsd-schema"></a>C. Inserindo um registro usando a relação pai-filho e a anotação de inverso especificada no esquema XSD  
 Este exemplo ilustra como a lógica de diagrama de atualização usa a relação pai-filho especificada no XSD para processar atualizações e como a anotação `inverse` é usada. Para obter mais informações sobre `inverse` a anotação, consulte [especificando o atributo SQL: inverso em sql: relationship &#40;SQLXML 4,0&#41;](../../sqlxml-annotated-xsd-schemas-using/specifying-the-sql-inverse-attribute-on-sql-relationship-sqlxml-4-0.md).  
  
 Este exemplo pressupõe que as tabelas a seguir estão no banco de dados **tempdb** :  
  
-   
  `Cust (CustomerID, CompanyName)`, onde `CustomerID` é a chave primária  
  
-   
  `Ord (OrderID, CustomerID)`, onde `CustomerID` é uma chave estrangeira que recorre à chave primária `CustomerID` na tabela `Cust`.  
  
 O diagrama de atualização usa o seguinte esquema XSD para inserir registros nas tabelas Cust e Ord:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
       <sql:relationship name="OrdCust" inverse="true"  
                  parent="Ord"  
                  parent-key="CustomerID"  
                  child-key="CustomerID"  
                  child="Cust"/>  
  </xsd:appinfo>  
</xsd:annotation>  
  
<xsd:element name="Order" sql:relation="Ord">  
  <xsd:complexType>  
    <xsd:sequence>  
      <xsd:element ref="Customer" sql:relationship="OrdCust"/>  
    </xsd:sequence>  
    <xsd:attribute name="OrderID"   type="xsd:int"/>  
    <xsd:attribute name="CustomerID" type="xsd:string"/>  
  </xsd:complexType>  
</xsd:element>  
  
<xsd:element name="Customer" sql:relation="Cust">  
  <xsd:complexType>  
     <xsd:attribute name="CustomerID"  type="xsd:string"/>  
    <xsd:attribute name="CompanyName" type="xsd:string"/>  
  </xsd:complexType>  
</xsd:element>  
  
</xsd:schema>  
```  
  
 O esquema XSD neste exemplo tem ** \<** os elementos de>do cliente e de ** \<ordem>** e especifica uma relação pai-filho entre os dois elementos. Ele identifica ** \<a ordem>** como o elemento pai e ** \<o cliente>** como o elemento filho.  
  
 A lógica de processamento do diagrama de atualização usa as informações sobre a relação pai-filho para determinar a ordem na qual os registros são inseridos nas tabelas. Neste exemplo, a lógica updategram primeiro tenta inserir um registro na tabela Ord (porque ** \<a ordem>** é o pai) e, em seguida, tenta inserir um registro na tabela Cust (porque ** \<o cliente>** é o filho). No entanto, devido às informações de chave primária/chave estrangeira contidas no esquema da tabela do banco de dados, esta operação de inserção gera um erro de violação de chave estrangeira no banco de dados e a inserção não é bem sucedida.  
  
 Para instruir a lógica do updategram a reverter a relação pai-filho durante a operação de `inverse` atualização, a anotação é especificada no elemento de ** \<>de relação** . Como resultado, os registros são adicionados primeiro na tabela Cust e, depois, na tabela Ord, e a operação é bem-sucedida.  
  
 O seguinte diagrama de atualização insere um pedido (OrderID=2) na tabela Ord e um cliente (CustomerID='AAAAA') na tabela Cust usando o esquema XSD especificado:  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync mapping-schema="SampleUpdateSchema.xml" >  
    <updg:before/>  
    <updg:after>  
      <Order OrderID="2" CustomerID="AAAAA" >  
        <Customer CustomerID="AAAAA" CompanyName="AAAAA Company" />  
      </Order>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>Para testar o diagrama de atualização  
  
1.  Crie essas tabelas no banco de dados **tempdb** :  
  
    ```  
    USE tempdb  
    CREATE TABLE Cust(CustomerID varchar(5) primary key,   
                      CompanyName varchar(20))  
    GO  
    CREATE TABLE Ord (OrderID int primary key,   
                      CustomerID varchar(5) references Cust(CustomerID))  
    GO  
    ```  
  
2.  Copie o código de esquema acima e cole-o em um arquivo de texto. Salve o arquivo como SampleUpdateSchema.xml.  
  
3.  Copie o modelo de diagrama de atualização acima e cole-o em um arquivo de texto. Salve o arquivo como SampleUpdategram.xml no mesmo diretório em que você salvou SampleUpdateSchema.xml.  
  
     O caminho de diretório especificado para o esquema de mapeamento (SampleUpdateSchema.xml) é relativo ao diretório onde o modelo foi salvo. Também é possível especificar um caminho absoluto, por exemplo:  
  
    ```  
    mapping-schema="C:\SqlXmlTest\SampleUpdateSchema.xml"  
    ```  
  
4.  Crie e use o script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o modelo.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4,0](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Considerações de segurança do updategram &#40;SQLXML 4,0&#41;](../security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
