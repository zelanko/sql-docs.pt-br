---
title: Elemento StatusGraphic (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: StatusGraphic Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: StatusGraphic
helpviewer_keywords: StatusGraphic element
ms.assetid: 14b365bc-924d-4791-ad4a-a38155fec42e
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 65ab66359a90108c543665257a15037dfd43b382
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="statusgraphic-element-assl"></a>Elemento StatusGraphic (ASSL)
  Contém a representação gráfica recomendada do status do [Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md) elemento.  
  
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
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
