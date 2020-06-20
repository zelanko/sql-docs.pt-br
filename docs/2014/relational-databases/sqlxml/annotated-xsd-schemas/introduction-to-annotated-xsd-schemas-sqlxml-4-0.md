---
title: Introdução aos esquemas XSD anotados (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- namespaces [SQLXML], annotated XSD schemas
- mapping schema [SQLXML], about mapping schema
- views [SQLXML]
- valid XSD schemas [SQLXML]
- annotations [SQLXML]
- XSD schemas [SQLXML], creating XML views
- annotated XSD schemas, creating XML views
- minimum XSD schema
- annotated XSD schemas, examples
- XML views [SQLXML]
ms.assetid: 15282db1-65c4-43be-bdb7-e9ef49cb33a2
author: rothja
ms.author: jroth
ms.openlocfilehash: d3f3764a8f41d0d6ce8d59cc5aa727676d9282e9
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85043050"
---
# <a name="introduction-to-annotated-xsd-schemas-sqlxml-40"></a>Introdução a esquemas XSD anotados (SQLXML 4.0)
  É possível criar exibições XML de dados relacionais usando a linguagem XSD. Dessa forma, essas exibições podem ser consultadas por meio de consultas em linguagem XPath. Isso é semelhante à criação de exibições usando instruções CREATE VIEW e especificando consultas SQL com base na exibição.  
  
 Um esquema XML descreve a estrutura de um documento XML, além das várias restrições referentes aos dados do documento. Quando você especifica as consultas XPath com base no esquema, a estrutura do documento XML retornado é determinada pelo esquema que serve de base para a consulta XPath executada.  
  
 Em um esquema XSD, o **\<xsd:schema>** elemento inclui todo o esquema; todas as declarações de elemento devem estar contidas dentro **\<xsd:schema>** do elemento. Você pode descrever atributos que definem o namespace no qual reside o esquema e os namespaces que são usados no esquema como propriedades do **\<xsd:schema>** elemento.  
  
 Um esquema XSD válido deve conter o **\<xsd:schema>** elemento definido da seguinte maneira:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<!-- additional schema definitions here -->  
</xsd:schema>  
```  
  
 O **\<xsd:schema>** elemento é derivado da especificação de namespace de esquema XML em http://www.w3.org/2001/XMLSchema .  
  
## <a name="annotations-to-the-xsd-schema"></a>Anotações para o esquema XSD  
 É possível usar um esquema XSD com anotações que descrevam o mapeamento para um banco de dados, consultem o banco de dados e retornem os resultados na forma de um documento XML. São fornecidas anotações para mapear um esquema XSD para tabelas e colunas de banco de dados. As consultas XPath podem ser especificadas com base na exibição XML criada pelo esquema XSD para consultar o banco de dados e obter os resultados como um XML.  
  
> [!NOTE]  
>  No [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0, a linguagem XSD oferece suporte a anotações introduzidas com a linguagem XDR no [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)]. A XDR anotada está preterida no SQLXML 4.0.  
  
 No contexto do banco de dados relacional, é útil mapear o esquema XSD arbitrário para um armazenamento relacional. Uma maneira de fazer isso é anotar o esquema XSD. Um esquema XSD com as anotações é conhecido como um esquema de *mapeamento*, que fornece informações sobre como os dados XML serão mapeados para a Relational Store. Um esquema de mapeamento é, com efeito, uma exibição XML dos dados relacionais. Esses mapeamentos podem ser usados para recuperar dados relacionais como um documento XML.  
  
## <a name="namespace-for-annotations"></a>Namespace para anotações  
 Em um esquema XSD, as anotações são especificadas usando o namespace **urn: schemas-microsoft-com: Mapping-Schema**. Conforme mostrado no exemplo a seguir, a maneira mais fácil de especificar o namespace é especificá-lo na **\<xsd:schema>** marca.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
...  
</xsd:schema>  
```  
  
 O prefixo de namespace usado é arbitrário. Nesta documentação, o prefixo **SQL** é usado para denotar o namespace Annotation e distinguir as anotações nesse namespace deles em outros namespaces.  
  
## <a name="example-of-an-annotated-xsd-schema"></a>Exemplo de um esquema XSD anotado  
 No exemplo a seguir, o esquema XSD consiste em um **\<Person.Contact>** elemento. O **\<Employee>** elemento tem um atributo **ContactID** e **\<FirstName>** os **\<LastName>** elementos filho:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
  <xsd:element name="Contact" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="FName"    
                     type="xsd:string" />   
        <xsd:element name="LName"  
                     type="xsd:string" />  
     </xsd:sequence>  
        <xsd:attribute name="ConID" type="xsd:integer" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 As anotações são adicionadas ao esquema XSD para mapear seus elementos e atributos para as tabelas e colunas do banco de dados:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Contact" sql:relation="Person.Contact" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="FName"  
                     sql:field="FirstName"   
                     type="xsd:string" />   
        <xsd:element name="LName"    
                     sql:field="LastName"    
                     type="xsd:string" />  
     </xsd:sequence>  
        <xsd:attribute name="ConID"   
                       sql:field="ContactID"   
                       type="xsd:integer" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 No esquema de mapeamento, o **\<Contact>** elemento é mapeado para a tabela Person. Contact no banco de dados AdventureWorks de exemplo usando a `sql:relation` anotação. Os atributos ConID, FName e LName são mapeados para as colunas ContactID, FirstName e LastName na tabela Person.Contact usando as anotações `sql:field`.  
  
 Esse esquema XSD anotado fornece a exibição XML dos dados relacionais. Essa exibição XML pode ser consultada usando a linguagem XPath. Uma consulta XPath retorna um documento XML como resultado, e não o conjunto de linhas retornado pelas consultas SQL.  
  
> [!NOTE]  
>  No esquema de mapeamento, a diferenciação de maiúsculas e minúsculas nos valores relacionais especificados (como, por exemplo, o nome da tabela e o nome da coluna) depende do uso das configurações de ordenação de maiúsculas e minúsculas pelo SQL Server. Para obter mais informações, consulte [Suporte a ordenações e a Unicode](../../collations/collation-and-unicode-support.md).  
  
## <a name="other-resources"></a>Outros recursos  
 Você pode encontrar mais informações sobre as linguagens XSD (XML Schema Definition), XPath (XML Path) e XSLT (Linguagem XSL Transformations) nos seguintes sites:  
  
-   Esquema XML parte 0: Primer, recomendação do W3C (http://www.w3.org/TR/xmlschema-0/)  
  
-   Esquema XML parte 1: estruturas, recomendação do W3C (http://www.w3.org/TR/xmlschema-1/)  
  
-   Esquema XML parte 2: tipos de texto, recomendação do W3C (http://www.w3.org/TR/xmlschema-2/)  
  
-   Linguagem de caminho XML (XPath) (http://www.w3.org/TR/xpath)  
  
-   Transformações XSL (XSLT) (http://www.w3.org/TR/xslt)  
  
## <a name="see-also"></a>Consulte Também  
 [Considerações de segurança de esquema anotadas &#40;SQLXML 4,0&#41;](../../sqlxml-annotated-xsd-schemas-xpath-queries/security/annotated-schema-security-considerations-sqlxml-4-0.md)   
 [Esquemas XDR anotados &#40;preteridos no SQLXML 4,0&#41;](annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)  
  
  
