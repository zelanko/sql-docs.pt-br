---
title: Elemento (ASSL) de destino | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Target Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Target
helpviewer_keywords:
- Target element
ms.assetid: 08ce0441-94b6-4f1d-acba-f31c8212cb79
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 23d55d909179fd568075feba54199514a7396c6b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48169056"
---
# <a name="target-element-assl"></a>Elemento Target (ASSL)
  Identifica o destino do [ação](../objects/action-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Action>  
   ...  
   <Target>...</Target>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres|  
|Valor padrão|None|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[Ação](../objects/action-element-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 O valor esperado deste elemento depende do valor da [TargetType](targettype-element-assl.md) elemento para o pai `Action`. A tabela a seguir descreve os valores esperados de `Target` com base no valor de `TargetType`.  
  
|Valor de TargetType|Valor esperado|  
|----------------------|--------------------|  
|*Cube*|Nome de um cubo.|  
|*Células*|Uma expressão de subcubo.|  
|*Definir*|Uma expressão de conjunto ou o nome de um conjunto nomeado. **Observação:** uma instrução de Subseleção não pode ser usada.|  
|*Hierarquia de HierarchyMembers*|O nome de uma hierarquia.|  
|*Dimensão, DimensionMembers*|O nome de uma dimensão.|  
|*Nível, LevelMembers*|Nome de um nível.|  
|*Atributo, AttributeMembers*|Nome de um atributo.|  
  
 O elemento que corresponde ao pai de `Target` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.Action>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
