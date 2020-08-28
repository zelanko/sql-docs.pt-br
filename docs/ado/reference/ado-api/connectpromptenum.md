---
description: ConnectPromptEnum
title: ConnectPromptEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 171cc7706cc00b48c3373a0e40d5de221d4d00ce
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974677"
---
# <a name="connectpromptenum"></a>ConnectPromptEnum
Especifica se uma caixa de diálogo deve ser exibida para solicitar parâmetros ausentes ao abrir uma conexão com uma fonte de dados.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adPromptAlways**|1|Solicita sempre.|  
|**adPromptComplete**|2|Solicita se mais informações forem necessárias.|  
|**adPromptCompleteRequired**|3|Solicita se mais informações são necessárias, mas parâmetros opcionais não são permitidos.|  
|**adPromptNever**|4|Nunca solicita.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums. ConnectPrompt. ALWAYs|  
|AdoEnums. ConnectPrompt. COMPLETE|  
|AdoEnums.ConnectPrompt.COMPLETEREQUIRED|  
|AdoEnums. ConnectPrompt. NEVEr|  
  
## <a name="applies-to"></a>Aplica-se A  
 [Solicitar a propriedade dinâmica (ADO)](./prompt-property-dynamic-ado.md)