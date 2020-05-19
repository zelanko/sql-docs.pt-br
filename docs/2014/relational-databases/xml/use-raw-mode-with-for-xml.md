---
title: Usar modo RAW com FOR XML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 06054f9a107e2aaf9fea83cb3879ef672a8520b6
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82702349"
---
# <a name="use-raw-mode-with-for-xml"></a>Usar modo RAW com FOR XML
  O modo RAW transforma cada linha no conjunto de resultados da consulta em um elemento XML que tem o identificador genérico \<row> ou o nome do elemento fornecido opcionalmente. Por padrão, cada valor de coluna no conjunto de linhas que não é NULL é mapeado para um atributo do elemento \<row>. Se a diretiva ELEMENTS for adicionada à cláusula FOR XML, cada valor de coluna será mapeado para um subelemento do elemento \<row>. Em conjunto com a diretiva ELEMENTS, é possível especificar opcionalmente a opção XSINIL para mapear valores de coluna NULL no conjunto de resultados para um elemento que tem o atributo xsi:nil=`"`true`"`.  
  
 É possível solicitar um esquema para o XML resultante. A especificação da opção XMLDATA retorna um esquema XDR embutido. A especificação da opção XMLSCHEMA retorna um esquema XSD embutido. O esquema aparece no início dos dados. No resultado, a referência ao namespace do esquema é repetida para cada elemento de alto nível.  
  
 A opção BINARY BASE64 deve ser especificada na cláusula FOR XML para retornar os dados binários em formato codificado na base64. Em modo RAW, a recuperação de dados binários sem especificar a opção BINARY BASE64 resulta em um erro.  
  
## <a name="in-this-section"></a>Nesta seção  
 Esta seção contém os seguintes exemplos:  
  
-   [Exemplo: recuperando informações de modelo de produto como XML](example-retrieving-product-model-information-as-xml.md)  
  
-   [Exemplo: Especificando XSINIL com a política ELEMENTS](example-specifying-xsinil-with-the-elements-directive.md)  
  
-   [Exemplo: Solicitando esquemas como resultados com as opções XMLDATA e XMLSCHEMA](example-requesting-schemas-as-results-with-the-xmldata-and-xmlschema-options.md)  
  
-   [Exemplo: recuperando dados binários](example-retrieving-binary-data.md)  
  
-   [Exemplo: Renomeando o elemento &#60;row&#62;](example-renaming-the-row-element.md)  
  
-   [Exemplo: especificando um elemento raiz para o XML gerado pela FOR XML](example-specifying-a-root-element-for-the-xml-generated-by-for-xml.md)  
  
-   [Exemplo: consultando colunas XMLType](example-querying-xmltype-columns.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Adicionar namespaces a consultas com WITH XMLNAMESPACES](add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [Usar o modo AUTO com FOR XML](use-auto-mode-with-for-xml.md)   
 [Usar o modo EXPLICIT com FOR XML](use-explicit-mode-with-for-xml.md)   
 [Usar o modo PATH com FOR XML](use-path-mode-with-for-xml.md)   
 [SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql)   
 [FOR XML &#40;SQL Server&#41;](../xml/for-xml-sql-server.md)  
  
  
