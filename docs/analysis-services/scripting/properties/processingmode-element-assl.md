---
title: Elemento ProcessingMode (ASSL) | Microsoft Docs
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
apiname: ProcessingMode Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: ProcessingMode
helpviewer_keywords: ProcessingMode element
ms.assetid: dff6eeba-f09c-4d8c-ad81-caef76254af0
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c57e716da746a83c3310ccfa071cb0c43d8b64ab
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="processingmode-element-assl"></a>Elemento ProcessingMode (ASSL)
  Indica se a instância deve fazer indexação e agregação durante ou após o processamento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Cube> <!-- or Dimension, MeasureGroup, Partition -->  
   ...  
   <ProcessingMode>...</ProcessingMode>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Regular*|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Cubo](../../../analysis-services/scripting/objects/cube-element-assl.md), [dimensão](../../../analysis-services/scripting/objects/dimension-element-assl.md), [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md), [partição](../../../analysis-services/scripting/objects/partition-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O valor **ProcessingMode** no **Cube** fornece o padrão para o cubo e pode ser substituído pela configuração **ProcessingMode** de cada partição.  
  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Regular*|A instância indexa e executa agregações durante o processamento.|  
|*LazyOptimizations*|A instância indexa e executa agregações após o processamento.|  
  
 A enumeração que corresponde aos valores permitidos para **ProcessingMode** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.ProcessingMode>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
