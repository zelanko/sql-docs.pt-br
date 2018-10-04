---
title: Tipo de dados MiningStructureColumn (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MiningStructureColumn Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MiningStructureColumn
helpviewer_keywords:
- MiningStructureColumn data type
ms.assetid: b6d6e7a5-9c48-40c4-b147-8fcd5e429ae3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0bcf11bef82aa9cb2abb2e8a08b7d567e5eb0159
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48153062"
---
# <a name="miningstructurecolumn-data-type-assl"></a>Tipo de dados MiningStructureColumn (ASSL)
  Define um tipo de dados primitivo abstrato que representa informações sobre uma coluna em uma [MiningStructure](../objects/miningstructure-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<MiningStructureColumn>  
   <Name>...</Name>  
   <ID>...</ID>  
   <Description>...</Description>  
   <Type>...</Type>  
   <Annotations>...</Annotations>  
</MiningStructureColumn>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipos de dados base|None|  
|Tipos de dados derivados|[ScalarMiningStructureColumn](miningstructurecolumn-data-type-assl.md), [TableMiningStructureColumn](tableminingstructurecolumn-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|None|  
|Elementos filho|[Anotações](../collections/annotations-element-assl.md), [descrição](../properties/description-element-assl.md), [ID](../properties/id-element-assl.md), [nome](../properties/name-element-assl.md), [tipo](../properties/type-element-miningstructurecolumn-assl.md)|  
|Elementos derivados|[Coluna](../objects/column-element-assl.md) ([colunas](../collections/columns-element-assl.md) coleção de [MiningStructure](../objects/miningstructure-element-assl.md))|  
  
## <a name="remarks"></a>Comentários  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.MiningStructureColumn>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
