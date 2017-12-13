---
title: Elemento UnaryOperatorColumn (ASSL) | Microsoft Docs
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
apiname: UnaryOperatorColumn Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: UnaryOperatorColumn
helpviewer_keywords: UnaryOperatorColumn element
ms.assetid: 10889e51-69e5-4f50-9749-ecbc66c247d3
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 535e5027b5708e74e0350b21f388c528a88fe160
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="unaryoperatorcolumn-element-assl"></a>Elemento UnaryOperatorColumn (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Define os detalhes de uma coluna que fornece um operador unário.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DimensionAttribute>  
   ...  
   <UnaryOperatorColumn xsi:type="DataItem">...</UnaryOperatorColumn>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|[O item de dados](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 Para obter mais informações sobre o **DataItem** tipo, incluindo uma tabela de objetos do Analysis Services Scripting Language (ASSL) e propriedades do **DataItem** de tipo, consulte [tipo de dados de item de dados &#40; ASSL &#41; ](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md).  
  
 O elemento que corresponde ao pai do **UnaryOperatorColumn** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.DimensionAttribute>.  
  
## <a name="see-also"></a>Consulte também  
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
