---
title: Elemento FoldingParameters (ASSL) | Microsoft Docs
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
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- FoldIndex
- FoldCount
- MaxCases
- FoldingParameters
- FoldTargetAttribute
helpviewer_keywords:
- FoldingParameters element
ms.assetid: 5f5c5a3e-4aed-48fb-bca5-e67f421bef2f
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8f6fa2a178bc1d8f9722a101d7305cedfa248663
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="foldingparameters-element-assl"></a>Elemento FoldingParameters (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Especifica os parâmetros usados pelo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] servidor quando ele executa a validação cruzada de modelos de mineração.  
  
> [!NOTE]  
>  Esses parâmetros são apenas para uso interno. As informações fornecidas aqui servem apenas para referência.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<MiningModel>  
   ...  
   <ddl100_100:FoldingParameters>...  
      <ddl100_100:FoldIndex>...</ddl100_100:FoldIndex>  
      <ddl100_100:FoldCount>...</ddl100_100:FoldCount>  
      <ddl100_100:MaxCases>...</ddl100_100:MAxCases>  
      <ddl100_100:FoldTargetAttribute>...</ddl100_100:FoldTargetAttribute  
...</ddl100_100:FoldingParameters>  
</MiningStructure>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|*FoldIndex*|Inteiro que indica a posição inicial da partição que é usada para validação cruzada.|  
|*FoldCount*|Inteiro que indica o número de partições no modelo depois da validação cruzada.|  
|*MaxCases*|Inteiro que indica quantos casos de modelo são usados para validação cruzada.<br /><br /> Um valor 0 indica que todos os casos são usados.|  
|*FoldTargetAttribute*|Cadeia de caracteres que indica a ID da coluna de modelo que contém o atributo previsível.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)|  
|Elementos filho|*FoldIndex*<br /><br /> *FoldCount*<br /><br /> *MaxCases*<br /><br /> *FoldTargetAttribute*|  
  
## <a name="remarks"></a>Remarks  
 Essas propriedades são apenas para uso interno e não são suportadas para serem usadas em instruções DDL.  
  
 Para obter informações sobre como usar a validação cruzada no [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], consulte [medidas no relatório de validação cruzada](../../../analysis-services/data-mining/measures-in-the-cross-validation-report.md).  
  
 Para obter informações sobre como executar a validação cruzada usando [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] procedimentos armazenados, consulte [procedimentos armazenados do mineração de dados &#40; Analysis Services – mineração de dados &#41; ](../../../analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
