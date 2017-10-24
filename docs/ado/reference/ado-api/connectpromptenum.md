---
title: ConnectPromptEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- ConnectPromptEnum
helpviewer_keywords:
- ConnectPromptEnum enumeration [ADO]
ms.assetid: 21026e24-62b7-4cc9-8aef-62c1fc6cba75
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8ae0c2179e321e521a86fdc76e5f8978ab4ab747
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="connectpromptenum"></a>ConnectPromptEnum
Especifica se deve ser exibida uma caixa de diálogo para solicitar parâmetros ausentes ao abrir uma conexão com uma fonte de dados.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adPromptAlways**|1|Solicita sempre.|  
|**adPromptComplete**|2|Avisa se são necessárias mais informações.|  
|**adPromptCompleteRequired**|3|Avisa se são necessárias mais informações, mas não são permitidos parâmetros opcionais.|  
|**adPromptNever**|4|Nunca prompts.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC equivalente  
 Pacote: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.ConnectPrompt.ALWAYS|  
|AdoEnums.ConnectPrompt.COMPLETE|  
|AdoEnums.ConnectPrompt.COMPLETEREQUIRED|  
|AdoEnums.ConnectPrompt.NEVER|  
  
## <a name="applies-to"></a>Aplica-se a  
 [Solicitar a propriedade dinâmica (ADO)](../../../ado/reference/ado-api/prompt-property-dynamic-ado.md)

