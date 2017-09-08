---
title: Elemento (ASSL) de destino | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Target Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Target
helpviewer_keywords:
- Target element
ms.assetid: 08ce0441-94b6-4f1d-acba-f31c8212cb79
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 09e5337cbdc4cd909b2251f42544bb930b9461f6
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="target-element-assl"></a>Elemento Target (ASSL)
  Identifica o destino do [ação](../../../analysis-services/scripting/objects/action-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Action>  
   ...  
   <Target>...</Target>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|String|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[Ação](../../../analysis-services/scripting/objects/action-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O valor esperado deste elemento depende do valor da [TargetType](../../../analysis-services/scripting/properties/targettype-element-assl.md) elemento pai **ação**. A tabela a seguir descreve os valores esperados de **Target** com base no valor de **TargetType**.  
  
|Valor de TargetType|Valor esperado|  
|----------------------|--------------------|  
|*Cube*|Nome de um cubo.|  
|*Células*|Uma expressão de subcubo.|  
|*Definir*|Uma expressão de conjunto ou o nome de um conjunto nomeado.<br /><br /> Observação: Uma instrução de Subseleção não pode ser usada.|  
|*Hierarquia de HierarchyMembers*|O nome de uma hierarquia.|  
|*Dimensão, DimensionMembers*|O nome de uma dimensão.|  
|*Nível de LevelMembers*|Nome de um nível.|  
|*Atributo, AttributeMembers*|Nome de um atributo.|  
  
 O elemento que corresponde ao pai do **destino** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.Action>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
