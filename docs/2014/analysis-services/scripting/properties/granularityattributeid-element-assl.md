---
title: Elemento GranularityAttributeID (ASSL) | Microsoft Docs
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
- GranularityAttributeID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- GranularityAttributeID element
ms.assetid: 90e6c939-71bd-462a-a377-4854cb9d5266
caps.latest.revision: 9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0d29d88dcc7317388e2baab3415509f52299883f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37308426"
---
# <a name="granularityattributeid-element-assl"></a>Elemento GranularityAttributeID (ASSL)
  Contém o identificador (ID) do atributo associado ao pai [MeasureGroupAttributeBinding](../data-type/measuregroupattributebinding-data-type-out-of-line-assl.md) tipo de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<MeasureGroupAttributeBinding>  
   ...  
   <GranularityAttributeID>...</GranularityAttributeID>  
   ...  
</MeasureGroupAttributeBinding>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres|  
|Valor padrão|Nenhum|  
|Cardinalidade|1-1: elemento obrigatório que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[MeasureGroupAttributeBinding](../data-type/measuregroupattributebinding-data-type-out-of-line-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 Para obter mais informações sobre associações fora de linha, consulte [fontes de dados e associações &#40;Multidimensional do SSAS&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
