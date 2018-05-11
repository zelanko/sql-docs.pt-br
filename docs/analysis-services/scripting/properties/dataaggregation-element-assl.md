---
title: Elemento DataAggregation (ASSL) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c315e40b15d7bf83cdc317a9498998387fd4d3ee
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="dataaggregation-element-assl"></a>Elemento DataAggregation (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Determina se a instância pode agregar dados persistidos ou dados armazenados em cache para o [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<MeasureGroup>  
   ...  
   <DataAggregation>...</DataAggregation>  
   ...  
</MeasureGroup>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*DataAndCacheAggregatable*|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Nenhuma*|A agregação não é executada para este grupo de medidas.|  
|*DataAggregatable*|Os dados persistidos podem ser agregados para este grupo de medidas.|  
|*CacheAggregatable*|Os dados armazenados em cache podem ser agregados para este grupo de medidas.|  
|*DataAndCacheAggregatable*|Ambos os dados persistidos e armazenados em cache podem ser agregados para este grupo de medidas.|  
  
 O elemento que corresponde ao pai do **DataAggregation** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.MeasureGroup>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento Cube & #40; ASSL & #41;](../../../analysis-services/scripting/objects/cube-element-assl.md)   
 [Elemento Dimension & #40; ASSL & #41;](../../../analysis-services/scripting/objects/dimension-element-assl.md)   
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
