---
title: -(Comentário) (DMX) resumo | Microsoft Docs
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
- double hyphens
- -- (comment character)
ms.assetid: 487b580b-5b81-4e52-8868-4fa809e4ef58
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 40b4189e6ce20c49ad7aab24b53ea41900b022f5
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="---comment-dmx-summary"></a>– Resumo (comentário) (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Indica uma cadeia de caracteres de texto que o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] não deve executar. É possível aninhar comentários em uma instrução DMX (Data Mining Extensions), incluí-los no final de uma linha de código ou inseri-los em uma linha separada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
-- Comment_Text      
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Comment_Text*  
 Cadeia de caracteres que contém o texto do comentário.  
  
## <a name="remarks"></a>Remarks  
 Use esse operador para comentários de linha única ou aninhados. Os comentários inseridos com o uso de -- são delimitados pelo caractere de nova linha.  
  
 Não há comprimento máximo para comentários.  
  
 Para obter mais informações sobre como usar tipos diferentes de comentários em DMX, consulte [comentários &#40; DMX &#41;](../dmx/comments-dmx.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Barra estrela &#40; Comentário &#41; &#40; DMX &#41;](../dmx/slash-star-comment-dmx.md)   
 [Barras duplas &#40; Comentário &#41; &#40; DMX &#41;](../dmx/double-slash-comment-dmx.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Referência de operador](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operadores &#40; DMX &#41;](../dmx/operators-dmx.md)  
  
  
