---
title: Elemento ActionID (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
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
apiname: ActionID Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: ActionID
helpviewer_keywords: ActionID element
ms.assetid: 2c9c66b2-a7ea-4874-a0ed-020ce3feab20
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 47ced926c091ed13f473afd2c8c7f92d778887ba
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="actionid-element-assl"></a>Elemento ActionID (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Contém o nome de um [ação](../../../analysis-services/scripting/objects/action-element-assl.md) elemento definido em um [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md) elemento que é disponibilizado em um [perspectiva](../../../analysis-services/scripting/objects/perspective-element-assl.md) elemento como um [PerspectiveAction](../../../analysis-services/scripting/data-type/perspectiveaction-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<PerspectiveAction>  
   <ActionID>...</ActionID  
</PerspectiveAction>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|String|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[PerspectiveAction](../../../analysis-services/scripting/data-type/perspectiveaction-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O elemento que corresponde ao pai do **ActionID** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.PerspectiveAction>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento Actions &#40; ASSL &#41;](../../../analysis-services/scripting/collections/actions-element-assl.md)   
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
