---
title: Elemento Algorithm (ASSL) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f02e571f28f43e82ec6f01a3796252176da2ce20
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
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
  
  
