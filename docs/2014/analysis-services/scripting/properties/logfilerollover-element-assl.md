---
title: Elemento LogFileRollover (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- LogFileRollover Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- LogFileRollover
helpviewer_keywords:
- LogFileRollover element
ms.assetid: 5484e167-b891-431a-bbae-946ea6eb4a3c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4c9c07dd08cacfbc273f2b0e691b178d4953ce42
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48054846"
---
# <a name="logfilerollover-element-assl"></a>Elemento LogFileRollover (ASSL)
  Especifica se o registro de [rastreamento](../objects/trace-element-assl.md) saída deve captar um novo arquivo ou deve parar quando o arquivo de log máximo tamanho especificado em [LogFileSize](logfilesize-element-assl.md) for atingido.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Trace>  
   ...  
   <LogFileRollover>...</LogFileRollover>  
   ...  
</Trace>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Booliano|  
|Valor padrão|Falso|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[Rastreamento](../objects/trace-element-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 Se o valor do elemento `LogFileRollover` for definido como True, um novo arquivo será iniciado quando o tamanho do arquivo de log excede o valor especificado no elemento `LogFileSize` do elemento pai `Trace`; caso contrário, o registro para.  
  
 O elemento que corresponde ao pai de `LogFileRollover` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.Trace>.  
  
## <a name="see-also"></a>Consulte também  
 [Rastreia o elemento &#40;ASSL&#41;](../collections/traces-element-assl.md)   
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
