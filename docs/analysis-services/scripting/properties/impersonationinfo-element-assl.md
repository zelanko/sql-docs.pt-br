---
title: Elemento ImpersonationInfo (ASSL) | Microsoft Docs
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
apiname: ImpersonationInfo Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
helpviewer_keywords: ImpersonationInfo element
ms.assetid: d4b9c372-1023-43f7-97e9-b0a90f544fbb
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 91bc024cd8d42bc77f4df1b431d4df25c053a133
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="impersonationinfo-element-assl"></a>Elemento ImpersonationInfo (ASSL)
  Contém as informações usadas para determinar o comportamento de personificação ao acessar ou executar um assembly.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Assembly> <!-- or one of the elements listed in the Element Relationships table -->  
   <ImpersonationInfo>  
      <!-- Child elements are only those that are inherited from ImpersonationInfo -->  
   </ImpersonationInfo>  
</Assembly>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|[ImpersonationInfo](../../../analysis-services/scripting/data-type/impersonationinfo-data-type-assl.md)|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Assembly](../../../analysis-services/scripting/data-type/assembly-data-type-assl.md), [a fonte de dados](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
