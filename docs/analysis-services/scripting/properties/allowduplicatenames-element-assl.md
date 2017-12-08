---
title: Elemento AllowDuplicateNames (ASSL) | Microsoft Docs
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
apiname: AllowDuplicateNames Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: AllowDuplicateNames
helpviewer_keywords: AllowDuplicateNames element
ms.assetid: d0a80040-115f-4490-926f-4d64d8977e67
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 45beca28a1a17afdf7645d8a42cbab519e51373e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="allowduplicatenames-element-assl"></a>Elemento AllowDuplicateNames (ASSL)
  Determina se são permitidos nomes duplicados em um [hierarquia](../../../analysis-services/scripting/objects/hierarchy-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Hierarchy>  
      ...  
   <AllowDuplicateNames>...</AllowDuplicateNames>  
   ...  
</Hierarchy>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Boolean|  
|Valor padrão|**Verdadeiro**|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[Hierarchy](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O elemento que corresponde ao pai do **AllowDuplicateNames** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.Hierarchy>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
