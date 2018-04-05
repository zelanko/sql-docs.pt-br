---
title: Elemento Annotations (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Annotations Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Annotations
helpviewer_keywords:
- Annotations element
ms.assetid: b2236075-6a48-470d-8182-b0de112e258a
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f092133a6b4b7b61eb738bb1adc1e54a89c51209
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="annotations-element-assl"></a>Elemento Annotations (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Contém a coleção de [anotação](../../../analysis-services/scripting/objects/annotation-element-assl.md) elementos associados ao elemento pai.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Account>  
<!-- or another object in the Analysis Services Scripting Language -->  
   ...  
   <Annotations>  
      <Annotation>...</Annotation>  
   </Annotations>  
   ...  
</Account>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|A maioria dos objetos no Idioma do Script do Analysis Services|  
|Elementos filho|[Anotação](../../../analysis-services/scripting/objects/annotation-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.AnnotationCollection>.  
  
  
