---
title: "Função NonEmptyCrossjoin (MDX) | Microsoft Docs"
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
f1_keywords: NONEMPTYCROSSJOIN
dev_langs: kbMDX
helpviewer_keywords: NonEmptyCrossjoin function
ms.assetid: 3dc9522d-9126-4f7a-b587-216fa7a06c62
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: ffa983a749245022d0815906fe8e17850f9aabdf
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="nonemptycrossjoin-mdx"></a>Função NonEmptyCrossjoin (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna um conjunto que contém o produto cruzado de um ou mais conjuntos, com exceção de tuplas vazias e tuplas sem dados da tabela de fatos associados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
NonEmptyCrossjoin(Set_Expression1 [ ,Set_Expression2,...] [,Count ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression1*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Set_Expression2*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Contagem*  
 Uma expressão numérica válida que especifica o número de conjuntos a ser retornado.  
  
## <a name="remarks"></a>Remarks  
 O **NonEmptyCrossjoin** função retorna o produto cruzado de dois ou mais conjuntos como um conjunto, excluindo tuplas vazias ou tuplas sem dados fornecidos por tabelas de fatos subjacentes. Devido ao funcionamento da **NonEmptyCrossjoin** função funciona, calculado por todos os membros são excluídos automaticamente.  
  
 Se *contagem* não for especificado, a função cruza todos os conjuntos especificados e exclui membros vazios do conjunto resultante. Se um número de conjuntos for especificado, a função cruza os números de conjuntos especificados, começando com o primeiro conjunto especificado. O **NonEmptyCrossjoin** função usa todos os conjuntos restantes que são especificados nos conjuntos subsequentes, mas que não foram cruzado para determinar quais membros são considerados não vazios no conjunto cruzado resultante. O **NonEmptyCrossjoin** função respeita o **NON_EMPTY_BEHAVIOR** configuração de medidas calculadas.  
  
> [!IMPORTANT]  
>  Esta função é substituída e você não deveria usá-la; ela só existe para manter a compatibilidade com versões anteriores. Em vez disso, você deve usar o [Exists (MDX)](../mdx/exists-mdx.md) função com o argumento de nome de grupo de medidas ou [NonEmpty (MDX)](../mdx/nonempty-mdx.md) função.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
