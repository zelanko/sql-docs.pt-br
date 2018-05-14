---
title: Elemento FoldingParameters (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 51a035c923f1598147c36e4b0860b5ab233577de
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="foldingparameters-element-assl"></a>Elemento FoldingParameters (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Especifica os parâmetros usados pelo servidor do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] durante a execução de uma validação cruzada de modelos de mineração.  
  
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
  
 Para obter informações sobre como executar a validação cruzada usando [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] procedimentos armazenados, consulte [mineração de dados armazenados, procedimentos &#40;Analysis Services - mineração de dados&#41;](../../../analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining.md).  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
