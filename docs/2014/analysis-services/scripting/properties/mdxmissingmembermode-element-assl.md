---
title: Elemento MdxMissingMemberMode (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MdxMissingMemberMode Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- MdxMissingMemberMode element
ms.assetid: aca6130b-5fb8-4fa1-af8b-8e1ef361926f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c942587601c5e62d9e876be8eb1277f638eaa7ef
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48126727"
---
# <a name="mdxmissingmembermode-element-assl"></a>Elemento MdxMissingMemberMode (ASSL)
  Determina como são tratados membros ausentes para linguagens MDX.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Dimension>  
   ...  
   <MdxMissingMemberMode>...</MdxMissingMemberMode>  
   ...  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Default*|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[Dimension](../data-type/dimension-data-type-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Ignorar*|São ignorados membros ausentes.|  
|*Erro*|Um erro surgirá se membros ausentes forem encontrados.|  
|*Default*|São ignorados membros ausentes.|  
  
 O elemento que corresponde ao pai de `MdxMissingMemberMode` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.Dimension>.  
  
## <a name="see-also"></a>Consulte também  
 [Expressões multidimensionais &#40;MDX&#41; referência](/sql/mdx/multidimensional-expressions-mdx-reference)   
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
