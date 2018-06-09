---
title: Unorder (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3b5e360c8f15eafba2b4565ca41a557c9e1ceda9
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34743445"
---
# <a name="unorder-mdx"></a>Unorder (MDX)


  Remove qualquer classificação forçada de um conjunto especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Unorder(Set_Expression)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
## <a name="remarks"></a>Remarks  
 O **Unorder** função remove qualquer ordenação imposta sobre as tuplas contidas no conjunto por qualquer outra função ou instrução, como o [ordem](../mdx/order-mdx.md) função. A ordem das tuplas no conjunto retornado pelo **Unorder** função é indeterminada.  
  
 O **Unorder** função é usada como uma dica para otimização de consulta para o processamento de conjunto. Se a ordem das tuplas em um conjunto é relevante para um cálculo ou consulta, usando o **Unorder** função pode fornecer um benefício de desempenho em tais casos. Por exemplo, o [NonEmpty (MDX)](../mdx/nonempty-mdx.md) função pode executar melhor quando o conjunto fornecido para essa função é desordenado do que se [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] precisar preservar a ordem, embora com [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)], o processador de consulta tenta executar essa função automaticamente para muitas funções, como **soma** e **agregação**. O benefício de usar **Unorder** só é devem ser observadas em conjuntos muito grandes que consistem em milhões de tuplas.  
  
## <a name="example"></a>Exemplo  
 O pseudocódigo a seguir ilustra a sintaxe dessa função.  
  
```  
NonEmpty (UnOrder (<set_expression>))  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
