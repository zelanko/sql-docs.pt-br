---
title: "Entendendo a ordem de passagem e resolução Order (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- evaluation order [MDX]
- calculation order [MDX]
- SOLVE_ORDER property
- queries [MDX], solve orders
- solve orders [MDX]
- pass orders [MDX]
- expressions [MDX], solve orders
ms.assetid: 7ed7d4ee-4644-4c5d-99a4-c4b429d0203c
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8f690c0226a15794d36b70a72d679972a5f34918
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="mdx-data-manipulation---understanding-pass-order-and-solve-order"></a>Manipulação de dados MDX - Noções básicas sobre a fase de ordem e a ordem de resolução
  Quando um cubo é calculado como resultado de um script MDX, ele pode passar por várias fases de cálculo dependendo do uso de diversos recursos relacionados ao cálculo. Cada uma dessas fases é chamada de fase de cálculo.  
  
 Uma fase de cálculo pode ser denominada por uma posição ordinal, chamada número de fase de cálculo. A quantidade de fases de cálculo necessária para computar por completo todas as células de um cubo é conhecida como profundidade de fase de cálculo do cubo.  
  
 Dados da tabela de fatos e de write-back afetam somente a passagem 0. Os scripts preenchem os dados depois da passagem 0; cada atribuição e instrução calculada de um script criam uma nova passagem. Fora do script MDX, as referências à passagem 0 absoluta referem-se à última passagem criada pelo script para o cubo.  
  
 São criados membros calculados em todas as passagens, mas a expressão é aplicada à passagem atual. Passagens anteriores contêm a medida calculada, mas com um valor nulo.  
  
## <a name="solve-order"></a>Ordem de resolução  
 A ordem de resolução determina a prioridade de cálculo no caso de expressões concorrentes. Em uma mesma passagem, a ordem de resolução determina duas coisas:  
  
-   A ordem na qual o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] avalia dimensões, membros, membros calculados, rollups personalizados e células calculadas.  
  
-   A ordem na qual o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] calcula membros personalizados, membros calculados, rollups personalizados e células calculadas.  
  
 O membro com a ordem de resolução mais alta tem precedência.  
  
> [!NOTE]  
>  A exceção a essa precedência é a função Aggregate. A ordem de resolução de membros calculados com a função Aggregate é inferior a qualquer medida calculada de intersecção.  
  
## <a name="solve-order-values-and-precedence"></a>Valores e precedência da ordem de resolução  
 Os valores da ordem de resolução podem variar de -8181 a 65535. Nesse intervalo, alguns valores da ordem de resolução correspondem a tipos específicos de cálculos, como mostra a tabela a seguir.  
  
|Cálculo|Ordem de resolução|  
|-----------------|-----------------|  
|Fórmulas de membro personalizado|-5119|  
|Operadores unários|-5119|  
|Cálculo de totais visuais|-4096|  
|Todos os outros cálculos (se não for especificado de outra forma)|0|  
  
 É altamente recomendável o uso exclusivo de números inteiros positivos ao definir valores da ordem de resolução. Se você atribuir valores inferiores aos valores da ordem de resolução mostrados na tabela anterior, a fase de cálculo pode tornar-se imprevisível. Por exemplo, o cálculo de um membro calculado receberá um valor de ordem de resolução inferior ao valor da fórmula de rollup personalizado de -5119. Esse valor de ordem de resolução baixo faz com que os membros calculados sejam calculados antes das fórmulas de rollup personalizado, podendo produzir resultados incorretos.  
  
### <a name="creating-and-changing-solve-order"></a>Criando e alterando a ordem de resolução  
 No Designer de Cubo, no **Painel de Cálculos**, é possível alterar a ordem de resolução de membros calculados e células calculadas mudando a ordem dos cálculos.  
  
 No formato MDX, você pode usar a palavra-chave **SOLVE_ORDER** para criar ou alterar membros calculados e células calculadas.  
  
## <a name="solve-order-examples"></a>Exemplos de ordem de resolução  
 Para ilustrar as complexidades inerentes da ordem de resolução, a sequência de consultas MDX a seguir começa com duas consultas, sem problemas de ordem de resolução individualmente. Em seguida, essas duas consultas são combinadas em uma consulta que requer uma ordem de resolução.  
  
> [!NOTE]  
>  Você pode executar essas consultas MDX no banco de dados multidimensional de amostra da Adventure Works. Você pode baixar o exemplo de [Modelos multidimensionais do SQL Server 2012 da AdventureWorks](http://msftdbprodsamples.codeplex.com/releases/view/55330) do site do codeplex.  
  
### <a name="query-1differences-in-income-and-expenses"></a>Consulta 1 – Diferenças em Receita e Despesa  
 Para a primeira consulta MDX, calcule a diferença entre vendas e custos de cada ano construindo uma consulta MDX simples semelhante a este exemplo:  
  
```  
WITH   
MEMBER  
[Date].[Calendar].[Year Difference] AS ([Date].[Calendar].[Calendar Year].&[2008] - [Date].[Calendar].[Calendar Year].&[2007] )  
SELECT   
{[Measures].[Internet Sales Amount], [Measures].[Internet Total Product Cost] }  
ON COLUMNS ,  
{ [Date].[Calendar].[Calendar Year].&[2007], [Date].[Calendar].[Calendar Year].&[2008], [Date].[Year Difference] }  
ON ROWS  
FROM [Adventure Works]  
```  
  
 Nessa consulta, existe apenas um membro calculado, `Year Difference`. Como há somente um membro calculado, a ordem de resolução não é uma preocupação, pois o cubo não usará nenhum membro calculado.  
  
 Essa consulta MDX produz um conjunto de resultados semelhante à tabela a seguir.  
  
||Valor das Vendas pela Internet|Custo Total do Produto da Internet|  
|-|---------------------------|---------------------------------|  
|**AS 2007**|$9,791,060.30|$5,718,327.17|  
|**CY 2008**|$9,770,899.74|$5,721,205.24|  
|**Diferença anual**|($20,160.56)|$2,878.06|  
  
### <a name="query-2percentage-of-income-after-expenses"></a>Consulta 2 – Porcentagem de receita menos despesas  
 Para a segunda consulta MDX, calcule a porcentagem da receita menos as despesas de cada ano, usando a consulta MDX a seguir:  
  
```  
WITH   
MEMBER  
[Measures].[Profit Margin] AS   
([Measures].[Internet Sales Amount] - [Measures].[Internet Total Product Cost] ) / [Measures].[Internet Sales Amount] ,  
FORMAT_STRING="Percent"  
SELECT   
{[Measures].[Internet Sales Amount], [Measures].[Internet Total Product Cost], [Measures].[Profit Margin] }  
ON COLUMNS ,  
{ [Date].[Calendar].[Calendar Year].&[2007], [Date].[Calendar].[Calendar Year].&[2008] }  
ON ROWS  
FROM [Adventure Works]  
```  
  
 Essa consulta MDX, como a anterior, possui apenas um membro calculado, `Profit Margin`, e, portanto, não tem complicações com a ordem de resolução.  
  
 Essa consulta MDX produz um conjunto de resultados um pouco diferente, semelhante à tabela a seguir.  
  
||Valor das Vendas pela Internet|Custo Total do Produto da Internet|Margem de Lucro|  
|-|---------------------------|---------------------------------|-------------------|  
|**AS 2007**|$9,791,060.30|$5,718,327.17|41.60%|  
|**CY 2008**|$9,770,899.74|$5,721,205.24|41.45%|  
  
 A diferença entre os conjuntos de resultados da primeira e da segunda consultas é proveniente da diferença no posicionamento do membro calculado. Na primeira consulta, o membro calculado faz parte do eixo ROWS e não no eixo COLUMNS mostrado na segunda consulta. A diferença de posicionamento passa a ser importante na próxima consulta, que combina os dois membros calculados em uma única consulta MDX.  
  
### <a name="query-3combined-year-difference-and-net-income-calculations"></a>Consulta 3 – Combinação dos cálculos de Diferença anual e Receita líquida  
 Nessa consulta final, a combinação dos exemplos anteriores em uma única consulta MDX, a ordem de resolução passa a ser importante devido aos cálculos nas colunas e nas linhas. Para confirmar se os cálculos são feitos na sequência correta, defina a sequência de cálculo usando a palavra-chave **SOLVE_ORDER** .  
  
 A palavra-chave **SOLVE_ORDER** especifica a ordem de resolução de membros calculados em uma consulta MDX ou em um comando **CREATE MEMBER** . Os valores de números inteiros usados com a palavra-chave **SOLVE_ORDER** são relativos, não precisam começar em zero e nem serem consecutivos. O valor simplesmente orienta o MDX a calcular um membro com base nos valores derivados do cálculo dos membros com um valor mais alto. Se um membro calculado for definido sem a palavra-chave **SOLVE_ORDER** , o valor padrão desse membro calculado será zero.  
  
 Por exemplo, se você combinar os cálculos usados nos dois primeiros exemplos de consulta, os dois membros calculados, `Year Difference` e `Profit Margin`, encontram-se em uma intersecção em uma única célula do conjunto de dados do resultado da consulta MDX de exemplo. A única maneira de determinar como o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] avaliará essa célula é pela ordem de resolução. As fórmulas usadas para construir essa célula produzirão resultados diferentes de acordo com a ordem de resolução dos dois membros calculados.  
  
 Primeiro, tente combinar os cálculos usados nas duas primeiras consultas na consulta MDX a seguir:  
  
```  
WITH   
MEMBER  
[Date].[Calendar].[Year Difference] AS ([Date].[Calendar].[Calendar Year].&[2008] - [Date].[Calendar].[Calendar Year].&[2007] ) ,  
SOLVE_ORDER = 1  
MEMBER  
[Measures].[Profit Margin] AS   
( [Measures].[Internet Sales Amount] - [Measures].[Internet Total Product Cost] ) / [Measures].[Internet Sales Amount] ,  
FORMAT_STRING="Percent" ,  
SOLVE_ORDER = 2  
SELECT   
{[Measures].[Internet Sales Amount], [Measures].[Internet Total Product Cost], [Measures].[Profit Margin] }  
ON COLUMNS ,  
{ [Date].[Calendar].[Calendar Year].&[2007], [Date].[Calendar].[Calendar Year].&[2008], [Date].[Year Difference] }  
ON ROWS  
FROM [Adventure Works]  
```  
  
 Neste exemplo de consulta MDX combinada, `Profit Margin` tem a ordem de resolução mais alta, portanto terá precedência quando as duas expressões interagirem. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] avalia a célula em questão usando a fórmula `Profit Margin` . Os resultados desse cálculo aninhado são mostrados na tabela a seguir.  
  
||Valor das Vendas pela Internet|Custo Total do Produto da Internet|Margem de Lucro|  
|-|---------------------------|---------------------------------|-------------------|  
|**AS 2007**|$9,791,060.30|$5,718,327.17|41.60%|  
|**CY 2008**|$9,770,899.74|$5,721,205.24|41.45%|  
|**Diferença anual**|($20,160.56)|$2,878.06|114.28%|  
  
 O resultado na célula compartilhada baseia-se na fórmula para `Profit Margin`. Ou seja, o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] calcula o resultado da célula compartilhada com os dados de `Year Difference` , produzindo a fórmula a seguir (o resultado foi arredondado para facilitar a leitura):  
  
```  
((9,770,899.74 - 9,791,060.30) - (5,721,205.24 - 5,718,327.17)) / (9,770,899.74 - 9,791,060.30) = 1.14275744   
```  
  
 ou  
  
```  
(23,038.63) / (20,160.56) = 114.28%  
```  
  
 Isso está claramente incorreto. No entanto, o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] calculará o resultado da célula compartilhada de forma diferente se você mudar as ordens de resolução dos membros calculados da consulta MDX. A consulta MDX combinada a seguir inverte a ordem de resolução dos membros calculados:  
  
```  
WITH   
MEMBER  
[Date].[Calendar].[Year Difference] AS ([Date].[Calendar].[Calendar Year].&[2008] - [Date].[Calendar].[Calendar Year].&[2007] ) ,  
SOLVE_ORDER = 2  
MEMBER  
[Measures].[Profit Margin] AS   
( [Measures].[Internet Sales Amount] - [Measures].[Internet Total Product Cost] ) / [Measures].[Internet Sales Amount] ,  
FORMAT_STRING="Percent" ,  
SOLVE_ORDER = 1  
SELECT   
{[Measures].[Internet Sales Amount], [Measures].[Internet Total Product Cost], [Measures].[Profit Margin] }  
ON COLUMNS ,  
{ [Date].[Calendar].[Calendar Year].&[2007], [Date].[Calendar].[Calendar Year].&[2008], [Date].[Year Difference] }  
ON ROWS  
FROM [Adventure Works]  
```  
  
 Como a ordem dos membros calculados foi alterada, o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] usa a fórmula `Year Difference` para avaliar a célula, como mostra a tabela a seguir.  
  
||Valor das Vendas pela Internet|Custo Total do Produto da Internet|Margem de Lucro|  
|-|---------------------------|---------------------------------|-------------------|  
|**AS 2007**|$9,791,060.30|$5,718,327.17|41.60%|  
|**CY 2008**|$9,770,899.74|$5,721,205.24|41.45%|  
|**Diferença anual**|($20,160.56)|$2,878.06|(0.15%)|  
  
 Como essa consulta usa a fórmula `Year Difference` com os dados de `Profit Margin` , a fórmula da célula compartilhada assemelha-se a este cálculo:  
  
```  
(($9,770,899.74 - 5,721,205.24) / $9,770,899.74) - ((9,791,060.30 - 5,718,327.17) / 9,791,060.30) = -0.15   
```  
  
 ou  
  
```  
0.4145 - 0.4160= -0.15  
```  
  
## <a name="additional-considerations"></a>Considerações adicionais  
 A ordem de resolução pode ser uma questão bastante complexa com que lidar, especialmente em cubos com um grande número de dimensões envolvendo membro calculado, fórmulas de rollup personalizado ou células calculadas. Quando o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] avalia uma consulta MDX, o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] leva em consideração os valores da ordem de resolução de tudo que esteja envolvido em uma determinada passagem, incluindo as dimensões do cubo especificadas na consulta MDX.  
  
## <a name="see-also"></a>Consulte também  
 [CalculationCurrentPass &#40;MDX&#41;](../../../mdx/calculationcurrentpass-mdx.md)   
 [CalculationPassValue &#40; MDX &#41;](../../../mdx/calculationpassvalue-mdx.md)   
 [Instrução CREATE MEMBER &#40;MDX&#41;](../../../mdx/mdx-data-definition-create-member.md)   
 [Manipulando dados &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-manipulation-manipulating-data.md)  
  
  

