---
title: Especifique um namespace de destino com targetNamespace (SQLXML)
description: Saiba como especificar um namespace de destino em um esquema XSD usando o atributo targetNamespace no SQLXML 4,0.
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- namespaces [SQLXML], annotated XSD schemas
- targetNamespace attribute
- XSD schemas [SQLXML], target namespaces
- annotated XSD schemas, target namespaces
- xsd:targetNamespace
- attributeFormDefault attribute
- elementFormDefault attribute
- target namespaces [SQLXML]
ms.assetid: f3df9877-6672-4444-8245-2670063c9310
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: bfa6234aae5e2744a88c4fcfb158575cb07000f5
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85764896"
---
# <a name="specifying-a-target-namespace-using-the-targetnamespace-attribute-sqlxml-40"></a>Especificando um namespace de destino usando o atributo targetNamespace (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Ao escrever esquemas XSD, você pode usar o atributo de XSD **targetNamespace** para especificar um namespace de destino. Este tópico descreve como os atributos de **targetNamespace**, **elementFormDefault**e **attributeFormDefault** do xsd funcionam, como eles afetam a instância XML gerada e como as consultas XPath são especificadas com namespaces.  
  
 Você pode usar o atributo **xsd: targetNamespace** para posicionar elementos e atributos do namespace padrão em um namespace diferente. Você também pode especificar se os elementos e atributos do esquema declarados localmente devem aparecer qualificados por um namespace, seja explicitamente, usando um prefixo, ou implicitamente, por padrão. Você pode usar os atributos **elementFormDefault** e **attributeFormDefault** no **\<xsd:schema>** elemento para especificar globalmente a qualificação de elementos e atributos locais, ou pode usar o atributo **Form** para especificar elementos e atributos individuais separadamente.  
  
## <a name="examples"></a>Exemplos  
 Para criar exemplos de funcionamento usando os exemplos a seguir, é necessário atender a determinados requisitos. Para obter mais informações, consulte [Requirements for running SQLXML examples](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-a-target-namespace"></a>a. Especificando um namespace de destino  
 O esquema XSD a seguir especifica um namespace de destino usando o atributo **xsd: targetNamespace** . O esquema também define os valores de atributo **elementFormDefault** e **attributeFormDefault** como **"unqualified"** (o valor padrão para esses atributos). Essa é uma declaração global e afeta todos os elementos locais ( **\<Order>** no esquema) e atributos (**CustomerID**, **ContactName**e **OrderID** no esquema).  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema"  
            xmlns:CO="urn:MyNamespace"   
            targetNamespace="urn:MyNamespace" >  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustOrders"  
          parent="Sales.Customer"  
          parent-key="CustomerID"  
          child="Sales.SalesOrderHeader"  
          child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customer"   
               sql:relation="Sales.Customer"   
               type="CO:CustomerType" />  
  
  <xsd:complexType name="CustomerType" >  
     <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Sales.SalesOrderHeader"  
                     sql:relationship="CustOrders"  
                     type="CO:OrderType" />  
     </xsd:sequence>  
        <xsd:attribute name="CustomerID"   type="xsd:string" />   
        <xsd:attribute name="SalesPersonID"  type="xsd:string" />  
  </xsd:complexType>  
  <xsd:complexType name="OrderType" >  
     <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
     <xsd:attribute name="CustomerID" type="xsd:string" />  
  </xsd:complexType>  
</xsd:schema>  
```  
  
 No esquema:  
  
-   As declarações de tipo **CustomerType** e **ordertype** são globais e, portanto, são incluídas no namespace de destino do esquema. Como resultado, quando esses tipos são referenciados na declaração do **\<Customer>** elemento e seu **\<Order>** elemento filho, é especificado um prefixo associado ao namespace de destino.  
  
-   O **\<Customer>** elemento também é incluído no namespace de destino do esquema porque ele é um elemento global no esquema.  
  
 Execute a consulta XPath a seguir no esquema:  
  
```  
(/CO:Customer[@CustomerID=1)   
```  
  
 A consulta de XPath gera este documento da instância (somente alguns pedidos são mostrados):  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <y0:Customer xmlns:y0="urn:MyNamespace"   
      CustomerID="ALFKI" ContactName="Maria Anders">  
        <Order CustomerID="ALFKI" OrderID="10643" />   
        <Order CustomerID="ALFKI" OrderID="10692" />   
        ...  
  </y0:Customer>  
  </ROOT>  
```  
  
 Este documento de instância define o namespace urn: MyNamespace e associa um prefixo (y0) a ele. O prefixo é aplicado somente ao **\<Customer>** elemento global. (O elemento é global porque está declarado como um filho do **\<xsd:schema>** elemento no esquema.)  
  
 O prefixo não é aplicado aos elementos e atributos locais porque o valor dos atributos **elementFormDefault** e **attributeFormDefault** está definido como **"unqualified"** no esquema. Observe que o **\<Order>** elemento é local porque sua declaração aparece como um filho do **\<complexType>** elemento que define o **\<CustomerType>** elemento. Da mesma forma, os atributos (**CustomerID**, **OrderID**e **ContactName**) são locais, e não globais.  
  
##### <a name="to-create-a-working-sample-of-this-schema"></a>Para criar um exemplo de funcionamento deste esquema  
  
1.  Copie o código de esquema acima e cole-o em um arquivo de texto. Salve o arquivo como target.NameSpace.xml.  
  
2.  Copie o modelo a seguir e cole-o em um arquivo de texto. Salve o arquivo como target.NameSpaceT.xml no mesmo diretório em que você salvou targetNamespace.xml.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="targetNamespace.xml"  
                       xmlns:CO="urn:MyNamespace" >  
        /CO:Customer[@CustomerID=1]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     A consulta XPath no modelo retorna o **\<Customer>** elemento para o cliente com um CustomerID de 1. Observe que a consulta XPath especifica o prefixo de namespace para o elemento na consulta e não para o atributo. (Não são qualificados atributos locais, como especificado no esquema.)  
  
     O caminho de diretório especificado para o esquema de mapeamento (targetNamespace.xml) é relativo ao diretório onde o modelo está salvo. Também é possível especificar um caminho absoluto, por exemplo:  
  
    ```  
    mapping-schema="C:\MyDir\targetNamepsace.xml"  
    ```  
  
3.  Crie e use o script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o modelo.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Se o esquema especificar os atributos **elementFormDefault** e **attributeFormDefault** com o valor **"qualified"**, o documento de instância terá todos os elementos e atributos locais qualificados. Você pode alterar o esquema anterior para incluir esses atributos no **\<xsd:schema>** elemento e executar o modelo novamente. Como os atributos agora são qualificados também na instância, a consulta XPath será alterada para incluir o prefixo de namespace.  
  
 Esta é a consulta XPath revisada:  
  
```  
/CO:Customer[@CO:CustomerID=1]  
```  
  
 Este é o documento XML retornado:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
   <y0:Customer xmlns:y0="urn:MyNamespace" CustomerID="1" SalesPersonID="280">  
      <Order SalesOrderID="43860" CustomerID="1" />   
      <Order SalesOrderID="44501" CustomerID="1" />   
      <Order SalesOrderID="45283" CustomerID="1" />   
      <Order SalesOrderID="46042" CustomerID="1" />   
   </y0:Customer>  
</ROOT>  
```  
  
  
