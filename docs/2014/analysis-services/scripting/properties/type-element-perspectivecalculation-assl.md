---
title: Tipo de elemento (PerspectiveCalculation) (ASSL) | Microsoft Docs
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
- Type Element (PerspectiveCalculation)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TYPE
helpviewer_keywords:
- Type element
ms.assetid: d7b87aea-3265-4f3c-a7ee-4f3e90f9a0b7
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 242d4d779da87c155371047fd2bb21128da51abf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36010984"
---
# <a name="type-element-perspectivecalculation-assl"></a>Elemento Type (PerspectiveCalculation) (ASSL)
  Indica o tipo do [PerspectiveCalculation](../data-type/perspectivecalculation-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<PerspectiveCalculation>  
   ...  
   <Type>...</Type>  
   ...  
</PerspectiveCalculation>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|Nenhum|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[PerspectiveCalculation](../data-type/perspectivecalculation-data-type-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Membro*|membro calculado|  
|*definir*|Conjunto nomeado|  
  
 A enumeração que corresponde aos valores permitidos para `Type` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.PerspectiveCalculationType>.  
  
 O elemento que corresponde ao pai do `Type` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.PerspectiveCalculation>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  