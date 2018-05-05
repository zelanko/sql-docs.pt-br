---
title: Paralelo elemento (XMLA) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.custom: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Parallel Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Parallel
- http://schemas.microsoft.com/analysisservices/2003/engine#Parallel
- microsoft.xml.analysis.parallel
helpviewer_keywords:
- Parallel element
ms.assetid: 04726d94-37ee-460b-9744-d62b45f536b9
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 418abdbe67b68af87f9e072ba46957d337a6127f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="parallel-element-xmla"></a>Parallel Element (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Especifica o número de trabalhos de processamento pode ser executado em paralelo usando o pai [lote](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md) comando.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Batch>  
   ....  
   <Parallel maxParallel="Integer">  
      <!-- An XMLA process command -->  
   </Parallel>  
   ....  
</Batch>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Lote](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)|  
|Elementos filho|[Elemento Process](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)|  
  
## <a name="attributes"></a>Atributos  
  
|Atributo|Description|  
|---------------|-----------------|  
|maxParallel|Atributo **Integer** opcional. Indica o número de máximo de threads nos quais devem ser executados comandos em paralelo. Se não for especificado ou definido como 0, a instância de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] determina um número ideal de threads com base no número de processadores disponíveis no computador.|  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
