---
title: IIf (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- IIF
dev_langs:
- kbMDX
helpviewer_keywords:
- IIf function
ms.assetid: ec7b35e6-f4c5-40bf-93c8-b83c1cc26fe2
caps.latest.revision: 41
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 0b520aa3c3761c8dd8452b1732923b7415bcbca6
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="iif-mdx"></a>IIF (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Avalia expressões diferentes da ramificação dependendo de a condição booliana ser verdadeira ou falsa.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
IIf(Logical_Expression, Expression1 [HINT <hints>], Expression2 [HINT <hints>])  
```  
  
## <a name="arguments"></a>Argumentos  
 A função IIf usa três argumentos: iif (\<condição >, \<, em seguida, branch >, \<else branch >).  
  
 *Logical_Expression*  
 Uma condição que é avaliada como **true** (1) ou **false** (0). Ela deve ser uma expressão MDX lógica válida.  
  
 *Dica de Expression1 [Eager | Estrito | Lento]]*  
 Usado quando a expressão lógica é avaliada como **true**. Expression1 deve ser uma expressão MDX válida.  
  
 *Dica Expression2 [Eager | Estrito | Lento]]*  
 Usado quando a expressão lógica é avaliada como **false**. Expression2 deve ser uma expressão MDX válida.  
  
## <a name="remarks"></a>Comentários  
 A condição especificada pela expressão lógica é avaliada como **false** quando o valor dessa expressão é zero. Qualquer outro valor for avaliada como **true**.  
  
 Quando a condição é **true**, o **IIf** função retorna a primeira expressão. Caso contrário, a função retornará a segunda expressão.  
  
 As expressões especificadas podem retornar valores ou objetos MDX. Além disso, as expressões especificadas não precisam corresponder ao tipo.  
  
 O **IIf** função não é recomendada para criação de um conjunto de membros com base em critérios de pesquisa. Em vez disso, use o [filtro](../mdx/filter-mdx.md) função para avaliar cada membro em um conjunto especificado em relação a uma expressão lógica e retornar um subconjunto de membros.  
  
> [!NOTE]  
>  Se qualquer expressão for avaliada como NULL, o conjunto de resultados será NULL quando aquela condição for atendida.  
  
 Hint é um modificador opcional que determina como e quando a expressão será avaliada. Ele permite que você substitua o plano de consulta padrão, especificando como a expressão é avaliada.  
  
-   EAGER avalia a expressão no subespaço de IIF original.  
  
-   STRICT avalia a expressão somente no subespaço restrito que é criado pela expressão lógica da condição.  
  
-   LAZY avalia a expressão em modo célula a célula.  
  
 EAGER e STRICT se aplicam apenas às ramificações then-else de IIF, enquanto LAZY se aplica a todas as expressões MDX. Qualquer expressão MDX pode vir seguida de HINT LAZY, que avaliará essa expressão no modo célula a célula.  
  
 EAGER e STRICT são mutuamente exclusivos na dica. Eles podem ser usados no mesmo IIF(,,) sobre expressões diferentes.  
  
 Para obter mais informações, consulte [dicas de consulta de função IIF no SQL Server Analysis Services 2008](http://go.microsoft.com/fwlink/?LinkId=269540) e [planos de execução e dicas de plano para a função IIF de MDX e instrução CASE](http://go.microsoft.com/fwlink/?LinkId=269565).  
  
## <a name="examples"></a>Exemplos  
 A consulta a seguir mostra um uso simples de **IIF** dentro de uma medida calculada para retornar um de dois valores de cadeia de caracteres diferentes quando a medida quantidade de vendas pela Internet é maior ou menor que US $10.000:  
  
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
  
 A seguir está um exemplo de **IIF** retornando um de dois conjuntos na função Generate para criar um conjunto complexo de tuplas em linhas:  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

