---
title: Exists (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ba2cef1cfb95319cbe0aff827cb251ff7e2317c2
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893616"
---
# <a name="exists-mdx"></a>Exists (MDX)


  Retorna o conjunto de tuplas do primeiro conjunto especificado que existe com uma ou mais tuplas do segundo conjunto especificado. Essa função executa manualmente o que o auto exists executa automaticamente. Para obter mais informações sobre a existência automática, consulte os [principais &#40;conceitos&#41;em MDX Analysis Services](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services).  
  
 Se o nome \<do grupo de medidas opcional > for fornecido, a função retornará tuplas que existem com uma ou mais tuplas do segundo conjunto e as tuplas que têm linhas associadas na tabela de fatos do grupo de medidas especificado.  
  
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
  
1.  As linhas do grupo de medidas com medidas que contêm valores nulos contribuem para **existir** quando o argumento MeasureGroupName for especificado. Essa é a diferença entre essa forma de Exists e a função não vazia: se a Propriedade NullProcessing dessas medidas estiver definida como preserve, isso significa que as medidas mostrarão valores nulos quando as consultas forem executadas nessa parte do cubo; Não vazio sempre removerá tuplas de um conjunto que tem valores de medida nulos, enquanto existirá com o argumento MeasureGroupname não filtrará tuplas que têm linhas de grupo de medidas associadas, mesmo que os valores de medida sejam nulos.  
  
2.  Se o parâmetro MeasureGroupName for usado, os resultados dependerão de se há medidas visíveis no grupo de medidas referenciado; Se não houver nenhuma medida visível no grupo de medidas referenciado, EXISTa sempre retornará um conjunto vazio, independentemente dos valores de *Set_Expression1* e *Set_Expression2*.  
  
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
 [MDX &#40;de interjunção&#41;](../mdx/crossjoin-mdx.md)   
 [NonEmptyCrossjoin &#40;MDX&#41;](../mdx/nonemptycrossjoin-mdx.md)   
 [MDX não &#40;vazia&#41;](../mdx/nonempty-mdx.md)   
 [IsEmpty &#40;MDX&#41;](../mdx/isempty-mdx.md)  
  
  
