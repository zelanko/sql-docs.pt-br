---
title: Elemento AllMemberName (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- AllMemberName Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AllMemberName
helpviewer_keywords:
- AllMemberName element
ms.assetid: 5fda5563-cb7a-4402-82ad-3d6c432b6a7e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b5a9e16de5a541b9d95cb50c0e2585f6f29ab3ba
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48139536"
---
# <a name="allmembername-element-assl"></a>Elemento AllMemberName (ASSL)
  Contém a legenda no idioma padrão para todos os membros de um [hierarquia](../objects/hierarchy-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Hierarchy>  
      ...  
      <AllMemberName>...</AllMemberName>  
   ...  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres|  
|Valor padrão|None|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[Hierarchy](../objects/hierarchy-element-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 O elemento que corresponde ao pai de `AllMemberName` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.Hierarchy>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
