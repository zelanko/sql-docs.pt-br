---
title: Anotações XSD (SQLXML)
description: Veja uma lista de anotações XSD (SQLXML 4,0) introduzidas no SQL Server 2005 (9. x), com uma comparação com as anotações XDR introduzidas no SQL Server 2000 (8. x).
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- annotated XSD schemas, annotations listed
- XSD schemas [SQLXML], annotations
ms.assetid: c62a6785-8d66-40a2-9c5d-80c73d600a3b
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: baf79cfd4048bad018df2314b9d891c47871f0d6
ms.sourcegitcommit: 5b7457c9d5302f84cc3baeaedeb515e8e69a8616
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/20/2020
ms.locfileid: "83689228"
---
# <a name="xsd-annotations-sqlxml-40"></a>Anotações XSD (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  A tabela a seguir lista as anotações XSD introduzidas no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e as compara com as anotações XDR introduzidas no [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].  
  
|Anotação XSD|Description|Link do tópico|Anotação XDR|  
|--------------------|-----------------|----------------|--------------------|  
|**sql:encode**|Quando um elemento ou atributo XML é mapeado para uma coluna BLOB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], permite solicitar um URI de referência. Esse URI pode ser usado posteriormente para retornar dados BLOB.|[Solicitando referências de URL a dados de BLOB usando SQL: encode &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/requesting-url-references-to-blob-data-using-sql-encode-sqlxml-4-0.md)|**codificação de URL**|  
|**SQL: GUID**|Permite especificar se será usado um valor de GUID gerado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o valor fornecido pelo updategram daquela coluna.|[Usando as anotações sql:identity e sql:guid](../../relational-databases/sqlxml-annotated-xsd-schemas-using/using-the-sql-identity-and-sql-guid-annotations.md)|Sem suporte|  
|**sql:hide**|Oculta o elemento ou atributo especificado no esquema do documento XML resultante.|[Ocultando elementos e atributos usando sql:hide](../../relational-databases/sqlxml-annotated-xsd-schemas-using/hiding-elements-and-attributes-by-using-sql-hide.md)|Sem suporte|  
|**sql:identity**|Pode ser especificado em qualquer nó que mapeia para uma coluna de banco de dados do tipo IDENTITY. O valor especificado para esta anotação define o modo como é atualizada a coluna do tipo IDENTITY correspondente no banco de dados.|[Usando as anotações sql:identity e sql:guid](../../relational-databases/sqlxml-annotated-xsd-schemas-using/using-the-sql-identity-and-sql-guid-annotations.md)|Sem suporte|  
|**sql:inverse**|Instrui a lógica updategram a inverter sua interpretação da relação pai-filho que foi especificada usando ** \< SQL: relationship>**.|[Especificando o atributo SQL: inverso em SQL: relationship &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-the-sql-inverse-attribute-on-sql-relationship-sqlxml-4-0.md)|Sem suporte|  
|**sql:is-constant**|Cria um elemento XML que não é mapeado para nenhuma tabela. O elemento aparece na saída da consulta.|[Criando elementos constantes usando SQL: is-constant &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/creating-constant-elements-using-sql-is-constant-sqlxml-4-0.md)|Idêntico|  
|**sql:key-fields**|Permite a especificação de coluna(s) que identifica(m) exclusivamente as linhas em uma tabela.|[Identificando colunas de chave usando SQL: campos de chave &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/identifying-key-columns-using-sql-key-fields-sqlxml-4-0.md)|Idêntico|  
|**sql:limit-field**<br /><br /> **sql:limit-value**|Permite limitar os valores retornados com base em um valor limitador.|[Filtrando valores usando SQL: limit-field e SQL: limit-value &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/filtering-values-using-sql-limit-field-and-sql-limit-value-sqlxml-4-0.md)|Idêntico|  
|**sql:mapped**|Permite que itens de esquema sejam excluídos do resultado.|[Excluindo elementos de esquema do documento XML resultante usando SQL: mapeado &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/excluding-schema-elements-from-the-xml-document-using-sql-mapped.md)|**map-field**|  
|**sql:max-depth**|Permite especificar a profundidade em relações recursivas especificadas no esquema.|[Especificando a profundidade em relações recursivas usando sql:max-depth](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-depth-in-recursive-relationships-by-using-sql-max-depth.md)|Sem suporte|  
|**sql:overflow-field**|Identifica a coluna de banco de dados que contém os dados de estouro.|[Recuperando dados não consumidos usando o SQL: overflow-field &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/retrieving-unconsumed-data-using-the-sql-overflow-field-sqlxml-4-0.md)|Idêntico|  
|**sql:prefix**|Cria ID, IDREF e IDREFS de XML válidos. Precede os valores de ID, IDREF e IDREFS com uma cadeia de caracteres.|[Criando atributos de tipo ID, IDREF e IDREFS válidos usando SQL: prefix &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/creating-valid-id-idref-and-idrefs-type-attributes-using-sql-prefix-sqlxml-4-0.md)|Idêntico|  
|**sql:relationship**|Especifica relações entre elementos XML. Os atributos **pai**, **filho**, **Parent-Key**e **Child-Key** são usados para estabelecer a relação.|[Especificando relações usando SQL: relationship &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-relationships-using-sql-relationship-sqlxml-4-0.md)|Os nomes de atributo são diferentes:<br /><br /> **relação de chave**<br /><br /> **relação estrangeira**<br /><br /> **chave**<br /><br /> **chave estrangeira**|  
|**sql:use-cdata**|Permite especificar seções CDATA a serem usadas para determinados elementos no documento XML.|[Criando seções CDATA usando SQL: use-cdata &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/creating-cdata-sections-using-sql-use-cdata-sqlxml-4-0.md)|Idêntico|  
  
> [!NOTE]  
>  O atributo XSD nativo **targetNamespace** substitui a anotação de **namespace de destino** que foi introduzida no esquema de mapeamento do [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] XDR.  
  
## <a name="see-also"></a>Consulte Também  
 [Especificando um namespace de destino usando o atributo targetNamespace &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-a-target-namespace-using-the-targetnamespace-attribute-sqlxml-4-0.md)  
  
  
