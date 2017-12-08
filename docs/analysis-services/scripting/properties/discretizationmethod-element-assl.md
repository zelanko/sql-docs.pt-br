---
title: Elemento DiscretizationMethod (ASSL) | Microsoft Docs
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
apiname: DiscretizationMethod Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: DiscretizationMethod
helpviewer_keywords: DiscretizationMethod element
ms.assetid: 4cfe015f-ad6c-47e1-8aff-c9c7677867b1
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0b084caccf3b44cc6b43021551f227f61c0de0e7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="discretizationmethod-element-assl"></a>Elemento DiscretizationMethod (ASSL)
  Define o método a ser usado para diferenciação.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DimensionAttribute> <!-- or ScalarMiningStructureColumn -->  
   ...  
   <DiscretizationMethod>...</DiscretizationMethod>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Nenhuma*|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md), [ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O valor do elemento **DiscretizationMethod** determina como os valores de **DimensionAttribute** ou **ScalarMiningStructureColumn** são diferenciados ou organizados em um conjunto específico de grupos. Para obter mais informações sobre os métodos de diferenciação, consulte [os métodos de diferenciação &#40; mineração de dados &#41;](../../../analysis-services/data-mining/discretization-methods-data-mining.md).  
  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|*Automático*|Equivalente ao método de diferenciação AUTOMATIC para colunas de estrutura de mineração.|  
|*EqualAreas*|Equivalente ao método de diferenciação EQUAL_AREAS para colunas de estrutura de mineração.|  
|*Clusters*|Equivalente ao método de diferenciação CLUSTERS para colunas de estrutura de mineração.|  
|*Limites*|Equivalente ao método de diferenciação THRESHOLDS para colunas de estrutura de mineração.|  
|*EqualRanges*|Equivalente ao método de diferenciação EQUAL_RANGES para colunas de estrutura de mineração.|  
  
 A enumeração que corresponde aos valores permitidos para **DiscretizationMethod** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.DiscretizationMethod>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
