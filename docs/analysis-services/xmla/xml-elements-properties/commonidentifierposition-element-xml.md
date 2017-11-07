---
title: Elemento CommonIdentifierPosition (XML) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: c3b64132-3b2e-46f5-ae11-a3cb3c42099c
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4fe8eea6f5252adcf17f4c1f350c23042b2aeba6
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="commonidentifierposition-element-xml"></a>Elemento CommonIdentifierPosition (XML)
  Contém informações sobre a posição do elemento em uma coleção de elementos.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<RelationshipEndVisualizationProperties>  
   ...  
   <CommonIdentifierPosition>...</CommonIdentifierPosition>  
   ...  
</RelationshipEndVisualizationProperties>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Integer|  
|Valor padrão|-1|  
|Cardinalidade|0-1: elemento opcional que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[RelationshipEndVisualizationProperties](../../../analysis-services/scripting/data-type/relationshipendvisualizationproperties-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 Para **RelationshipEndVisualizationProperties** elementos, o **CommonIdentifierPosition** elemento contém a posição do elemento de identificador comum em uma coleção de detalhes. O valor padrão de **false** indica que não há nenhum identificador comum a ser usado.  
  
  

