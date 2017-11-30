---
title: Unorder (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: UNORDER
dev_langs: kbMDX
helpviewer_keywords: Unorder function
ms.assetid: a805df2a-6320-45bc-989f-90e85faf027f
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 84bdcc8bff38451389dffc2b98f0f66ebdd50e70
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
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
  
## <a name="remarks"></a>Comentários  
 O **Unorder** função remove qualquer ordenação imposta sobre as tuplas contidas no conjunto por qualquer outra função ou instrução, como o [ordem](../mdx/order-mdx.md) função. A ordem das tuplas no conjunto retornado pelo **Unorder** função é indeterminada.  
  
 O **Unorder** função é usada como uma dica para [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para otimização de consulta de processamento de conjunto. Se a ordem das tuplas em um conjunto é relevante para um cálculo ou consulta, usando o **Unorder** função pode fornecer um benefício de desempenho em tais casos. Por exemplo, o [NonEmpty (MDX)](../mdx/nonempty-mdx.md) função pode executar melhor quando o conjunto fornecido para essa função é desordenado do que se [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] precisar preservar a ordem, embora com [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)], o processador de consulta tenta executar essa função automaticamente para muitas funções, como **soma** e **agregação**. O benefício de usar **Unorder** só é devem ser observadas em conjuntos muito grandes que consistem em milhões de tuplas.  
  
## <a name="example"></a>Exemplo  
 O pseudocódigo a seguir ilustra a sintaxe dessa função.  
  
```  
NonEmpty (UnOrder (<set_expression>))  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
