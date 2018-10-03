---
title: Elemento NotificationTechnique (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- NotificationTechnique Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- NotificationTechnique element
ms.assetid: 80c43de3-f147-4bf5-bb85-da9d182ce415
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8dc05b03286785e2d06d5595897a263a294ae97e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48139468"
---
# <a name="notificationtechnique-element-assl"></a>Elemento NotificationTechnique (ASSL)
  Especifica se [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou um aplicativo cliente externo processa as notificações.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<ProactiveCachingBinding>  
   <NotificationTechnique>...</NotificationTechnique>  
</ProactiveCachingBinding>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Cliente*|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[ProactiveCachingBinding](../data-type/binding-data-type-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Cliente*|O aplicativo cliente externo processa a notificação.|  
|*Servidor*|O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] processa a notificação.|  
  
 O elemento que corresponde ao pai de `NotificationTechnique` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.ProactiveCachingBinding>.  
  
 A enumeração que corresponde aos valores permitidos para `NotificationTechnique` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.NotificationTechnique>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipo de dados ProactiveCachingBinding &#40;ASSL&#41;](../data-type/binding-data-type-assl.md)  
  
  
