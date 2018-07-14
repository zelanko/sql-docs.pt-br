---
title: Elemento AggregationStorage (ASSL) | Microsoft Docs
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
- AggregationStorage Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AggregationStorage
helpviewer_keywords:
- AggregationStorage element
ms.assetid: dd082388-534d-4847-9232-8f80fc9fe96e
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1f66a2161d7c5d5983366fd67cd695e7d90c4917
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37200076"
---
# <a name="aggregationstorage-element-assl"></a>Elemento AggregationStorage (ASSL)
  Identifica o método de armazenamento para agregações.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<ProactiveCaching>  
   ...  
   <AggregationStorage>...</AggregationStorage>  
   ...  
</ProactiveCaching>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Regular*|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[ProactiveCaching](../objects/proactivecaching-element-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O valor desse elemento é limitado a uma das cadeias de caracteres a seguir:  
  
|Valor|Description|  
|-----------|-----------------|  
|*Regular*|São armazenados dados de agregação da maneira padrão.|  
|*MolapOnly*|Os dados de agregação são armazenados usando apenas o armazenamento MOLAP (OLAP multidimensional).|  
  
 O *MolapOnly* opção está disponível somente para o [partição](../objects/partition-element-assl.md) elemento.  
  
 A enumeração que corresponde aos valores permitidos para `AggregationStorage` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.ProactiveCachingAggregationStorage>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
