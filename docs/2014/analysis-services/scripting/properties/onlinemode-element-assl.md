---
title: Elemento OnlineMode (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- OnlineMode Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- OnlineMode
helpviewer_keywords:
- OnlineMode element
ms.assetid: 0bbac4e2-002f-4be4-8dd6-ccd7034f5f93
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a7a4469a522b1364df645fc1dcb0362647397a89
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48196836"
---
# <a name="onlinemode-element-assl"></a>Elemento OnlineMode (ASSL)
  Especifica se o banco de dados volta a ficar online imediatamente quando a recriação do cache é iniciada ou somente quando a recriação do cache é concluída.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<ProactiveCaching>  
   ...  
   <OnlineMode>...</OnlineMode>  
   ...  
</ProactiveCaching>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Imediata*|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[ProactiveCaching](../objects/proactivecaching-element-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Imediata*|O banco de dados volta a ficar online imediatamente quando a recriação do cache é iniciada.|  
|*OnCacheComplete*|O banco de dados volta a ficar online somente quando a recriação do cache é concluída.|  
  
 A enumeração que corresponde aos valores permitidos para `OnlineMode` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.ProactiveCaching>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento ProactiveCaching &#40;ASSL&#41;](../objects/proactivecaching-element-assl.md)  
  
  
