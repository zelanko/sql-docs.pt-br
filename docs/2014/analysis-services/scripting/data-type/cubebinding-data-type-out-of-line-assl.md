---
title: Tipo de dados CubeBinding (fora de linha) (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- CubeBinding Data Type (out-of-line)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CubeBinding
helpviewer_keywords:
- CubeBinding data type
ms.assetid: 5e1ee8ef-855c-4f3d-ae21-a33360d00d66
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ee354905f21670a143d8ec711bb45495086dbf05
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48136646"
---
# <a name="cubebinding-data-type-out-of-line-assl"></a>Tipo de dados CubeBinding (fora de linha) (ASSL)
  Define um tipo de dados primitivo que representa a relação entre um [cubo](../objects/cube-element-assl.md) elemento e um [DataSource](../objects/datasource-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<CubeBinding>  
   <ID>...</ID>  
   <DataSourceID>...</DataSourceID>  
   <DataSource>...</DataSource>  
   <MeasureGroup>...</MeasureGroup>  
</CubeBinding>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipos de dados base|None|  
|Tipos de dados derivados|None|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|None|  
|Elementos filho|[Fonte de dados](../objects/datasource-element-assl.md), [DataSourceID](../properties/id-element-assl.md), [ID](../properties/id-element-assl.md), [MeasureGroup](../objects/group-element-assl.md)|  
|Elementos derivados|[Associando](../../xmla/xml-elements-properties/binding-element-xmla.md) ([associações](../../xmla/xml-elements-properties/bindings-element-xmla.md) coleção de [processo](../../xmla/xml-elements-commands/process-element-xmla.md) ou [lote](../../xmla/xml-elements-commands/batch-element-xmla.md) comandos)|  
  
## <a name="remarks"></a>Comentários  
 Para obter mais informações sobre associações fora de linha, consulte [fontes de dados e associações &#40;Multidimensional do SSAS&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
## <a name="see-also"></a>Consulte também  
 [Tipo de dados de associação &#40;ASSL&#41;](binding-data-type-assl.md)   
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
