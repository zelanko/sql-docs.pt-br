---
title: Elemento AlgorithmParameters (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
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
apiname: AlgorithmParameters Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: AlgorithmParameters
helpviewer_keywords: AlgorithmParameters element
ms.assetid: 240cbb60-7fa3-46ef-b5be-cd14c9ec10de
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1470ce42b2dada9d96c61e34716800b71fb63f26
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="algorithmparameters-element-assl"></a>Elemento AlgorithmParameters (ASSL)
  Contém a coleção de parâmetros para o algoritmo usado por um [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<MiningModel>  
   ...  
   <AlgorithmParameters>  
      <AlgorithmParameter>...</AlgorithmParameter>  
   </AlgorithmParameters>  
   ...  
</MiningModel>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum (coleção)|  
|Valor padrão|Nenhum (coleção)|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)|  
|Elementos filho|[AlgorithmParameter](../../../analysis-services/scripting/objects/algorithmparameter-element-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 A coleção **AlgorithmParameters** contém um conjunto extensível de parâmetros, representados como pares de nome/valor, para um algoritmo de modelo de mineração. O conjunto de parâmetros aplicáveis é dependente de algoritmo. Para obter mais informações sobre parâmetros de algoritmo para um determinado algoritmo, consulte a documentação apropriada para aquele algoritmo.  
  
 Os parâmetros de algoritmo disponíveis, inclusive validação e informações de exibição, podem ser recuperados do conjunto de linhas de esquema DMSCHEMA_MINING_SERVICE_PARAMETERS.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.AlgorithmParameterCollection>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento Algorithm &#40; ASSL &#41;](../../../analysis-services/scripting/properties/algorithm-element-assl.md)   
 [Conjunto de linhas DMSCHEMA_MINING_SERVICE_PARAMETERS](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-service-parameters-rowset.md)   
 [Coleções de &#40; ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
