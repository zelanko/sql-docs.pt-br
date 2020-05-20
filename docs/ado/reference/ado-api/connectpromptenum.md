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
author: rothja
ms.author: jroth
ms.openlocfilehash: 61a66866f8206f2df4cbdeb3f2144e0ac12ac695
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762587"
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
 [Solicitar a propriedade dinâmica (ADO)](../../../ado/reference/ado-api/prompt-property-dynamic-ado.md)
