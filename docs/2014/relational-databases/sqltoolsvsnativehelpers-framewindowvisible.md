---
title: FrameWindowVisible | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 9091d714-98bc-43ec-b8d1-9c892cb57f19
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 789445b46712ebfd832a5ccc28f078d8993d5901
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2018
ms.locfileid: "34423503"
---
# <a name="framewindowvisible"></a>FrameWindowVisible
  Propriedade que especifica se uma determinada moldura de janela é visível. O método auxiliar é usado no código gerenciado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
BOOL WINAPI IsFrameWindowVisible(IVsWindowFrame* frame)  
{  
    if (NULL == frame)  
    {  
        return FALSE;  
    }  
  
    return S_OK == frame->IsVisible();  
}  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *quadro*  
  
 Ponteiro IVsWindowFrame* para um WindowFrame do Visual Studio.  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor booliano que especifica se a moldura da janela especificada por *frame* é visível.  
  

<!-- Necessary temporarily. GeneMi, 2018-05-01.
     But 'release-sql2014-migration' should win the Conflict Resolution later in May, because this will then be a good link!
## See Also  
 [SqlToolsVSNativeHelpers](sqltoolsvsnativehelpers.md)  
-->
  
  