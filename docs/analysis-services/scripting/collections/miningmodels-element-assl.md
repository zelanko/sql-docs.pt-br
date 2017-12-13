---
title: Elemento MiningModels (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
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
apiname: MiningModels Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: MiningModels
helpviewer_keywords: MiningModels element
ms.assetid: 19824d92-2e23-4e5e-b329-e46baf709c4a
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: bae04d64619e24cc89140908d60506c9a09554d9
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="miningmodels-element-assl"></a>Elemento MiningModels (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Contém a coleção de [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md) elementos associados a um [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<MiningStructure>  
   ...  
   <MiningModels>  
      <MiningModel>...</MiningModel>  
   </MiningModels>  
   ...  
</MiningStructure>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)|  
|Elementos filho|[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.MiningModelCollection>.  
  
## <a name="see-also"></a>Consulte também  
 [Coleções de &#40; ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
