---
title: 'Solicitando referências URL a dados BLOB usando sql: encode (SQLXML 4.0) | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- sql:encode
- encode annotation
- URL references to BLOB data [SQLXML]
- references to BLOB data [SQLXML]
- annotated XSD schemas, URL references to BLOB data
- requesting URL references to BLOB data
- BLOBs, URL references
- Base 64-encoded format
ms.assetid: 2f8cd93b-c636-462b-8291-167197233ee0
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a5b5ccbda52e9a01c75d0fe653a6a78dec4afd2e
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43083046"
---
# <a name="requesting-url-references-to-blob-data-using-sqlencode-sqlxml-40"></a>Solicitando referências URL a dados BLOB usando sql:encode (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Em um esquema XSD anotado, quando um atributo (ou elemento) é mapeado para uma coluna BLOB no Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], os dados são retornados no formato codificado na base 64 no XML.  
  
 Se você quiser que uma referência aos dados (um URI) a ser retornado que pode ser usado posteriormente para recuperar os dados BLOB em um formato binário, especifique o **sql: codificar** anotação. Você pode especificar **sql: codificar** em um atributo ou elemento de tipo simples.  
  
 Especifique o **sql: codificar** anotação para indicar que uma URL para o campo deve ser retornada em vez do valor do campo. **SQL: codificar** depende da chave primária para gerar uma seleção singleton na URL. A chave primária pode ser especificada usando o **SQL: Key-campos** anotação.  
  
 O **sql: codificar** anotação pode ser atribuída a "url" ou o valor "default". Um valor "default" retorna dados codificados na base 64.  
  
 O **sql: codificar** anotação não pode ser usada com **SQL: Use-cdata** ou na ID, IDREF, IDREFS, NMTOKEN ou NMTOKENS tipos de atributo. Ele não também pode ser usado com XSD **corrigido** atributo.  
  
> [!NOTE]  
>  As colunas de tipo BLOB não podem ser usadas como parte de uma chave ou chave estrangeira.  
  
## <a name="examples"></a>Exemplos  
 Para criar exemplos de funcionamento usando os exemplos a seguir, é necessário atender a determinados requisitos. Para obter mais informações, consulte [requisitos para executar exemplos do SQLXML](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-sqlencode-to-obtain-a-url-reference-to-blob-data"></a>A. Especificando sql:encode para obter uma referência URL aos dados BLOB  
 Neste exemplo, o esquema de mapeamento especifica **sql: codificar** sobre o **LargePhoto** atributo para recuperar a referência URI para uma foto de produto específico (em vez de recuperar os dados binários na Base 64 - formato codificado).  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  
  <xsd:element name="ProductPhoto" sql:relation="Production.ProductPhoto"   
               sql:key-fields="ProductPhotoID" >  
   <xsd:complexType>  
      <xsd:attribute name="ProductPhotoID"  type="xsd:int"  />  
     <xsd:attribute name="LargePhoto" type="xsd:string" sql:encode="url" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Para testar uma consulta XPath de exemplo com relação ao esquema  
  
1.  Copie o código de esquema acima e cole-o em um arquivo de texto. Salve o arquivo como sqlEncode.xml.  
  
2.  Copie o modelo a seguir e cole-o em um arquivo de texto. Salve o arquivo como sqlEncodeT.xml no mesmo diretório onde você salvou sqlEncode.xml.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="sqlEncode.xml">  
            /ProductPhoto[@ProductPhotoID=100]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     O caminho de diretório especificado para o esquema de mapeamento (sqlEncode.xml) é relativo ao diretório onde o modelo foi salvo. Também é possível especificar um caminho absoluto, por exemplo:  
  
    ```  
    mapping-schema="C:\SqlXmlTest\sqlEncode.xml"  
    ```  
  
3.  Crie e use o script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o modelo.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4.0](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Este é o resultado:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
   <ProductPhoto ProductPhotoID="100"  
                 LargePhoto="dbobject/Production.ProductPhoto[@ProductPhotoID="100"]/@LargePhoto" />   
</ROOT>  
```  
  
  
