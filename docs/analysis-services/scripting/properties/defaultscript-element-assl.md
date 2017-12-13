---
title: Elemento DefaultScript (ASSL) | Microsoft Docs
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
apiname: DefaultScript Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: DefaultScript
helpviewer_keywords: DefaultScript element
ms.assetid: 60716e63-2d64-4774-9ac9-253efe612fa5
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 525f0060bdcdce8a82850ee78717e41f83e945ac
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="defaultscript-element-assl"></a>Elemento DefaultScript (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Identifica o padrão [MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md) elemento o [MdxScripts](../../../analysis-services/scripting/collections/mdxscripts-element-assl.md) coleção.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<MdxScript>  
   ...  
   <DefaultScript>...</DefaultScript>  
   ...  
</MdxScript>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Boolean|  
|Valor padrão|**Verdadeiro**|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 A definição do valor de **DefaultScript** to **True** para um script define o valor de **DefaultScript** como **False** para todos os outros elementos **MdxScript** na coleção **MdxScripts** .  
  
 O elemento que corresponde ao pai do **DefaultScript** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.MdxScript>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
