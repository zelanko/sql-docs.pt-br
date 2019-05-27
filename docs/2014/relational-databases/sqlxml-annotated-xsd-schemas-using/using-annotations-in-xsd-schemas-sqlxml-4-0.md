---
title: Usando anotações em esquemas XSD (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- annotated XSD schemas, about annotated XSD schemas
- annotations [SQLXML]
- relationships [SQLXML]
- relationships [SQLXML], hierarchical relationships
- hierarchical relationships [SQLXML]
- mapping schema [SQLXML], scenarios for using
ms.assetid: 78f318a4-7a36-473b-9852-a4bae6940ce5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7c62357496d0b143fcd8736bc61117d43c6a0fac
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/22/2019
ms.locfileid: "66013599"
---
# <a name="using-annotations-in-xsd-schemas-sqlxml-40"></a>Usando anotações em esquemas XSD (SQLXML 4.0)
  No [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQLXML 4.0, a linguagem de esquema XSD dá suporte a anotações de forma semelhante às anotações introduzidas na linguagem de esquema XDR (XML-Data Reduced). Há anotações adicionais introduzidas no XSD para as quais não há suporte no XDR.  
  
 Essas anotações podem ser usadas dentro do esquema XSD para especificar o mapeamento de XML para relacional. Isso inclui o mapeamento entre elementos e atributos no esquema XSD para tabelas (exibições) e colunas nos bancos de dados.  
  
 Se você não especificar as anotações, será utilizado o mapeamento padrão. Por padrão, um elemento XSD com um tipo complexo é mapeado para um nome de tabela (exibição) no banco de dados especificado, e um elemento ou atributo com um tipo simples é mapeado para a coluna com o mesmo nome que o elemento ou o atributo.  
  
 Essas anotações também podem ser usadas para especificar as relações hierárquicas em XML, o que representa as relações no banco de dados, como um esquema XSD é simplesmente uma exibição XML de dados relacionais.  
  
 Esta seção fornece descrições das anotações que podem ser usadas com esquemas XSD e exemplos de sua utilização.  
  
> [!NOTE]  
>  Todos os exemplos nesta seção especificam consultas XPath simples no esquema XSD anotado descrito em cada exemplo. É presumido que haja familiaridade com a linguagem XPath.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Anotações XSD &#40;SQLXML 4.0&#41;](xsd-annotations-sqlxml-4-0.md)  
 Lista as anotações que podem ser usadas com esquemas XSD, suas descrições e as anotações equivalentes para XDR.  
  
 [Mapeamento padrão dos atributos e elementos XSD para tabelas e colunas &#40;SQLXML 4.0&#41;](default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)  
 Explica o mapeamento padrão e fornece exemplos de tarefas relacionados a ele.  
  
 [Mapeamento explícito de atributos e elementos XSD para tabelas e colunas &#40;SQLXML 4.0&#41;](explicit-mapping-xsd-elements-and-attributes-to-tables-and-columns.md)  
 Explica o mapeamento explícito com as anotações `sql:relation` e `sql:field` e fornece exemplos.  
  
 [Especificando relações usando SQL: Relationship &#40;SQLXML 4.0&#41;](specifying-relationships-using-sql-relationship-sqlxml-4-0.md)  
 Descreve e fornece exemplos da anotação `sql:relationship`.  
  
 [Especificando o atributo SQL: Inverse em SQL: Relationship &#40;SQLXML 4.0&#41;](specifying-the-sql-inverse-attribute-on-sql-relationship-sqlxml-4-0.md)  
 Descreve a anotação `sql:inverse`.  
  
 [Criando elementos constantes usando sql: constante é &#40;SQLXML 4.0&#41;](creating-constant-elements-using-sql-is-constant-sqlxml-4-0.md)  
 Descreve e fornece exemplos da anotação `sql:is-constant`.  
  
 [Excluindo elementos de esquema do documento XML resultante usando sql: mapeada &#40;SQLXML 4.0&#41;](excluding-schema-elements-from-the-xml-document-using-sql-mapped.md)  
 Descreve e fornece exemplos da anotação `sql:mapped`.  
  
 [Filtrando valores usando SQL: limit-campo e SQL: limit-valor &#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-limit-field-and-sql-limit-value.md)  
 Descreve e fornece exemplos das anotações `sql:limit-field` e `sql:limit-value`.  
  
 [Identificando colunas de chave usando SQL: Key-campos de &#40;SQLXML 4.0&#41;](identifying-key-columns-using-sql-key-fields-sqlxml-4-0.md)  
 Descreve e fornece exemplos da anotação `sql:key-fields`.  
  
 [Especificando um destino Namespace usando o atributo targetNamespace &#40;SQLXML 4.0&#41;](specifying-a-target-namespace-using-the-targetnamespace-attribute-sqlxml-4-0.md)  
 Descreve e fornece exemplos de como o **targetNamespace** atributo.  
  
 [Criando válido de ID, IDREF e IDREFS tipo atributos usando SQL: prefix &#40;SQLXML 4.0&#41;](creating-valid-id-idref-and-idrefs-type-attributes-using-sql-prefix-sqlxml-4-0.md)  
 Descreve e fornece exemplos da anotação `sql:prefix`.  
  
 [Coerções de tipo de dados e a anotação SQL: DataType &#40;SQLXML 4.0&#41;](data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md)  
 Descreve e fornece exemplos da anotação `sql:datatype`.  
  
 [Mapeando tipos de dados XSD para tipos de dados XPath &#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/xpath-data-types-sqlxml-4-0.md)  
 Fornece uma tabela que compara tipos de dados XSD, XDR e XPath e lista as conversões relevantes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Criando seções CDATA usando SQL: Use-cdata &#40;SQLXML 4.0&#41;](creating-cdata-sections-using-sql-use-cdata-sqlxml-4-0.md)  
 Descreve e fornece exemplos da anotação `sql:use-data`.  
  
 [Solicitando referências URL a dados BLOB usando sql: codificar &#40;SQLXML 4.0&#41;](requesting-url-references-to-blob-data-using-sql-encode-sqlxml-4-0.md)  
 Descreve e fornece exemplos da anotação `sql:encode`.  
  
 [Recuperando dados não consumidos usando SQL: overflow-campo &#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-overflow-field.md)  
 Descreve e fornece exemplos da anotação `sql:overflow-field`.  
  
 [Ocultando elementos e atributos usando sql:hide](hiding-elements-and-attributes-by-using-sql-hide.md)  
 Descreve e fornece exemplos da anotação `sql:hide`.  
  
 [Usando as anotações sql:identity e sql:guid](using-the-sql-identity-and-sql-guid-annotations.md)  
 Descreve e fornece exemplos das anotações `sql:identity` e `sql:guid`.  
  
 [Especificando a profundidade em relações recursivas usando sql:max-depth](specifying-depth-in-recursive-relationships-by-using-sql-max-depth.md)  
 Descreve e fornece exemplos da anotação `sql:max-depth`.  
  
## <a name="see-also"></a>Consulte também  
 [Anotado considerações de segurança do esquema &#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/security/annotated-schema-security-considerations-sqlxml-4-0.md)  
  
  
