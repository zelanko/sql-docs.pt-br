---
title: '&lt;&gt;(Diferente de) (MDX) | Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 032505ee0714bc10baa698b1a229e5456710c81d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68088326"
---
# <a name="ltgt-not-equal-to-mdx"></a>&lt;&gt;(Diferente de) LINGUAGEM


  Realiza uma operação de comparação que determina se o valor de uma linguagem MDX não é igual ao valor de outra linguagem MDX.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
MDX_Expression <> MDX_Expression  
```  
  
#### <a name="parameters"></a>parâmetros  
 *MDX_Expression*  
 Uma expressão MDX válida.  
  
## <a name="return-value"></a>Valor retornado  
 Um valor booliano baseado nas seguintes condições:  
  
-   **true** se ambos os parâmetros forem não nulos e o primeiro parâmetro não for igual ao segundo parâmetro.  
  
-   **false** se ambos os parâmetros forem não nulos e o primeiro parâmetro for igual ao segundo parâmetro.  
  
-   nulo se um ou os dois parâmetros forem avaliados como um valor nulo.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de operador MDX &#40;&#41;MDX](../mdx/mdx-operator-reference-mdx.md)  
  
  
