---
title: Elemento LogFileRollover (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 73762fbfb606067d7f90beb2b11364d9e8dd0b4d
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="logfilerollover-element-assl"></a>Elemento LogFileRollover (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Especifica se o registro de [rastreamento](../../../analysis-services/scripting/objects/trace-element-assl.md) saída deve passar para um novo arquivo ou deve parar quando o arquivo de log máximo tamanho especificado em [LogFileSize](../../../analysis-services/scripting/properties/logfilesize-element-assl.md) for atingido.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Trace>  
   ...  
   <LogFileRollover>...</LogFileRollover>  
   ...  
</Trace>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Boolean|  
|Valor padrão|False|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[Rastreamento](../../../analysis-services/scripting/objects/trace-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 Se o valor do elemento **LogFileRollover** for definido como True, um novo arquivo será iniciado quando o tamanho do arquivo de log excede o valor especificado no elemento **LogFileSize** do elemento pai **Trace** ; caso contrário, o registro para.  
  
 O elemento que corresponde ao pai do **LogFileRollover** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.Trace>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento de rastreamentos & #40; ASSL & #41;](../../../analysis-services/scripting/collections/traces-element-assl.md)   
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
