---
title: Especificando um destino Namespace usando o atributo targetNamespace (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
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
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a52ce206eee69fa585a72788e46f8f7174d936a8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65980822"
---
# <a name="specifying-a-target-namespace-using-the-targetnamespace-attribute-sqlxml-40"></a>Especificando um namespace de destino usando o atributo targetNamespace (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Ao escrever esquemas XSD, você pode usar o XSD **targetNamespace** atributo para especificar um namespace de destino. Este tópico descreve como XSD **targetNamespace**, **elementFormDefault**, e **attributeFormDefault** atributos funcionam, como eles afetam a instância XML que é gerado, e como são especificadas consultas XPath com namespaces.  
  
 Você pode usar o **xsd: targetNamespace** atributo para colocar elementos e atributos do namespace padrão em um namespace diferente. Você também pode especificar se os elementos e atributos do esquema declarados localmente devem aparecer qualificados por um namespace, seja explicitamente, usando um prefixo, ou implicitamente, por padrão. Você pode usar o **elementFormDefault** e **attributeFormDefault** atributos no  **\<XSD >** elemento para especificar globalmente a qualificação de atributos e elementos locais ou você pode usar o **formulário** atributo para especificar atributos e elementos individuais separadamente.  
  
## <a name="examples"></a>Exemplos  
 Para criar exemplos de funcionamento usando os exemplos a seguir, é necessário atender a determinados requisitos. Para obter mais informações, consulte [requisitos para executar exemplos do SQLXML](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-a-target-namespace"></a>A. Especificando um namespace de destino  
 O seguinte esquema XSD Especifica um namespace de destino usando o **xsd: targetNamespace** atributo. O esquema também define o **elementFormDefault** e **attributeFormDefault** valores de atributo **"unqualified"** (o valor padrão para esses atributos). Essa é uma declaração global e afeta todos os elementos locais ( **\<ordem >** no esquema) e atributos (**CustomerID**, **ContactName**e  **OrderID** no esquema).  
  
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
  
-   O **CustomerType** e **OrderType** declarações de tipo são globais e, portanto, são incluídas no namespace de destino do esquema. Como resultado, quando esses tipos são referenciados na declaração de  **\<cliente >** elemento e seu  **\<Order >** elemento filho, um prefixo é especificado, que está associado o namespace de destino.  
  
-   O  **\<cliente >** elemento também está incluído no namespace de destino do esquema porque ele é um elemento global no esquema.  
  
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
  
 Este documento de instância define o namespace ' urn: MyNamespace e associa um prefixo (y0) a ele. O prefixo é aplicado apenas à  **\<cliente >** elemento global. (O elemento é global porque é declarado como um filho do  **\<XSD >** elemento no esquema.)  
  
 O prefixo não é aplicado aos elementos locais e atributos porque o valor de **elementFormDefault** e **attributeFormDefault** atributos é definida como **"unqualified"** no esquema. Observe que o  **\<ordem >** elemento é local, porque sua declaração aparece como um filho do  **\<complexType >** elemento que define o  **\< CustomerType >** elemento. Da mesma forma, os atributos (**CustomerID**, **OrderID**, e **ContactName**) são locais, e não globais.  
  
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
  
     A consulta XPath no modelo retorna o  **\<cliente >** elemento para o cliente com uma CustomerID igual a 1. Observe que a consulta XPath especifica o prefixo de namespace para o elemento na consulta e não para o atributo. (Não são qualificados atributos locais, como especificado no esquema.)  
  
     O caminho de diretório especificado para o esquema de mapeamento (targetNamespace.xml) é relativo ao diretório onde o modelo está salvo. Também é possível especificar um caminho absoluto, por exemplo:  
  
    ```  
    mapping-schema="C:\MyDir\targetNamepsace.xml"  
    ```  
  
3.  Crie e use o script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o modelo.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas SQLXML](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Se o esquema especifica **elementFormDefault** e **attributeFormDefault** atributos com o valor **"qualificado"** , o documento de instância terá todos os locais elementos e atributos qualificados. Você pode alterar o esquema anterior para incluir esses atributos na  **\<XSD >** elemento e executar o modelo novamente. Como os atributos agora são qualificados também na instância, a consulta XPath será alterada para incluir o prefixo de namespace.  
  
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
  
  
