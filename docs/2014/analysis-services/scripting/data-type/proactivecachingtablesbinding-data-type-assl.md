---
title: Tipo de dados ProactiveCachingTablesBinding (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ProactiveCachingTablesBinding Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- ProactiveCachingTablesBinding data type
ms.assetid: f6b3f6fc-757c-4b1e-bb3a-d26482888d14
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f157503cc77235ad4f249da1390d4504f7d05569
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48065496"
---
# <a name="proactivecachingtablesbinding-data-type-assl"></a>Tipo de dados ProactiveCachingTablesBinding (ASSL)
  Define um tipo de dados derivado que representa informações para o [ProactiveCaching](../objects/proactivecaching-element-assl.md) elemento sobre as alterações da fonte de dados em tabelas e exibições que requerem a recriação do cache especificadas.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<ProactiveCachingTablesBinding>  
   <!-- The following elements extend ProactiveCachingObjectNotificationBinding -->  
   <TableNotification>...</TableNotification>  
</ProactiveCachingTablesBinding>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipos de dados base|[ProactiveCachingObjectNotificationBinding](binding-data-type-assl.md)|  
|Tipos de dados derivados|None|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|None|  
|Elementos filho|[TableNotification](../objects/tablenotification-element-assl.md)|  
|Elementos derivados|None|  
  
## <a name="remarks"></a>Comentários  
 Para obter mais informações sobre o `ProactiveCachingBinding` tipo, incluindo uma tabela da hierarquia de herança `ProactiveCachingBinding` tipos, consulte [tipo de dados ProactiveCachingBinding &#40;ASSL&#41;](proactivecachingbinding-data-type-assl.md).  
  
 Para obter mais informações sobre o `Binding` tipo, incluindo tabelas de objetos do Analysis Services Scripting Language (ASSL) da `Binding` tipo e a hierarquia de herança dos `Binding` tipos, consulte [tipo de associação de dados &#40;ASSL &#41;](binding-data-type-assl.md).  
  
 Para uma visão geral de associações de dados em ASSL, consulte [fontes de dados e associações &#40;Multidimensional do SSAS&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.ProactiveCachingTablesBinding>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
