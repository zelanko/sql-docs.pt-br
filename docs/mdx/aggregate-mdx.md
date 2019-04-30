---
title: Aggregate (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 11e10d5a03702329a5ed59ed42acee0abc2d27c8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63200629"
---
# <a name="aggregate-mdx"></a>Função Aggregate (MDX)


  Retorna um número que é calculado com a agregação nas células retornadas pela expressão de conjunto. Se uma expressão numérica não for fornecida, essa função agregará cada medida no contexto atual de consulta usando o operador padrão de agregação especificado para cada medida. Se uma exressão numérica for fornecida, essa função primeiro avalia e, em seguida, soma a expressão numérica de cada célula no conjunto especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Aggregate(Set_Expression [ ,Numeric_Expression ])  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Numeric_Expression*  
 Uma expressão numérica válida, geralmente uma linguagem MDX de coordenadas de célula, que retorna um número.  
  
## <a name="remarks"></a>Comentários  
 Se um conjunto de tuplas vazias ou um conjunto vazio for especificado, essa função retornará um valor vazio.  
  
 A tabela a seguir descreve como o **agregação** função se comporta com funções de agregação diferentes.  
  
|Operador de agregação|Resultado|  
|--------------------------|------------|  
|Sum|Retorna a soma dos valores no conjunto.|  
|Count|Retorna a contagem dos valores no conjunto.|  
|Max|Retorna o valor máximo no conjunto.|  
|Mín|Retorna o valor mínimo no conjunto.|  
|Funções de agregação semiaditivas|Retorna o cálculo de comportamento semiaditivo no conjunto depois de projetar a forma no eixo de tempo.|  
|Contagem Distinta|Faz agregações nos dados de fatos que contribuem com o subcubo quando o eixo do slicer inclui um conjunto.<br /><br /> Retorna a contagem distinta para cada membro do conjunto. O resultado depende da segurança das células que estão sendo agregadas e não da segurança das células obrigatórias para o cálculo. A segurança de célula no conjunto gera um erro; a segurança de célula abaixo da granularidade do conjunto especificado é ignorada. Os cálculos no conjunto geram um erro. Os cálculos abaixo da granularidade do conjunto são ignorados. A contagem distinta em um conjunto que inclui um membro e um ou mais filhos retorna a contagem distinta dos fatos que contribuem com o membro filho.|  
|Atributos que não podem ser agregados|Retorna a soma dos valores.|  
|Funções de agregação mista|Sem suporte e gera um erro.|  
|Operadores unários|Não respeitados; os valores são agregados pela adição.|  
|Medidas calculadas|A ordem de resolução é definida para assegurar a adequação da medida calculada.|  
|Membros calculados|Regras normais se aplicam, quer dizer, a última ordem de resolução tem prioridade.|  
|Atribuições|As atribuições são agregadas de acordo com a função de agregação de medida. Se a função de agregação de medida for uma contagem distinta, a atribuição será somada.|  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna a soma do `Measures.[Order Quantity]` membro, agregado durante os primeiros oito meses do ano calendário 2003 contidos na `Date` dimensão, da **Adventure Works** cubo.  
  
```  
WITH MEMBER [Date].[Calendar].[First8Months2003] AS  
    Aggregate(  
        PeriodsToDate(  
            [Date].[Calendar].[Calendar Year],   
            [Date].[Calendar].[Month].[August 2003]  
        )  
    )  
SELECT   
    [Date].[Calendar].[First8Months2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
 O exemplo a seguir mostra a agregação durante os primeiros dois meses do segundo semestre do ano calendário 2003.  
  
```  
WITH MEMBER [Date].[Calendar].[First2MonthsSecondSemester2003] AS  
    Aggregate(  
        PeriodsToDate(  
            [Date].[Calendar].[Calendar Semester],   
            [Date].[Calendar].[Month].[August 2003]  
        )  
    )  
SELECT   
    [Date].[Calendar].[First2MonthsSecondSemester2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
 O exemplo a seguir retorna a contagem dos revendedores cujas vendas caíram ao longo do período anterior, com base em valores de Estado do membro, selecionados pelo usuário, avaliados usando a função Aggregate. O **Hierarchize** e **DrillDownLevel** funções são usadas para retornar valores por queda de vendas para categorias de produto na dimensão produto.  
  
```  
WITH MEMBER Measures.[Declining Reseller Sales] AS   
   Count(  
      Filter(  
         Existing(Reseller.Reseller.Reseller),   
            [Measures].[Reseller Sales Amount] < ([Measures].[Reseller Sales Amount],  
            [Date].Calendar.PrevMember)  
            )  
         )  
MEMBER [Geography].[State-Province].x AS   
   Aggregate (   
      {[Geography].[State-Province].&[WA]&[US],   
      [Geography].[State-Province].&[OR]&[US] }   
         )  
SELECT NON EMPTY Hierarchize (  
   AddCalculatedMembers (  
      {DrillDownLevel({[Product].[All Products]})}  
         )  
   )  
        DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS   
FROM [Adventure Works]  
WHERE ([Geography].[State-Province].x,   
    [Date].[Calendar].[Calendar Quarter].&[2003]&[4],  
    [Measures].[Declining Reseller Sales])  
```  
  
## <a name="see-also"></a>Consulte também  
 [PeriodsToDate &#40;MDX&#41;](../mdx/periodstodate-mdx.md)   
 [Children &#40;MDX&#41;](../mdx/children-mdx.md)   
 [Hierarchize &#40;MDX&#41;](../mdx/hierarchize-mdx.md)   
 [Count &#40;Set&#41; &#40;MDX&#41;](../mdx/count-set-mdx.md)   
 [Filter &#40;MDX&#41;](../mdx/filter-mdx.md)   
 [AddCalculatedMembers &#40;MDX&#41;](../mdx/addcalculatedmembers-mdx.md)   
 [DrilldownLevel &#40;MDX&#41;](../mdx/drilldownlevel-mdx.md)   
 [Properties &#40;MDX&#41;](../mdx/properties-mdx.md)   
 [PrevMember &#40;MDX&#41;](../mdx/prevmember-mdx.md)   
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
