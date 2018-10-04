---
title: Elemento SortPropertiesPosition (XML) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: 68b040a7-ab16-46f5-8610-21db07df9181
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0838a11aab6fa73060365b38c0f834749726a18d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48101256"
---
# <a name="sortpropertiesposition-element-xml"></a>Elemento SortPropertiesPosition (XML)
  Contém informações sobre a posição do elemento em uma coleção de elementos.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<RelationshipEndVisualizationProperties>  
   ...  
   <SortPropertiesPosition>...</SortPropertiesPosition>  
   ...  
</RelationshipEndVisualizationProperties>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Integer|  
|Valor padrão|-1|  
|Cardinalidade|0-1: elemento opcional que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[RelationshipEndVisualizationProperties](../../scripting/data-type/relationshipendvisualizationproperties-data-type-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 Para elementos `RelationshipEndVisualizationProperties`, o elemento `SortPropertiesPosition` contém a posição do elemento de propriedades de classificação em uma coleção de detalhes. O valor padrão indica que não há propriedades de classificação a serem usadas.  
  
  
