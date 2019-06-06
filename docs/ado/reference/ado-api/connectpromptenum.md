---
title: ConnectPromptEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ConnectPromptEnum
helpviewer_keywords:
- ConnectPromptEnum enumeration [ADO]
ms.assetid: 21026e24-62b7-4cc9-8aef-62c1fc6cba75
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 40ce74748e15a2715de26e813007e00be0c33729
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66698597"
---
# <a name="connectpromptenum"></a>ConnectPromptEnum
Especifica se uma caixa de diálogo deve ser exibida para solicitar parâmetros ausentes ao abrir uma conexão a uma fonte de dados.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adPromptAlways**|1|Sempre prompts.|  
|**adPromptComplete**|2|Solicita que se forem necessárias mais informações.|  
|**adPromptCompleteRequired**|3|Avisa se mais informações são necessárias, mas os parâmetros opcionais não são permitidos.|  
|**adPromptNever**|4|Nunca prompts.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Package: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.ConnectPrompt.ALWAYS|  
|AdoEnums.ConnectPrompt.COMPLETE|  
|AdoEnums.ConnectPrompt.COMPLETEREQUIRED|  
|AdoEnums.ConnectPrompt.NEVER|  
  
## <a name="applies-to"></a>Aplica-se a  
 [Solicitar a propriedade dinâmica (ADO)](../../../ado/reference/ado-api/prompt-property-dynamic-ado.md)
