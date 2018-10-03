---
title: Cubo de elemento (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Cube Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.cube
- urn:schemas-microsoft-com:xml-analysis#Cube
- http://schemas.microsoft.com/analysisservices/2003/engine#Cube
helpviewer_keywords:
- Cube element
ms.assetid: 2e8662f4-fb2e-43af-b70a-9e0b5872c9b9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: de5c375e5e517e155bd6efb4beeeef61e9f31a79
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48103356"
---
# <a name="cube-element-xmla"></a>Elemento Cube (XMLA)
  Identifica o cubo que contém a dimensão representada pelo pai [objeto](object-element-dimension-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Object>  
   ...  
   <Cube>...</Cube>  
   ...  
</Object>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres|  
|Valor padrão|None|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Objeto](object-element-dimension-xmla.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 O elemento `Cube` é um identificador de objeto que contém o nome do cubo que contém a dimensão representada pelo elemento `Object`.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento de banco de dados &#40;XMLA&#41;](database-element-xmla.md)   
 [Elemento de dimensão &#40;XMLA&#41;](dimension-element-xmla.md)   
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
