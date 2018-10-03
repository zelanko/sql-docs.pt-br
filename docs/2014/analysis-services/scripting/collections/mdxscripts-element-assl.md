---
title: Elemento MdxScripts (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MdxScripts Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MdxScripts
helpviewer_keywords:
- MdxScripts element
ms.assetid: 0aaa849f-e723-4245-8c16-7ed049590fd2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 684549f87a4fe8e5d8f5e34093cd30d9b99fe80d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48047618"
---
# <a name="mdxscripts-element-assl"></a>Elemento MdxScripts (ASSL)
  Contém a coleção de [MdxScript](../objects/mdxscript-element-assl.md) elementos associados a um [cubo](../objects/cube-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Cube>  
   ...  
   <MdxScripts>  
      <MdxScript>...</MdxScript>  
   </MdxScripts>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|None|  
|Valor padrão|None|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Cube](../objects/cube-element-assl.md)|  
|Elementos filho|[MdxScript](../objects/mdxscript-element-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.MdxScriptCollection>.  
  
## <a name="see-also"></a>Consulte também  
 [Coleções &#40;ASSL&#41;](collections-assl.md)  
  
  
