---
title: Usando anotações em esquemas XSD (SQLXML)
description: Saiba como usar as anotações com suporte na linguagem de esquema XSD no SQLXML 4,0 para especificar o mapeamento de XML para relacional em um esquema XSD.
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ec539fce08e832f2d92032bd48fce76f12ff73e2
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97479327"
---
# <a name="using-annotations-in-xsd-schemas-sqlxml-40"></a>Usando anotações em esquemas XSD (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  No [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQLXML 4.0, a linguagem de esquema XSD dá suporte a anotações de forma semelhante às anotações introduzidas na linguagem de esquema XDR (XML-Data Reduced). Há anotações adicionais introduzidas no XSD para as quais não há suporte no XDR.  
  
 Essas anotações podem ser usadas dentro do esquema XSD para especificar o mapeamento de XML para relacional. Isso inclui o mapeamento entre elementos e atributos no esquema XSD para tabelas (exibições) e colunas nos bancos de dados.  
  
 Se você não especificar as anotações, será utilizado o mapeamento padrão. Por padrão, um elemento XSD com um tipo complexo é mapeado para um nome de tabela (exibição) no banco de dados especificado, e um elemento ou atributo com um tipo simples é mapeado para a coluna com o mesmo nome que o elemento ou o atributo.  
  
 Essas anotações também podem ser usadas para especificar as relações hierárquicas em XML, representando, portanto, as relações no banco de dados, porque um esquema XSD é simplesmente uma exibição de XML do dado relacional.  
  
 Esta seção fornece descrições das anotações que podem ser usadas com esquemas XSD e exemplos de sua utilização.  
  
> [!NOTE]  
>  Todos os exemplos nesta seção especificam consultas XPath simples no esquema XSD anotado descrito em cada exemplo. É presumido que haja familiaridade com a linguagem XPath.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Anotações XSD &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/xsd-annotations-sqlxml-4-0.md)  
 Lista as anotações que podem ser usadas com esquemas XSD, suas descrições e as anotações equivalentes para XDR.  
  
 [Mapeamento padrão de elementos e atributos XSD para tabelas e colunas &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)  
 Explica o mapeamento padrão e fornece exemplos de tarefas relacionados a ele.  
  
 [Mapeamento explícito de elementos e atributos XSD para tabelas e colunas &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/explicit-mapping-xsd-elements-and-attributes-to-tables-and-columns.md)  
 Explica o mapeamento explícito com as anotações **SQL: relation** e **SQL: Field** e fornece exemplos.  
  
 [Especificando relações usando SQL: relationship &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-relationships-using-sql-relationship-sqlxml-4-0.md)  
 Descreve e fornece exemplos da anotação **SQL: relationship** .  
  
 [Especificando o atributo SQL: inverso em SQL: relationship &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-the-sql-inverse-attribute-on-sql-relationship-sqlxml-4-0.md)  
 Descreve a anotação **SQL: inverso** .  
  
 [Criando elementos constantes usando SQL: is-constant &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/creating-constant-elements-using-sql-is-constant-sqlxml-4-0.md)  
 Descreve e fornece exemplos da anotação **SQL: is-constant** .  
  
 [Excluindo elementos de esquema do documento XML resultante usando SQL: mapeado &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/excluding-schema-elements-from-the-xml-document-using-sql-mapped.md)  
 Descreve e fornece exemplos da anotação **SQL: mapeada** .  
  
 [Filtrando valores usando SQL: limit-field e SQL: limit-value &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/filtering-values-using-sql-limit-field-and-sql-limit-value-sqlxml-4-0.md)  
 Descreve e fornece exemplos das anotações **SQL: limit-field** e **SQL: limit-value** .  
  
 [Identificando colunas de chave usando SQL: campos de chave &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/identifying-key-columns-using-sql-key-fields-sqlxml-4-0.md)  
 Descreve e fornece exemplos da anotação **SQL: key-fields** .  
  
 [Especificando um namespace de destino usando o atributo targetNamespace &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-a-target-namespace-using-the-targetnamespace-attribute-sqlxml-4-0.md)  
 Descreve e fornece exemplos do atributo **targetNamespace** .  
  
 [Criando atributos de tipo ID, IDREF e IDREFS válidos usando SQL: prefix &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/creating-valid-id-idref-and-idrefs-type-attributes-using-sql-prefix-sqlxml-4-0.md)  
 Descreve e fornece exemplos da anotação **SQL: prefix** .  
  
 [Conversões de tipo de dados e a anotação sql: DataType &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md)  
 Descreve e fornece exemplos da anotação **SQL: DataType** .  
  
 [Mapeando tipos de dados XSD para tipos de dados XPath &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/mapping-xsd-data-types-to-xpath-data-types-sqlxml-4-0.md)  
 Fornece uma tabela que compara tipos de dados XSD, XDR e XPath e lista as conversões relevantes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Criando seções CDATA usando SQL: use-cdata &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/creating-cdata-sections-using-sql-use-cdata-sqlxml-4-0.md)  
 Descreve e fornece exemplos da anotação **SQL: Use-data** .  
  
 [Solicitando referências de URL a dados de BLOB usando SQL: encode &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/requesting-url-references-to-blob-data-using-sql-encode-sqlxml-4-0.md)  
 Descreve e fornece exemplos da anotação **SQL: encode** .  
  
 [Recuperando dados não consumidos usando o SQL: overflow-field &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/retrieving-unconsumed-data-using-the-sql-overflow-field-sqlxml-4-0.md)  
 Descreve e fornece exemplos da anotação **SQL: overflow-field** .  
  
 [Ocultando elementos e atributos usando sql:hide](../../relational-databases/sqlxml-annotated-xsd-schemas-using/hiding-elements-and-attributes-by-using-sql-hide.md)  
 Descreve e fornece exemplos da anotação **SQL: Hide** .  
  
 [Usando as anotações sql:identity e sql:guid](../../relational-databases/sqlxml-annotated-xsd-schemas-using/using-the-sql-identity-and-sql-guid-annotations.md)  
 Descreve e fornece exemplos de anotações **SQL: Identity** e **SQL: GUID** .  
  
 [Especificando a profundidade em relações recursivas usando sql:max-depth](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-depth-in-recursive-relationships-by-using-sql-max-depth.md)  
 Descreve e fornece exemplos da anotação **SQL: Max-Depth** .  
  
## <a name="see-also"></a>Consulte Também  
 [Considerações de segurança de esquema anotadas &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/annotated-schema-security-considerations-sqlxml-4-0.md)  
  
  
