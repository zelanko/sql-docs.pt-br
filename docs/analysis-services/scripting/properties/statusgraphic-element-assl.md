---
title: Elemento StatusGraphic (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 0caf023d5405b6b97b24f733a59624d0d7dea9bd
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="statusgraphic-element-assl"></a>Elemento StatusGraphic (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Contém a representação gráfica recomendada do status do elemento [Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Kpi>  
   ...  
   <StatusGraphic>...</StatusGraphic>  
   ...  
</Kpi>  
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
|Elemento pai|[KPI](../../../analysis-services/scripting/objects/kpi-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Sinal de trânsito - único*|Sinal de trânsito (único)|  
|*Sinal de trânsito - várias*|Sinal de trânsito (vários)|  
|*Placas de trânsito*|Placas de trânsito|  
|*Medidor - crescente*|Medidor|  
|*Medidor - decrescente*|Medidor invertido|  
|*Termômetro*|Termômetro|  
|*Cilindro*|Cilindro|  
|*Rosto feliz*|Aparência|  
  
 O elemento que corresponde ao pai do **StatusGraphic** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.Kpi>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
