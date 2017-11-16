---
title: Tipo de dados ProactiveCachingInheritedBinding (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- ProactiveCachingInheritedBinding Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- ProactiveCachingInheritedBinding data type
ms.assetid: 913fa19f-1ecb-4fca-897e-12f0fb02cf8b
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8692a0fc3f714f9654d3e4aabd85e0617b0dcee2
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="proactivecachinginheritedbinding-data-type-assl"></a>Tipo de Dados ProactiveCachingInheritedBinding (ASSL)
  Define um tipo de dados derivado que representa informações para o [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md) elemento sobre as alterações da fonte de dados em tabelas e exibições identificadas por meio de ligações de dados existentes que requerem a recriação do cache.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<ProactiveCachingInheritedBinding>  
   <!-- This element has no child elements that extend ProactiveCachingObjectNotificationBinding -->  
</ProactiveCachingInheritedBinding>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Tipos de dados base|[ProactiveCachingObjectNotificationBinding](../../../analysis-services/scripting/data-type/proactivecachingobjectnotificationbinding-data-type-assl.md)|  
|Tipos de dados derivados|Nenhuma|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhuma|  
|Elementos filho|Nenhuma|  
|Elementos derivados|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 Para obter mais informações sobre o **ProactiveCachingBinding** tipo, incluindo uma tabela de hierarquia de herança de **ProactiveCachingBinding** tipos, consulte [dados ProactiveCachingBinding Tipo de &#40; ASSL &#41; ](../../../analysis-services/scripting/data-type/proactivecachingbinding-data-type-assl.md).  
  
 Para obter mais informações sobre o **associação** tipo, incluindo tabelas de objetos do Analysis Services Scripting Language (ASSL) da **associação** tipo e a hierarquia de herança de **de associação**  tipos, consulte [associação de tipo de dados &#40; ASSL &#41; ](../../../analysis-services/scripting/data-type/binding-data-type-assl.md).  
  
 Para obter uma visão geral de associações de dados em ASSL, consulte [fontes de dados e associações &#40; SSAS Multidimensional &#41; ](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.ProactiveCachingInheritedBinding>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem de script &#40; do Analysis Services ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

