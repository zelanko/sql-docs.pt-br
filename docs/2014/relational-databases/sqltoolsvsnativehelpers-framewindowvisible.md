---
title: FrameWindowVisible | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: 9091d714-98bc-43ec-b8d1-9c892cb57f19
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 414f1a03ea87f6cc6b0916a0122ca2a66d5855a2
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85060189"
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
  
#### <a name="parameters"></a>parâmetros  
 *quadro*  
  
 Ponteiro IVsWindowFrame* para um WindowFrame do Visual Studio.  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor booliano que especifica se a moldura da janela especificada por *frame* é visível.  
  

<!-- Necessary temporarily. GeneMi, 2018-05-01.
     But 'release-sql2014-migration' should win the Conflict Resolution later in May, because this will then be a good link!
## See Also  
 [SqlToolsVSNativeHelpers](sqltoolsvsnativehelpers.md)  
-->
  
  
