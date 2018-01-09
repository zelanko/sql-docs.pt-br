---
title: Legenda do elemento (ASSL) | Microsoft Docs
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
apiname: Caption Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Caption
helpviewer_keywords: Caption element
ms.assetid: ed2be851-0ddc-4fa5-8aee-b2acb2e6d25e
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 61c9c0f7cec3056c98cc00275cff275602368a6b
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="caption-element-assl"></a>Elemento Caption (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Contém a legenda do elemento pai associado.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Action> <!-- or Translation -->  
   ...  
  <Caption>...</Caption>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[Ação](../../../analysis-services/scripting/objects/action-element-assl.md), [tradução](../../../analysis-services/scripting/objects/translation-element-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 Os elementos que correspondem aos pais de **legenda** no modelo de objeto de Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.Action> e <xref:Microsoft.AnalysisServices.Translation>.  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
