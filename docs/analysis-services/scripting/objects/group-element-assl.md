---
title: Grupo de elemento (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
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
apiname: Group Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: GROUP
helpviewer_keywords: Group element
ms.assetid: 7df4ba90-b39f-4d8a-8db1-b73639a522a6
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6cf72e2c4acc936037b51a197820325aa690b9e2
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="group-element-assl"></a>Elemento Group (ASSL)
  Define um grupo de membros associado a um atributo.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Groups>  
   <Group>  
      <Name>...</Name>  
      <Members>...</Members>  
   </Group>  
<Groups/>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-n: elemento obrigatório que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Grupos](../../../analysis-services/scripting/collections/groups-element-assl.md)|  
|Elementos filho|[Membros](../../../analysis-services/scripting/collections/members-element-assl.md), [Nome](../../../analysis-services/scripting/properties/name-element-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.Group>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipo de dados UserDefinedGroupBinding &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/userdefinedgroupbinding-data-type-assl.md)   
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
