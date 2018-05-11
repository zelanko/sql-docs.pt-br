---
title: Elemento TargetType (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 5261d212777049c907af8d4db8f3b085ded8740e
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="targettype-element-assl"></a>Elemento TargetType (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Identifica o tipo de item do item identificado no [destino](../../../analysis-services/scripting/properties/target-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Action>  
   ...  
   <TargetType>...</TargetType>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[Ação](../../../analysis-services/scripting/objects/action-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Cube*|O destino da ação é um cubo.|  
|*Células*|O destino da ação é um subcubo.|  
|*Definir*|O destino da ação é um conjunto.|  
|*Hierarquia*|O destino da ação é uma hierarquia.|  
|*Nível*|O destino da ação é um nível.|  
|*DimensionMembers*|O destino da ação são os membros de uma dimensão.|  
|*HierarchyMembers*|O destino da ação são os membros de uma hierarquia.|  
|*LevelMembers*|O destino da ação são os membros de um nível.|  
|*AttributeMembers*|O destino da ação são os membros de um atributo.|  
  
 A enumeração que corresponde aos valores permitidos para **TargetType** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.ActionTargetType>.  
  
 O elemento que corresponde ao pai do **TargetType** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.Action>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
