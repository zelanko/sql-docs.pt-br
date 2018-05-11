---
title: Elemento AggregateFunction (ASSL) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 09ac3bb4798538fad0d91a40b385887dd3285060
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="aggregatefunction-element-assl"></a>Elemento AggregateFunction (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
## <a name="remarks"></a>Remarks  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Sum*|A medida é agregada usando a função **Sum** .|  
|*Count*|A medida é agregada usando a função **Count** .|  
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
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
