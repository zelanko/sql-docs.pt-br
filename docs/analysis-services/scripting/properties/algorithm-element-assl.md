---
title: Elemento Algorithm (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Algorithm Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Algorithm
helpviewer_keywords:
- Algorithm element
ms.assetid: 188bf7ce-c5c9-406a-af75-5a026c92a569
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: c73bc1f9a1b3a1cb7130cb52c5c8b199a9a3be8c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="algorithm-element-assl"></a>Elemento Algorithm (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define o algoritmo usado por um [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<MiningModel>  
      ...  
   <Algorithm>...</Algorithm>  
      ...  
</MiningModel>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|String|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-1: elemento obrigatório que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 O valor de **algoritmo** elemento é uma cadeia de caracteres que identifica o algoritmo. Por exemplo, a cadeia de caracteres pode ser *Microsoft_Naive_Bayes*, *Microsoft_Decision_Trees*, ou *Microsoft_Clustering.* A cadeia de caracteres identifica os algoritmos fornecidos pelo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] e personaliza os algoritmos fornecidos pelo usuário. Os valores disponíveis para o **algoritmo** elemento pode ser recuperado da coluna SERVICE_NAME do [DMSCHEMA_MINING_SERVICES](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-services-rowset.md) de linhas de esquema.  
  
 O elemento que corresponde ao pai do **algoritmo** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.MiningModel>. Um elemento relacionado bastante próximo ao modelo de objeto AMO é <xref:Microsoft.AnalysisServices.MiningModelAlgorithms>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento AlgorithmParameter & #40; ASSL & #41;](../../../analysis-services/scripting/objects/algorithmparameter-element-assl.md)   
 [Elemento AlgorithmParameters & #40; ASSL & #41;](../../../analysis-services/scripting/collections/algorithmparameters-element-assl.md)   
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
