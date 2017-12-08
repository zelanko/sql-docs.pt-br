---
title: Elemento DeniedSet (ASSL) | Microsoft Docs
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
apiname: DeniedSet Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: DeniedSet
helpviewer_keywords: DeniedSet element
ms.assetid: 898deefb-822d-458b-96d8-880da287b687
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2a750f409d45a50fca4c7cc5efbdf1240de74f88
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="deniedset-element-assl"></a>Elemento DeniedSet (ASSL)
  Contém uma expressão de conjunto que define a lista de permissões negadas no atributo associado.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<AttributePermission>  
      ...  
   <DeniedSet>...</DeniedSet>  
      ...  
</AttributePermission>  
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
|Elemento pai|[AttributePermission](../../../analysis-services/scripting/objects/attributepermission-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O elemento que corresponde ao pai do **DeniedSet** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.AttributePermission>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
