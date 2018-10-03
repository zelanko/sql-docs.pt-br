---
title: Elemento UnknownMember (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- UnknownMember Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- UnknownMember
helpviewer_keywords:
- UnknownMember element
ms.assetid: 5558961e-e3c6-4f4e-817d-5b12b0734c03
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dab3908376520a67e1192a0a4a2d52c76b6a88df
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48052326"
---
# <a name="unknownmember-element-assl"></a>Elemento UnknownMember (ASSL)
  Indica se o membro desconhecido é visível.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Dimension>  
      ...  
   <UnknownMember>...</UnknownMember>  
   ...  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Nenhuma*|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[Dimension](../objects/dimension-element-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Visível*|O membro desconhecido existe e é exibido.|  
|*Oculto*|O membro desconhecido existe, mas não é exibido.|  
|*Nenhuma*|O membro desconhecido não é usado.|  
  
 A enumeração que corresponde aos valores permitidos para `UnknownMember` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.UnknownMemberBehavior>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento UnknownMemberName &#40;ASSL&#41;](name-element-assl.md)   
 [Elemento UnknownMemberTranslation &#40;ASSL&#41;](../objects/translation-element-assl.md)   
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
