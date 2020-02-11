---
title: CoalesceEmpty (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f760220b02396591e684a83305111e487908d19b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68006307"
---
# <a name="coalesceempty-mdx"></a>CoalesceEmpty (MDX)


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
  
## <a name="remarks"></a>Comentários  
 Se uma ou mais expressões numéricas forem especificadas, a função **CoalesceEmpty** retornará o valor numérico da primeira expressão numérica (da esquerda para a direita) que pode ser resolvida como um valor não vazio. Se nenhuma das expressões numéricas especificadas puder ser resolvida para um valor não vazio, a função retornará o valor de célula vazio. Geralmente, o valor da segunda expressão numérica é o valor numérico substituído por um NULL retornado pela primeira expressão numérica.  
  
 Se uma ou mais expressões de cadeia de caracteres forem especificadas, a função retornará o valor de cadeia de caracteres da primeira expressão de cadeia de caracteres (da esquerda para a direita) que pode ser resolvido como um valor não vazio. Se nenhuma das expressões de cadeia de caracteres especificadas puder ser resolvida para um valor não vazio, a função retornará o valor de célula vazio. Geralmente, o valor da segunda expressão de cadeia de caracteres é um valor de cadeia de caracteres, substituída por um NULL retornado pela primeira expressão de cadeia de caracteres.  
  
 A função **CoalesceEmpty** só pode receber valores do mesmo tipo. Em outras palavras, todas as expressões de valores especificadas devem ser avaliadas apenas como tipos de dados numéricos ou um valor de célula vazio ou todas as expressões de valores especificados devem ser avaliadas como tipos de dados de cadeia de caracteres ou como um valor de célula vazio. Uma única chamada para essa função não pode incluir expressões de cadeias de caracteres e numéricas.  
  
 Para obter mais informações sobre células vazias, consulte a documentação OLE DB.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir consulta o cubo **Adventure Works** . Esse exemplo retorna a quantidade de pedido de cada produto e a porcentagem de quantidades de pedidos por categoria. A função **CoalesceEmpty** garante que os valores nulos sejam representados como zero (0) ao formatar os membros calculados.  
  
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
 [Referência de função MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)  
  
  
