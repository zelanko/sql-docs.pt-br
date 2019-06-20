---
title: 'Solicitando referências URL a dados BLOB usando sql: encode (SQLXML 4.0) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
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
manager: craigg
ms.openlocfilehash: 153a88bcb31f65d4e6aff007cfbee7d1f7afc6df
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66013727"
---
# <a name="requesting-url-references-to-blob-data-using-sqlencode-sqlxml-40"></a>Solicitando referências URL a dados BLOB usando sql:encode (SQLXML 4.0)
  Em um esquema XSD anotado, quando um atributo (ou elemento) é mapeado para uma coluna BLOB no Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], os dados são retornados no formato codificado na base 64 no XML.  
  
 Caso queira que uma referência aos dados (um URI) seja retornada e que possa ser usada posteriormente para recuperar os dados BLOB em um formato binário, especifique a anotação `sql:encode`. Você pode especificar `sql:encode` em um atributo ou elemento de tipo simples.  
  
 Especifique a anotação `sql:encode` para indicar que deve ser retornada uma URL para o campo em vez do valor do campo. `sql:encode` depende da chave primária para gerar uma seleção singleton na URL. A chave primária pode ser especificada usando o `sql:key-fields` anotação.  
  
 À anotação `sql:encode` é possível atribuir o valor "url" ou "default". Um valor "default" retorna dados codificados na base 64.  
  
 A anotação `sql:encode` não pode ser usada com `sql:use-cdata` ou nos tipos de atributo ID, IDREF, IDREFS, NMTOKEN ou NMTOKENS. Ele não também pode ser usado com XSD **corrigido** atributo.  
  
> [!NOTE]  
>  As colunas de tipo BLOB não podem ser usadas como parte de uma chave ou chave estrangeira.  
  
## <a name="examples"></a>Exemplos  
 Para criar exemplos de funcionamento usando os exemplos a seguir, é necessário atender a determinados requisitos. Para obter mais informações, consulte [requisitos para executar exemplos do SQLXML](../sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-sqlencode-to-obtain-a-url-reference-to-blob-data"></a>A. Especificando sql:encode para obter uma referência URL aos dados BLOB  
 Neste exemplo, o esquema de mapeamento especifica `sql:encode` sobre o **LargePhoto** atributo para recuperar a referência URI para uma foto de produto específico (em vez de recuperar os dados binários em formato codificado em Base 64).  
  
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
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4.0](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Esse é o resultado:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
   <ProductPhoto ProductPhotoID="100"  
                 LargePhoto="dbobject/Production.ProductPhoto[@ProductPhotoID="100"]/@LargePhoto" />   
</ROOT>  
```  
  
  
