---
title: Usando esquemas XSD em consultas (SQLXML 4.0) anotados | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6cd63b4426bdc1b4adf9020b5cf4bd3e50622528
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2018
---
# <a name="using-annotated-xsd-schemas-in-queries-sqlxml-40"></a>Usando esquemas XSD anotados em consultas (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Você pode especificar consultas com relação a um esquema anotado para recuperar dados do banco de dados especificando consultas XPath em um modelo com relação ao esquema XSD.  
  
 O  **\<sql:xpath-consulta >** elemento permite que você especifique uma consulta XPath contra a exibição XML definida pelo esquema anotado. O esquema anotado com a qual a consulta XPath será executada é identificado usando o **esquema de mapeamento** atributo o  **\<sql:xpath-consulta >** elemento.  
  
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
  
 Em seguida, você poderá criar e usar o Script de Teste SQLXML 4.0 (Sqlxml4test.vbs) para executar a consulta como parte de um arquivo de modelo. Para obter mais informações, consulte [os esquemas XDR anotados &#40; preteridos no SQLXML 4.0 &#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md).  
  
## <a name="using-inline-mapping-schemas"></a>Usando esquemas de mapeamento embutidos  
 Um esquema anotado pode ser incluído diretamente em um modelo e, em seguida, uma consulta XPath pode ser especificada no modelo com relação ao esquema embutido. O modelo pode também ser um diagrama de atualização.  
  
 Um modelo pode incluir vários esquemas embutidos. Para usar um esquema embutido que é incluído em um modelo, especifique o **id** atributo com um valor exclusivo no  **\<xsd: schema >** elemento e use **#idvalue**para referenciar o esquema embutido. O **id** atributo é idêntico em comportamento para o **SQL: ID** ({urn: schemas-microsoft-com: XML-sql} id) usado em esquemas XDR.  
  
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
  
 O modelo também especifica duas consultas XPath. Cada uma da  **\<consulta xpath >** elementos identifica exclusivamente o esquema de mapeamento especificando o **esquema de mapeamento** atributo.  
  
 Quando você especificar um esquema embutido no modelo, o **sql: esquema é de mapeamento** anotação também deverá ser especificada no  **\<xsd: schema >** elemento. O **sql: esquema é de mapeamento** tem um valor booleano (0 = false, 1 = true). Um esquema embutido com **sql: for-mapping-schema = "1"** é tratado como esquema anotado embutido e não é retornado no documento XML.  
  
 O **sql: esquema é de mapeamento** anotação pertence ao namespace de modelo **urn: schemas-microsoft-com: XML-sql**.  
  
 Para testar este exemplo, salve o modelo (InlineSchemaTemplate.xml) em um diretório local e, em seguida, crie e use o Script de Teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o modelo. Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Além de especificar o **esquema de mapeamento** atributo no  **\<sql:xpath-consulta >** elemento em um modelo (quando há uma consulta XPath) ou em  **\< updg:Sync >** elemento em um diagrama de atualização, você pode fazer o seguinte:  
  
-   Especifique o **esquema de mapeamento** atributo no  **\<raiz >** elemento (declaração global) no modelo. Este esquema de mapeamento torna-se o esquema padrão que será usado por todos os nós de XPath e diagrama de atualização que têm explícita não **esquema de mapeamento** anotação.  
  
-   Especifique o **esquema de mapeamento** atributo usando o ADO **comando** objeto.  
  
 O **esquema de mapeamento** que é especificado no atributo de  **\<consulta xpath >** ou  **\<updg:sync >** elemento tem o mais alto precedência; o ADO **comando** objeto tem a precedência mais baixa.  
  
 Observe que, se você especifica uma consulta XPath em um modelo e não especificar um esquema de mapeamento no qual a consulta XPath é executada, a consulta XPath é tratada como um **dbobject** consulta do tipo. Por exemplo, considere este modelo:  
  
```  
<sql:xpath-query   
     xmlns:sql="urn:schemas-microsoft-com:xmlsql">  
          Production.ProductPhoto[@ProductPhotoID='100']/@LargePhoto  
</sql:xpath-query>  
```  
  
 O modelo especifica uma consulta Xpath, mas não especifica um esquema de mapeamento. Portanto, essa consulta é tratada uma **dbobject** Production. ProductPhoto é o nome da tabela de consulta do tipo e @ProductPhotoID= '100' é um predicado que localiza uma foto do produto com o valor da ID de 100. @LargePhoto é a coluna da qual recuperar o valor.  
  
  
