---
title: Elemento CancelAssociated (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- CancelAssociated Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.cancelassociated
- urn:schemas-microsoft-com:xml-analysis#CancelAssociated
- http://schemas.microsoft.com/analysisservices/2003/engine#CancelAssociated
helpviewer_keywords:
- CancelAssociated element
ms.assetid: fd890440-d1a7-4c05-9e81-c81e6b8c274c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 294f1060c0a52c357e791d5b3db7ad87d0d98309
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48126586"
---
# <a name="cancelassociated-element-xmla"></a>Elemento CancelAssociated (XMLA)
  Indica se o elemento pai [Cancel](../xml-elements-commands/cancel-element-xmla.md) deve cancelar todos os comandos associados.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Cancel>  
   ...  
   <ConnectionID>...</ConnectionID>  
   ...  
</Cancel>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Booliano|  
|Valor padrão|Falso|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Cancelar](../xml-elements-commands/cancel-element-xmla.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 Se esse elemento for especificado e definido como `True`, cada conexão correspondente, sessão e comando identificado no pai `Cancel` comando seja cancelado.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento ConnectionID &#40;XMLA&#41;](id-element-xmla.md)   
 [Elemento SessionID &#40;XMLA&#41;](sessionid-element-xmla.md)   
 [Elemento SPID &#40;XMLA&#41;](spid-element-xmla.md)   
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
