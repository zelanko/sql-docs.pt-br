---
title: Elemento TargetType (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- TargetType Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TargetType
helpviewer_keywords:
- TargetType element
ms.assetid: 2c69ea6e-2af7-435b-9841-86117d5554a7
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0b21033bb9a7e20923adccfa135475cf93dafb7c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37237556"
---
# <a name="targettype-element-assl"></a>Elemento TargetType (ASSL)
  Identifica o tipo de item do item identificado na [destino](target-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Action>  
   ...  
   <TargetType>...</TargetType>  
   ...  
</Action>  
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
|Elemento pai|[Ação](../objects/action-element-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Cube*|O destino da ação é um cubo.|  
|*Células*|O destino da ação é um subcubo.|  
|*Definir*|O destino da ação é um conjunto.|  
|*Hierarchy*|O destino da ação é uma hierarquia.|  
|*Level*|O destino da ação é um nível.|  
|*DimensionMembers*|O destino da ação são os membros de uma dimensão.|  
|*HierarchyMembers*|O destino da ação são os membros de uma hierarquia.|  
|*LevelMembers*|O destino da ação são os membros de um nível.|  
|*AttributeMembers*|O destino da ação são os membros de um atributo.|  
  
 A enumeração que corresponde aos valores permitidos para `TargetType` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.ActionTargetType>.  
  
 O elemento que corresponde ao pai de `TargetType` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.Action>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
