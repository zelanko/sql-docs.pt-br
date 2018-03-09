---
title: Avg (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: AVG
dev_langs: kbMDX
helpviewer_keywords: Avg function [MDX]
ms.assetid: efe61272-c3eb-4a33-b231-e00c30be16aa
caps.latest.revision: "42"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 4972d38cb5cd52d0da7d76c6eb771520a89fb896
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="avg-mdx"></a>Avg (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Avalia um conjunto e retorna a média dos valores não vazios das células no conjunto, com base nas medidas no conjunto ou em uma medida especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Avg( Set_Expression [ , Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX válida que retorna um conjunto.  
  
 *Numeric_Expression*  
 Uma expressão numérica válida, geralmente uma linguagem MDX de coordenadas de célula, que retorna um número.  
  
## <a name="remarks"></a>Remarks  
 Se um conjunto de tuplas vazias ou um conjunto vazio for especificado, o **Avg** função retorna um valor vazio.  
  
 O **Avg** função calcula a média de valores não vazios de células no conjunto especificado pelo primeiro calcula a soma dos valores em células no conjunto especificado e, em seguida, dividindo a soma calculada pela contagem de células não vazias no conjunto especificado.  
  
> [!NOTE]  
>  O [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ignora nulos ao calcular o valor médio em um conjunto de números.  
  
 Se uma expressão numérica específica (normalmente uma medida) não for especificada, o **Avg** função calcula a média de cada medida dentro do contexto de consulta atual. Se uma medida específica for fornecida, o **Avg** função primeiro avalia a medida no conjunto e, em seguida, a função calcula a média com base na medida especificada.  
  
> [!NOTE]  
>  Ao usar o **CurrentMember** função em uma declaração de membro calculado, você deve especificar uma expressão numérica como não existe nenhuma medida padrão para a coordenada atual em tal contexto de consulta.  
  
 Para forçar a inclusão de células vazias, o aplicativo deve usar o [CoalesceEmpty](../mdx/coalesceempty-mdx.md) de função ou especificar uma opção válida *Numeric_Expression* que fornece um valor de zero (0) para valores vazios. Para obter mais informações sobre células vazias, consulte a documentação OLE DB.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna a média para uma medida em um determinado conjunto. Observe que a medida especificada pode ser a medida padrão para os membros do conjunto especificado ou uma medida especificada.  
  
 `WITH SET [NW Region] AS`  
  
 `{[Geography].[State-Province].[Washington]`  
  
 `, [Geography].[State-Province].[Oregon]`  
  
 `, [Geography].[State-Province].[Idaho]}`  
  
 `MEMBER [Geography].[Geography].[NW Region Avg] AS`  
  
 `AVG ([NW Region]`  
  
 `--Uncomment the line below to get an average by Reseller Gross Profit Margin`  
  
 `--otherwise the average will be by whatever the default measure is in the cube,`  
  
 `--or whatever measure is specified in the query`  
  
 `--, [Measures].[Reseller Gross Profit Margin]`  
  
 `)`  
  
 `SELECT [Date].[Calendar Year].[Calendar Year].Members ON 0`  
  
 `FROM [Adventure Works]`  
  
 `WHERE ([Geography].[Geography].[NW Region Avg])`  
  
 O exemplo a seguir retorna a média diária do `Measures.[Gross Profit Margin]` medida calculada nos dias de cada mês do ano fiscal de 2003, a partir de **Adventure Works** cubo. O **Avg** função calcula a média do conjunto de dias em que estão contidos em cada mês do `[Ship Date].[Fiscal Time]` hierarquia. A primeira versão do cálculo mostra o comportamento padrão da função Avg ao excluir os dias em que nenhuma venda foi registrada a partir da média e a segunda versão mostra como incluir os dias sem venda na média.  
  
 `WITH MEMBER Measures.[Avg Gross Profit Margin] AS`  
  
 `Avg(`  
  
 `Descendants(`  
  
 `[Ship Date].[Fiscal].CurrentMember,`  
  
 `[Ship Date].[Fiscal].[Date]`  
  
 `),`  
  
 `Measures.[Gross Profit Margin]`  
  
 `), format_String='percent'`  
  
 `MEMBER Measures.[Avg Gross Profit Margin Including Empty Days] AS`  
  
 `Avg(`  
  
 `Descendants(`  
  
 `[Ship Date].[Fiscal].CurrentMember,`  
  
 `[Ship Date].[Fiscal].[Date]`  
  
 `),`  
  
 `CoalesceEmpty(Measures.[Gross Profit Margin],0)`  
  
 `), Format_String='percent'`  
  
 `SELECT`  
  
 `{Measures.[Avg Gross Profit Margin],Measures.[Avg Gross Profit Margin Including Empty Days]} ON COLUMNS,`  
  
 `[Ship Date].[Fiscal].[Fiscal Year].Members ON ROWS`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
 `WHERE([Product].[Product Categories].[Product].&[344])`  
  
 O exemplo a seguir retorna a média diária do `Measures.[Gross Profit Margin]` medida calculada nos dias de cada semestre do ano fiscal de 2003, a partir de **Adventure Works** cubo.  
  
```  
WITH MEMBER Measures.[Avg Gross Profit Margin] AS  
   Avg(  
      Descendants(  
         [Ship Date].[Fiscal].CurrentMember,   
            [Ship Date].[Fiscal].[Date]  
      ),   
      Measures.[Gross Profit Margin]  
   )  
SELECT  
   Measures.[Avg Gross Profit Margin] ON COLUMNS,  
      [Ship Date].[Fiscal].[Fiscal Year].[FY 2003].Children ON ROWS  
FROM  
   [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
