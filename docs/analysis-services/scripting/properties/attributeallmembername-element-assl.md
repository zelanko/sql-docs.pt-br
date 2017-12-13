---
title: Elemento AttributeAllMemberName (ASSL) | Microsoft Docs
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
apiname: AttributeAllMemberName Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: AttributeAllMemberName
helpviewer_keywords: AttributeAllMemberName element
ms.assetid: 5ede46a7-d8b0-40be-98d7-b01047b27d2e
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 17e2e2f3ddd5cc65774276b33ef85871a287109e
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="attributeallmembername-element-assl"></a>Elemento AttributeAllMemberName (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Contém a legenda, no idioma padrão, para todos os membros da dimensão.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Dimension>  
      ...  
   <AttributeAllMemberName>...</AttributeAllMemberName>  
   ...  
</Dimension>  
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
|Elemento pai|[Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O elemento que corresponde ao pai do **AttributeAllMemberName** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.Dimension>.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar o &#40; Todos os &#41; Nível para hierarquias de atributo](../../../analysis-services/multidimensional-models/database-dimensions-configure-the-all-level-for-attribute-hierarchies.md)   
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
