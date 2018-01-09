---
title: Elemento OrderBy (ASSL) | Microsoft Docs
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
apiname: OrderBy Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: OrderBy
helpviewer_keywords: OrderBy element
ms.assetid: d7a0564b-430e-44eb-913a-fe1f98917d0f
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 168e8f528459f30b612219e9fa1e2d3cdc7e0af1
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="orderby-element-assl"></a>Elemento OrderBy (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Descreve como ordenar os membros contidos no atributo.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DimensionAttribute>  
   ...  
      <OrderBy>...</OrderBy>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Nome*|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Nome*|Ordene pelo nome de membro.|  
|*Chave*|Ordene pela chave de membro.|  
|*AttributeKey*|Ordenar por chave de membro do atributo especificado no [OrderByAttributeID](../../../analysis-services/scripting/properties/orderbyattributeid-element-assl.md) elemento **DimensionAttribute**.|  
|*AttributeName*|Ordene pelo nome de membro do atributo especificado no elemento **OrderByAttributeID** de **DimensionAttribute**.|  
  
 A enumeração que corresponde aos valores permitidos para **OrderBy** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.OrderBy>.  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
