---
title: Anotações XSD (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- annotated XSD schemas, annotations listed
- XSD schemas [SQLXML], annotations
ms.assetid: c62a6785-8d66-40a2-9c5d-80c73d600a3b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1b9e50cc418ef1fa2076b3207d7d3429694f160a
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/22/2019
ms.locfileid: "66013553"
---
# <a name="xsd-annotations-sqlxml-40"></a>Anotações XSD (SQLXML 4.0)
  A tabela a seguir lista as anotações XSD introduzidas no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e as compara com as anotações XDR introduzidas no [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].  
  
|Anotação XSD|Descrição|Link do tópico|Anotação XDR|  
|--------------------|-----------------|----------------|--------------------|  
|`sql:encode`|Quando um elemento ou atributo XML é mapeado para uma coluna BLOB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], permite solicitar um URI de referência. Esse URI pode ser usado posteriormente para retornar dados BLOB.|[Solicitando referências URL a dados BLOB usando sql: codificar &#40;SQLXML 4.0&#41;](requesting-url-references-to-blob-data-using-sql-encode-sqlxml-4-0.md)|`url-encode`|  
|`sql:guid`|Permite especificar se será usado um valor de GUID gerado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o valor fornecido pelo updategram daquela coluna.|[Usando as anotações sql:identity e sql:guid](using-the-sql-identity-and-sql-guid-annotations.md)|Sem suporte|  
|`sql:hide`|Oculta o elemento ou atributo especificado no esquema do documento XML resultante.|[Ocultando elementos e atributos usando sql:hide](hiding-elements-and-attributes-by-using-sql-hide.md)|Sem suporte|  
|`sql:identity`|Pode ser especificado em qualquer nó que mapeia para uma coluna de banco de dados do tipo IDENTITY. O valor especificado para esta anotação define o modo como é atualizada a coluna do tipo IDENTITY correspondente no banco de dados.|[Usando as anotações sql:identity e sql:guid](using-the-sql-identity-and-sql-guid-annotations.md)|Sem suporte|  
|`sql:inverse`|Instrui a lógica do diagrama de atualização a inverter sua interpretação da relação pai-filho que foi especificada usando  **\<SQL: Relationship >**.|[Especificando o atributo SQL: Inverse em SQL: Relationship &#40;SQLXML 4.0&#41;](specifying-the-sql-inverse-attribute-on-sql-relationship-sqlxml-4-0.md)|Sem suporte|  
|`sql:is-constant`|Cria um elemento XML que não é mapeado para nenhuma tabela. O elemento aparece na saída da consulta.|[Criando elementos constantes usando sql: constante é &#40;SQLXML 4.0&#41;](creating-constant-elements-using-sql-is-constant-sqlxml-4-0.md)|Igual|  
|`sql:key-fields`|Permite a especificação de coluna(s) que identifica(m) exclusivamente as linhas em uma tabela.|[Identificando colunas de chave usando SQL: Key-campos de &#40;SQLXML 4.0&#41;](identifying-key-columns-using-sql-key-fields-sqlxml-4-0.md)|Igual|  
|`sql:limit-field`<br /><br /> `sql:limit-value`|Permite limitar os valores retornados com base em um valor limitador.|[Filtrando valores usando SQL: limit-campo e SQL: limit-valor &#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-limit-field-and-sql-limit-value.md)|Igual|  
|`sql:mapped`|Permite que itens de esquema sejam excluídos do resultado.|[Excluindo elementos de esquema do documento XML resultante usando sql: mapeada &#40;SQLXML 4.0&#41;](excluding-schema-elements-from-the-xml-document-using-sql-mapped.md)|`map-field`|  
|`sql:max-depth`|Permite especificar a profundidade em relações recursivas especificadas no esquema.|[Especificando a profundidade em relações recursivas usando sql:max-depth](specifying-depth-in-recursive-relationships-by-using-sql-max-depth.md)|Sem suporte|  
|`sql:overflow-field`|Identifica a coluna de banco de dados que contém os dados de estouro.|[Recuperando dados não consumidos usando SQL: overflow-campo &#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-overflow-field.md)|Igual|  
|`sql:prefix`|Cria ID, IDREF e IDREFS de XML válidos. Precede os valores de ID, IDREF e IDREFS com uma cadeia de caracteres.|[Criando válido de ID, IDREF e IDREFS tipo atributos usando SQL: prefix &#40;SQLXML 4.0&#41;](creating-valid-id-idref-and-idrefs-type-attributes-using-sql-prefix-sqlxml-4-0.md)|Igual|  
|`sql:relationship`|Especifica relações entre elementos XML. Os atributos `parent`, `child`, `parent-key` e `child-key` são usados para estabelecer a relação.|[Especificando relações usando SQL: Relationship &#40;SQLXML 4.0&#41;](specifying-relationships-using-sql-relationship-sqlxml-4-0.md)|Os nomes de atributo são diferentes:<br /><br /> `key-relation`<br /><br /> `foreign-relation`<br /><br /> `key`<br /><br /> `foreign-key`|  
|`sql:use-cdata`|Permite especificar seções CDATA a serem usadas para determinados elementos no documento XML.|[Criando seções CDATA usando SQL: Use-cdata &#40;SQLXML 4.0&#41;](creating-cdata-sections-using-sql-use-cdata-sqlxml-4-0.md)|Igual|  
  
> [!NOTE]  
>  O atributo `targetNamespace` nativo XSD substitui a anotação `target-namespace` introduzida no esquema de mapeamento XDR do [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Especificando um destino Namespace usando o atributo targetNamespace &#40;SQLXML 4.0&#41;](specifying-a-target-namespace-using-the-targetnamespace-attribute-sqlxml-4-0.md)  
  
  
