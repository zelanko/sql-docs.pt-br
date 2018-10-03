---
title: Tipo de dados ProactiveCachingObjectNotificationBinding (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ProactiveCachingObjectNotificationBinding Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- ProactiveCachingObjectNotificationBinding data type
ms.assetid: b3cf5fb6-6121-4f25-8de6-f171792c440d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 201774fd7b46bf3d4fc30dfe304c8ffd80f7c6eb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48080376"
---
# <a name="proactivecachingobjectnotificationbinding-data-type-assl"></a>Tipo de dados ProactiveCachingObjectNotificationBinding (ASSL)
  Define um tipo de dados derivado abstrato que representa informações para o [ProactiveCaching](../objects/proactivecaching-element-assl.md) elemento sobre alterações de fonte de dados, em tabelas e exibições especificadas ou em tabelas e exibições identificadas por meio de associações de dados existentes que exigem a recriação do cache.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<ProactiveCachingObjectNotificationBinding>  
   <!-- The following elements extend ProactiveCachingBinding -->  
   <NotificationTechnique>...</NotificationTechnique>  
</ProactiveCachingObjectNotificationBinding>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipos de dados base|[ProactiveCachingBinding](binding-data-type-assl.md)|  
|Tipos de dados derivados|[ProactiveCachingInheritedBinding](inheritedbinding-data-type-assl.md), [ProactiveCachingTablesBinding](proactivecachingtablesbinding-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|None|  
|Elementos filho|[NotificationTechnique](../properties/notificationtechnique-element-assl.md)|  
|Elementos derivados|None|  
  
## <a name="remarks"></a>Comentários  
 Para obter mais informações sobre o `ProactiveCachingBinding` tipo, incluindo uma tabela da hierarquia de herança `ProactiveCachingBinding` tipos, consulte [tipo de dados ProactiveCachingBinding &#40;ASSL&#41;](binding-data-type-assl.md).  
  
 Para obter mais informações sobre o `Binding` tipo, incluindo tabelas de objetos do Analysis Services Scripting Language (ASSL) da `Binding` tipo e a hierarquia de herança dos `Binding` tipos, consulte [tipo de associação de dados &#40;ASSL &#41;](binding-data-type-assl.md).  
  
 Para uma visão geral de associações de dados em ASSL, consulte [fontes de dados e associações &#40;Multidimensional do SSAS&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.ProactiveCachingObjectNotificationBinding>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
