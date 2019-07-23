---
title: Usar modo RAW com FOR XML | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML RAW mode
- XMLSCHEMA option
- FOR XML clause, RAW mode
- RAW FOR XML mode
- ELEMENTS directive
- RAW mode
- XMLDATA option
ms.assetid: 02c1bc0b-760c-4589-9ab1-6927c6d9c734
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ac5e5ccf60594d41ff89d9ef5bd2c4342944a6da
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68016154"
---
# <a name="use-raw-mode-with-for-xml"></a>Usar modo RAW com FOR XML

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

O modo RAW transforma cada linha no conjunto de resultados da consulta em um elemento XML que tem o identificador genérico \<row> ou o nome do elemento fornecido opcionalmente. Por padrão, cada valor de coluna no conjunto de linhas que não é NULL é mapeado para um atributo do elemento \<row>. Se a diretiva ELEMENTS for adicionada à cláusula FOR XML, cada valor de coluna será mapeado para um subelemento do elemento \<row>. Em conjunto com a diretiva ELEMENTS, você pode especificar opcionalmente a opção XSINIL para mapear valores de coluna NULL no conjunto de resultados para um elemento que tem o atributo `xsi:nil="true"`.
  
 É possível solicitar um esquema para o XML resultante. A especificação da opção XMLDATA retorna um esquema XDR embutido. A especificação da opção XMLSCHEMA retorna um esquema XSD embutido. O esquema aparece no início dos dados. No resultado, a referência ao namespace do esquema é repetida para cada elemento de alto nível.  
  
 A opção BINARY BASE64 deve ser especificada na cláusula FOR XML para retornar os dados binários em formato codificado na base64. Em modo RAW, a recuperação de dados binários sem especificar a opção BINARY BASE64 resulta em um erro.  
  
## <a name="in-this-section"></a>Nesta seção  
 Esta seção contém os seguintes exemplos:  
  
-   [Exemplo: Recuperando informações de modelo do produto como XML](../../relational-databases/xml/example-retrieving-product-model-information-as-xml.md)  
  
-   [Exemplo: Especificando XSINIL com a diretiva ELEMENTS](../../relational-databases/xml/example-specifying-xsinil-with-the-elements-directive.md)  
  
-   [Exemplo: Solicitando esquemas como resultados com as opções XMLDATA e XMLSCHEMA](../../relational-databases/xml/example-requesting-schemas-as-results-with-the-xmldata-and-xmlschema-options.md)  
  
-   [Exemplo: Recuperando dados binários](../../relational-databases/xml/example-retrieving-binary-data.md)  
  
-   [Exemplo: Renomeando o elemento &#60;row&#62;](../../relational-databases/xml/example-renaming-the-row-element.md)  
  
-   [Exemplo: Especificando um elemento raiz para o XML gerado por FOR XML](../../relational-databases/xml/example-specifying-a-root-element-for-the-xml-generated-by-for-xml.md)  
  
-   [Exemplo: Consultando colunas XMLType](../../relational-databases/xml/example-querying-xmltype-columns.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Adicionar namespaces a consultas com WITH XMLNAMESPACES](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [Usar o modo AUTO com FOR XML](../../relational-databases/xml/use-auto-mode-with-for-xml.md)   
 [Usar o modo EXPLICIT com FOR XML](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)   
 [Usar o modo PATH com FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md)   
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)   
 [FOR XML (SQL Server)](../../relational-databases/xml/for-xml-sql-server.md)
  
  
