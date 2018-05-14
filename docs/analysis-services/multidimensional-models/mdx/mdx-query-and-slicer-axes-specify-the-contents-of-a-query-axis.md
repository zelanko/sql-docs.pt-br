---
title: Especificando o conteúdo de um eixo de consulta (MDX) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bceafa9fb8ddd89162deca105404c317001a86bb
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="mdx-query-and-slicer-axes---specify-the-contents-of-a-query-axis"></a>Consulta MDX e o eixo da segmentação de dados - especificar o conteúdo de um eixo de consulta
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Eixos de consulta especificam as extremidades de um conjunto de células retornadas por uma instrução MDX SELECT. Especificar as extremidades de um conjunto de células permitir restringir os dados retornados que ficam visíveis ao cliente.  
  
 Para especificar eixos de consulta, use a `<SELECT query axis clause>` para atribuir um conjunto a um eixo de consulta em particular. Cada valor da `<SELECT query axis clause>` define um eixo de consulta. O número de eixos do conjunto de dados é igual ao número de valores da `<SELECT query axis clause>` na instrução SELECT.  
  
## <a name="query-axis-syntax"></a>Sintaxe do eixo de consulta  
 A sintaxe a seguir mostra a sintaxe da `<SELECT query axis clause>`:  
  
```  
  
<SELECT query axis clause> ::=  
   [ NON EMPTY ] Set_Expression [ <SELECT dimension property list clause> ] [<HAVING clause>]  
   ON {  
      Integer_Expression |   
      AXIS( Integer_Expression ) |   
      {COLUMNS | ROWS | PAGES | SECTIONS | CHAPTERS}     
      }  
  
```  
  
 Cada eixo de consulta possui um número: zero (0) para o eixo x, 1 para o eixo y, 2 para o eixo z e assim por diante. Na sintaxe da `<SELECT query axis clause>`, o valor `Integer_Expression` especifica o número do eixo. Uma consulta MDX comporta até 128 eixos especificados, mas bem poucas consultas MDX usarão mais de 5 eixos. Para os primeiros 5 eixos, podem ser usados os aliases COLUMNS, ROWS, PAGES, SECTIONS e CHAPTERS.  
  
 Uma consulta MDX não pode ignorar eixos de consulta. Ou seja, uma consulta que contém um ou mais eixos de consultas não deve excluir eixos intermediários ou de baixa numeração. Por exemplo, uma consulta não pode ter um eixo ROWS sem um eixo COLUMNS nem os eixos COLUMNS e PAGES sem um eixo ROWS.  
  
 Contudo, você pode especificar uma cláusula SELECT sem eixos (ou seja, uma cláusula SELECT vazia). Nesse caso, todas as dimensões são dimensões de slicer e a consulta MDX seleciona uma célula.  
  
 Na sintaxe do eixo de consulta mostrada anteriormente, cada valor `Set_Expression` especifica o conjunto que define o conteúdo do eixo de consulta. Para obter mais informações sobre conjuntos, consulte [Trabalhando com membros, tuplas e conjuntos &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md).  
  
## <a name="examples"></a>Exemplos  
 A seguinte instrução SELECT simples retorna a medida Quantidade de Vendas pela Internet no eixo Columns, e utiliza a função MDX MEMBERS para retornar todos os membros da hierarquia Calendar da dimensão Date no eixo Rows:  
  
```  
SELECT {[Measures].[Internet Sales Amount]} ON COLUMNS,  
{[Date].[Calendar].MEMBERS} ON ROWS  
FROM [Adventure Works]  
  
```  
  
 As duas consultas seguintes retorna os mesmos resultados exatamente mas demonstra o uso de números de eixo em lugar de aliases:  
  
```  
SELECT {[Measures].[Internet Sales Amount]} ON 0,  
{[Date].[Calendar].MEMBERS} ON 1  
FROM [Adventure Works]  
  
SELECT {[Measures].[Internet Sales Amount]} ON AXIS(0),  
{[Date].[Calendar].MEMBERS} ON AXIS(1)  
FROM [Adventure Works]  
  
```  
  
 A palavra-chave NON EMPTY, usada antes da definição fixa, é um modo fácil de remover todas as tuplas vazias de um eixo. Por exemplo, nos exemplos observamos que não existem dados no cubo desde agosto de 2004. Para remover todas as linhas do conjunto de células que não têm dados em nenhuma coluna, basta adicionar NON EMPTY antes do conjunto na definição do eixo Rows, desta forma:  
  
```  
SELECT {[Measures].[Internet Sales Amount]} ON COLUMNS,  
NON EMPTY  
{[Date].[Calendar].MEMBERS} ON ROWS  
FROM [Adventure Works]  
  
```  
  
 NON EMPTY pode ser usado em todos os eixos de uma consulta. Compare os resultados destas duas consultas, o primeiro não usa a palavra-chave NON EMPTY e o segundo a utiliza nos dois eixos:  
  
```  
SELECT {[Measures].[Internet Sales Amount]}   
* [Promotion].[Promotion].[Promotion].MEMBERS  
ON COLUMNS,  
{[Date].[Calendar].[Calendar Year].MEMBERS} ON ROWS  
FROM [Adventure Works]  
WHERE([Product].[Subcategory].&[19])  
  
SELECT NON EMPTY {[Measures].[Internet Sales Amount]}   
* [Promotion].[Promotion].[Promotion].MEMBERS  
ON COLUMNS,  
NON EMPTY  
{[Date].[Calendar].[Calendar Year].MEMBERS} ON ROWS  
FROM [Adventure Works]  
WHERE([Product].[Subcategory].&[19])  
  
```  
  
 A cláusula HAVING pode ser usada para filtrar os conteúdo de um eixo com base em critérios específicos; este método é menos flexível que outros métodos que podem obter os mesmos resultados, como a função FILTER, mas seu uso é mais simples. Veja um exemplo que retorna apenas as datas em que a Quantidade de Vendas pela Internet superou $15.000:  
  
```  
SELECT {[Measures].[Internet Sales Amount]}   
ON COLUMNS,  
NON EMPTY  
{[Date].[Calendar].[Date].MEMBERS}   
HAVING [Measures].[Internet Sales Amount]>15000  
ON ROWS  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Especificando o conteúdo de um eixo do Slicer & #40; MDX & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-slicer-axis.md)  
  
  
