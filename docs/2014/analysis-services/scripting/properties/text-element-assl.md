---
title: Elemento Text (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Text Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- text
helpviewer_keywords:
- Text element
ms.assetid: 0edece73-236f-4661-8102-3fcc29326bf4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a53693bc2a102061c84e7c44c4155c21adb51756
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48057788"
---
# <a name="text-element-assl"></a>Elemento Text (ASSL)
  Contém o texto de um [comando](../objects/command-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Command>  
   <Text>...</Text>  
</Command>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres|  
|Valor padrão|None|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[Comando](../objects/command-element-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 O elemento que corresponde ao pai de `Text` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.Command>.  
  
## <a name="see-also"></a>Consulte também  
 [Comandos do elemento &#40;ASSL&#41;](../collections/commands-element-assl.md)   
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
