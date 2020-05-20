---
title: Seção de esquema | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Schema section [ADO]
ms.assetid: 4ac6e524-2c92-48e8-b871-0a4b5c8fda18
author: rothja
ms.author: jroth
ms.openlocfilehash: 8222b697fec7d0dd5bd1f32425cf48761f25308e
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760892"
---
# <a name="schema-section"></a>Seção de esquema
A seção de esquema é necessária. Como mostra o exemplo anterior, o ADO grava metadados detalhados sobre cada coluna para preservar a semântica dos valores de dados tanto quanto possível para atualização. No entanto, para carregar no XML, o ADO requer apenas os nomes das colunas e do conjunto de linhas ao qual elas pertencem. Aqui está um exemplo de um esquema mínimo:  
  
```  
<xml xmlns:s="uuid:BDC6E3F0-6DA3-11d1-A2A3-00AA00C14882"  
    xmlns:rs="urn:schemas-microsoft-com:rowset"  
    xmlns:z="#RowsetSchema">  
  <s:Schema id="RowsetSchema">  
    <s:ElementType name="row" content="eltOnly">  
      <s:AttributeType name="ShipperID"/>  
      <s:AttributeType name="CompanyName"/>  
      <s:AttributeType name="Phone"/>  
      <s:Extends type="rs:rowbase"/>  
    </s:ElementType>  
  </s:Schema>  
  <rs:data>  
...  
  </rs:data>  
</xml>  
```  
  
 No exemplo anterior, o ADO tratará os dados como cadeias de caracteres de comprimento variável porque nenhuma informação de tipo está incluída no esquema.  
  
## <a name="creating-aliases-for-column-names"></a>Criando aliases para nomes de coluna  
 O atributo RS: Name permite que você crie um alias para um nome de coluna para que um nome amigável possa aparecer nas informações da coluna expostas pelo conjunto de linhas e um nome mais curto possa ser usado na seção de dados. Por exemplo, o esquema anterior poderia ser modificado para mapear a transportadora para S1, CompanyName para S2 e telefone para S3 da seguinte maneira:  
  
```  
<s:Schema id="RowsetSchema">   
<s:ElementType name="row" content="eltOnly" rs:updatable="true">   
<s:AttributeType name="s1" rs:name="ShipperID" rs:number="1" ...>   
...  
</s:AttributeType>   
<s:AttributeType name="s2" rs:name="CompanyName" rs:number="2" ...>   
...  
</s:AttributeType>   
<s:AttributeType name="s3" rs:name="Phone" rs:number="3" ...>   
...  
</s:AttributeType>   
...  
</s:ElementType>   
</s:Schema>  
```  
  
 Em seguida, na seção dados, a linha usaria o atributo Name (não RS: Name) para se referir a essa coluna:  
  
```  
"<row s1="1" s2="Speedy Express" s3="(503) 555-9831"/>  
```  
  
 A criação de aliases para nomes de coluna é necessária sempre que um nome de coluna não é um nome de atributo ou de marca válido em XML. Por exemplo, "LastName" deve ter um alias porque os nomes com espaços inseridos são atributos inválidos. A linha a seguir não será manipulada corretamente pelo analisador XML, portanto, você deve criar um alias para algum outro nome que não tenha um espaço inserido.  
  
```  
<row last name="Jones"/>  
```  
  
 Qualquer valor que você use para o atributo name deve ser usado de forma consistente em cada lugar em que a coluna é referenciada nas seções Schema e data do documento XML. O exemplo a seguir mostra o uso consistente de S1:  
  
```  
<s:Schema id="RowsetSchema">  
  <s:ElementType name="row" content="eltOnly">  
    <s:attribute type="s1"/>  
    <s:attribute type="CompanyName"/>  
    <s:attribute type="s3"/>  
    <s:extends type="rs:rowbase"/>  
  </s:ElementType>  
  <s:AttributeType name="s1" rs:name="ShipperID" rs:number="1"   
    rs:maydefer="true" rs:writeunknown="true">  
    <s:datatype dt:type="i4" dt:maxLength="4" rs:precision="10"   
      rs:fixedlength="true" rs:maybenull="true"/>  
  </s:AttributeType>  
</s:Schema>  
<rs:data>  
  <z:row s1="1" CompanyName="Speedy Express" s3="(503) 555-9831"/>  
</rs:data>  
```  
  
 Da mesma forma, como não há nenhum alias definido para `CompanyName` no exemplo anterior, o `CompanyName` deve ser usado consistentemente em todo o documento.  
  
## <a name="data-types"></a>Tipos de dados  
 Você pode aplicar um tipo de dados a uma coluna com o atributo dt: Type. Para obter o guia definitivo para tipos XML permitidos, consulte a seção tipos de dados da [especificação de dados XML do W3C](http://www.w3.org/TR/1998/NOTE-XML-data/). Você pode especificar um tipo de dados de duas maneiras: especifique o atributo dt: Type diretamente na própria definição de coluna ou use a construção s:DataType como um elemento aninhado da definição de coluna. Por exemplo,  
  
```  
<s:AttributeType name="Phone" >  
  <s:datatype dt:type="string"/>  
</s:AttributeType>  
```  
  
 é equivalente a  
  
```  
<s:AttributeType name="Phone" dt:type="string"/>  
```  
  
 Se você omitir o atributo dt: Type inteiramente da definição de linha, por padrão, o tipo da coluna será uma cadeia de caracteres de comprimento variável.  
  
 Se você tiver mais informações de tipo do que simplesmente o nome do tipo (por exemplo, DT: maxLength), ele tornará mais legível usar o elemento filho s:DataType. No entanto, essa é apenas uma convenção e não um requisito.  
  
 Os exemplos a seguir mostram mais sobre como incluir informações de tipo em seu esquema.  
  
```  
<!-- 1. String with no max length -->  
<s:AttributeType name="title_id"/>  
<!-or -->  
<s:AttributeType name="title_id" dt:type="string"/>  
  
<!-- 2. Fixed length string with max length of 6 -->  
<s:AttributeType name="title_id">  
    <s:datatype dt:type="string" dt:maxLength="6" rs:fixedlength="true" />  
</s:AttributeType>  
  
<!-- 3. Variable length string with max length of 6 -->  
<s:AttributeType name="title_id">  
    <s:datatype dt:type="string" dt:maxLength="6" />  
</s:AttributeType>  
  
<!-- 4. Integer -->  
<s:AttributeType name="title_id" dt:type="int"/>  
```  
  
 Há um uso sutil do atributo RS: cadeia no segundo exemplo. Uma coluna com o atributo RS: cadeia definida como true significa que os dados devem ter o comprimento definido no esquema. Nesse caso, um valor válido para title_id é "123456", como é "123". No entanto, "123" não seria válido porque seu comprimento é 3, e não 6. Consulte o guia do programador de OLE DB para obter uma descrição mais completa da propriedade cadeia.  
  
## <a name="handling-nulls"></a>Manipulando valores nulos  
 Os valores nulos são tratados pelo atributo RS: maybenull. Se esse atributo for definido como true, o conteúdo da coluna poderá conter um valor nulo. Além disso, se a coluna não for encontrada em uma linha de dados, o usuário que lê os dados de volta do conjunto de linhas receberá um status nulo de IRowset:: GetData (). Considere as seguintes definições de coluna da tabela transportadoras.  
  
```  
<s:AttributeType name="ShipperID">  
  <s:datatype dt:type="int" dt:maxLength="4"/>  
</s:AttributeType>  
<s:AttributeType name="CompanyName">  
  <s:datatype dt:type="string" dt:maxLength="40" rs:maybenull="true"/>  
</s:AttributeType>  
```  
  
 A definição permite `CompanyName` ser NULL, mas `ShipperID` não pode conter um valor nulo. Se a seção de dados contiver a linha a seguir, o provedor de persistência definiria o status dos dados da `CompanyName` coluna para a constante de status OLE DB DBSTATUS_S_ISNULL:  
  
```  
<z:row ShipperID="1"/>  
```  
  
 Se a linha estava totalmente vazia, como a seguir, o provedor de persistência retornaria um OLE DB status de DBSTATUS_E_UNAVAILABLE para `ShipperID` e DBSTATUS_S_ISNULL para CompanyName.  
  
```  
<z:row/>   
```  
  
 Observe que uma cadeia de caracteres de comprimento zero não é igual a NULL.  
  
```  
<z:row ShipperID="1" CompanyName=""/>  
```  
  
 Para a linha anterior, o provedor de persistência retornará um status de OLE DB de DBSTATUS_S_OK para ambas as colunas. O, `CompanyName` nesse caso, é simplesmente "" (uma cadeia de caracteres de comprimento zero).  
  
 Para obter mais informações sobre as construções de OLE DB disponíveis para uso no esquema de um documento XML para OLE DB, consulte a definição de "urn: schemas-microsoft-com: Rowset" e o guia do programador do OLE DB.  
  
## <a name="see-also"></a>Consulte Também  
 [Persistência de registros em formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
