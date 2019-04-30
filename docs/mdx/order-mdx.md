---
title: Order (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 43a75f4a42193c231c1acc710512b05537675991
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63277853"
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
 O **ordem** função pode ser hierárquica (conforme especificado, usando o **ASC** ou **DESC** sinalizador) ou não hierárquico (conforme especificado por meio o **BASC**  ou **BDESC** sinalizador; o **B** significa "quebra de hierarquia"). Se **ASC** ou **DESC** for especificado, o **ordem** função primeiro organizará os membros de acordo com sua posição na hierarquia e, em seguida, ordenará cada nível. Se **BASC** ou **BDESC** for especificado, o **ordem** função organiza os membros no conjunto, independentemente da hierarquia. Nenhum sinalizador for especificado, **ASC** é o padrão.  
  
 Se o **ordem** função é usada com um conjunto onde duas ou mais hierarquias são interjuntadas e o **DESC** sinalizador é usado, somente os membros da última hierarquia no conjunto são ordenados. Esta é uma alteração do Analysis Services 2000 onde foram ordenadas todas as hierarquias no conjunto.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna, do **Adventure Works** do cubo, o número de pedidos do revendedor para todos os trimestres do calendário da hierarquia da dimensão Date. O **ordem** função reordena o conjunto para o eixo de linhas. O **ordem** função ordena o conjunto por `[Reseller Order Count]` em ordem hierárquica descendente conforme determinado pela `[Calendar]` hierarquia.  
  
 `SELECT`  
  
 `Measures.[Reseller Order Count] ON COLUMNS,`  
  
 `Order(`  
  
 `[Date].[Calendar].[Calendar Quarter].MEMBERS`  
  
 `,Measures.[Reseller Order Count]`  
  
 `,DESC`  
  
 `) ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 Observe como neste exemplo, quando o **DESC** sinalizador é alterado para **BDESC**, a hierarquia é interrompida e a lista de trimestres do calendário é retornada sem consideração para a hierarquia:  
  
 `SELECT`  
  
 `Measures.[Reseller Order Count] ON COLUMNS,`  
  
 `Order(`  
  
 `[Date].[Calendar].[Calendar Quarter].MEMBERS`  
  
 `,Measures.[Reseller Order Count]`  
  
 `,BDESC`  
  
 `) ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 O exemplo a seguir retorna a medida Valor das Vendas do Revendedor para as cinco subcategorias principais de vendas dos produtos, independentemente da hierarquia, com base no Lucro Bruto do Revendedor. O **subconjunto** função é usada para retornar apenas as 5 primeiras tuplas no conjunto após o resultado é ordenado com o **ordem** função.  
  
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
  
 O exemplo a seguir usa o **classificação** função para classificar os membros da hierarquia cidade com base na medida vendas do revendedor e, em seguida, exibe-os em ordem de classificação. Usando o **ordem** o conjunto de membros da hierarquia cidade de função à primeira ordem, a classificação é feita apenas uma vez e, em seguida, seguida por uma verificação linear antes que está sendo apresentado na ordem de classificação.  
  
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
  
 O exemplo a seguir retorna o número de produtos no conjunto que são exclusivos, usando o **ordem** função para solicitar as tuplas não vazias antes de utilizar o **filtro** função. O **CurrentOrdinal** função é usada para comparar e eliminar associações.  
  
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
  
 Para entender como o **DESC** sinalizador funciona com conjuntos de tuplas, primeiro considere os resultados da consulta a seguir:  
  
```  
  
SELECT  
{[Measures].[Tax Amount]} ON 0,  
ORDER(  
[Sales Territory].[Sales Territory].[Group].MEMBERS  
,[Measures].[Tax Amount], DESC)  
ON 1  
FROM [Adventure Works]  
  
```  
  
 No eixo de linhas, você pode ver que os Sales Territory Groups foram colocados em ordem decrescente por Tax Amount, como segue: América do Norte, Europa, Pacific, NA. Agora veja o que acontece se nós interjuntarmos o conjunto de Sales Territory Groups com o conjunto de subcategorias de produtos e aplicar a **ordem** funcionar da mesma forma, da seguinte maneira:  
  
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
  
 Enquanto o conjunto de Product Subcategories foi colocado em decrescente ordem hierárquica, os Sales Territory Groups agora não são classificados e aparecem na ordem em que aparecem na hierarquia: Europa, NA, América do Norte e Pacífico. Isto é porque somente a última hierarquia no conjunto de tuplas, Product Subcategories, é classificado. Para reproduzir o comportamento do Analysis Services 2000, use uma série de aninhados **gerar** funções para classificar cada conjunto antes de interjuntar, por exemplo:  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
