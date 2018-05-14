---
title: Elemento StorageMode (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 72b2963293c6c59338ad23f8e4f4f5c0e9d19001
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="storagemode-element-assl"></a>Elemento StorageMode (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*MOLAP*|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Elemento de cubo &#40;ASSL&#41;](../../../analysis-services/scripting/objects/cube-element-assl.md), [dimensão elemento &#40;ASSL&#41;](../../../analysis-services/scripting/objects/dimension-element-assl.md), [elemento MeasureGroup &#40;ASSL&#41;](../../../analysis-services/scripting/objects/measuregroup-element-assl.md), [partição Elemento &#40;ASSL&#41;](../../../analysis-services/scripting/objects/partition-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*MOLAP*|O pai usa o armazenamento MOLAP (OLAP multidimensional).|  
|*ROLAP*|O pai usa o armazenamento ROLAP (OLAP relacional).|  
|*HOLAP*|O pai usa o armazenamento HOLAP (OLAP híbrido).<br /><br /> Observação: Esse valor não é válido para [dimensão](../../../analysis-services/scripting/objects/dimension-element-assl.md) elementos pai.|  
|*InMemory*|O pai usa o armazenamento IMBI.|  
  
 A enumeração que corresponde aos valores permitidos para **StorageMode** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.StorageMode>.  
  
 Os elementos que correspondem aos pais de **StorageMode** no modelo de objeto de Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.Dimension>, <xref:Microsoft.AnalysisServices.MeasureGroup>, e <xref:Microsoft.AnalysisServices.Partition>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
