---
title: Usar a pesquisa de texto completo com colunas XML | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- xml columns [full-text search]
- indexes [full-text search]
ms.assetid: 8096cfc6-1836-4ed5-a769-a5d63b137171
caps.latest.revision: "14"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5564331e341498a5c63550e08e466db859f5762b
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="use-full-text-search-with-xml-columns"></a>Usar a pesquisa de texto completo com colunas XML
  É possível criar um índice de texto completo em colunas de XML que indexa o conteúdo dos valores de XML, mas ignora a marcação XML. Marcas de elemento são usadas como limites do token. Os seguintes itens são indexados:  
  
-   O conteúdo dos elementos XML.  
  
-   O conteúdo de atributos XML apenas do elemento de nível superior, a menos que esses valores sejam valores numéricos.  
  
 Quando possível, você pode combinar pesquisa de texto completo com índice XML da seguinte maneira:  
  
1.  Primeiro, filtre os valores de XML de interesse usando a pesquisa de texto completo do SQL.  
  
2.  Em seguida, consulte esses valores de XML que usam o índice XML na coluna XML.  
  
## <a name="example-combining-full-text-search-with-xml-querying"></a>Exemplo: Combinando pesquisa de texto completo com consulta XML  
 Após o índice de texto completo ter sido criado na coluna XML, a seguinte consulta verifica se um valor XML contém as palavras "custom" no título de um manual:  
  
```  
SELECT *   
FROM   T   
WHERE  CONTAINS(xCol,'custom')   
AND    xCol.exist('/book/title/text()[contains(.,"custom")]') =1  
```  
  
 O método **contains()** usa o índice de texto completo para subdividir os valores de XML que contêm a palavra “custom” em qualquer lugar do documento. A cláusula **exist()** garante que a palavra “custom” ocorre no título de um manual.  
  
 Uma pesquisa de texto completo que usa **contains()** e **contains()** do XQuery tem semânticas diferentes. O último é uma correspondência de subcadeia de caracteres e o anterior é uma correspondência de tokens que usa lematização. Portanto, se a pesquisa se destinar à cadeia de caracteres que contém “run” no título, as correspondências incluirão “run”, “runs” e “running”, porque tanto **contains()** quanto **contains()** do XQuery são atendidos. No entanto, a consulta não corresponde à palavra “customizable” no título em que **contains()** de texto completo falha, mas **contains()** do XQuery é atendido. Geralmente, para a correspondência pura de subcadeia de caracteres, a cláusula **contains()** de texto completo deve ser removida.  
  
 Além disso, a pesquisa de texto completo usa a lematização de palavras, mas **contains()** do XQuery é uma correspondência literal. Essa diferença é ilustrada no próximo exemplo.  
  
## <a name="example-full-text-search-on-xml-values-using-stemming"></a>Exemplo: Pesquisa de texto completo em valores de XML usando lematização  
 A verificação de **contains()** do XQuery executada no exemplo anterior, geralmente, não pode ser eliminada. Considere esta consulta:  
  
```  
SELECT *   
FROM   T   
WHERE  CONTAINS(xCol,'run')   
```  
  
 A palavra "ran" no documento corresponde à critério de pesquisa por causa da lematização. Além disso, o contexto da pesquisa não é verificado usando XQuery.  
  
 Quando o XML é decomposto em colunas relacionais usando AXSD que são indexadas por texto completo, as consultas XPath que ocorrem sobre a exibição em XML não executam pesquisa de texto completo nas tabelas subjacentes.  
  
## <a name="see-also"></a>Consulte também  
 [Índices XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)  
  
  
