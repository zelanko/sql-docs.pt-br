---
title: Funções XQuery no tipo de dados XML | Microsoft Docs
description: Saiba mais sobre as funções do XQuery com suporte para uso no tipo de dados XML.
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, functions
- xml data type [SQL Server], XQuery
- functions [SQL Server], XQuery
ms.assetid: 8df0877d-a03f-4ca9-b84e-908c4bb42b5e
author: rothja
ms.author: jroth
ms.openlocfilehash: 8e92148b5a85ced147599eafe09156cf41c47021
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037009"
---
# <a name="xquery-functions-against-the-xml-data-type"></a>Funções XQuery em tipos de dados xml
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  Este tópico e seus subtópicos descrevem as funções que você pode usar ao especificar XQuery em relação ao tipo de dados **XML** . Para obter as especificações do W3C, consulte [http://www.w3.org/TR/2004/WD-xpath-functions-20040723](https://go.microsoft.com/fwlink/?LinkId=4873) .  
  
 As funções XQuery pertencem ao http://www.w3.org/2004/07/xpath-functions namespace. As especificações de W3C usam o prefixo de namespace "fn:" para descrever essas funções. Você não tem que especificar explicitamente o prefixo de namespace "fn:" quando estiver usando as funções. Por causa disso e para melhorar a legibilidade, os prefixos de namespace geralmente não são usados nesta documentação.  
  
 A tabela a seguir lista as funções do XQuery com suporte no tipo de dados **XML**.  
  
|Categoria|Nome da função|  
|--------------|-------------------|  
|[Funções em valores numéricos]()|[limite](../xquery/numeric-values-functions-ceiling.md)|  
||[Floor](../xquery/numeric-values-functions-floor.md)|  
||[idas](../xquery/numeric-values-functions-round.md)|  
|[Funções XQuery em valores de cadeia de caracteres]()|[concat](../xquery/functions-on-string-values-concat.md)|  
||[contains](../xquery/functions-on-string-values-contains.md)|  
||[substring](../xquery/functions-on-string-values-substring.md)|  
||[Função minúscula &#40;XQuery&#41;](../xquery/functions-on-string-values-lower-case.md)|  
||[comprimento da cadeia de caracteres](../xquery/functions-on-string-values-string-length.md)|  
||[Função maiúscula &#40;&#41;XQuery ](../xquery/functions-on-string-values-upper-case.md)|  
|Funções em valores boolianos|[not](../xquery/functions-on-boolean-values-not-function.md)|  
|[Funções em nós]()|[number](../xquery/functions-on-nodes-number.md)|  
||[Função local-name (XQuery)](../xquery/functions-on-nodes-local-name.md)|  
||[Função namespace-uri (XQuery)](../xquery/functions-on-nodes-namespace-uri.md)|  
|[Funções de contexto]()|[last](../xquery/context-functions-last-xquery.md)|  
||[position](../xquery/context-functions-position-xquery.md)|  
|[Funções em sequências]()|[empty](../xquery/functions-on-sequences-empty.md)|  
||[distinct-values](../xquery/functions-on-sequences-distinct-values.md)|  
||[Função id (XQuery)](../xquery/functions-on-sequences-id.md)|  
|[Funções de agregação &#40;XQuery&#41;]()|[contagem](../xquery/aggregate-functions-count.md)|  
||[avg](../xquery/aggregate-functions-avg.md)|  
||[min](../xquery/aggregate-functions-min.md)|  
||[max](../xquery/aggregate-functions-max.md)|  
||[sum](../xquery/aggregate-functions-sum.md)|  
|[Funções de Construtor &#40;&#41;XQuery ](../xquery/constructor-functions-xquery.md)|[Funções de construtor](../xquery/constructor-functions-xquery.md)|  
|[Funções do acessador de dados](../xquery/data-accessor-functions.md)|[cadeia de caracteres](../xquery/data-accessor-functions-string-xquery.md)|  
||[data](../xquery/data-accessor-functions-data-xquery.md)|  
|[Funções de Construtor boolianas &#40;&#41;XQuery ]()|[Função true (XQuery)](../xquery/boolean-constructor-functions-true-xquery.md)|  
||[Função false (XQuery)](../xquery/boolean-constructor-functions-false-xquery.md)|  
|[Funções relacionadas a QNames &#40;&#41;XQuery ](./functions-related-to-qnames-expanded-qname.md)|[expanded-QName (XQuery)](../xquery/functions-related-to-qnames-expanded-qname.md)|  
||[local-name-from-QName (XQuery)](../xquery/functions-related-to-qnames-local-name-from-qname.md)|  
||[namespace-uri-from-QName (XQuery)](../xquery/functions-related-to-qnames-namespace-uri-from-qname.md)|  
|[Funções de extensão XQuery do SQL Server](./xquery-extension-functions-sql-column.md)|[função SQL: Column () (XQuery)](../xquery/xquery-extension-functions-sql-column.md)|  
||[função sql:variable() (XQuery)](../xquery/xquery-extension-functions-sql-variable.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos de tipos de dados xml](../t-sql/xml/xml-data-type-methods.md)   
 [Referência de linguagem XQuery &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)   
 [Dados XML &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)  
  
