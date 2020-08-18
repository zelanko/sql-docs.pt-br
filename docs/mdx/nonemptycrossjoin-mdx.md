---
description: Função NonEmptyCrossjoin (MDX)
title: NonEmptyCrossjoin (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6fafaad2f6fa0f46d826bf94b26ceb6fdbe9df55
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471798"
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
 A função **NonEmptyCrossjoin** retorna o produto cruzado de dois ou mais conjuntos como um conjunto, excluindo tuplas ou tuplas vazias sem dados fornecidos por tabelas de fatos subjacentes. Devido a como a função **NonEmptyCrossjoin** funciona, todos os membros calculados são excluídos automaticamente.  
  
 Se *Count* não for especificado, a função cruzará todos os conjuntos especificados e excluirá Membros vazios do conjunto resultante. Se um número de conjuntos for especificado, a função cruza os números de conjuntos especificados, começando com o primeiro conjunto especificado. A função **NonEmptyCrossjoin** usa todos os conjuntos restantes que são especificados em conjuntos especificados subsequentes, mas que não foram adicionados entre si para determinar quais membros são considerados não vazios no conjunto de junção cruzada resultante. A função **NonEmptyCrossjoin** respeita a configuração **NON_EMPTY_BEHAVIOR** de medidas calculadas.  
  
> [!IMPORTANT]  
>  Esta função é substituída e você não deveria usá-la; ela só existe para manter a compatibilidade com versões anteriores. Em vez disso, você deve usar a função [Exists (MDX)](../mdx/exists-mdx.md) com o argumento Nome do grupo de medidas ou com a função não [vazia (MDX)](../mdx/nonempty-mdx.md) .  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
