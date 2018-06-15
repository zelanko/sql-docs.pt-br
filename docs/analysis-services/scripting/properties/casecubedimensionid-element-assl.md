---
title: Elemento CaseCubeDimensionID (ASSL) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 04223d0af275bbfbe153ad988a1823a5f110d502
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34030647"
---
# <a name="casecubedimensionid-element-assl"></a>Elemento CaseCubeDimensionID (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Contém o identificador (ID) da dimensão de cubo que relaciona a dimensão de mineração de dados ao grupo de medidas.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DataMiningMeasureGroupDimension>  
   ...  
   <CaseCubeDimensionID>...</CaseCubeDimensionID>  
   ...  
</DataMiningMeasureGroupDimension>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|String|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-1: elemento obrigatório que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[DataMiningMeasureGroupDimension](../../../analysis-services/scripting/data-type/dataminingmeasuregroupdimension-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 O elemento que corresponde ao pai do **CaseCubeDimensionID** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.DataMiningMeasureGroupDimension>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
