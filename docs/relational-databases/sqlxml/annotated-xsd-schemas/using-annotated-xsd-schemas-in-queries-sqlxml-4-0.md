---
title: Usando schemas XSD anotados em consultas (SQLXML)
description: Saiba como especificar consultas do XPath contra um esquema XSD anotado no SQLXML 4.0 para recuperar dados do banco de dados.
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- queries [SQLXML]
- inline schemas [SQLXML]
- XPath queries [SQLXML], annotated XSD schemas in queries
- queries [SQLXML], annotated XSD schemas
- retrieving data
- mapping schema [SQLXML], queries
- multiple inline schemas
- annotated XSD schemas, queries
- XSD schemas [SQLXML], queries
- templates [SQLXML], annotated XSD schemas in queries
ms.assetid: 927a30a2-eae8-420d-851d-551c5f884f3c
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e9ecd9d65d0f70f7c25328c15bb886ca52122de2
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388687"
---
# <a name="using-annotated-xsd-schemas-in-queries-sqlxml-40"></a>Usando esquemas XSD anotados em consultas (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Você pode especificar consultas com relação a um esquema anotado para recuperar dados do banco de dados especificando consultas XPath em um modelo com relação ao esquema XSD.  
  
 O elemento ** \<sql:xpath-query>** permite especificar uma consulta XPath contra a exibição XML definida pelo esquema anotado. O esquema anotado contra o qual a consulta XPath deve ser executada é identificado usando o atributo **mapeamento-esquema** do ** \<elemento sql:xpath-query>.**  
  
 Os modelos são documentos XML válidos que contêm uma ou mais consultas. As consultas FOR XML e XPath retornam um fragmento de documento. Os modelos atuam como contêineres dos fragmentos de documento; os modelos oferecem uma maneira de especificar um único elemento de nível superior.  
  
 Os exemplos deste tópico usam modelos para especificar uma consulta XPath com relação a um esquema anotado para recuperar dados do banco de dados.  
  
 Por exemplo, considere este esquema anotado:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Person.Contact" >  
     <xsd:complexType>  
       <xsd:attribute name="ContactID" type="xsd:string" />   
       <xsd:attribute name="FirstName" type="xsd:string" />   
       <xsd:attribute name="LastName"  type="xsd:string" />   
     </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 Para fins de ilustração, este esquema XSD é armazenado em arquivo nomeado Schema2.xml. Você poderá ter uma consulta XPath com relação ao esquema anotado especificado no seguinte arquivo de modelo (Schema2T.xml):  
  
```  
<sql:xpath-query   
     xmlns:sql="urn:schemas-microsoft-com:xmlsql"  
     >  
          Person.Contact[@ContactID="1"]  
</sql:xpath-query>  
```  
  
 Em seguida, você poderá criar e usar o Script de Teste SQLXML 4.0 (Sqlxml4test.vbs) para executar a consulta como parte de um arquivo de modelo. Para obter mais informações, consulte [Schemas XDR anotados &#40;Preteridos em SQLXML 4.0&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md).  
  
## <a name="using-inline-mapping-schemas"></a>Usando esquemas de mapeamento embutidos  
 Um esquema anotado pode ser incluído diretamente em um modelo e, em seguida, uma consulta XPath pode ser especificada no modelo com relação ao esquema embutido. O modelo pode também ser um diagrama de atualização.  
  
 Um modelo pode incluir vários esquemas embutidos. Para usar um esquema inline incluído em um modelo, especifique o atributo **id** com um valor único no elemento ** \<>xsd:schema** e use **#idvalue** para referenciar o esquema inline. O atributo **id** é idêntico no comportamento do **sql:id** ({urn:schemas-microsoft-com:xml-sql}id) usado em schemas XDR.  
  
 Por exemplo, o seguinte modelo especifica dois esquemas anotados embutidos:  
  
```  
<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'>  
<xsd:schema xmlns:xsd='http://www.w3.org/2001/XMLSchema'  
        xmlns:ms='urn:schemas-microsoft-com:mapping-schema'  
        id='InLineSchema1' sql:is-mapping-schema='1'>  
  <xsd:element name='Employees' ms:relation='HumanResources.Employee'>  
    <xsd:complexType>  
      <xsd:attribute name='LoginID'   
                     type='xsd:string'/>  
      <xsd:attribute name='Title'   
                     type='xsd:string'/>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
  
<xsd:schema xmlns:xsd='http://www.w3.org/2001/XMLSchema'  
        xmlns:ms='urn:schemas-microsoft-com:mapping-schema'  
        id='InLineSchema2' sql:is-mapping-schema='1'>  
  <xsd:element name='Contacts' ms:relation='Person.Contact'>  
    <xsd:complexType>  
  
      <xsd:attribute name='ContactID'   
                     type='xsd:string' />  
      <xsd:attribute name='FirstName'   
                     type='xsd:string' />  
      <xsd:attribute name='LastName'   
                     type='xsd:string' />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
  
<sql:xpath-query xmlns:sql='urn:schemas-microsoft-com:xml-sql'   
        mapping-schema='#InLineSchema1'>  
    /Employees[@LoginID='adventure-works\guy1']  
</sql:xpath-query>  
  
<sql:xpath-query xmlns:sql='urn:schemas-microsoft-com:xml-sql'   
        mapping-schema='#InLineSchema2'>  
    /Contacts[@ContactID='1']  
</sql:xpath-query>  
</ROOT>  
```  
  
 O modelo também especifica duas consultas XPath. Cada um ** \<** dos elementos de consulta xpath>identifica exclusivamente o esquema de mapeamento especificando o atributo **mapeamento-esquema.**  
  
 Quando você especifica rumina um esquema inline no modelo, a anotação **sql:is-mapping-schema** também deve ser especificada no elemento ** \<xsd:esquema>.** O **esquema sql:is-mapping** leva um valor booleano (0=falso, 1=verdadeiro). Um esquema inline com **sql:is-mapping-schema="1"** é tratado como esquema anotado inline e não é devolvido no documento XML.  
  
 A anotação **sql:is-mapping-schema** pertence ao modelo namespace **urn:schemas-microsoft-com:xml-sql**.  
  
 Para testar este exemplo, salve o modelo (InlineSchemaTemplate.xml) em um diretório local e, em seguida, crie e use o Script de Teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o modelo. Para obter mais informações, consulte [Usando OA para executar consultas SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Além de especificar o atributo **mapeamento-esquema** no elemento ** \<sql:xpath-query>** em um modelo (quando há uma consulta XPath) ou em ** \<updg:sync>** elemento em um updategram, você pode fazer o seguinte:  
  
-   Especifique o atributo **mapeamento-esquema** no elemento ** \<>ROOT** (declaração global) no modelo. Esse esquema de mapeamento torna-se, então, o esquema padrão que será usado por todos os nós xpath e updategram que não têm nenhuma anotação explícita **de esquema de mapeamento.**  
  
-   Especifique o atributo **do esquema de mapeamento** usando o objeto **Comando** ADO.  
  
 O atributo **mapeamento-esquema** especificado no ** \<>de consulta xpath** ou ** \<updg:sync>** elemento tem a maior precedência; o **objeto** Comando ADO tem a menor precedência.  
  
 Observe que se você especificar uma consulta XPath em um modelo e não especificar um esquema de mapeamento com o qual a consulta XPath é executada, a consulta XPath será tratada como uma consulta de tipo **dbobject.** Por exemplo, considere este modelo:  
  
```  
<sql:xpath-query   
     xmlns:sql="urn:schemas-microsoft-com:xmlsql">  
          Production.ProductPhoto[@ProductPhotoID='100']/@LargePhoto  
</sql:xpath-query>  
```  
  
 O modelo especifica uma consulta Xpath, mas não especifica um esquema de mapeamento. Portanto, essa consulta é tratada como uma consulta do tipo **dbobject** na @ProductPhotoIDqual Production.ProductPhoto é o nome da tabela e ='100' é um predicado que encontra uma foto do produto com o valor de ID de 100. @LargePhotoé a coluna a partir da qual recuperar o valor.  
  
  
