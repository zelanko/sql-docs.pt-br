---
description: Barra asterisco (comentário) (DMX)
title: Barra asterisco (comentário) (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 011d72bfcb0b72d1b73579e81dc6f82e4d50da69
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500849"
---
# <a name="slash-star-comment-dmx"></a>Barra asterisco (comentário) (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Indica uma cadeia de caracteres de texto que o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] não deve executar. O servidor não avalia o texto entre os caracteres de comentário/* e \* /. É possível aninhar comentários em uma instrução DMX (Data Mining Extensions), incluí-los no final de uma linha de código ou inseri-los em uma linha separada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
/* Comment_Text */  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Comment_Text*  
 Cadeia de caracteres que contém o texto do comentário.  
  
## <a name="remarks"></a>Comentários  
 Os comentários de várias linhas precisam ser indicados por /* e \*/.  
  
 Não há comprimento máximo para comentários.  
  
 Para obter mais informações sobre como usar diferentes tipos de comentários no DMX, consulte [comentários &#40;&#41;DMX ](../dmx/comments-dmx.md).  
  
## <a name="see-also"></a>Consulte Também  
 [&#40;comentário de barra dupla&#41; &#40;DMX&#41;](../dmx/double-slash-comment-dmx.md)   
 [--Comentário de &#40;&#41; &#40;Resumo de&#41; do DMX](../dmx/comment-dmx-summary.md)   
 [Referência de operador de&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operadores &#40;&#41;DMX ](../dmx/operators-dmx.md)  
  
  
