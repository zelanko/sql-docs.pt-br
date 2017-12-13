---
title: Elemento CaptionColumn (ASSL) | Microsoft Docs
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
apiname: CaptionColumn Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: CaptionColumn
helpviewer_keywords: CaptionColumn element
ms.assetid: bdb1b9b8-b5d5-4d91-81c7-8de8635bbb83
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2ac5076a20cf8c42b1c4441cef8ad01babaca2a3
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="captioncolumn-element-assl"></a>Elemento CaptionColumn (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Define a coluna que fornece a legenda para o atributo.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<AttributeTranslation>  
   ...  
   <CaptionColumn xsi:type="DataItem">...</CaptionColumn>  
   ...  
</AttributeTranslation>  
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
|Elementos pai|[AttributeTranslation](../../../analysis-services/scripting/data-type/attributetranslation-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 Para obter mais informações sobre o **DataItem** tipo, incluindo uma tabela de objetos do Analysis Services Scripting Language (ASSL) e propriedades do **DataItem** de tipo, consulte [tipo de dados de item de dados &#40; ASSL &#41; ](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md).  
  
 O elemento que corresponde ao pai do **CaptionColumn** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.AttributeTranslation>.  
  
## <a name="see-also"></a>Consulte também  
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
