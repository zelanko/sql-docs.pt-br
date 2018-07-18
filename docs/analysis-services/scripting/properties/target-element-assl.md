---
title: Elemento (ASSL) de destino | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 98ec5c729f5735343f5eaa87e5232fcfb138cf38
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38045774"
---
# <a name="target-element-assl"></a>Elemento Target (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
 O valor esperado deste elemento depende do valor da [TargetType](../../../analysis-services/scripting/properties/targettype-element-assl.md) elemento para o pai **ação**. A tabela a seguir descreve os valores esperados de **Target** com base no valor de **TargetType**.  
  
|Valor de TargetType|Valor esperado|  
|----------------------|--------------------|  
|*Cube*|Nome de um cubo.|  
|*Células*|Uma expressão de subcubo.|  
|*Definir*|Uma expressão de conjunto ou o nome de um conjunto nomeado.<br /><br /> Observação: Uma instrução de Subseleção não pode ser usada.|  
|*Hierarquia de HierarchyMembers*|O nome de uma hierarquia.|  
|*Dimensão, DimensionMembers*|O nome de uma dimensão.|  
|*Nível, LevelMembers*|Nome de um nível.|  
|*Atributo, AttributeMembers*|Nome de um atributo.|  
  
 O elemento que corresponde ao pai de **alvo** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.Action>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
