---
title: Barra de estrela (comentário) (DMX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- commenting characters
- forward slash-asterisk character pairs
- /*...*/ (comment)
ms.assetid: 163976cc-aa47-4eda-bd98-03c1a397f80e
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: ad69726d5cdba7b421c33bdde86f46c187af4049
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="slash-star-comment-dmx"></a>Estrela de barra (comentário) (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Indica uma cadeia de caracteres de texto que o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] não deve executar. O servidor não avalia o texto entre os caracteres de comentário / * e \*/. É possível aninhar comentários em uma instrução DMX (Data Mining Extensions), incluí-los no final de uma linha de código ou inseri-los em uma linha separada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
/* Comment_Text */  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Comment_Text*  
 Cadeia de caracteres que contém o texto do comentário.  
  
## <a name="remarks"></a>Remarks  
 Os comentários de várias linhas precisam ser indicados por /* e \*/.  
  
 Não há comprimento máximo para comentários.  
  
 Para obter mais informações sobre como usar tipos diferentes de comentários em DMX, consulte [comentários &#40;DMX&#41;](../dmx/comments-dmx.md).  
  
## <a name="see-also"></a>Consulte também  
 [Barras duplas &#40;comentário&#41; &#40;DMX&#41;](../dmx/double-slash-comment-dmx.md)   
 [– &#40;Comentário&#41; &#40;DMX&#41; resumo](../dmx/comment-dmx-summary.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de operador](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operadores &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
