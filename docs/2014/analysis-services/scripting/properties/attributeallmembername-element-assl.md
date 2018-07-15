---
title: Elemento AttributeAllMemberName (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- AttributeAllMemberName Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AttributeAllMemberName
helpviewer_keywords:
- AttributeAllMemberName element
ms.assetid: 5ede46a7-d8b0-40be-98d7-b01047b27d2e
caps.latest.revision: 36
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 425e9c092dff8cc3c303672b6bfb1e2b3a8096ad
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37208046"
---
# <a name="attributeallmembername-element-assl"></a>Elemento AttributeAllMemberName (ASSL)
  Contém a legenda, no idioma padrão, do membro All da dimensão.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Dimension>  
      ...  
   <AttributeAllMemberName>...</AttributeAllMemberName>  
   ...  
</Dimension>  
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
|Elemento pai|[Dimension](../objects/dimension-element-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O elemento que corresponde ao pai de `AttributeAllMemberName` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.Dimension>.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar o &#40;todos os&#41; nível para hierarquias de atributo](../../multidimensional-models/database-dimensions-configure-the-all-level-for-attribute-hierarchies.md)   
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
