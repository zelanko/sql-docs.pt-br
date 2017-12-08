---
title: Estado do elemento (ASSL) | Microsoft Docs
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
apiname: State Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: State
helpviewer_keywords: State element
ms.assetid: b6ee1144-89f7-4ced-bc87-c2e33ca25f73
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 24cd06cd906eca3d40cb0eb0b06f10cf7e870a66
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="state-element-assl"></a>Elemento State (ASSL)
  Contém um valor somente leitura que descreve o estado de processamento atual do elemento pai.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Cube> <!-- or Dimension, MeasureGroup, MiningModel, MiningStructure, Partition -->  
      ...  
   <State>...</State>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Cubo](../../../analysis-services/scripting/objects/cube-element-assl.md), [dimensão](../../../analysis-services/scripting/objects/dimension-element-assl.md), [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md), [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md), [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md), [partição](../../../analysis-services/scripting/objects/partition-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Processados*|O elemento foi totalmente processado.|  
|*PartiallyProcessed*|O elemento foi parcialmente processado. ([Cubo](../../../analysis-services/scripting/objects/cube-element-assl.md) e [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md) somente.)|  
|*Não processado*|O elemento não foi processado.|  
  
 A enumeração que corresponde aos valores permitidos para **estado** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.AnalysisState>.  
  
 Os elementos que correspondem aos pais de **estado** no modelo de objeto de Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.Dimension>, <xref:Microsoft.AnalysisServices.MeasureGroup>, <xref:Microsoft.AnalysisServices.MiningModel>, <xref:Microsoft.AnalysisServices.MiningStructure>, e <xref:Microsoft.AnalysisServices.Partition>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
