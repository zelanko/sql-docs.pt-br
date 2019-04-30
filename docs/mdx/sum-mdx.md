---
title: Sum (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bdf003a65e6923acf2bbf5c17e93d412e2d194fa
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63241375"
---
# <a name="sum-mdx"></a>Função Sum (MDX)


  Retorna a soma de uma expressão numérica avaliada em um conjunto especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Sum( Set_Expression [ , Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão de conjunto de expressões multidimensionais (MDX) válida.  
  
 *Numeric_Expression*  
 Uma expressão numérica válida, geralmente uma linguagem MDX de coordenadas de célula, que retorna um número.  
  
## <a name="remarks"></a>Comentários  
 Se uma expressão numérica for especificada, a expressão numérica especificada será avaliada no conjunto e, em seguida, somada. Se uma expressão numérica não for especificada, o conjunto especificado será avaliado no contexto atual dos membros do conjunto e, em seguida, somado. Se a função SUM for aplicada a uma expressão não numérica, os resultados serão indefinidos.  
  
> [!NOTE]  
>  O Analysis Services ignora valores nulos ao calcular a soma de um conjunto de números.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna a soma dos Valores das Vendas do Revendedor para todos os membros da hierarquia de atributo Product.Category para os anos de calendário 2001 e 2002.  
  
```  
WITH MEMBER Measures.x AS SUM  
   ( { [Date].[Calendar Year].&[2001]  
         , [Date].[Calendar Year].&[2002] }  
      , [Measures].[Reseller Sales Amount]  
    )  
SELECT Measures.x ON 0  
,[Product].[Category].Members ON 1  
FROM [Adventure Works]  
```  
  
 O exemplo a seguir retorna a soma dos custos de frete mensais para as vendas de Internet do mês de julho de 2002 até o dia 20.  
  
```  
WITH MEMBER Measures.x AS SUM   
   (  
      MTD([Date].[Calendar].[Date].[July 20, 2002])  
     , [Measures].[Internet Freight Cost]  
     )  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
 O exemplo a seguir usa a palavra-chave WITH MEMBER e o **soma** função para definir um membro calculado na dimensão de medidas que contém a soma da medida vendas do revendedor para os membros Canadá e Estados Unidos das Hierarquia de atributo país na dimensão Geografia.  
  
```  
WITH MEMBER Measures.NorthAmerica AS SUM   
      (  
         {[Geography].[Country].&[Canada]  
            , [Geography].[Country].&[United States]}  
       ,[Measures].[Reseller Sales Amount]  
      )  
SELECT {[Measures].[NorthAmerica]} ON 0,  
[Product].[Category].members ON 1  
FROM [Adventure Works]  
```  
  
 Muitas vezes, o **soma** função é usada com o **CURRENTMEMBER** função ou funções, como **YTD** que retornam um conjunto que varia dependendo do currentmember de uma hierarquia. Por exemplo, a consulta seguinte retorna a soma da medida do Valor das Vendas pela Internet para todas as datas desde o início do ano civil à data exibida no eixo de Linhas:  
  
 `WITH MEMBER MEASURES.YTDSUM AS`  
  
 `SUM(YTD(), [Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount], MEASURES.YTDSUM} ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
