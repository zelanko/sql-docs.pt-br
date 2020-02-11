---
title: 'Criando seções CDATA usando SQL: use-cdata (SQLXML)'
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- markup characters [SQLXML]
- special characters [SQLXML]
- use-cdata annotation
- plain text [SQLXML]
- CDATA sections
- escaping blocks of text [SQLXML]
- annotated XSD schemas, CDATA sections
- sql:use-cdata
ms.assetid: 26d2b9dc-f857-44ff-bcd4-aaf64ff809d0
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 289e0e7ecb720afc4440283a97bcb7d55ccee8b8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75257492"
---
# <a name="creating-cdata-sections-using-sqluse-cdata-sqlxml-40"></a>Criando seções CDATA usando sql:use-cdata (SQLXML 4.0)

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Em XML, as seções CDATA são usadas para sair de blocos de texto que contenham caracteres que seriam reconhecidos como caracteres de marcação.  
  
 Um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no Microsoft às vezes pode conter caracteres que são tratados como caracteres de marcação pelo analisador XML; por exemplo, colchetes angulares (< e >), o símbolo de menor que ou-igual a (<=) e o e comercial (&) são tratados como caracteres de marcação. No entanto, é possível quebrar esse tipo de caracteres especiais em uma seção CDATA para impedi-los de serem tratados como caracteres de marcação. O texto na seção CDATA é tratado pelo analisador XML como texto sem-formatação.  
  
 A anotação **SQL: use-cdata** é usada para especificar que os dados retornados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devem ser encapsulados em uma seção CDATA (ou seja, indica se o valor de uma coluna especificada pelo **campo SQL:** deve ser incluído em uma seção CDATA). A anotação **SQL: use-cdata** pode ser especificada somente em elementos que são mapeados para uma coluna de banco de dados.  
  
 A anotação **SQL: use-cdata** usa um valor booliano (0 = false, 1 = true). Os valores aceitáveis são 0, 1, true e false.  
  
 Esta anotação não pode ser usada com **SQL: url-encode** ou nos tipos de atributo ID, IDREF, IDREFS, NMTOKEN e NMTOKENS.  
  
## <a name="examples"></a>Exemplos  
 Para criar exemplos de funcionamento usando os exemplos a seguir, é necessário atender a determinados requisitos. Para obter mais informações, consulte [Requirements for running SQLXML examples](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-sqluse-cdata-on-an-element"></a>a. Especificando sql:use-cdata em um elemento  
 No esquema a seguir, **SQL: use-cdata** é definido como 1 (true) para o ** \<>AddressLine1** no elemento ** \<address>** . Como resultado, os dados são retornados em uma seção CDATA.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Address"   
               sql:relation="Person.Address"   
               sql:key-fields="AddressID" >  
   <xsd:complexType>  
        <xsd:sequence>  
          <xsd:element name="AddressID"  type="xsd:string" />  
          <xsd:element name="AddressLine1" type="xsd:string"   
                       sql:use-cdata="1" />  
        </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Para testar uma consulta XPath de exemplo com relação ao esquema  
  
1.  Copie o código de esquema acima e cole-o em um arquivo de texto. Salve o arquivo como UseCData.xml.  
  
2.  Copie o modelo a seguir e cole-o em um arquivo de texto. Salve o arquivo como UseCDataT.xml no mesmo diretório em que você salvou UseCData.xml.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="UseCData.xml">  
            /Address[AddressID < 11]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     O caminho de diretório especificado para o esquema de mapeamento (UseCData.xml) é relativo ao diretório onde o modelo está salvo. Também é possível especificar um caminho absoluto, por exemplo:  
  
    ```  
    mapping-schema="C:\SqlXmlTest\UseCData.xml"  
    ```  
  
3.  Crie e use o script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o modelo.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4,0](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Este é o conjunto de resultados parcial:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
  <Address>   
    <AddressID>1</CustomerID>   
    <AddressLine1>   
      <![CDATA[ 1970 Napa Ct.  ]]>   
    </AddressLine1>   
  </Address>  
  <Address>  
    <AddressLine1>   
      <![CDATA[ 9833 Mt. Dias Blv. ]]>   
    </AddressLine1>   
  </Address>  
  ...  
</ROOT>  
```  
  
  
