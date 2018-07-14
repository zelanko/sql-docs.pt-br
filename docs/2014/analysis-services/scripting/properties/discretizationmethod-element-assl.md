---
title: Elemento DiscretizationMethod (ASSL) | Microsoft Docs
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
- DiscretizationMethod Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DiscretizationMethod
helpviewer_keywords:
- DiscretizationMethod element
ms.assetid: 4cfe015f-ad6c-47e1-8aff-c9c7677867b1
caps.latest.revision: 31
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6347db0e5d964b10112516b4c607a5185f247b65
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37252998"
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
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Nenhuma*|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md), [ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O valor do elemento `DiscretizationMethod` determina como os valores de `DimensionAttribute` ou `ScalarMiningStructureColumn` são diferenciados ou organizados em um conjunto específico de grupos. Para obter mais informações sobre os métodos de diferenciação, consulte [métodos de discretização &#40;mineração de dados&#41;](../../data-mining/discretization-methods-data-mining.md).  
  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Automático*|Equivalente ao método de diferenciação AUTOMATIC para colunas de estrutura de mineração.|  
|*EqualAreas*|Equivalente ao método de diferenciação EQUAL_AREAS para colunas de estrutura de mineração.|  
|*Clusters*|Equivalente ao método de diferenciação CLUSTERS para colunas de estrutura de mineração.|  
|*Limites*|Equivalente ao método de diferenciação THRESHOLDS para colunas de estrutura de mineração.|  
|*EqualRanges*|Equivalente ao método de diferenciação EQUAL_RANGES para colunas de estrutura de mineração.|  
  
 A enumeração que corresponde aos valores permitidos para `DiscretizationMethod` no modelo de objeto AMO (Objetos de Gerenciamento de Análise) é <xref:Microsoft.AnalysisServices.DiscretizationMethod>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
