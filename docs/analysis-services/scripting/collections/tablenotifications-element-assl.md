---
title: Elemento TableNotifications (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- TableNotifications Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- TableNotifications element
ms.assetid: 4cecdfea-0d4d-4bd6-bbb3-4d0d2284c665
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 373f16ec036ae898639ed84b03f87afdde8ca497
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="tablenotifications-element-assl"></a>Elemento TableNotifications (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Contém a coleção de [TableNotification](../../../analysis-services/scripting/objects/tablenotification-element-assl.md) elementos que fornecem informações para o [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md) elemento sobre tabelas ou exibições em uma fonte de dados que foram modificadas.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<ProactiveCachingTablesBinding>  
   <TableNotifications>  
      <TableNotification>...</TableNotification>  
...</TableNotifications>  
</ProactiveCachingTablesBinding>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum|  
|Valor padrão|Nenhum|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[ProactiveCachingTablesBinding](../../../analysis-services/scripting/data-type/proactivecachingtablesbinding-data-type-assl.md)|  
|Elementos filho|[TableNotification](../../../analysis-services/scripting/objects/tablenotification-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.TableNotificationCollection>.  
  
## <a name="see-also"></a>Consulte Também  
 [Tipo de dados ProactiveCachingBinding &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/proactivecachingbinding-data-type-assl.md)   
 [Tipo de dados ProactiveCachingObjectNotificationBinding &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/proactivecachingobjectnotificationbinding-data-type-assl.md)   
 [Coleções de &#40; ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
