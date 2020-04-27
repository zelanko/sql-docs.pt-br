---
title: Pesquisar palavras perto de outra palavra com NEAR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- word searches [full-text search]
- NEAR option [full-text search]
- phrase searches [full-text search]
- proximity searches [full-text search]
- full-text search [SQL Server], proximity searches
- full-text queries [SQL Server], proximity
- queries [full-text search], proximity
ms.assetid: 87520646-4865-49ae-8790-f766b80a41f3
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: fadff7e68404ffae528cb4630e1f6c4b8156ccc0
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66011073"
---
# <a name="search-for-words-close-to-another-word-with-near"></a>Procurar palavras perto de outra palavra com NEAR
  Você pode usar uma condição de proximidade (NEAR) em um predicado [CONTAINS](/sql/t-sql/queries/contains-transact-sql) ou uma função [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) para procurar palavras ou frases próximas umas das outras. Você também pode especificar o número máximo de condições não relacionadas à pesquisa que separam a primeira e a última condição da pesquisa. Além disso, você pode pesquisar palavras ou frases em qualquer ordem, ou pode pesquisar palavras ou frases na ordem em que especificá-las. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]dá suporte à [condição de proximidade genérica](#Generic_NEAR)anterior, que agora é preterida e a [condição de proximidade personalizada](#Custom_NEAR), que é [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]nova no.  
  
##  <a name="the-custom-proximity-term"></a><a name="Custom_NEAR"></a>A condição de proximidade personalizada  
 A condição de proximidade personalizada introduz os novos recursos a seguir:  
  
-   Você pode especificar o número máximo de condições não relacionadas à pesquisa ou *distância máxima*que separa a primeira e o último critério de pesquisa para constituir uma correspondência.  
  
-   Se você especificar o número máximo de condições, também poderá especificar as correspondências que contêm condições de pesquisa na ordem especificada.  
  
 Para se qualificar como uma correspondência, uma cadeia de caracteres de texto deve:  
  
-   Iniciar com uma das condições de pesquisa especificadas e terminar com uma das outras condições de pesquisa especificadas.  
  
-   Conter todas as condições de pesquisa especificadas.  
  
-   O número de condições não relacionadas à pesquisa, incluindo palavras irrelevantes, que ocorre entre a primeira e a última condição de pesquisa deve ser menor ou igual à distância máxima, se especificado.  
  
 A sintaxe básica é:  
  
 NEAR (  
  
 {  
  
 *search_term* [,... *n* ]  
  
 |  
  
 (*search_term* [,... *n* ]) [, <maximum_distance> [, <match_order>]]  
  
 }  
  
 )  
  
> [!NOTE]  
>  Para obter mais informações sobre a sintaxe <custom_proximity_term>, veja [CONTAINS &#40;Transact-SQL&#41;](/sql/t-sql/queries/contains-transact-sql).  
  
 Por exemplo, você pode procurar 'John' dentro de duas condições de 'Smith', da seguinte maneira:  
  
```  
CONTAINS(column_name, 'NEAR((John, Smith), 2)')  
```  
  
 Alguns exemplos de cadeias de caracteres que correspondem são "`John Jacob Smith`" e "`Smith, John`". A cadeia de caracteres "`John Jones knows Fred Smith`" contém três condições de intervenção não relacionadas à pesquisa, portanto, não é uma correspondência.  
  
 Para exigir que as condições sejam localizadas na ordem especificada, você deve alterar a condição de proximidade do exemplo para `NEAR((John, Smith),2, TRUE).` Dessa maneira, é possível procurar "`John`" dentro de duas condições de "`Smith`", mas somente quando "`John`" precede "`Smith`". Em um idioma lido da esquerda para a direita, como o inglês, um exemplo de uma cadeia de caracteres correspondente é "`John Jacob Smith`".  
  
 Observe que, para um idioma que lê da direita para a esquerda, como árabe ou hebraico, o Mecanismo de texto completo aplica as condições especificadas em ordem invertida. Além disso, o Pesquisador de Objetos no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] inverte automaticamente a ordem de exibição de palavras especificada em idiomas da direita para a esquerda.  
  
> [!NOTE]  
>  Para obter mais informações, consulte "[Considerações adicionais sobre pesquisas de proximidade](#Additional_Considerations)", posteriormente neste tópico.  
  
### <a name="how-maximum-distance-is-measured"></a>Como a distância máxima é medida  
 Uma distância máxima específica, como 10 ou 25, determina quantas condições não relacionadas à pesquisa, inclusive palavras irrelevantes, podem ocorrer entre a primeira e a última condição de pesquisa em uma determinada cadeia de caracteres. Por exemplo, `NEAR((dogs, cats, "hunting mice"), 3)` retorna a linha a seguir na qual o número total de condições não relacionadas à pesquisa é três ("`enjoy`", "`but`" e "`avoid`"):  
  
 "`Cats` `enjoy` `hunting mice``, but avoid` `dogs``.`"  
  
 A mesma condição de proximidade não retorna a linha a seguir, porque a distância máxima é excedida pelas quatro condições não relacionadas à pesquisa ("`enjoy`", "`but`", "`usually`" e "`avoid`"):  
  
 "`Cats` `enjoy` `hunting mice``, but usually avoid` `dogs``.`"  
  
### <a name="combining-a-custom-proximity-term-with-other-terms"></a>Combinando uma condição de proximidade personalizada com outras condições  
 Você pode combinar uma condição de proximidade personalizada com outras condições. Você pode usar AND (&), OR (|) ou AND NOT (&!) para combinar uma condição de proximidade personalizada com outra, uma condição simples ou uma condição de prefixo. Por exemplo:  
  
-   CONTAINS('NEAR((*term1*,*term2*),5) AND *term3*')  
  
-   CONTAINS('NEAR((*term1*,*term2*),5) OR *term3*')  
  
-   CONTAINS('NEAR((*term1*,*term2*),5) AND NOT *term3*')  
  
-   CONTAINS('NEAR((*term1*,*term2*),5) AND NEAR((*term3*,*term4*),2)')  
  
-   CONTAINS('NEAR((*term1*,*term2*),5) OR NEAR((*term3*,*term4*),2, TRUE)')  
  
 Por exemplo,  
  
```  
CONTAINS(column_name, 'NEAR((term1, term2), 5, TRUE) AND term3')  
```  
  
 Não é possível combinar uma condição de proximidade personalizada com uma condição de proximidade genérica (*Term1* perto de *Term2*), um termo de geração (ISABOUT...) ou um termo ponderado (FORMSOF...).  
  
### <a name="example-using-the-custom-proximity-term"></a>Exemplo: usando a condição de proximidade personalizada  
 O exemplo a seguir pesquisa a tabela `Production.Document` do banco de dados de exemplo `AdventureWorks2012` para todos os resumos de documento que contêm o palavra "reflector" no mesmo documento que a palavra "bracket".  
  
```  
SELECT DocumentNode, Title, DocumentSummary  
FROM Production.Document AS DocTable   
INNER JOIN CONTAINSTABLE(Production.Document, Document,  
  'NEAR(bracket, reflector)' ) AS KEY_TBL  
  ON DocTable.DocumentNode = KEY_TBL.[KEY]  
WHERE KEY_TBL.RANK > 50  
ORDER BY KEY_TBL.RANK DESC;  
GO  
```  
  

  
##  <a name="additional-considerations-for-proximity-searches"></a><a name="Additional_Considerations"></a>Considerações adicionais para pesquisas de proximidade  
 Esta seção discute considerações que afetam pesquisas de proximidade genéricas e personalizadas:  
  
-   Sobrepondo ocorrências de condições de pesquisa  
  
     Todas as pesquisas de proximidade sempre procuram somente ocorrências sem sobreposição. Sobrepor ocorrências de condições de pesquisa nunca se qualifica como correspondências. Por exemplo, considere a condição de proximidade a seguir, que pesquisa "`A`" e "`AA`" nesta ordem com uma distância máxima de dois termos:  
  
    ```  
    CONTAINS(column_name, 'NEAR((A,AA),2, TRUE')  
    ```  
  
     As correspondências possíveis são "`AAA`", "`A.AA`" e "`A..AA`". Linhas que contêm apenas "`AA`" não corresponderiam.  
  
    > [!NOTE]  
    >  Você pode especificar condições que sobrepõem, por exemplo, `NEAR("mountain bike", "bike trails")` ou `(NEAR(comfort*, comfortable), 5)`. Especificar condições de sobreposição aumenta a complexidade da consulta aumentando as possíveis permutações de correspondência. Se você especificar um número grande deste tipo de condições sobrepostas, a consulta poderá ficar sem recursos e falhar. Se isto ocorrer, simplifique a consulta e tente novamente.  
  
-   O NEAR genérico e o NEAR personalizado (independentemente de uma distância máxima ter sido especificada) indicam a distância lógica entre condições, em vez de a distância absoluta entre elas. Por exemplo, termos dentro de frases diferentes ou orações dentro de um parágrafo são tratadas de forma muito diferente dos termos na mesma frase ou oração, independentemente da proximidade real, supondo que eles estejam menos relacionados. Da mesma forma, termos em parágrafos diferentes são tratados de forma muito mais diferente. Se uma correspondência ultrapassar o final de uma frase, parágrafo ou capítulo, o intervalo usado para classificar um documento será aumentado em 8, 128 ou 1024, respectivamente.  
  
-   Impacto de condições de proximidade sobre a classificação pela função CONTAINSTABLE  
  
     Quando NEAR é usado na função CONTAINSTABLE, o número de ocorrências em um documento relativo a seu comprimento, assim como a distância entre a primeira e a última condição de pesquisa em cada uma das ocorrências afeta a posição de cada documento. Para uma condição de proximidade genérica, se os termos de pesquisa correspondidos estiverem separados em >50 termos lógicos, a classificação retornada em um documento será 0. Para uma condição de proximidade personalizada que não especifica um valor inteiro como a distância máxima, um documento que só contém ocorrências cujo intervalo seja >100 termos lógicos receberá uma classificação de 0. Para obter mais informações sobre como classificar pesquisas de proximidade personalizada, veja [Limitar resultados da pesquisa com RANK](limit-search-results-with-rank.md).  
  
-   A opção **transformar palavras de ruído** do servidor  
  
     O valor de **transformar palavras de ruído** afetará como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trata palavras irrelevantes se elas forem especificadas em pesquisas de proximidade. Para saber mais, veja [transform noise words Server Configuration Option](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md).  
  

  
##  <a name="the-deprecated-generic-proximity-term"></a><a name="Generic_NEAR"></a>O termo de proximidade genérico preterido  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Recomendamos que você use a [condição de proximidade personalizada](#Custom_NEAR).  
  
 Um termo de proximidade genérico indica que todos os termos de pesquisa especificados devem ocorrer em um documento para que uma correspondência seja retornada, independentemente do número de termos não relacionados à pesquisa (a *distância*) entre os termos de pesquisa. A sintaxe básica é:  
  
 { *search_term* {Near | ~} *search_term* } [ ,... *n* ]  
  
 Por exemplo, nos exemplos a seguir, as palavras 'fox' e 'chicken' ambos devem aparecer, em qualquer ordem, para gerar uma correspondência:  
  
-   `CONTAINS(column_name, 'fox NEAR chicken')`  
  
-   `CONTAINSTABLE(table_name, column_name, 'fox ~ chicken')`  
  
> [!NOTE]  
>  Para obter informações sobre a sintaxe <generic_proximity_term>, veja [CONTAINS &#40;Transact-SQL&#41;](/sql/t-sql/queries/contains-transact-sql).  
  
 Para obter mais informações, consulte "[Considerações adicionais sobre pesquisas de proximidade](#Additional_Considerations)", posteriormente neste tópico.  
  
### <a name="combining-a-generic-proximity-term-with-other-terms"></a>Combinando uma condição de proximidade genérica com outras condições  
 Você pode usar AND (&), OR (|) ou AND NOT (&!) para combinar uma condição de proximidade genérica com outra, uma condição simples ou uma condição de prefixo. Por exemplo:  
  
```  
CONTAINSTABLE (Production.ProductDescription,  
   Description,   
   '(light NEAR aluminum) OR  
   (lightweight NEAR aluminum)'  
)  
```  
  
 Não é possível combinar uma condição de proximidade genérica com uma condição de proximidade personalizada `NEAR((term1,term2),5)`, como, um termo ponderado (ISABOUT...) ou um termo de geração (FORMSOF...).  
  
### <a name="example-using-the-generic-proximity-term"></a>Exemplo: usando a condição de proximidade genérica  
 O exemplo a seguir usa a condição de proximidade genérica para procurar o palavra "reflector" no mesmo documento que a palavra "bracket".  
  
```  
USE AdventureWorks2012;  
GO  
  
SELECT DocumentNode, Title, DocumentSummary  
FROM Production.Document AS DocTable INNER JOIN  
  CONTAINSTABLE(Production.Document, Document,  
  '(reflector NEAR bracket)' ) AS KEY_TBL  
  ON DocTable.DocumentNode = KEY_TBL.[KEY]  
ORDER BY KEY_TBL.RANK DESC;  
GO  
```  
  
 Observe que você também pode inverter as condições em CONTAINSTABLE e obterá o mesmo resultado:  
  
```  
CONTAINSTABLE(Production.Document, Document, '(bracket NEAR reflector)' ) AS KEY_TBL  
```  
  
 É possível utilizar o caractere til (~) no lugar da palavra-chave NEAR na consulta anterior e obter os mesmos resultados:  
  
```  
CONTAINSTABLE(Production.Document, Document, '(reflector ~ bracket)' ) AS KEY_TBL  
```  
  
 É possível especificar mais de duas palavras ou frases nos critérios de pesquisa. Por exemplo, é possível escrever:  
  
```  
CONTAINSTABLE(Production.Document, Document, '(reflector ~ bracket ~ installation)' ) AS KEY_TBL  
```  
  
 Isso significa que "reflector" deve estar no mesmo documento que "bracket", e "bracket" deve estar no mesmo documento que "installation".  
  

  
## <a name="see-also"></a>Consulte Também  
 [CONTAINSTABLE &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/containstable-transact-sql)   
 [Consulta com pesquisa de texto completo](query-with-full-text-search.md)   
 [CONTAINS &#40;Transact-SQL&#41;](/sql/t-sql/queries/contains-transact-sql)  
  
  
