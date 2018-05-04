---
title: Elemento TargetType (ASSL) | Microsoft Docs
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
- TargetType Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- TargetType
helpviewer_keywords:
- TargetType element
ms.assetid: 2c69ea6e-2af7-435b-9841-86117d5554a7
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 67c53bb07cfb9144869ce759af25b42b12478107
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
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
  
  
