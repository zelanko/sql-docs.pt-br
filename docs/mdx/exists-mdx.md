---
title: Existe (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 781c03283c39ab5ec100ba7f7d83b3cbe19a7c19
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139180"
---
# <a name="exists-mdx"></a>Exists (MDX)


  Retorna o conjunto de tuplas do primeiro conjunto especificado que existe com uma ou mais tuplas do segundo conjunto especificado. Essa função executa manualmente o que o auto exists executa automaticamente. Para obter mais informações sobre auto exists, consulte [principais conceitos em MDX &#40;Analysis Services&#41;](../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md).  
  
 Se o opcional \<nome do grupo de medidas > for fornecido, a função retorna as tuplas existentes com uma ou mais tuplas do segundo conjunto e elas terão linhas na tabela de fatos do grupo de medidas especificado associadas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Exists( Set_Expression1 , Set_Expression2 [, MeasureGroupName] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression1*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Set_Expression2*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *MeasureGroupName*  
 Uma expressão de cadeia de caracteres válida que especifica um nome de grupo de medidas.  
  
## <a name="remarks"></a>Comentários  
  
1.  Linhas de grupo de medidas com medidas que contêm valores nulos contribuem para **Exists** quando o argumento MeasureGroupName é especificado. Essa é a diferença entre essa forma de Exists e a função Nonempty: se a propriedade NullProcessing dessas medidas for definida como Preserve, isso significa que as medidas mostrará valores nulos quando as consultas são executadas em relação a essa parte do cubo; NonEmpty sempre removerá as tuplas de um conjunto que têm valores de medida nulos, ao passo que Exists com o argumento MeasureGroupName não filtrará as tuplas que associaram linhas do grupo de medidas, mesmo se os valores de medida são Null.  
  
2.  Se *MeasureGroupName* parâmetro é usado, os resultados dependerão se há medidas visíveis no grupo de medidas referenciado; se não há nenhum medidas visíveis no grupo de medidas referenciado, então EXISTS sempre retornará um conjunto vazio, independentemente dos valores de *Set_Expression1* e *Set_Expression2*.  
  
## <a name="examples"></a>Exemplos  
 Clientes que moram na Califórnia:  
  
```  
SELECT [Measures].[Internet Sales Amount] ON 0,  
EXISTS(  
[Customer].[Customer].[Customer].MEMBERS  
, {[Customer].[State-Province].&[CA]&[US]}  
) ON 1   
FROM [Adventure Works]  
  
```  
  
 Clientes que moram na Califórnia com vendas:  
  
```  
SELECT [Measures].[Internet Sales Amount] ON 0,  
EXISTS(  
[Customer].[Customer].[Customer].MEMBERS  
, {[Customer].[State-Province].&[CA]&[US]}  
, "Internet Sales") ON 1   
FROM [Adventure Works]  
  
```  
  
 Clientes com vendas:  
  
```  
SELECT [Measures].[Internet Sales Amount] ON 0,  
EXISTS(  
[Customer].[Customer].[Customer].MEMBERS  
, , "Internet Sales") ON 1   
FROM [Adventure Works]  
  
```  
  
 Clientes que compraram bicicletas:  
  
```  
SELECT [Measures].[Internet Sales Amount] ON 0,  
EXISTS(  
[Customer].[Customer].[Customer].MEMBERS  
, {[Product].[Product Categories].[Category].&[1]}  
, "Internet Sales") ON 1   
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [Junção cruzada &#40;MDX&#41;](../mdx/crossjoin-mdx.md)   
 [NonEmptyCrossjoin &#40;MDX&#41;](../mdx/nonemptycrossjoin-mdx.md)   
 [Não vazia &#40;MDX&#41;](../mdx/nonempty-mdx.md)   
 [IsEmpty &#40;MDX&#41;](../mdx/isempty-mdx.md)  
  
  
