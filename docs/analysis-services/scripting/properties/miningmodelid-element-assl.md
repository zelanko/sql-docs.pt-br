---
title: Elemento MiningModelID (ASSL) | Microsoft Docs
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
- MiningModelID Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- MiningModelID
helpviewer_keywords:
- MiningModelID element
ms.assetid: fada8720-1590-44be-bafc-0ab3612b00e5
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 4f4a199b14a91dd73f9c756ebe50664e43c315fb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="miningmodelid-element-assl"></a>Elemento MiningModelID (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Associa um modelo de mineração com uma dimensão de mineração de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Dimension>  
   ...  
   <MiningModelID>...</MiningModelID>  
   ...  
</Dimension>  
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
|Elemento pai|[Dimensão](../../../analysis-services/scripting/objects/dimension-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 O elemento que corresponde ao pai do **MiningModelID** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.Dimension>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento MiningModel &#40;ASSL&#41;](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)   
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
