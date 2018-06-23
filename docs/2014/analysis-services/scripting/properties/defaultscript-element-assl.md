---
title: Elemento DefaultScript (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- DefaultScript Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DefaultScript
helpviewer_keywords:
- DefaultScript element
ms.assetid: 60716e63-2d64-4774-9ac9-253efe612fa5
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b0a26b8b703636aebb6d3701c5c7c99d24a25ade
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36130643"
---
# <a name="defaultscript-element-assl"></a>Elemento DefaultScript (ASSL)
  Identifica o padrão [MdxScript](../objects/mdxscript-element-assl.md) elemento o [MdxScripts](../collections/mdxscripts-element-assl.md) coleção.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<MdxScript>  
   ...  
   <DefaultScript>...</DefaultScript>  
   ...  
</MdxScript>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Booliano|  
|Valor padrão|`True`|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[MdxScript](../objects/mdxscript-element-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 A definição do valor de `DefaultScript` to `True` para um script define o valor de `DefaultScript` como `False` para todos os outros elementos `MdxScript` na coleção `MdxScripts`.  
  
 O elemento que corresponde ao pai do `DefaultScript` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.MdxScript>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  