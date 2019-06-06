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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: bb09e954640554c5375539b4104ab58ae71ddaab
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700410"
---
# <a name="schema-section"></a>Seção de esquema
A seção do esquema é necessária. Como mostra o exemplo anterior, o ADO grava metadados detalhados sobre cada coluna para preservar a semântica dos valores de dados tanto quanto possível para a atualização. No entanto, para carregar no XML, ADO requer apenas os nomes das colunas e o conjunto de linhas aos quais eles pertencem. Aqui está um exemplo de um esquema mínimo:  
  
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
  
 No exemplo anterior, o ADO irá tratar os dados como cadeias de caracteres de comprimento variável porque nenhuma informação de tipo está incluída no esquema.  
  
## <a name="creating-aliases-for-column-names"></a>Criar Aliases para nomes de coluna  
 O atributo de rs: nome permite que você crie um alias para um nome de coluna para que um nome amigável pode aparecer nas informações de coluna expostas pelo conjunto de linhas e um nome mais curto pode ser usado na seção de dados. Por exemplo, o esquema anterior poderia ser modificado para mapear CódigoDaTransportadora para s1, CompanyName para s2 e telefone para s3, da seguinte maneira:  
  
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
  
 Em seguida, na seção de dados, a linha usaria o atributo de nome (não rs: nome) para se referir a essa coluna:  
  
```  
"<row s1="1" s2="Speedy Express" s3="(503) 555-9831"/>  
```  
  
 É necessário criar aliases para nomes de coluna, sempre que um nome de coluna não é um atributo válido ou nome de marca em XML. Por exemplo, "LastName" deve ter um alias como os nomes com espaços incorporados são atributos inválidos. A linha a seguir não serão ser tratada corretamente pelo analisador XML, portanto, você deve criar um alias para outro nome que não tem um espaço inserido.  
  
```  
<row last name="Jones"/>  
```  
  
 Qualquer valor usado para o atributo de nome deve ser usado consistentemente em cada local que a coluna for referenciada em seções o esquema e os dados do documento XML. O exemplo a seguir mostra o uso consistente de s1:  
  
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
  
 Da mesma forma, porque não há nenhum alias definido para `CompanyName` no exemplo anterior, `CompanyName` deve ser usado de forma consistente em todo o documento.  
  
## <a name="data-types"></a>Tipos de dados  
 Você pode aplicar um tipo de dados para uma coluna com o atributo dt: Type. Para obter o guia definitivo para tipos permitidos de XML, consulte a seção tipos de dados do [especificação W3C XML-Data](http://www.w3.org/TR/1998/NOTE-XML-data/). Você pode especificar um tipo de dados de duas maneiras: especifique o atributo dt: Type diretamente na definição de coluna em si ou usar a construção de s:datatype como um elemento aninhado da definição de coluna. Por exemplo,  
  
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
  
 Se você tiver mais de informações de tipo que simplesmente o nome do tipo (por exemplo, dt: MaxLength), ela torna mais legível para usar o elemento filho de s:datatype. Isso é simplesmente uma convenção, no entanto e não é um requisito.  
  
 Ainda mais, os exemplos a seguir mostram como incluir informações de tipo em seu esquema.  
  
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
  
 Há um uso sutil do atributo rs: fixedlength no segundo exemplo. Uma coluna com o atributo do rs: fixedlength definida como true significa que os dados devem ter o comprimento definido no esquema. Nesse caso, um valor válido para id_título é "123456" como está "123". No entanto, "123" não é válido porque seu tamanho é 3, 6 não. Consulte o OLE DB guia do programador para uma mais a descrição da propriedade fixedlength completa.  
  
## <a name="handling-nulls"></a>Manipulando valores nulos  
 Valores nulos são tratados pelo atributo rs: maybenull. Se esse atributo for definido como true, o conteúdo da coluna pode conter um valor nulo. Além disso, se a coluna não for encontrada em uma linha de dados, o usuário lendo os dados do conjunto de linhas obterá um status nulo do IRowset::GetData(). Considere as seguintes definições de coluna da tabela Shippers (transportadores).  
  
```  
<s:AttributeType name="ShipperID">  
  <s:datatype dt:type="int" dt:maxLength="4"/>  
</s:AttributeType>  
<s:AttributeType name="CompanyName">  
  <s:datatype dt:type="string" dt:maxLength="40" rs:maybenull="true"/>  
</s:AttributeType>  
```  
  
 Permite a definição `CompanyName` seja nulo, mas `ShipperID` não pode conter um valor nulo. Se a seção de dados contido a linha a seguir, o provedor de persistência definiria o status dos dados para o `CompanyName` coluna para a constante de status de OLE DB DBSTATUS_S_ISNULL:  
  
```  
<z:row ShipperID="1"/>  
```  
  
 Se a linha tiver sido totalmente vazia, da seguinte maneira, o provedor de persistência retornaria um status de OLE DB de DBSTATUS_E_UNAVAILABLE para `ShipperID` e DBSTATUS_S_ISNULL para CompanyName.  
  
```  
<z:row/>   
```  
  
 Observe que uma cadeia de caracteres de comprimento zero não é igual a null.  
  
```  
<z:row ShipperID="1" CompanyName=""/>  
```  
  
 Para a linha anterior, o provedor de persistência retornará um status de OLE DB de DBSTATUS_S_OK para ambas as colunas. O `CompanyName` nesse caso é simplesmente "" (uma cadeia de caracteres de comprimento zero).  
  
 Para obter mais informações sobre o OLE DB constrói disponíveis para uso dentro do esquema de um documento XML para OLE DB, consulte a definição de "urn: schemas-microsoft-com:rowset" e o OLE DB guia do programador.  
  
## <a name="see-also"></a>Consulte também  
 [Persistência de registros em formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
