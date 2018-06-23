---
title: Tipo de dados ProactiveCachingBinding (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ProactiveCachingBinding Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- ProactiveCachingBinding data type
ms.assetid: 02e6ff2f-2f18-4607-9198-bb46f113f9ac
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 881e593fda57d63a4041e469c48807d434324856
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36020790"
---
# <a name="proactivecachingbinding-data-type-assl"></a>Tipo de dados ProactiveCachingBinding (ASSL)
  Define um tipo de dados derivado abstrato que representa informações para o [ProactiveCaching](../objects/proactivecaching-element-assl.md) elemento sobre as alterações de fonte de dados que requerem a recriação do cache ou sobre o status do processo de recriação.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<ProactiveCachingBinding>  
   <!-- ProactiveCachingBinding is an abstract base class with no child elements -->  
</ProactiveCachingBinding>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipos de dados base|[Associação](binding-data-type-assl.md)|  
|Tipos de dados derivados|[ProactiveCachingIncrementalProcessingBinding](proactivecachingincrementalprocessingbinding-data-type-assl.md), [ProactiveCachingObjectNotificationBinding](proactivecachingobjectnotificationbinding-data-type-assl.md), [ProactiveCachingQueryBinding](querybinding-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhum|  
|Elementos filho|Nenhum|  
|Elementos derivados|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 Para obter mais informações sobre o `Binding` tipo, incluindo tabelas de objetos do Analysis Services Scripting Language (ASSL) da `Binding` tipo e a hierarquia de herança de `Binding` tipos, consulte [tipo de dados de associação &#40;ASSL &#41;](binding-data-type-assl.md).  
  
 Para obter uma visão geral de associações de dados em ASSL, consulte [fontes de dados e associações &#40;multidimensionais do SSAS&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.ProactiveCachingBinding>.  
  
## <a name="inheritance-hierarchy-of-proactivecachingbinding-types"></a>Hierarquia de herança dos tipos ProactiveCachingBinding  
 A hierarquia a seguir mostra a herança dos tipos `ProactiveCachingBinding`.  
  
 [Associação](binding-data-type-assl.md) elemento  
  
 Elemento `ProactiveCachingBinding`  
  
 [ProactiveCachingObjectNotificationBinding](proactivecachingobjectnotificationbinding-data-type-assl.md) elemento  
  
 [ProactiveCachingInheritedBinding](inheritedbinding-data-type-assl.md) elemento  
  
 [ProactiveCachingTablesBinding](proactivecachingtablesbinding-data-type-assl.md) elemento  
  
 [ProactiveCachingQueryBinding](querybinding-data-type-assl.md) elemento  
  
 [ProactiveCachingIncrementalProcessingBinding](proactivecachingincrementalprocessingbinding-data-type-assl.md) elemento  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  