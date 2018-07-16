---
title: Elemento StorageMode (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- StorageMode Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- StorageMode
helpviewer_keywords:
- StorageMode element
ms.assetid: 197e8153-1ab6-43ba-a7e9-ae9be19ac511
caps.latest.revision: 39
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3d61633743b4ce7e7b72f868b280e1bb376f1846
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37299006"
---
# <a name="storagemode-element-assl"></a>Elemento StorageMode (ASSL)
  Determina o modo de armazenamento para o elemento pai.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Cube> <!-- or Dimension, MeasureGroup, Partition -->  
   ...  
   <StorageMode>...</StorageMode>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*MOLAP*|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Elemento de cubo &#40;ASSL&#41;](../objects/cube-element-assl.md), [elemento da dimensão &#40;ASSL&#41;](../objects/dimension-element-assl.md), [elemento MeasureGroup &#40;ASSL&#41;](../objects/group-element-assl.md), [partição Elemento &#40;ASSL&#41;](../objects/partition-element-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*MOLAP*|O pai usa o armazenamento MOLAP (OLAP multidimensional).|  
|*ROLAP*|O pai usa o armazenamento ROLAP (OLAP relacional).|  
|*HOLAP*|O pai usa o armazenamento HOLAP (OLAP híbrido). **Observação:** esse valor não é válido para [dimensão](../objects/dimension-element-assl.md) elementos pai.|  
|*InMemory*|O pai usa o armazenamento IMBI.|  
  
 A enumeração que corresponde aos valores permitidos para `StorageMode` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.StorageMode>.  
  
 Os elementos que correspondem aos pais de `StorageMode` no modelo de objeto AMO (Objetos de Gerenciamento de Análise) são <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.Dimension>, <xref:Microsoft.AnalysisServices.MeasureGroup> e <xref:Microsoft.AnalysisServices.Partition>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
