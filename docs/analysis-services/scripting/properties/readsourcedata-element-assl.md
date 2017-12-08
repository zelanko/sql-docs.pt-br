---
title: Elemento ReadSourceData (ASSL) | Microsoft Docs
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
apiname: ReadSourceData Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
helpviewer_keywords: ReadSourceData element
ms.assetid: 7da4665a-fba3-4aae-8dee-678dc14d3b05
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 979333e3bd6a441d26c2ea069589b354d9fda43b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="readsourcedata-element-assl"></a>Elemento ReadSourceData (ASSL)
  Determina como nomes exclusivos são gerados para hierarquias que estão contidas dentro do [CubePermission](../../../analysis-services/scripting/objects/cubepermission-element-assl.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<CubePermission>  
   ...  
   <ReadSourceData>...</ReadSourceData>  
   ...  
</CubePermission>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Nenhuma*|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[CubePermission](../../../analysis-services/scripting/objects/cubepermission-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Nenhuma*|Nenhum acesso é permitido aos dados disponíveis na fase de cálculo 0.|  
|*Permitido*|O acesso é permitido aos dados disponíveis na fase de cálculo 0.|  
  
## <a name="remarks"></a>Comentários  
 O elemento que corresponde ao pai do **ReadSourceData** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.CubePermission>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento Cube &#40; ASSL &#41;](../../../analysis-services/scripting/objects/cube-element-assl.md)   
 [Elemento Dimension &#40; ASSL &#41;](../../../analysis-services/scripting/objects/dimension-element-assl.md)   
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
