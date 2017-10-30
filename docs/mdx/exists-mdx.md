---
title: Existe (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- Exists function
ms.assetid: 1e1d93b5-5be6-421c-b82b-839538ea50b1
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 5483a7da135f6e486610d8a53e9dc23078a6cd3b
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="exists-mdx"></a>Exists (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna o conjunto de tuplas do primeiro conjunto especificado que existe com uma ou mais tuplas do segundo conjunto especificado. Essa função executa manualmente o que o auto exists executa automaticamente. Para obter mais informações sobre auto existem, consulte [principais conceitos em MDX &#40; Analysis Services &#41; ](../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md).  
  
 Se o valor opcional \<nome do grupo de medidas > for fornecido, a função retorna tuplas existentes com uma ou mais tuplas do segundo conjunto e as tuplas que associaram linhas na tabela de fatos do grupo de medidas especificado.  
  
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
  
1.  Linhas de grupo de medidas com medidas que contêm valores nulos contribuem para **Exists** quando o argumento MeasureGroupName é especificado. Esta é a diferença entre esta forma de Exists e a função Nonempty: se a propriedade NullProcessing dessas medidas for definida como Preserve, isso significará que as medidas mostrarão valores nulos quando forem executadas consultas nessa parte do cubo; NonEmpty sempre removerá as tuplas de um conjunto que tiverem valores de medida nulos, ao passo que Exists com o argumento MeasureGroupName não filtrará as tuplas que tiverem linhas de grupo de medidas associadas, mesmo que os valores de medida sejam nulos.  
  
2.  Se *MeasureGroupName* parâmetro é usado, os resultados dependerão se há medidas visíveis no grupo de medidas referenciado; se não há nenhum medidas visíveis no grupo de medidas referenciado EXISTS sempre retornará um conjunto vazio, independentemente dos valores de *Set_Expression1* e *Set_Expression2*.  
  
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
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)   
 [Crossjoin &#40; MDX &#41;](../mdx/crossjoin-mdx.md)   
 [NonEmptyCrossjoin &#40; MDX &#41;](../mdx/nonemptycrossjoin-mdx.md)   
 [NonEmpty &#40; MDX &#41;](../mdx/nonempty-mdx.md)   
 [IsEmpty &#40; MDX &#41;](../mdx/isempty-mdx.md)  
  
  

