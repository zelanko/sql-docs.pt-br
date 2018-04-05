---
title: CoalesceEmpty (MDX) | Microsoft Docs
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
- COALESCEEMPTY
dev_langs:
- kbMDX
helpviewer_keywords:
- CoalesceEmpty function
ms.assetid: c00dd739-44bc-4af6-9871-c7e1e3f3e5ba
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: d02d253d39a605405df747b49fd0a762913030f1
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="coalesceempty-mdx"></a>CoalesceEmpty (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Converte um valor de célula vazio a um valor de célula não vazio, que pode ser um número ou uma cadeia de caracteres.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Numeric syntax  
CoalesceEmpty( Numeric_Expression1 [ ,Numeric_Expression2,...n] )  
  
String syntax  
CoalesceEmpty(String_Expression1 [ ,String_Expression2,...n] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Numeric_Expression1*  
 Uma expressão numérica válida, geralmente uma linguagem MDX de coordenadas de célula, que retorna um número.  
  
 *Numeric_Expression2*  
 Uma expressão numérica válida que é normalmente um valor numérico especificado.  
  
 *String_Expression1*  
 Uma cadeia de caracteres válida, geralmente uma linguagem MDX de coordenadas de célula, que retorna uma cadeia de caracteres.  
  
 *String_Expression2*  
 Uma expressão de cadeia de caracteres que geralmente é um valor de cadeia de caracteres especificado, substituída por um NULL retornado pela primeira expressão de cadeia de caracteres.  
  
## <a name="remarks"></a>Remarks  
 Se uma ou mais expressões numéricas forem especificadas, o **CoalesceEmpty** função retorna o valor numérico da primeira expressão numérica (da esquerda para a direita) que pode ser resolvido para um valor não vazio. Se nenhuma das expressões numéricas especificadas puder ser resolvida para um valor não vazio, a função retornará o valor de célula vazio. Geralmente, o valor da segunda expressão numérica é o valor numérico substituído por um NULL retornado pela primeira expressão numérica.  
  
 Se uma ou mais expressões de cadeia de caracteres forem especificadas, a função retornará o valor de cadeia de caracteres da primeira expressão de cadeia de caracteres (da esquerda para a direita) que pode ser resolvido como um valor não vazio. Se nenhuma das expressões de cadeia de caracteres especificadas puder ser resolvida para um valor não vazio, a função retornará o valor de célula vazio. Geralmente, o valor da segunda expressão de cadeia de caracteres é um valor de cadeia de caracteres, substituída por um NULL retornado pela primeira expressão de cadeia de caracteres.  
  
 O **CoalesceEmpty** função só pode ter valores do mesmo tipo. Em outras palavras, todas as expressões de valores especificadas devem ser avaliadas apenas como tipos de dados numéricos ou um valor de célula vazio ou todas as expressões de valores especificados devem ser avaliadas como tipos de dados de cadeia de caracteres ou como um valor de célula vazio. Uma única chamada para essa função não pode incluir expressões de cadeias de caracteres e numéricas.  
  
 Para obter mais informações sobre células vazias, consulte a documentação OLE DB.  
  
## <a name="example"></a>Exemplo  
 A exemplo a seguir consulta o **Adventure Works** cubo. Esse exemplo retorna a quantidade de pedido de cada produto e a porcentagem de quantidades de pedidos por categoria. O **CoalesceEmpty** função garante que valores nulos são representados como zero (0) ao formatar os membros calculados.  
  
```  
WITH   
   MEMBER [Measures].[Order Percent by Category] AS  
   CoalesceEmpty(   
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
  
## <a name="see-also"></a>Consulte Também  
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
