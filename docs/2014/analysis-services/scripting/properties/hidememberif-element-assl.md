---
title: Elemento HideMemberIf (ASSL) | Microsoft Docs
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
- HideMemberIf Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- HideMemberIf
helpviewer_keywords:
- HideMemberIf element
ms.assetid: ff0e6b19-6216-43ac-ba76-1628da8c333b
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0829804ae0225c848da3583c429e39d9bc176821
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37187023"
---
# <a name="hidememberif-element-assl"></a>Elemento HideMemberIf (ASSL)
  Indica se, e quando, um membro em um nível ficará oculto pelos aplicativos cliente.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Level>  
   ...  
   <HideMemberIf>...</HideMemberIf>  
   ...  
</Level>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Nunca*|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[Level](../objects/level-element-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Nunca*|Membros nunca são ocultados.|  
|*OnlyChildWithNoName*|Um membro é ocultado quando ele for o único filho de seu pai e seu nome estiver vazio.|  
|*OnlyChildWithParentName*|Um membro é ocultado quando ele for o único filho de seu pai e seu nome for idêntico ao de seu pai.|  
|*NoName*|Um membro é ocultado quando seu nome estiver vazio.|  
|*ParentName*|Um membro é ocultado quando seu nome for idêntico ao de seu pai.|  
  
## <a name="remarks"></a>Remarks  
 A enumeração que corresponde aos valores permitidos para `HideMemberIf` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.HideIfValue>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
