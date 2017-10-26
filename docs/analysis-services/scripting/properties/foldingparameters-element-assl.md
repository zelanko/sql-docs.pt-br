---
title: Elemento FoldingParameters (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
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
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ddfadd34b6d0b0ae7ba459f35ccb7c1fa7faa31a
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="foldingparameters-element-assl"></a>Elemento FoldingParameters (ASSL)
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
  
## <a name="remarks"></a>Comentários  
 Essas propriedades são apenas para uso interno e não são suportadas para serem usadas em instruções DDL.  
  
 Para obter informações sobre como usar a validação cruzada no [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], consulte [medidas no relatório de validação cruzada](../../../analysis-services/data-mining/measures-in-the-cross-validation-report.md).  
  
 Para obter informações sobre como executar a validação cruzada usando [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] procedimentos armazenados, consulte [procedimentos armazenados do mineração de dados &#40; Analysis Services – mineração de dados &#41; ](../../../analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining.md).  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

