---
title: 'Obter referências de URL para dados de BLOB com SQL: encode (SQLXML)'
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
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
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e1cd65cce635c89cb7ece1b88851d5f4a9b7cb09
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75257426"
---
# <a name="requesting-url-references-to-blob-data-using-sqlencode-sqlxml-40"></a>Solicitando referências URL a dados BLOB usando sql:encode (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Em um esquema XSD anotado, quando um atributo (ou elemento) é mapeado para uma coluna BLOB no Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], os dados são retornados no formato codificado na base 64 no XML.  
  
 Se você quiser que uma referência aos dados (um URI) seja retornada, que possa ser usada posteriormente para recuperar os dados de BLOB em um formato binário, especifique a anotação **SQL: encode** . Você pode especificar **SQL: encode** em um atributo ou elemento de tipo simples.  
  
 Especifique a anotação **SQL: encode** para indicar que uma URL para o campo deve ser retornada em vez do valor do campo. **SQL: a codificação** depende da chave primária para gerar um singleton SELECT na URL. A chave primária pode ser especificada usando a anotação **SQL: key-fields** .  
  
 A anotação **SQL: encode** pode ser atribuída ao valor "URL" ou "default". Um valor "default" retorna dados codificados na base 64.  
  
 A anotação **SQL: encode** não pode ser usada com **SQL: use-cdata** ou nos tipos de atributo ID, IDREF, IDREFS, NMTOKEN ou NMTOKENS. Ele também não pode ser usado com atributo XSD **fixo** .  
  
> [!NOTE]  
>  As colunas de tipo BLOB não podem ser usadas como parte de uma chave ou chave estrangeira.  
  
## <a name="examples"></a>Exemplos  
 Para criar exemplos de funcionamento usando os exemplos a seguir, é necessário atender a determinados requisitos. Para obter mais informações, consulte [Requirements for running SQLXML examples](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-sqlencode-to-obtain-a-url-reference-to-blob-data"></a>R. Especificando sql:encode para obter uma referência URL aos dados BLOB  
 Neste exemplo, o esquema de mapeamento especifica **SQL: encode** no atributo **LargePhoto** para recuperar a referência de URI para uma foto de produto específica (em vez de recuperar os dados binários no formato codificado em base 64).  
  
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
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4,0](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Este é o resultado:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
   <ProductPhoto ProductPhotoID="100"  
                 LargePhoto="dbobject/Production.ProductPhoto[@ProductPhotoID="100"]/@LargePhoto" />   
</ROOT>  
```  
  
  
