---
title: Barra estrela (comentário) (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 5d0b929ba60915f116d9ff6843b4f20b3105a7ae
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67942842"
---
# <a name="slash-star-comment-dmx"></a>Barra estrela (comentário) (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Indica uma cadeia de caracteres de texto que o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] não deve executar. O servidor não avalia o texto entre os caracteres de comentário / * e \*/. É possível aninhar comentários em uma instrução DMX (Data Mining Extensions), incluí-los no final de uma linha de código ou inseri-los em uma linha separada.  
  
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
  
 Para obter mais informações sobre como usar tipos diferentes de comentários em DMX, consulte [comentários &#40;DMX&#41;](../dmx/comments-dmx.md).  
  
## <a name="see-also"></a>Consulte também  
 [Barra dupla &#40;comentário&#41; &#40;DMX&#41;](../dmx/double-slash-comment-dmx.md)   
 [– &#40;Comentário&#41; &#40;DMX&#41; resumo](../dmx/comment-dmx-summary.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de operador](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operators &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
