---
title: CurrentMember (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CURRENTMEMBER
dev_langs:
- kbMDX
helpviewer_keywords:
- CurrentMember function
ms.assetid: 5da76496-7d13-4f17-9cee-3e1ef70c2d97
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: dc8b2cf387c9a094a0615b6e7a7ef7e2f4da381b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="currentmember-mdx"></a>Função CurrentMember (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna o membro atual ao longo de uma hierarquia especificada durante a iteração.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Hierarchy_Expression.CurrentMember  
```  
  
## <a name="arguments"></a>Argumentos  
 *Expressão_Hierarquia*  
 Uma linguagem MDX válida que retorna uma hierarquia.  
  
## <a name="remarks"></a>Remarks  
 Durante a iteração de um conjunto de membros de hierarquia, em cada etapa da iteração, o membro que está sendo operado é o membro atual. O **CurrentMember** função retorna esse membro.  
  
> [!IMPORTANT]  
>  Quando uma dimensão contém apenas uma única hierarquia visível, a hierarquia pode ser mencionada pelo nome da dimensão ou pelo nome da hierarquia porque o nome da dimensão é resolvido apenas na hierarquia visível. Por exemplo, `Measures.CurrentMember` é uma expressão MDX válida porque é resolvida na única hierarquia da dimensão Measures.  
  
## <a name="examples"></a>Exemplos  
 A consulta a seguir mostra como **Currentmember** pode ser usado para localizar o membro atual de hierarquias em colunas, linhas e eixo de fatia:  
  
 `WITH MEMBER MEASURES.CURRENTDATE AS`  
  
 `[Date].[Calendar].CURRENTMEMBER.NAME`  
  
 `MEMBER MEASURES.CURRENTPRODUCT AS`  
  
 `[Product].[Product Categories].CURRENTMEMBER.NAME`  
  
 `MEMBER MEASURES.CURRENTMEASURE AS`  
  
 `MEASURES.CURRENTMEMBER.NAME`  
  
 `MEMBER MEASURES.CURRENTCUSTOMER AS`  
  
 `[Customer].[Customer Geography].CURRENTMEMBER.NAME`  
  
 `SELECT`  
  
 `[Product].[Product Categories].[Category].MEMBERS`  
  
 `*`  
  
 `{MEASURES.CURRENTDATE, MEASURES.CURRENTPRODUCT,MEASURES.CURRENTMEASURE, MEASURES.CURRENTCUSTOMER}`  
  
 `ON 0,`  
  
 `[Date].[Calendar].MEMBERS`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 `WHERE([Customer].[Customer Geography].[Country].&[Australia])`  
  
 O membro atual é alterado em uma hierarquia usada em um eixo em uma consulta. Portanto, o membro atual em outras hierarquias na mesma dimensão que não são usados em um eixo também pode ser alterado; Esse comportamento é chamado de "auto-exists" e mais detalhes podem ser encontrados em [principais conceitos em MDX &#40;Analysis Services&#41;](../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md). Por exemplo, a consulta abaixo mostra como o membro atual na hierarquia Ano Civil da dimensão Data é alterado com o membro atual na hierarquia Calendário, quando este último é exibido no eixo Linhas:  
  
 `WITH MEMBER MEASURES.CURRENTYEAR AS`  
  
 `[Date].[Calendar Year].CURRENTMEMBER.NAME`  
  
 `SELECT`  
  
 `{MEASURES.CURRENTYEAR}`  
  
 `ON 0,`  
  
 `[Date].[Calendar].MEMBERS`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 **CurrentMember** é muito importante para que os cálculos reconheçam o contexto da consulta estão sendo usados no. O exemplo a seguir retorna a quantidade de pedidos de cada produto e a porcentagem da quantidade de pedidos por categoria e modelo, do **Adventure Works** cubo. O **CurrentMember** função identifica o produto cuja quantidade do pedido será usado durante o cálculo.  
  
```  
WITH   
   MEMBER [Measures].[Order Percent by Category] AS  
   CoalesceEmpty  
(   
      ([Product].[Product Categories].CurrentMember,  
        Measures.[Order Quantity]) /   
          (  
           Ancestor  
           ( [Product].[Product Categories].CurrentMember,   
             [Product].[Product Categories].[Category]  
           ), Measures.[Order Quantity]  
       ), 0  
   ), FORMAT_STRING='Percent'  
SELECT   
   {Measures.[Order Quantity],  
      [Measures].[Order Percent by Category]} ON COLUMNS,  
{[Product].[Product].Members} ON ROWS  
FROM [Adventure Works]  
WHERE {[Date].[Calendar Year].[Calendar Year].&[2003]}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
