---
title: Elemento Collation (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
apiname: Collation Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Collation
helpviewer_keywords: Collation element
ms.assetid: 9b6dbe19-543e-43e6-abe9-1e8b4dfaa275
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f749ab7afc19f848bf4ce17bc1f742ecc3ee45d9
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="collation-element-assl"></a>Elemento Collation (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Determina o agrupamento usado pelo elemento pai.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Database> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Collation>...</Collation>  
   ...  
</Database>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|String|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Cubo](../../../analysis-services/scripting/objects/cube-element-assl.md), [banco de dados](../../../analysis-services/scripting/objects/database-element-assl.md), [DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md), [dimensão](../../../analysis-services/scripting/objects/dimension-element-assl.md), [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md), [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 A cadeia de caracteres **Collation** consiste no LCID (identificador de localidade) e no sinalizador de comparação, separados por um caractere de sublinhado. Por exemplo, Latin1_General_CI_AS é uma cadeia de caracteres aceitável.  
  
 Os elementos que correspondem aos pais de **agrupamento** no modelo de objeto de Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.Database>, <xref:Microsoft.AnalysisServices.DataItem>, <xref:Microsoft.AnalysisServices.Dimension>, <xref:Microsoft.AnalysisServices.MiningModel>e <xref:Microsoft.AnalysisServices.MiningStructure>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
