---
title: Elemento OptimizedState (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: OptimizedState Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: OptimizedState
helpviewer_keywords: OptimizedState element
ms.assetid: 120dcc4c-8fe8-4471-bbd6-99ad534364f0
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 154348d593c3f1fff01a181be362ad6dbbe19631
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="optimizedstate-element-assl"></a>Elemento OptimizedState (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Determina o nível de otimização aplicado à hierarquia.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<CubeHierarchy>  
   ...  
   <OptimizedState>...</OptimizedState>  
   ...  
</CubeHierarchy>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*FullyOptimized*|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[CubeHierarchy](../../../analysis-services/scripting/data-type/cubehierarchy-data-type-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*FullyOptimized*|A instância cria índices para a hierarquia a fim de melhorar o desempenho das consultas.|  
|*NotOptimized*|A instância não cria índices adicionais.|  
  
 A enumeração que corresponde aos valores permitidos para **OptimizedState** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.OptimizationType>.  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
