---
title: Elemento AggregationType (ASSL) | Microsoft Docs
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
apiname: AggregationType Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
helpviewer_keywords: AggregationType element
ms.assetid: c1393bc6-d715-4397-8bc5-82abdb275330
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a9909b25a064602485c8540abaa244e6835302ec
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="aggregationtype-element-assl"></a>Elemento AggregationType (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Define o tipo de agregação armazenado pelo [partição](../../../analysis-services/scripting/objects/partition-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<AggregationInstance>  
   ...  
   <AggregationType>...</AggregationType>  
   ...  
</AggregationInstance>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-1: elemento obrigatório que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[AggregationInstance](../../../analysis-services/scripting/objects/aggregationinstance-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*IndexedView*|A agregação é armazenada em uma exibição indexada.|  
|*Table*|A agregação é armazenada em uma tabela.|  
|*UserDefined*|A agregação está definida pelo usuário.|  
  
 A enumeração que corresponde aos valores permitidos para **AggregationType** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.AggregationInstance>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
