---
title: Tipo de dados ProactiveCachingBinding (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 81bb1518277adbacf4566b201e1964e0860c2ff6
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34032377"
---
# <a name="proactivecachingbinding-data-type-assl"></a>Tipo de dados ProactiveCachingBinding (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define um tipo de dados derivado abstrato que representa informações para o elemento [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md) sobre as alterações da fonte de dados que requerem a recriação do cache ou sobre o status do processo de recriação.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<ProactiveCachingBinding>  
   <!-- ProactiveCachingBinding is an abstract base class with no child elements -->  
</ProactiveCachingBinding>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Tipos de dados base|[Associação](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
|Tipos de dados derivados|[ProactiveCachingIncrementalProcessingBinding](../../../analysis-services/scripting/data-type/proactivecachingincrementalprocessingbinding-data-type-assl.md), [ProactiveCachingObjectNotificationBinding](../../../analysis-services/scripting/data-type/proactivecachingobjectnotificationbinding-data-type-assl.md), [ProactiveCachingQueryBinding](../../../analysis-services/scripting/data-type/proactivecachingquerybinding-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhuma|  
|Elementos filho|Nenhuma|  
|Elementos derivados|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 Para obter mais informações sobre o **associação** tipo, incluindo tabelas de objetos do Analysis Services Scripting Language (ASSL) da **associação** tipo e a hierarquia de herança de **de associação**  tipos, consulte [tipo de dados de associação &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/binding-data-type-assl.md).  
  
 Para obter uma visão geral de associações de dados em ASSL, consulte [fontes de dados e associações & #40; SSAS Multidimensional & #41; ](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.ProactiveCachingBinding>.  
  
## <a name="inheritance-hierarchy-of-proactivecachingbinding-types"></a>Hierarquia de herança dos tipos ProactiveCachingBinding  
 A hierarquia a seguir mostra a herança dos tipos **ProactiveCachingBinding** .  
  
 Elemento[Binding](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)   
  
 Elemento**ProactiveCachingBinding**   
  
 Elemento[ProactiveCachingObjectNotificationBinding](../../../analysis-services/scripting/data-type/proactivecachingobjectnotificationbinding-data-type-assl.md)   
  
 Elemento[ProactiveCachingInheritedBinding](../../../analysis-services/scripting/data-type/proactivecachinginheritedbinding-data-type-assl.md)   
  
 Elemento[ProactiveCachingTablesBinding](../../../analysis-services/scripting/data-type/proactivecachingtablesbinding-data-type-assl.md)   
  
 Elemento[ProactiveCachingQueryBinding](../../../analysis-services/scripting/data-type/proactivecachingquerybinding-data-type-assl.md)   
  
 Elemento[ProactiveCachingIncrementalProcessingBinding](../../../analysis-services/scripting/data-type/proactivecachingincrementalprocessingbinding-data-type-assl.md)   
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem de script & #40; do Analysis Services ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
