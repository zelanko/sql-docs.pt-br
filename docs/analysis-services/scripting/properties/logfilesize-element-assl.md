---
title: Elemento LogFileSize (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- LogFileSize Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- LogFileSize
helpviewer_keywords:
- LogFileSize element
ms.assetid: d2135e68-57a9-4144-8403-9627041f2a58
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d950697bf156ab314d69fb4997816e6bca233e17
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="logfilesize-element-assl"></a>Elemento LogFileSize (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Especifica o tamanho máximo de arquivo de log em megabytes.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Trace>  
  
   <LogFileSize>...</LogFileSize>  
  
</Trace>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Integer|  
|Valor padrão|**5** (megabytes)|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[Rastreamento](../../../analysis-services/scripting/objects/trace-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 O elemento que corresponde ao pai do **LogFileSize** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.Trace>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento de rastreamentos & #40; ASSL & #41;](../../../analysis-services/scripting/collections/traces-element-assl.md)   
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
