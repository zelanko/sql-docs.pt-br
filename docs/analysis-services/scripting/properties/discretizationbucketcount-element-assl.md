---
title: Elemento DiscretizationBucketCount (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DiscretizationBucketCount Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: DiscretizationBucketCount
helpviewer_keywords: DiscretizationBucketCount element
ms.assetid: 551a73ae-59e1-4079-a2d9-988df96b5e07
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0dd6c923a98ccb273ff01cc508139a972a276b4c
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="discretizationbucketcount-element-assl"></a>Elemento DiscretizationBucketCount (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Contém o número de buckets nos quais são diferenciados.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DimensionAttribute> <!-- or ScalarMiningStructureColumn -->  
   ...  
   <DiscretizationBucketCount>...</DiscretizationBucketCount>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Integer|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md), [ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O valor do elemento **DiscretizationBucketCount** determina quantos grupos ou “recipientes” são criados quando os valores para **DimensionAttribute** ou **ScalarMiningStructureColumn** são diferenciados ou organizados em um conjunto específico de grupos. Se o elemento não for especificado, ou se zero for especificado para o valor do elemento, [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] cria um número apropriado de grupos, dependendo do método de diferenciação. Para obter mais informações sobre os métodos de diferenciação, consulte [os métodos de diferenciação &#40; mineração de dados &#41;](../../../analysis-services/data-mining/discretization-methods-data-mining.md).  
  
 Os elementos que correspondem aos pais de **DiscretizationBucketCount** no modelo de objeto de Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.DimensionAttribute> e <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento DiscretizationMethod &#40; ASSL &#41;](../../../analysis-services/scripting/properties/discretizationmethod-element-assl.md)   
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
