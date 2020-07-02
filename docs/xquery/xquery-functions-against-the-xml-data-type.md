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
ms.openlocfilehash: ad25db1aa5a10039bc80766b30e1d2ba478df123
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85730983"
---
# <a name="xquery-functions-against-the-xml-data-type"></a>Funções XQuery em tipos de dados xml
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  Este tópico e seus subtópicos descrevem as funções que você pode usar ao especificar XQuery em relação ao tipo de dados **XML** . Para obter as especificações do W3C, consulte [http://www.w3.org/TR/2004/WD-xpath-functions-20040723](https://go.microsoft.com/fwlink/?LinkId=4873) .  
  
 As funções XQuery pertencem ao http://www.w3.org/2004/07/xpath-functions namespace. As especificações de W3C usam o prefixo de namespace "fn:" para descrever essas funções. Você não tem que especificar explicitamente o prefixo de namespace "fn:" quando estiver usando as funções. Por causa disso e para melhorar a legibilidade, os prefixos de namespace geralmente não são usados nesta documentação.  
  
 A tabela a seguir lista as funções do XQuery com suporte no tipo de dados **XML**.  
  
|Categoria|Nome da função|  
|--------------|-------------------|  
|[Funções em valores numéricos](https://msdn.microsoft.com/library/d5740a32-b174-43b9-b64d-1cc6edc50cff)|[limite](../xquery/numeric-values-functions-ceiling.md)|  
||[Floor](../xquery/numeric-values-functions-floor.md)|  
||[idas](../xquery/numeric-values-functions-round.md)|  
|[Funções XQuery em valores de cadeia de caracteres](https://msdn.microsoft.com/library/2dccefef-5d90-4f56-bda7-4c1954d8a730)|[concat](../xquery/functions-on-string-values-concat.md)|  
||[contains](../xquery/functions-on-string-values-contains.md)|  
||[substring](../xquery/functions-on-string-values-substring.md)|  
||[Função minúscula &#40;XQuery&#41;](../xquery/functions-on-string-values-lower-case.md)|  
||[comprimento da cadeia de caracteres](../xquery/functions-on-string-values-string-length.md)|  
||[Função maiúscula &#40;&#41;XQuery](../xquery/functions-on-string-values-upper-case.md)|  
|Funções em valores boolianos|[not](../xquery/functions-on-boolean-values-not-function.md)|  
|[Funções em nós](https://msdn.microsoft.com/library/09a8affa-3341-4f50-aebc-fdf529e00c08)|[number](../xquery/functions-on-nodes-number.md)|  
||[Função local-name (XQuery)](../xquery/functions-on-nodes-local-name.md)|  
||[Função namespace-uri (XQuery)](../xquery/functions-on-nodes-namespace-uri.md)|  
|[Funções de contexto](https://msdn.microsoft.com/library/f7d8af33-9de9-450c-a667-23dee3129b5f)|[last](../xquery/context-functions-last-xquery.md)|  
||[position](../xquery/context-functions-position-xquery.md)|  
|[Funções em sequências](https://msdn.microsoft.com/library/672d2795-53ab-49c2-bf24-bc81a47ecd3f)|[empty](../xquery/functions-on-sequences-empty.md)|  
||[distinct-values](../xquery/functions-on-sequences-distinct-values.md)|  
||[Função id (XQuery)](../xquery/functions-on-sequences-id.md)|  
|[Funções de agregação &#40;XQuery&#41;](https://msdn.microsoft.com/library/be647ef1-291e-4a5d-ab18-07c759efe176)|[contagem](../xquery/aggregate-functions-count.md)|  
||[média](../xquery/aggregate-functions-avg.md)|  
||[min](../xquery/aggregate-functions-min.md)|  
||[max](../xquery/aggregate-functions-max.md)|  
||[sum](../xquery/aggregate-functions-sum.md)|  
|[Funções de Construtor &#40;&#41;XQuery](../xquery/constructor-functions-xquery.md)|[Funções de construtor](../xquery/constructor-functions-xquery.md)|  
|[Funções do acessador de dados](../xquery/data-accessor-functions.md)|[cadeia de caracteres](../xquery/data-accessor-functions-string-xquery.md)|  
||[dados](../xquery/data-accessor-functions-data-xquery.md)|  
|[Funções de Construtor boolianas &#40;&#41;XQuery](https://msdn.microsoft.com/library/fa907f39-d4b7-4495-b829-c788928e0f64)|[Função true (XQuery)](../xquery/boolean-constructor-functions-true-xquery.md)|  
||[Função false (XQuery)](../xquery/boolean-constructor-functions-false-xquery.md)|  
|[Funções relacionadas a QNames &#40;&#41;XQuery](https://msdn.microsoft.com/library/7e07eb26-f551-4b63-ab77-861684faff71)|[expanded-QName (XQuery)](../xquery/functions-related-to-qnames-expanded-qname.md)|  
||[local-name-from-QName (XQuery)](../xquery/functions-related-to-qnames-local-name-from-qname.md)|  
||[namespace-uri-from-QName (XQuery)](../xquery/functions-related-to-qnames-namespace-uri-from-qname.md)|  
|[Funções de extensão XQuery do SQL Server](https://msdn.microsoft.com/library/4bc5d499-5fec-4c3f-b11e-5ab5ef9d8f97)|[função SQL: Column () (XQuery)](../xquery/xquery-extension-functions-sql-column.md)|  
||[função sql:variable() (XQuery)](../xquery/xquery-extension-functions-sql-variable.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos de tipos de dados xml](../t-sql/xml/xml-data-type-methods.md)   
 [Referência de linguagem XQuery &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)   
 [Dados XML &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)  
  
  
