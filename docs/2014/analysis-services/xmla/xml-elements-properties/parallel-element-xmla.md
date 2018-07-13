---
title: Elemento (XMLA) em paralelo | Microsoft Docs
ms.custom: ''
ms.date: 2015-12-07
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Parallel Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Parallel
- http://schemas.microsoft.com/analysisservices/2003/engine#Parallel
- microsoft.xml.analysis.parallel
helpviewer_keywords:
- Parallel element
ms.assetid: 04726d94-37ee-460b-9744-d62b45f536b9
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b514732345cc8c4c7c0bc2c2f4f3fa0ad2d75993
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37161017"
---
# <a name="parallel-element-xmla"></a>Parallel Element (XMLA)
  Identifica comandos a serem executados em paralelo pelo comando pai [Batch](../xml-elements-commands/batch-element-xmla.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Batch>  
   ....  
   <Parallel maxParallel="Integer">  
      <!-- One or more XMLA commands -->  
   </Parallel>  
   ....  
</Batch>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Lote](../xml-elements-commands/batch-element-xmla.md)|  
|Elementos filho|[Elemento Process](../xml-elements-commands/process-element-xmla.md)|  
  
## <a name="attributes"></a>Atributos  
  
|attribute|Description|  
|---------------|-----------------|  
|maxParallel|Opcional `Integer` atributo. Indica o número de máximo de threads nos quais devem ser executados comandos em paralelo. Se não for especificado ou definido como 0, a instância de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] determina um número ideal de threads com base no número de processadores disponíveis no computador.|  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
