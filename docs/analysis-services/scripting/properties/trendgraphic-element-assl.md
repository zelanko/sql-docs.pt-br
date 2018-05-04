---
title: Elemento TrendGraphic (ASSL) | Microsoft Docs
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
- TrendGraphic Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- TrendGraphic
helpviewer_keywords:
- TrendGraphic element
ms.assetid: 7448fd80-3072-4d85-b3a0-6606d1d20885
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 7c584fe7797fd660fa860b9a5187d9f5c6e0d048
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="trendgraphic-element-assl"></a>Elemento TrendGraphic (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Contém a representação gráfica recomendada da tendência do [Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Kpi>  
   ...  
   <TrendGraphic>...</TrendGraphic>  
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
|*Seta padrão*|Seta padrão|  
|*Seta de status - crescente*|Seta de status|  
|*Seta de status - decrescente*|Seta de status invertida|  
|*Rosto feliz*|Aparência|  
  
 O elemento que corresponde ao pai do **TrendGraphic** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.Kpi>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
