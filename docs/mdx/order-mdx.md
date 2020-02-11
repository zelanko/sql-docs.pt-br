---
title: Ordem (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d540b299fd08aa78576b19040a4cfafb9046ae7c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68055684"
---
# <a name="order-mdx"></a>Order (MDX)


  Organiza membros de um conjunto especificado, preservando opcionalmente ou quebrando a hierarquia.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Numeric expression syntax  
Order(Set_Expression, Numeric_Expression   
[ , { ASC | DESC | BASC | BDESC } ] )  
  
String expression syntax  
Order(Set_Expression, String_Expression   
[ , { ASC | DESC | BASC | BDESC } ] )  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Numeric_Expression*  
 Uma expressão numérica válida, geralmente uma linguagem MDX de coordenadas de célula, que retorna um número.  
  
 *String_Expression*  
 Uma expressão de cadeia de caracteres válida, geralmente uma expressão MDX válida de coordenadas de célula, que retorna um número expresso como uma cadeia de caracteres.  
  
## <a name="remarks"></a>Comentários  
 A função **Order** pode ser hierárquica (conforme especificado usando o sinalizador **ASC** ou **desc** ) ou nonhierarquicamente (conforme especificado usando o sinalizador **BASC** ou **BDESC** ; o **B** significa "hierarquia de interrupção"). Se **ASC** ou **desc** for especificado, a função **Order** primeiro organizará os membros de acordo com sua posição na hierarquia e, em seguida, ordenará cada nível. Se **BASC** ou **BDESC** for especificado, a função **Order** organizará os membros no conjunto sem considerar a hierarquia. Em nenhum sinalizador é especificado, **ASC** é o padrão.  
  
 Se a função **Order** for usada com um conjunto em que duas ou mais hierarquias forem crossjoined e o sinalizador **desc** for usado, somente os membros da última hierarquia no conjunto serão ordenados. Esta é uma alteração do Analysis Services 2000 onde foram ordenadas todas as hierarquias no conjunto.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna, do cubo **Adventure Works** , o número de pedidos de revendedores de todos os trimestres de calendário da hierarquia de datas na dimensão de data. A função **Order** reordena o conjunto para o eixo ROWS. A função **Order** ordena o conjunto por `[Reseller Order Count]` em ordem hierárquica decrescente conforme determinado pela `[Calendar]` hierarquia.  
  
 `SELECT`  
  
 `Measures.[Reseller Order Count] ON COLUMNS,`  
  
 `Order(`  
  
 `[Date].[Calendar].[Calendar Quarter].MEMBERS`  
  
 `,Measures.[Reseller Order Count]`  
  
 `,DESC`  
  
 `) ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 Observe como neste exemplo, quando o sinalizador **desc** é alterado para **BDESC**, a hierarquia é quebrada e a lista de trimestres de calendário é retornada sem considerar a hierarquia:  
  
 `SELECT`  
  
 `Measures.[Reseller Order Count] ON COLUMNS,`  
  
 `Order(`  
  
 `[Date].[Calendar].[Calendar Quarter].MEMBERS`  
  
 `,Measures.[Reseller Order Count]`  
  
 `,BDESC`  
  
 `) ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 O exemplo a seguir retorna a medida Valor das Vendas do Revendedor para as cinco subcategorias principais de vendas dos produtos, independentemente da hierarquia, com base no Lucro Bruto do Revendedor. A função **subconjunto** é usada para retornar apenas as 5 primeiras tuplas no conjunto depois que o resultado é ordenado usando a função **Order** .  
  
 `SELECT Subset`  
  
 `(Order`  
  
 `([Product].[Product Categories].[SubCategory].members`  
  
 `,[Measures].[Reseller Gross Profit]`  
  
 `,BDESC`  
  
 `)`  
  
 `,0`  
  
 `,5`  
  
 `) ON 0`  
  
 `FROM [Adventure Works]`  
  
 O exemplo a seguir usa a função **Rank** para classificar os membros da hierarquia cidade, com base na medida valor das vendas do revendedor e, em seguida, os exibe em ordem classificada. Usando a função **Order** para primeiro ordenar o conjunto de membros da hierarquia City, a classificação é feita apenas uma vez e seguida por uma verificação linear antes de ser apresentada na ordem classificada.  
  
```  
WITH   
SET OrderedCities AS Order  
   ([Geography].[City].[City].members  
   , [Measures].[Reseller Sales Amount], BDESC  
   )  
MEMBER [Measures].[City Rank] AS Rank  
   ([Geography].[City].CurrentMember, OrderedCities)  
SELECT {[Measures].[City Rank],[Measures].[Reseller Sales Amount]}  ON 0   
,Order  
   ([Geography].[City].[City].MEMBERS  
   ,[City Rank], ASC)  
    ON 1  
FROM [Adventure Works]  
```  
  
 O exemplo a seguir retorna o número de produtos no conjunto que são exclusivos, usando a função **Order** para ordenar as tuplas não vazias antes de utilizar a função de **filtro** . A função **CurrentOrdinal** é usada para comparar e eliminar os vínculos.  
  
```  
WITH MEMBER [Measures].[PrdTies] AS Count  
   (Filter  
      (Order  
        (NonEmpty  
          ([Product].[Product].[Product].Members  
          , {[Measures].[Reseller Order Quantity]}  
          )  
       , [Measures].[Reseller Order Quantity]  
       , BDESC  
       ) AS OrdPrds  
    , (OrdPrds.CurrentOrdinal < OrdPrds.Count   
       AND [Measures].[Reseller Order Quantity] =   
          ( [Measures].[Reseller Order Quantity]  
            , OrdPrds.Item  
               (OrdPrds.CurrentOrdinal  
               )  
            )  
         )  
         OR (OrdPrds.CurrentOrdinal > 1   
            AND [Measures].[Reseller Order Quantity] =   
               ([Measures].[Reseller Order Quantity]  
               , OrdPrds.Item  
                  (OrdPrds.CurrentOrdinal-2)  
                )  
             )  
          )  
       )  
SELECT {[Measures].[PrdTies]} ON 0  
FROM [Adventure Works]  
```  
  
 Para entender como o sinalizador **desc** funciona com conjuntos de tuplas, primeiro considere os resultados da consulta a seguir:  
  
```  
  
SELECT  
{[Measures].[Tax Amount]} ON 0,  
ORDER(  
[Sales Territory].[Sales Territory].[Group].MEMBERS  
,[Measures].[Tax Amount], DESC)  
ON 1  
FROM [Adventure Works]  
  
```  
  
 No eixo de Linhas, você pode consultar que os Sales Territory Groups foram colocados em ordem decrescente por Tax Amount, como segue: North America, Europe, Pacific, NA. Agora, veja o que acontece se interferirmos o conjunto de grupos de regiões de vendas com o conjunto de subcategorias de produtos e aplicarei a função **Order** da mesma forma, da seguinte maneira:  
  
```  
  
SELECT  
{[Measures].[Tax Amount]} ON 0,  
ORDER(  
[Sales Territory].[Sales Territory].[Group].MEMBERS  
*  
{[Product].[Product Categories].[subCategory].Members}  
,[Measures].[Tax Amount], DESC)  
ON 1  
FROM [Adventure Works]  
  
```  
  
 Enquanto o conjunto de Product Subcategories foi colocado em ordem decrescente e hierárquica, os Sales Territory Groups agora não são classificados e aparecem na ordem que eles aparecem na hierarquia: Europe, NA, North America e Pacific. Isto é porque somente a última hierarquia no conjunto de tuplas, Product Subcategories, é classificado. Para reproduzir o comportamento do Analysis Services 2000, use uma série de funções de **geração** aninhadas para classificar cada conjunto antes de ser crossjoined, por exemplo:  
  
```  
  
SELECT  
{[Measures].[Tax Amount]} ON 0,  
GENERATE(  
ORDER(  
[Sales Territory].[Sales Territory].[Group].MEMBERS  
,[Measures].[Tax Amount], DESC)  
,  
ORDER(  
[Sales Territory].[Sales Territory].CURRENTMEMBER  
*  
{[Product].[Product Categories].[subCategory].Members}  
,[Measures].[Tax Amount], DESC))  
ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de função MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)  
  
  
