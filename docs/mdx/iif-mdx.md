---
title: IIf (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ca6449308f9683bccf55e58d9cec6d5d5a97a59e
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87247130"
---
# <a name="iif-mdx"></a>IIF (MDX)


  Avalia expressões diferentes da ramificação dependendo de a condição booliana ser verdadeira ou falsa.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
IIf(Logical_Expression, Expression1 [HINT <hints>], Expression2 [HINT <hints>])  
```  
  
## <a name="arguments"></a>Argumentos  
 A função IIf usa três argumentos: IIF ( \<condition> , \<then branch> , \<else branch> ).  
  
 *Logical_Expression*  
 Uma condição que é avaliada como **true** (1) ou **false** (0). Ela deve ser uma expressão MDX lógica válida.  
  
 *Dica de expressão1 [ansiosos | Estrito | Lazy]]*  
 Usado quando a expressão lógica é avaliada como **true**. Expression1 deve ser uma expressão MDX válida.  
  
 *Dica de expression2 [ansiosos | Estrito | Lazy]]*  
 Usado quando a expressão lógica é avaliada como **falsa**. Expression2 deve ser uma expressão MDX válida.  
  
## <a name="remarks"></a>Comentários  
 A condição especificada pela expressão lógica é avaliada como **falsa** quando o valor dessa expressão é zero. Qualquer outro valor é avaliado como **true**.  
  
 Quando a condição for **verdadeira**, a função **IIF** retornará a primeira expressão. Caso contrário, a função retornará a segunda expressão.  
  
 As expressões especificadas podem retornar valores ou objetos MDX. Além disso, as expressões especificadas não precisam corresponder ao tipo.  
  
 A função **IIF** não é recomendada para criar um conjunto de membros com base em critérios de pesquisa. Em vez disso, use a função de [filtro](../mdx/filter-mdx.md) para avaliar cada membro em um conjunto especificado em relação a uma expressão lógica e retornar um subconjunto de membros.  
  
> [!NOTE]  
>  Se qualquer expressão for avaliada como NULL, o conjunto de resultados será NULL quando aquela condição for atendida.  
  
 Hint é um modificador opcional que determina como e quando a expressão será avaliada. Ele permite que você substitua o plano de consulta padrão, especificando como a expressão é avaliada.  
  
-   EAGER avalia a expressão no subespaço de IIF original.  
  
-   STRICT avalia a expressão somente no subespaço restrito que é criado pela expressão lógica da condição.  
  
-   LAZY avalia a expressão em modo célula a célula.  
  
 EAGER e STRICT se aplicam apenas às ramificações then-else de IIF, enquanto LAZY se aplica a todas as expressões MDX. Qualquer expressão MDX pode vir seguida de HINT LAZY, que avaliará essa expressão no modo célula a célula.  
  
 EAGER e STRICT são mutuamente exclusivos na dica. Eles podem ser usados no mesmo IIF(,,) sobre expressões diferentes.  
  
 Para obter mais informações, consulte [dicas de consulta de função IIf em SQL Server Analysis Services 2008](http://www.ssas-info.com/analysis-services-articles/50-mdx/1103-iif-function-query-hints-in-sql-server-analysis-services-2008) e [planos de execução e dicas de plano para a função IIf MDX e a instrução Case](https://go.microsoft.com/fwlink/?LinkId=269565).  
  
## <a name="examples"></a>Exemplos  
 A consulta a seguir mostra um uso simples de **IIF** dentro de uma medida calculada para retornar um dos dois valores de cadeia de caracteres diferentes quando a medida valor de vendas pela Internet for maior ou menor que $10000:  
  
 `WITH MEMBER MEASURES.IIFDEMO AS`  
  
 `IIF([Measures].[Internet Sales Amount]>10000`  
  
 `, "Sales Are High", "Sales Are Low")`  
  
 `SELECT {[Measures].[Internet Sales Amount],MEASURES.IIFDEMO} ON 0,`  
  
 `[Date].[Date].[Date].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
 IIF normalmente é usado para tratar erros de “divisão por zero” em medidas calculadas, como no exemplo a seguir:  
  
 `WITH`  
  
 `//Returns 1.#INF when the previous period contains no value`  
  
 `//but the current period does`  
  
 `MEMBER MEASURES.[Previous Period Growth With Errors] AS`  
  
 `([Measures].[Internet Sales Amount]-([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER))`  
  
 `/`  
  
 `([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER)`  
  
 `,FORMAT_STRING='PERCENT'`  
  
 `//Traps division by zero and returns null when the previous period contains`  
  
 `//no value but the current period does`  
  
 `MEMBER MEASURES.[Previous Period Growth] AS`  
  
 `IIF(([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER)=0,`  
  
 `NULL,`  
  
 `([Measures].[Internet Sales Amount]-([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER))`  
  
 `/`  
  
 `([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER)`  
  
 `),FORMAT_STRING='PERCENT'`  
  
 `SELECT {[Measures].[Internet Sales Amount],MEASURES.[Previous Period Growth With Errors], MEASURES.[Previous Period Growth]} ON 0,`  
  
 `DESCENDANTS(`  
  
 `[Date].[Calendar].[Calendar Year].&[2004],`  
  
 `[Date].[Calendar].[Date])`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 `WHERE([Product].[Product Categories].[Subcategory].&[26])`  
  
 Veja a seguir um exemplo de **IIF** retornando um de dois conjuntos dentro da função Generate para criar um conjunto complexo de tuplas em linhas:  
  
 `SELECT {[Measures].[Internet Sales Amount]} ON 0,`  
  
 `//If Internet Sales Amount is zero or null`  
  
 `//returns the current year and the All Customers member`  
  
 `//else returns the current year broken down by Country`  
  
 `GENERATE(`  
  
 `[Date].[Calendar Year].[Calendar Year].MEMBERS`  
  
 `, IIF([Measures].[Internet Sales Amount]=0,`  
  
 `{([Date].[Calendar Year].CURRENTMEMBER, [Customer].[Country].[All Customers])}`  
  
 `, {{[Date].[Calendar Year].CURRENTMEMBER} * [Customer].[Country].[Country].MEMBERS}`  
  
 `))`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 `WHERE([Product].[Product Categories].[Subcategory].&[26])`  
  
 Por fim, este exemplo mostra como usar Dicas de Planos:  
  
 `WITH MEMBER MEASURES.X AS`  
  
 `IIF(`  
  
 `[Measures].[Internet Sales Amount]=0`  
  
 `, NULL`  
  
 `, (1/[Measures].[Internet Sales Amount]) HINT EAGER)`  
  
 `SELECT {[Measures].x} ON 0,`  
  
 `[Customer].[Customer Geography].[Country].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
