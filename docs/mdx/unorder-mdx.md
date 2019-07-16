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
ms.openlocfilehash: 954a71c8ca2e96d905892d77ff12b7270deded5f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68097264"
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
  
## <a name="remarks"></a>Comentários  
 O **Unorder=1=«conjunto»=retorna** função remove qualquer ordenação imposta sobre as tuplas contidas no conjunto por qualquer outra função ou instrução, como o [ordem](../mdx/order-mdx.md) função. A ordenação das tuplas no conjunto retornado pela **Unorder=1=«conjunto»=retorna** função é indeterminada.  
  
 O **Unorder=1=«conjunto»=retorna** função é usada como uma dica para otimização de consulta para o processamento de conjunto. Se a ordem das tuplas em um conjunto não é importante para um cálculo ou consulta, usando o **Unorder=1=«conjunto»=retorna** função pode fornecer um benefício de desempenho em tais casos. Por exemplo, o [NonEmpty (MDX)](../mdx/nonempty-mdx.md) função terá melhor desempenho quando o conjunto fornecido para essa função é desordenado do que se [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] precisar preservar a ordem, embora com [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)], o processador de consultas tenta executar Essa função automaticamente para muitas funções, como **soma** e **agregação**. O benefício de desempenho do uso **Unorder=1=«conjunto»=retorna** é só devem ser observadas em conjuntos muito grandes que consistem em milhões de tuplas.  
  
## <a name="example"></a>Exemplo  
 O pseudocódigo a seguir ilustra a sintaxe dessa função.  
  
```  
NonEmpty (UnOrder (<set_expression>))  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
