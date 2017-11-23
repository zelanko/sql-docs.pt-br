---
title: Elemento AggregateFunction (ASSL) | Microsoft Docs
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
apiname: AggregateFunction Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: AggregateFunction
helpviewer_keywords: AggregateFunction element
ms.assetid: 880b6bd0-d62a-4221-831c-39f748ee84f2
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4d228786bdf94c786856bdebd2c088bdf1b13227
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="aggregatefunction-element-assl"></a>Elemento AggregateFunction (ASSL)
  Define o tipo de função de agregação usado por um [medidas](../../../analysis-services/scripting/objects/measure-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Measure>  
   ...  
   <AggregateFunction>...</AggregateFunction>  
   ...  
</Measure>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Sum*|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Medida](../../../analysis-services/scripting/objects/measure-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Sum*|A medida é agregada usando a função **Sum** .|  
|*Contagem*|A medida é agregada usando a função **Count** .|  
|*Min*|A medida é agregada usando a função **Min** .|  
|*Max*|A medida é agregada usando a função **Max** .|  
|*DistinctCount*|A medida é agregada usando a função **DistinctCount** .|  
|*Nenhuma*|A medida não é agregada.|  
|*ByAccount*|A medida é agregada pela conta.|  
|*AverageOfChildren*|A medida é agregada retornando a média de seus filhos.|  
|*FirstChild*|A medida é agregada retornando seu primeiro membro filho.|  
|*LastChild*|A medida é agregada retornando seu último membro filho.|  
|*FirstNonEmpty*|A medida é agregada retornando seu primeiro membro não vazio.|  
|*LastNonEmpty*|A medida é agregada retornando seu último membro não vazio.|  
  
 A enumeração que corresponde aos valores permitidos para **AggregateFunction** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.AggregationFunction>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
