---
title: Criando seções CDATA usando sql:use-cdata (SQLXML)
description: Aprenda a criar seções CDATA no SQLXML 4.0 usando a anotação sql:use-cdata para escapar de blocos de texto que contenham caracteres de marcação.
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
ms.openlocfilehash: aa359c1c1e855c3652d7c6486d3993f588bae46d
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388197"
---
# <a name="creating-cdata-sections-using-sqluse-cdata-sqlxml-40"></a>Criando seções CDATA usando sql:use-cdata (SQLXML 4.0)

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Em XML, as seções CDATA são usadas para sair de blocos de texto que contenham caracteres que seriam reconhecidos como caracteres de marcação.  
  
 Um banco [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de dados na Microsoft às vezes pode conter caracteres que são tratados como caracteres de marcação pelo analisador XML; por exemplo, os suportes angulares (< e >), o símbolo menor ou igual a (<=) e o ampersand (&) são tratados como caracteres de marcação. No entanto, é possível quebrar esse tipo de caracteres especiais em uma seção CDATA para impedi-los de serem tratados como caracteres de marcação. O texto na seção CDATA é tratado pelo analisador XML como texto sem-formatação.  
  
 A anotação **sql:use-cdata** é usada para especificar que os dados retornados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devem ser embrulhados em uma seção CDATA (ou seja, indica se o valor de uma coluna especificada por **sql:field** deve ser incluído em uma seção CDATA). A anotação **sql:use-cdata** só pode ser especificada em elementos que mapeiam para uma coluna de banco de dados.  
  
 A anotação **sql:use-cdata** leva um valor booleano (0 = falso, 1 = verdadeiro). Os valores aceitáveis são 0, 1, true e false.  
  
 Esta anotação não pode ser usada com os tipos **de atributos SqL:url-encode** ou no ID, IDREFS, NMTOKEN e NMTOKENS.  
  
## <a name="examples"></a>Exemplos  
 Para criar exemplos de funcionamento usando os exemplos a seguir, é necessário atender a determinados requisitos. Para obter mais informações, consulte [Requisitos para executar exemplos de SQLXML](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-sqluse-cdata-on-an-element"></a>a. Especificando sql:use-cdata em um elemento  
 No esquema a seguir, **sql:use-cdata** é definido como 1 (True) para o ** \<AddressLine1>** dentro do ** \<** elemento Endereço>. Como resultado, os dados são retornados em uma seção CDATA.  
  
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
  
     Para obter mais informações, consulte [Usando OA para executar consultas SQLXML 4.0](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
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
  
  
