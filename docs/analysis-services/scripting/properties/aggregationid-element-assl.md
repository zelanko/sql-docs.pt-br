---
title: Elemento AggregationID (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- AggregationID Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- AggregationID element
ms.assetid: 6056da1d-b6b4-4074-84db-45be719df49a
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 839014c19a80b8689d4a94178c25af7fb4c673c8
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="aggregationid-element-assl"></a>Elemento AggregationID (ASSL)
  Identifica a definição de agregação do [AggregationDesign](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md) elemento usado para criar a instância de agregação.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<AggregationInstance>  
   ...  
   <AggregationID>...</AggregationID>  
   ...  
</AggregationInstance>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|String|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[AggregationInstance](../../../analysis-services/scripting/objects/aggregationinstance-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 Se esse elemento estiver ausente ou for definido como uma cadeia de caracteres em branco, o elemento **AggregationInstance** representará uma agregação definida pelo usuário.  
  
 O elemento que corresponde ao pai do **AggregationID** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.AggregationInstance>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

