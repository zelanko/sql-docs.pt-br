---
title: "A consulta básica de MDX (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/13/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- queries [MDX], SELECT statement
- queries [MDX], about queries
- cellsets [MDX]
- SELECT statement [MDX]
- cubes [Analysis Services], SELECT statement
ms.assetid: 4fa5a95a-fec9-4584-875c-dbf030c53e82
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Active
ms.openlocfilehash: 9abd75f8cbed78630caac64447b8df59cde3ea56
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2018
---
# <a name="mdx-query---the-basic-query"></a>Consulta MDX - a consulta básica
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
A consulta básica das expressões multidimensionais (MDX) é a instrução SELECT, a consulta MDX mais usada. Entendendo como a instrução MDX SELECT deve especificar um conjunto de resultados, como é sua sintaxe e como criar uma consulta simples usando a instrução SELECT, você terá uma compreensão sólida de como usar a linguagem MDX para consultar dados multidimensionais.  
  
## <a name="specifying-a-result-set"></a>Especificando um conjunto de resultados  
 Na linguagem MDX, a instrução SELECT especifica um conjunto de resultados que contém um subconjunto de dados multidimensionais retornados a partir de um cubo. Para especificar um conjunto de resultados, a consulta MDX deve conter as seguintes informações:  
  
-   O número de eixos que você deseja que o conjunto de resultados contenha. É possível especificar até 128 eixos em uma consulta MDX.  
  
-   O conjunto de membros ou tuplas a ser incluído em cada eixo da consulta MDX.  
  
-   O nome do cubo que define o contexto da consulta MDX.  
  
-   O conjunto de membros ou tuplas a ser incluído no eixo da segmentação de dados. Para obter mais informações sobre eixos de consulta e de segmentação de dados, consulte [Restrição à consulta com eixos de consulta e de segmentação de dados &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-restricting-the-query.md).  
  
 Para identificar os eixos de consulta, o cubo que será consultado e o eixo da segmentação de dados, a instrução MDX SELECT usa as seguintes cláusulas:  
  
-   Uma cláusula SELECT que determina os eixos de consulta de uma instrução MDX SELECT. Para obter mais informações sobre a construção de eixos de consulta em uma cláusula SELECT, consulte [Especificação do conteúdo de um eixo de consulta &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md).  
  
-   Uma cláusula FROM que determina qual cubo será consultado. Para obter mais informações sobre a cláusula FROM, consulte [SELECT Statement &#40;MDX&#41;](../../../mdx/mdx-data-manipulation-select.md).  
  
-   Uma cláusula WHERE opcional que determina quais membros ou tuplas usar no eixo da segmentação de dados para restringir os dados retornados. Para obter mais informações sobre a construção de eixos de segmentação de dados em uma cláusula WHERE, consulte [Especificação do conteúdo de um eixo de segmentação de dados &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-slicer-axis.md).  
  
> [!NOTE]  
>  Para obter informações mais detalhadas sobre as várias cláusulas da instrução SELECT, consulte [Instrução SELECT &#40;MDX&#41;](../../../mdx/mdx-data-manipulation-select.md).  
  
## <a name="select-statement-syntax"></a>Sintaxe da instrução SELECT  
 A sintaxe a seguir mostra uma instrução SELECT básica, incluindo o uso das cláusulas SELECT, FROM e WHERE:  
  
```  
[ WITH <SELECT WITH clause> [ , <SELECT WITH clause> ... ] ]   
SELECT [ * | ( <SELECT query axis clause>   
    [ , <SELECT query axis clause> ... ] ) ]  
FROM <SELECT subcube clause>   
[ <SELECT slicer axis clause> ]  
[ <SELECT cell property list clause> ]  
```  
  
 A instrução MDX SELECT oferece suporte à sintaxe opcional, como a palavra-chave WITH, ao uso de funções MDX para criar membros calculados para inclusão no eixo ou no eixo da segmentação de dados e à capacidade de retornar os valores das propriedades da célula específica como parte da consulta. Para obter mais informações sobre a instrução MDX SELECT, consulte [SELECT Statement &#40;MDX&#41;](../../../mdx/mdx-data-manipulation-select.md).  
  
### <a name="comparing-the-syntax-of-the-mdx-select-statement-to-sql"></a>Comparando a sintaxe da instrução MDX SELECT com o SQL  
 O formato da sintaxe da instrução MDX SELECT é similar à sintaxe do SQL. No entanto, há várias diferenças fundamentais:  
  
-   A sintaxe MDX distingue os conjuntos encerrando tuplas ou membros entre chaves (os caracteres { e }). Para obter mais informações sobre membro, tupla e conjunto de sintaxes, consulte [Como trabalhar com membros, tuplas e conjuntos &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md).  
  
-   As consultas MDX têm 0, 1, 2 ou até 128 eixos de consulta na instrução SELECT. Cada eixo se comporta exatamente da mesma maneira, diferentemente do SQL, onde há diferenças significativas entre o comportamento das linhas e das colunas de uma consulta.  
  
-   Como com uma consulta SQL, a cláusula FROM nomeia a fonte dos dados para a consulta MDX. No entanto, a cláusula MDX FROM é restrita a um único cubo. Informações de outros cubos podem ser recuperadas valor a valor usando a função LookupCube.  
  
-   A cláusula WHERE descreve o eixo da segmentação de dados em uma consulta MDX. Ela atua como um eixo extra, invisível na consulta, segmentando os valores que aparecem nas células do conjunto de resultados; diferentemente da cláusula WHERE do SQL, ela não afeta diretamente o que aparece nos eixos das linhas da consulta. A funcionalidade da cláusula WHERE do SQL está disponível por meio de outras funções MDX, como a função FILTER.  
  
## <a name="select-statement-example"></a>Exemplo de instrução SELECT  
 O exemplo a seguir mostra uma consulta MDX básica que usa a instrução SELECT. Ela retorna um conjunto de resultados que contém os valores de vendas e tributos de 2002 e 2003 da região sudoeste.  
  
```  
SELECT  
    { [Measures].[Sales Amount],   
        [Measures].[Tax Amount] } ON COLUMNS,  
    { [Date].[Fiscal].[Fiscal Year].&[2002],   
        [Date].[Fiscal].[Fiscal Year].&[2003] } ON ROWS  
FROM [Adventure Works]  
WHERE ( [Sales Territory].[Southwest] )  
```  
  
 Neste exemplo, a consulta define as seguintes informações do conjunto de resultados:  
  
-   A cláusula SELECT define os eixos da consulta como os membros Valor de Vendas e Valor de Tributos da dimensão Medidas e os membros 2002 e 2003 da dimensão Data.  
  
-   A cláusula FROM indica que a fonte de dados é o cubo Adventure Works.  
  
-   A cláusula WHERE define o eixo do slicer como o membro Sudoeste da dimensão Região de vendas.  
  
 Observe que o exemplo de consulta também usa os aliases de eixo COLUMNS e ROWS. As posições ordinais desses eixos também poderiam ser usadas. O exemplo a seguir mostra como a consulta MDX poderia ter sido escrita para usar a posição ordinal de cada eixo:  
  
```  
SELECT  
    { [Measures].[Sales Amount],   
        [Measures].[Tax Amount] } ON 0,  
    { [Date].[Fiscal].[Fiscal Year].&[2002],   
        [Date].[Fiscal].[Fiscal Year].&[2003] } ON 1  
FROM [Adventure Works]  
WHERE ( [Sales Territory].[Southwest] )  
```  
  
 Para obter exemplos mais detalhados, consulte [Especificação do conteúdo de um eixo de consulta &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md)e [Especificação do conteúdo de um eixo de segmentação de dados &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-slicer-axis.md).  
  
## <a name="see-also"></a>Consulte também  
 [Principais conceitos em MDX &#40; Analysis Services &#41;](../../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)   
 [Instrução SELECT &#40; MDX &#41;](../../../mdx/mdx-data-manipulation-select.md)  
  
  
