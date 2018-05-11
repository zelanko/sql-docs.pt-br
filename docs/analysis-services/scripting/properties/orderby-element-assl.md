---
title: Elemento OrderBy (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ac17b52d36b414854da027dc3cf2c4a8f768e9f6
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="orderby-element-assl"></a>Elemento OrderBy (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Descreve como ordenar os membros contidos no atributo.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DimensionAttribute>  
   ...  
      <OrderBy>...</OrderBy>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Nome*|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Nome*|Ordene pelo nome de membro.|  
|*Chave*|Ordene pela chave de membro.|  
|*AttributeKey*|Ordenar por chave de membro do atributo especificado no [OrderByAttributeID](../../../analysis-services/scripting/properties/orderbyattributeid-element-assl.md) elemento **DimensionAttribute**.|  
|*AttributeName*|Ordene pelo nome de membro do atributo especificado no elemento **OrderByAttributeID** de **DimensionAttribute**.|  
  
 A enumeração que corresponde aos valores permitidos para **OrderBy** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.OrderBy>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
