---
title: 'Criando seções CDATA usando SQL: use-cdata (SQLXML 4,0) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
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
author: rothja
ms.author: jroth
ms.openlocfilehash: a5d0283837d9344eaf529cf9818e6629cdc68065
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85060166"
---
# <a name="creating-cdata-sections-using-sqluse-cdata-sqlxml-40"></a>Criando seções CDATA usando sql:use-cdata (SQLXML 4.0)
  Em XML, as seções CDATA são usadas para sair de blocos de texto que contenham caracteres que seriam reconhecidos como caracteres de marcação.  
  
 Um banco de dados no Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] às vezes pode conter caracteres que são tratados como caracteres de marcação pelo analisador XML; por exemplo, colchetes angulares ( \< and > ), o símbolo de menor que ou-igual a (<=) e o e comercial (&) são tratados como caracteres de marcação. No entanto, é possível quebrar esse tipo de caracteres especiais em uma seção CDATA para impedi-los de serem tratados como caracteres de marcação. O texto na seção CDATA é tratado pelo analisador XML como texto sem-formatação.  
  
 A anotação `sql:use-cdata` é usada para especificar se os dados retornados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devem ser colocados em uma seção CDATA (ou seja, ela indica se o valor de uma coluna especificada por `sql:field` deve estar em uma seção CDATA). A anotação `sql:use-cdata` só pode ser especificada em elementos que mapeiam para uma coluna de banco de dados.  
  
 A anotação `sql:use-cdata` usa um valor Booliano (0 = false, 1 = true). Os valores aceitáveis são 0, 1, true e false.  
  
 Essa anotação não pode ser usada com `sql:url-encode` ou nos tipos de atributo ID, IDREF, IDREFS, NMTOKEN e NMTOKENS.  
  
## <a name="examples"></a>Exemplos  
 Para criar exemplos de funcionamento usando os exemplos a seguir, é necessário atender a determinados requisitos. Para obter mais informações, consulte [Requirements for running SQLXML examples](../sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-sqluse-cdata-on-an-element"></a>a. Especificando sql:use-cdata em um elemento  
 No esquema a seguir, `sql:use-cdata` é definido como 1 (true) para o **\<AddressLine1>** dentro do **\<Address>** elemento. Como resultado, os dados são retornados em uma seção CDATA.  
  
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
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4,0](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
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
  
  
