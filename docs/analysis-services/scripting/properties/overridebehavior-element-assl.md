---
title: Elemento OverrideBehavior (ASSL) | Microsoft Docs
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
apiname: OverrideBehavior Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
helpviewer_keywords: OverrideBehavior element
ms.assetid: 6a5b361a-6061-4b73-b1a7-1237fb77606c
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4f917a5ee24e47cf3989bd2b65d6e968774db637
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="overridebehavior-element-assl"></a>Elemento OverrideBehavior (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Indica o comportamento de substituição da relação descrita por um [AttributeRelationship](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<AttributeRelationship>  
   ...  
   <OverrideBehavior>...</OverrideBehavior>  
   ...  
</AttributeRelationship>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Alta segurança*|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[AttributeRelationship](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O elemento **OverrideBehavior** determina como o posicionamento no atributo relacionado afeta o posicionamento no atributo.  
  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Alta segurança*|Indica o comportamento substituto da relação descrita por um elemento AttributeRelationship. Dita como o posicionamento em um atributo afeta a posição do outro.|  
|*Nenhuma*|Nenhum efeito.|  
  
 A enumeração que corresponde aos valores permitidos para **OverrideBehavior** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.OverrideBehavior>.  
  
## <a name="see-also"></a>Consulte também  
 [Atributos e hierarquias de atributo](../../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
