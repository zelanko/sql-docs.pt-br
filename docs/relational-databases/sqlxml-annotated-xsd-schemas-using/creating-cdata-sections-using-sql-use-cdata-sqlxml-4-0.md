---
title: "Criando seções CDATA usando SQL: Use-cdata (SQLXML 4.0) | Microsoft Docs"
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
- markup characters [SQLXML]
- special characters [SQLXML]
- use-cdata annotation
- plain text [SQLXML]
- CDATA sections
- escaping blocks of text [SQLXML]
- annotated XSD schemas, CDATA sections
- sql:use-cdata
ms.assetid: 26d2b9dc-f857-44ff-bcd4-aaf64ff809d0
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 318c4d5dd0aba1b4195cebcd7c1815c4273b2077
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2018
---
# <a name="creating-cdata-sections-using-sqluse-cdata-sqlxml-40"></a>Criando seções CDATA usando sql:use-cdata (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Em XML, as seções CDATA são usadas para sair de blocos de texto que contenham caracteres que seriam reconhecidos como caracteres de marcação.  
  
 Às vezes, um banco de dados do Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode conter caracteres tratados como caracteres de marcação pelo analisador XML; por exemplo, colchetes angulares (< e >), o símbolo menor que ou igual a (<=) e o "e" comercial (&) são tratados como caracteres de marcação. No entanto, é possível quebrar esse tipo de caracteres especiais em uma seção CDATA para impedi-los de serem tratados como caracteres de marcação. O texto na seção CDATA é tratado pelo analisador XML como texto sem-formatação.  
  
 O **SQL: Use-cdata** anotação é usada para especificar que os dados retornados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devem ser envolvidos em uma seção CDATA (ou seja, ele indica se o valor de uma coluna que é especificado pelo **SQL: Field** deve ser incluído em uma seção CDATA). O **SQL: Use-cdata** anotação pode ser especificada somente em elementos que são mapeados para uma coluna de banco de dados.  
  
 O **SQL: Use-cdata** anotação usa um valor booliano (0 = false, 1 = true). Os valores aceitáveis são 0, 1, true e false.  
  
 Esta anotação não pode ser usada com **SQL: url-encode** ou a ID, IDREF, IDREFS, NMTOKEN e NMTOKENS tipos de atributo.  
  
## <a name="examples"></a>Exemplos  
 Para criar exemplos de funcionamento usando os exemplos a seguir, é necessário atender a determinados requisitos. Para obter mais informações, consulte [requisitos para executar exemplos do SQLXML](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-sqluse-cdata-on-an-element"></a>A. Especificando sql:use-cdata em um elemento  
 No esquema a seguir, **SQL: Use-cdata** está definida como 1 (verdadeiro) para o  **\<AddressLine1 >** dentro de  **\<endereço >** elemento. Como resultado, os dados são retornados em uma seção CDATA.  
  
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
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4.0](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
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
  
  
