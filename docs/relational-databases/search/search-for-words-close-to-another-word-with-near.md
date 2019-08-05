---
title: Pesquisar palavras perto de outra palavra com NEAR | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
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
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0e94bdcf4770190d3d84986b511996213fac17f9
ms.sourcegitcommit: e821cd8e5daf95721caa1e64c2815a4523227aa4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68702828"
---
# <a name="search-for-words-close-to-another-word-with-near"></a>Procurar palavras perto de outra palavra com NEAR
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Você pode usar um *termo de proximidade* **NEAR** em um predicado [CONTAINS](../../t-sql/queries/contains-transact-sql.md) ou uma função [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) para pesquisar palavras ou frases próximas umas das outras. 
  
##  <a name="Custom_NEAR"></a> Visão geral de NEAR  
**NEAR** inclui os seguintes recursos:  
-   Você pode especificar o número máximo de condições não relacionadas à pesquisa que separam a primeira e a última condição da pesquisa.

-   É possível pesquisar palavras ou frases em qualquer ordem ou pesquisar palavras ou frases em uma ordem especificada.
  
-   Você pode especificar o número máximo de condições não relacionadas à pesquisa ou *distância máxima*que separa a primeira e o último critério de pesquisa para constituir uma correspondência.  

-   Se você especificar o número máximo de condições, também poderá especificar as correspondências que contêm condições de pesquisa na ordem especificada.

 
 Para se qualificar como uma correspondência, uma cadeia de caracteres de texto deve:  
  
-   Iniciar com uma das condições de pesquisa especificadas e terminar com uma das outras condições de pesquisa especificadas.  
  
-   Conter todas as condições de pesquisa especificadas.  
  
-   O número de condições não relacionadas à pesquisa, incluindo palavras irrelevantes, que ocorre entre a primeira e a última condição de pesquisa deve ser menor ou igual à distância máxima, se especificada.  
  
## <a name="syntax-of-near"></a>Sintaxe de NEAR
A sintaxe básica de **NEAR** é:  

``` 
 NEAR (  
  
 {  
  
 *search_term* [ ,...*n* ]  
  
 |  
  
 (*search_term* [ ,...*n* ] ) [, <maximum_distance> [, <match_order> ] ]  
  
 }  
  
 )  
```

Para obter mais informações sobre a sintaxe, consulte [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md).  

## <a name="examples"></a>Exemplos
### <a name="example-1"></a>Exemplo 1
 Por exemplo, você pode procurar 'John' dentro de duas condições de 'Smith', da seguinte maneira:  
  
```sql
... CONTAINS(column_name, 'NEAR((John, Smith), 2)')
```  
  
 Alguns exemplos de cadeias de caracteres que correspondem são "`John Jacob Smith`" e "`Smith, John`". A cadeia de caracteres "`John Jones knows Fred Smith`" contém três condições de intervenção não relacionadas à pesquisa, portanto, não é uma correspondência.  
  
 Para exigir que as condições sejam localizadas na ordem especificada, você deve alterar a condição de proximidade do exemplo para `NEAR((John, Smith),2, TRUE).` Dessa maneira, é possível procurar "`John`" dentro de duas condições de "`Smith`", mas somente quando "`John`" precede "`Smith`". Em um idioma lido da esquerda para a direita, como o inglês, um exemplo de uma cadeia de caracteres correspondente é "`John Jacob Smith`".  
  
 Observe que, para um idioma que lê da direita para a esquerda, como árabe ou hebraico, o Mecanismo de texto completo aplica as condições especificadas em ordem invertida. Além disso, o Pesquisador de Objetos no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] inverte automaticamente a ordem de exibição de palavras especificada em idiomas da direita para a esquerda.   

### <a name="example-2"></a>Exemplo 2
 O exemplo a seguir pesquisa a tabela `Production.Document` do banco de dados de exemplo `AdventureWorks` para todos os resumos de documento que contêm o palavra "reflector" no mesmo documento que a palavra "bracket".  
  
```sql
SELECT DocumentNode, Title, DocumentSummary  
FROM Production.Document AS DocTable   
INNER JOIN CONTAINSTABLE(Production.Document, Document,  
  'NEAR(bracket, reflector)' ) AS KEY_TBL  
  ON DocTable.DocumentNode = KEY_TBL.[KEY]  
WHERE KEY_TBL.RANK > 50  
ORDER BY KEY_TBL.RANK DESC;  
GO  
``` 
 
## <a name="how-maximum-distance-is-measured"></a>Como a distância máxima é medida  
 Uma distância máxima específica, como 10 ou 25, determina quantas condições não relacionadas à pesquisa, inclusive palavras irrelevantes, podem ocorrer entre a primeira e a última condição de pesquisa em uma determinada cadeia de caracteres. Por exemplo, `NEAR((dogs, cats, "hunting mice"), 3)` retorna a linha a seguir na qual o número total de condições não relacionadas à pesquisa é três ("`enjoy`", "`but`" e "`avoid`"):  
  
 “`Cats` `enjoy` `hunting mice``, but avoid` `dogs``.`”  
  
 A mesma condição de proximidade não retorna a linha a seguir, porque a distância máxima é excedida pelas quatro condições não relacionadas à pesquisa ("`enjoy`", "`but`", "`usually`" e "`avoid`"):  
  
 “`Cats` `enjoy` `hunting mice``, but usually avoid` `dogs``.`”  
  
## <a name="combine-near-with-other-terms"></a>Combinar NEAR com outros termos  
 Você pode combinar NEAR com outros termos. Você pode usar AND (&), OR (|) ou AND NOT (&!) para combinar uma condição de proximidade personalizada com outra, uma condição simples ou uma condição de prefixo. Por exemplo:  
  
-   CONTAINS('NEAR((*term1*, *term2*),5) AND *term3*')  
  
-   CONTAINS('NEAR((*term1*, *term2*),5) OR *term3*')  
  
-   CONTAINS('NEAR((*term1*, *term2*),5) AND NOT *term3*')  
  
-   CONTAINS('NEAR((*term1*, *term2*),5) AND NEAR((*term3*, *term4*),2)')  
  
-   CONTAINS('NEAR((*term1*, *term2*),5) OR NEAR((*term3*, *term4*),2, TRUE)')  
  
 Por exemplo,  
  
```  
CONTAINS(column_name, 'NEAR((term1, term2), 5, TRUE) AND term3')  
```  
  
 Você não pode combinar NEAR com uma condição geracional (ISABOUT...) ou um termo ponderado (FORMSOF...).  
  
##  <a name="Additional_Considerations"></a> Mais informações sobre buscas de proximidade  
   
-   Sobrepondo ocorrências de condições de pesquisa  
  
     Todas as pesquisas de proximidade sempre procuram somente ocorrências sem sobreposição. Sobrepor ocorrências de condições de pesquisa nunca se qualifica como correspondências. Por exemplo, considere a condição de proximidade a seguir, que pesquisa "`A`" e "`AA`" nesta ordem com uma distância máxima de dois termos:  
  
    ```  
    CONTAINS(column_name, 'NEAR((A,AA), 2, TRUE)')
    ```  
  
     As correspondências possíveis são "`AAA`", "`A.AA`" e "`A..AA`". Linhas que contêm apenas "`AA`" não corresponderiam.  
  
    > [!NOTE]  
    >  Você pode especificar condições que sobrepõem, por exemplo, `NEAR("mountain bike", "bike trails")` ou `(NEAR(comfort*, comfortable), 5)`. Especificar condições de sobreposição aumenta a complexidade da consulta aumentando as possíveis permutações de correspondência. Se você especificar um número grande deste tipo de condições sobrepostas, a consulta poderá ficar sem recursos e falhar. Se isto ocorrer, simplifique a consulta e tente novamente.  
  
-   NEAR (independentemente de uma distância máxima ter sido especificada) indica a distância lógica entre os termos, em vez da distância absoluta entre eles. Por exemplo, termos dentro de frases diferentes ou orações dentro de um parágrafo são tratadas de forma muito diferente dos termos na mesma frase ou oração, independentemente da proximidade real, supondo que eles estejam menos relacionados. Da mesma forma, termos em parágrafos diferentes são tratados de forma muito mais diferente. Se uma correspondência ultrapassar o final de uma frase, parágrafo ou capítulo, o intervalo usado para classificar um documento será aumentado em 8, 128 ou 1024, respectivamente.  
  
-   Impacto de condições de proximidade sobre a classificação pela função CONTAINSTABLE  
  
    Quando NEAR é usado na função CONTAINSTABLE, o número de ocorrências em um documento relativo a seu comprimento, assim como a distância entre a primeira e a última condição de pesquisa em cada uma das ocorrências afeta a posição de cada documento. Para uma condição de proximidade genérica, se os termos de pesquisa correspondidos estiverem separados em >50 termos lógicos, a classificação retornada em um documento será 0. Para uma condição de proximidade personalizada que não especifica um valor inteiro como a distância máxima, um documento que só contém ocorrências cujo intervalo seja >100 termos lógicos receberá uma classificação de 0. Para obter mais informações sobre como classificar pesquisas de proximidade personalizada, veja [Limitar resultados da pesquisa com RANK](../../relational-databases/search/limit-search-results-with-rank.md).  
  
-   A opção **transformar palavras de ruído** do servidor  
  
     O valor de **transformar palavras de ruído** afetará como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trata palavras irrelevantes se elas forem especificadas em pesquisas de proximidade. Para saber mais, veja [transform noise words Server Configuration Option](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md).   
  
## <a name="see-also"></a>Consulte Também  
 [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)  
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [Consulta com pesquisa de texto completo](../../relational-databases/search/query-with-full-text-search.md)   
