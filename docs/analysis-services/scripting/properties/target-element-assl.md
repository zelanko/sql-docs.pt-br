---
title: Elemento (ASSL) de destino | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
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
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 948f6a2b21ced3ecbdca2e039464f25a03980de4
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="target-element-assl"></a>Elemento Target (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Identifica o destino do [ação](../../../analysis-services/scripting/objects/action-element-assl.md) elemento.  
  
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
|Valor padrão|Nenhum|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[Ação](../../../analysis-services/scripting/objects/action-element-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
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
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
