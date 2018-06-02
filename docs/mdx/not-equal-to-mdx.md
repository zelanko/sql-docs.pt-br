---
title: '&lt;&gt; (Não igual a) (MDX) | Microsoft Docs'
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0ccccc64c4a6b2048a50ac1099c4a31b07537ae0
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34580548"
---
# <a name="ltgt-not-equal-to-mdx"></a>&lt;&gt; (Não igual a) (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Realiza uma operação de comparação que determina se o valor de uma linguagem MDX não é igual ao valor de outra linguagem MDX.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
MDX_Expression <> MDX_Expression  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *MDX_Expression*  
 Uma expressão MDX válida.  
  
## <a name="return-value"></a>Valor retornado  
 Um valor booliano baseado nas seguintes condições:  
  
-   **True** se ambos os parâmetros forem não nulos e o primeiro parâmetro não é igual ao segundo parâmetro.  
  
-   **False** se ambos os parâmetros forem não nulos e o primeiro parâmetro for igual ao segundo parâmetro.  
  
-   nulo se um ou os dois parâmetros forem avaliados como um valor nulo.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de operador MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
