---
title: Elemento TableNotifications (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- TableNotifications Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- TableNotifications element
ms.assetid: 4cecdfea-0d4d-4bd6-bbb3-4d0d2284c665
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8c146f223d0819c8570b051d77d5764ae384d1b1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37163381"
---
# <a name="tablenotifications-element-assl"></a>Elemento TableNotifications (ASSL)
  Contém a coleção de [TableNotification](../objects/tablenotification-element-assl.md) elementos que fornecem informações para o [ProactiveCaching](../objects/proactivecaching-element-assl.md) elemento sobre tabelas ou exibições em uma fonte de dados que foram modificadas.  
  
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
|Elementos pai|[ProactiveCachingTablesBinding](../data-type/binding-data-type-assl.md)|  
|Elementos filho|[TableNotification](../objects/tablenotification-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.TableNotificationCollection>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipo de dados ProactiveCachingBinding &#40;ASSL&#41;](../data-type/proactivecachingbinding-data-type-assl.md)   
 [Tipo de dados ProactiveCachingObjectNotificationBinding &#40;ASSL&#41;](../data-type/proactivecachingobjectnotificationbinding-data-type-assl.md)   
 [Coleções &#40;ASSL&#41;](collections-assl.md)  
  
  
