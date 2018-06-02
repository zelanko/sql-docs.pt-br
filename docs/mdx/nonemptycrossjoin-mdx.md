---
title: Função NonEmptyCrossjoin (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5d77262ce3f6cf4f9e9cb1720d42b1bcbd85f31f
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34580678"
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
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
