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
ms.openlocfilehash: afd5d9ca0de6b8d2ffba75f862e6ca0afb594848
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67919441"
---
# <a name="connectpromptenum"></a>ConnectPromptEnum
Especifica se uma caixa de diálogo deve ser exibida para solicitar parâmetros ausentes ao abrir uma conexão com uma fonte de dados.  
  
|Constante|Valor|DESCRIÇÃO|  
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
