---
title: Elemento ProcessingMode (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ProcessingMode Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ProcessingMode
helpviewer_keywords:
- ProcessingMode element
ms.assetid: dff6eeba-f09c-4d8c-ad81-caef76254af0
caps.latest.revision: 33
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9a966a1d800107b18316e875bd8c9552df613cfe
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37273782"
---
# <a name="processingmode-element-assl"></a>Elemento ProcessingMode (ASSL)
  Indica se a instância deve fazer indexação e agregação durante ou após o processamento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Cube> <!-- or Dimension, MeasureGroup, Partition -->  
   ...  
   <ProcessingMode>...</ProcessingMode>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Regular*|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Cubo](../objects/cube-element-assl.md), [dimensão](../objects/dimension-element-assl.md), [MeasureGroup](../objects/group-element-assl.md), [partição](../objects/partition-element-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O valor `ProcessingMode` no `Cube` fornece o padrão para o cubo e pode ser substituído pela configuração `ProcessingMode` de cada partição.  
  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Regular*|A instância indexa e executa agregações durante o processamento.|  
|*LazyOptimizations*|A instância indexa e executa agregações após o processamento.|  
  
 A enumeração que corresponde aos valores permitidos para `ProcessingMode` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.ProcessingMode>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
