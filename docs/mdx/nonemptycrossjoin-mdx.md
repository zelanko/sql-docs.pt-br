---
title: NonEmptyCrossjoin (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7da56ac658f57d6eb664762f9dd94351df39fe0f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63456570"
---
# <a name="nonemptycrossjoin-mdx"></a>Função NonEmptyCrossjoin (MDX)


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
  
 *Count*  
 Uma expressão numérica válida que especifica o número de conjuntos a ser retornado.  
  
## <a name="remarks"></a>Comentários  
 O **NonEmptyCrossjoin** função retorna o produto cruzado de dois ou mais conjuntos como um conjunto, excluindo as tuplas vazias ou tuplas sem dados fornecidos por tabelas de fatos subjacentes. Devido a como o **NonEmptyCrossjoin** função funciona, calculado por todos os membros são excluídos automaticamente.  
  
 Se *contagem* não for especificado, a função cruza todos os conjuntos especificados e exclui membros vazios do conjunto resultante. Se um número de conjuntos for especificado, a função cruza os números de conjuntos especificados, começando com o primeiro conjunto especificado. O **NonEmptyCrossjoin** função usa todos os conjuntos restantes que são especificados nos conjuntos subsequentes, mas que não foram cruzado para determinar quais membros são considerados não vazios no conjunto cruzado resultante. O **NonEmptyCrossjoin** função respeita as **NON_EMPTY_BEHAVIOR** configuração de medidas calculadas.  
  
> [!IMPORTANT]  
>  Esta função é substituída e você não deveria usá-la; ela só existe para manter a compatibilidade com versões anteriores. Em vez disso, você deve usar o [Exists (MDX)](../mdx/exists-mdx.md) função com o argumento de nome do grupo de medidas ou o [NonEmpty (MDX)](../mdx/nonempty-mdx.md) função.  
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
