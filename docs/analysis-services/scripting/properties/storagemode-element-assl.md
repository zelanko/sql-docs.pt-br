---
title: Elemento StorageMode (ASSL) | Microsoft Docs
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
apiname: StorageMode Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: StorageMode
helpviewer_keywords: StorageMode element
ms.assetid: 197e8153-1ab6-43ba-a7e9-ae9be19ac511
caps.latest.revision: "40"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 599760e2df021d6fd06a841ca97fbe3a92418721
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="storagemode-element-assl"></a>Elemento StorageMode (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Determina o modo de armazenamento para o elemento pai.  
  
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
|Elementos pai|[Elemento Cube &#40; ASSL &#41; ](../../../analysis-services/scripting/objects/cube-element-assl.md), [Dimensão elemento &#40; ASSL &#41; ](../../../analysis-services/scripting/objects/dimension-element-assl.md), [Elemento MeasureGroup &#40; ASSL &#41; ](../../../analysis-services/scripting/objects/measuregroup-element-assl.md), [Partição elemento &#40; ASSL &#41;](../../../analysis-services/scripting/objects/partition-element-assl.md)|  
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
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
