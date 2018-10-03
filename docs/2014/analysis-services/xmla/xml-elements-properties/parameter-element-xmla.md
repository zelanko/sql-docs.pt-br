---
title: Elemento Parameter (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Parameter Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Parameter
- microsoft.xml.analysis.parameter
- http://schemas.microsoft.com/analysisservices/2003/engine#Parameter
helpviewer_keywords:
- Parameter element
ms.assetid: fe31ac3d-a3e8-4f60-a81a-c43271ddbed4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7638e033cab8f940972b35ea6c7a7a4abb402ee3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48079246"
---
# <a name="parameter-element-xmla"></a>Elemento Parameter (XMLA)
  Contém o nome e valor de um parâmetro usados pelo método [Execute](../xml-elements-methods-execute.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<Parameters>  
...  
   <Parameter>  
      <Name>...</Name>  
      <Value>...</Value>  
   </Parameter>  
...  
</Parameters>  
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
|Elementos pai|[Parâmetros](parameters-element-xmla.md)|  
|Elementos filho|[Nome](name-element-parameter-xmla.md), [Value](value-element-parameter-xmla.md)|  
  
## <a name="remarks"></a>Comentários  
 Alguns comandos do XMLA (XML for Analysis), como o comando [Process](../xml-elements-commands/process-element-xmla.md) , podem requerer informações adicionais. O elemento `Parameter` fornece um mecanismo para fornecer informações adicionais, incluindo partes de informações, de um comando XMLA.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
