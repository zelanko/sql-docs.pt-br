---
title: Elemento MemberUniqueNameStyle (ASSL) | Microsoft Docs
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
- MemberUniqueNameStyle Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- MemberUniqueNameStyle element
ms.assetid: f0771c81-0127-4203-9501-ae4f864730fa
caps.latest.revision: 14
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2448f2f45f76610e9d7298c855086cc74ab0611e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37226356"
---
# <a name="memberuniquenamestyle-element-assl"></a>Elemento MemberUniqueNameStyle (ASSL)
  Determina como nomes exclusivos são gerados para membros de hierarquias contidas dentro de [CubeDimension](../data-type/dimension-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<CubeDimension>  
   ...  
   <MemberUniqueNameStyle>...</MemberUniqueNameStyle>  
   ...  
</CubeDimension>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Nativo*|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[CubeDimension](../data-type/dimension-data-type-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Nativo*|A instância determina automaticamente os nomes exclusivos dos membros.|  
|*NamePath*|A instância gera um nome composto formado por cada nível e a legenda do membro.|  
  
## <a name="remarks"></a>Remarks  
 O elemento que corresponde ao pai de `MemberUniqueNameStyle` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.CubeDimension>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento de cubo &#40;ASSL&#41;](../objects/cube-element-assl.md)   
 [Elemento de dimensão &#40;ASSL&#41;](../objects/dimension-element-assl.md)   
 [Tipo de dados CubeDimension &#40;ASSL&#41;](../data-type/dimension-data-type-assl.md)  
  
  
