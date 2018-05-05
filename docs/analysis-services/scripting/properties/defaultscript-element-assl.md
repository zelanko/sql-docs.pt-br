---
title: Elemento DefaultScript (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- DefaultScript Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- DefaultScript
helpviewer_keywords:
- DefaultScript element
ms.assetid: 60716e63-2d64-4774-9ac9-253efe612fa5
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 87055949cf70435c1bbae4b34ff0d34aaa769e6b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="defaultscript-element-assl"></a>Elemento DefaultScript (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Identifica o padrão [MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md) elemento o [MdxScripts](../../../analysis-services/scripting/collections/mdxscripts-element-assl.md) coleção.  
  
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
  
## <a name="remarks"></a>Remarks  
 A definição do valor de **DefaultScript** to **True** para um script define o valor de **DefaultScript** como **False** para todos os outros elementos **MdxScript** na coleção **MdxScripts** .  
  
 O elemento que corresponde ao pai do **DefaultScript** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.MdxScript>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
