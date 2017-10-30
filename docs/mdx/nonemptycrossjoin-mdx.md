---
title: "Função NonEmptyCrossjoin (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- NONEMPTYCROSSJOIN
dev_langs:
- kbMDX
helpviewer_keywords:
- NonEmptyCrossjoin function
ms.assetid: 3dc9522d-9126-4f7a-b587-216fa7a06c62
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 54ea9a17d94b73d5423384023d49e4c86771f072
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="nonemptycrossjoin-mdx"></a>Função NonEmptyCrossjoin (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 O **NonEmptyCrossjoin** função retorna o produto cruzado de dois ou mais conjuntos como um conjunto, excluindo tuplas vazias ou tuplas sem dados fornecidos por tabelas de fatos subjacentes. Devido ao funcionamento da **NonEmptyCrossjoin** função funciona, calculado por todos os membros são excluídos automaticamente.  
  
 Se *contagem* não for especificado, a função cruza todos os conjuntos especificados e exclui membros vazios do conjunto resultante. Se um número de conjuntos for especificado, a função cruza os números de conjuntos especificados, começando com o primeiro conjunto especificado. O **NonEmptyCrossjoin** função usa todos os conjuntos restantes que são especificados nos conjuntos subsequentes, mas que não foram cruzado para determinar quais membros são considerados não vazios no conjunto cruzado resultante. O **NonEmptyCrossjoin** função respeita o **NON_EMPTY_BEHAVIOR** configuração de medidas calculadas.  
  
> [!IMPORTANT]  
>  Esta função é substituída e você não deveria usá-la; ela só existe para manter a compatibilidade com versões anteriores. Em vez disso, você deve usar o [Exists (MDX)](../mdx/exists-mdx.md) função com o argumento de nome de grupo de medidas ou [NonEmpty (MDX)](../mdx/nonempty-mdx.md) função.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

