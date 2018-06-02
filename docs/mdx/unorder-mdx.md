---
title: Unorder (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9fe8d86b322aaf753f1ce45be2332095e2b85af9
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34581328"
---
# <a name="unorder-mdx"></a>Unorder (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
 O **Unorder** função é usada como uma dica para [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para otimização de consulta de processamento de conjunto. Se a ordem das tuplas em um conjunto é relevante para um cálculo ou consulta, usando o **Unorder** função pode fornecer um benefício de desempenho em tais casos. Por exemplo, o [NonEmpty (MDX)](../mdx/nonempty-mdx.md) função pode executar melhor quando o conjunto fornecido para essa função é desordenado do que se [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] precisar preservar a ordem, embora com [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)], o processador de consulta tenta executar essa função automaticamente para muitas funções, como **soma** e **agregação**. O benefício de usar **Unorder** só é devem ser observadas em conjuntos muito grandes que consistem em milhões de tuplas.  
  
## <a name="example"></a>Exemplo  
 O pseudocódigo a seguir ilustra a sintaxe dessa função.  
  
```  
NonEmpty (UnOrder (<set_expression>))  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
