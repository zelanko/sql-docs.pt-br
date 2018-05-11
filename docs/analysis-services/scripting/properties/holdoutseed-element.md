---
title: Elemento HoldoutSeed | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 3e9b38b6fbc552ac46453df8d95d8332f44eb422
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="holdoutseed-element"></a>Elemento HoldoutSeed
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Especifica a semente para uma partição de validação repetível que contém o conjunto de teste de um [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md) elemento. Esta semente assegura que o conteúdo do modelo permaneça o mesmo durante o reprocessamento. Se não for especificado ou definido como 0, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] cria uma semente, usando um algoritmo de hash no nome da estrutura de mineração.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<MiningStructure>  
   ...  
   <ddl100_100:HoldoutSeed>...</ddl100_100:HoldoutSeed>  
   ...  
</MiningStructure>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Longo|  
|Valor padrão|0|  
|Cardinalidade|0-1: Elemento opcional que poderá ocorrer uma vez, e somente uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 Quando você criar uma estrutura de mineração pela primeira vez, a ID e o nome serão os mesmos. Porém, você poderá alterar o nome da estrutura de mineração. Portanto, se você quiser assegurar que a partição é repetível, não deverá confiar na semente criada pelo nome, mas deverá definir explicitamente uma semente.  
  
 Além disso, quando você cria uma cópia de uma estrutura de mineração usando o **exportar** instrução, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] reterá o nome para a nova estrutura de mineração, mas irá gerar automaticamente uma nova ID. Portanto, é possível ter duas estruturas de mineração que compartilhem o mesmo nome, porém, com IDs diferentes. Quaisquer duas estruturas de mineração que tenham o mesmo nome terão a mesma semente. No entanto, como o particionamento dos dados também depende dos dados de origem, o conteúdo real das partições poderá ser diferente em cada estrutura.  
  
 As novas propriedades **HoldoutMaxCases**, **HoldoutMaxPercent**, **HoldoutSeed**, ou **HoldoutActualSize** estão disponíveis apenas em [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] e versões posteriores. Portanto, você deve prefixar essas propriedades com o namespace conforme mostrado na descrição de sintaxe ou o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] retornará um erro.  
  
 **Observação** na [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] não oferecia suporte ao uso de partições de validação em uma estrutura de mineração. Portanto, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instruções de linguagem de script (ASSL) que contêm os parâmetros de validação **HoldoutMaxCases**, **HoldoutMaxPercent**, **HoldoutSeed**, ou **HoldoutActualSize** não pode ser usado em [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Se você utilizar um destes parâmetros de validação em uma instrução ASSL em [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] retornará um erro.  
  
 O elemento que corresponde ao pai do **HoldoutSeed** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.MiningStructure>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](../../../analysis-services/scripting/properties/properties-assl.md)   
 [Elemento HoldoutActualSize](../../../analysis-services/scripting/properties/holdoutactualsize-element.md)   
 [Elemento HoldoutMaxPercent](../../../analysis-services/scripting/properties/holdoutmaxpercent-element.md)   
 [Elemento HoldoutMaxCases](../../../analysis-services/scripting/properties/holdoutmaxcases-element.md)  
  
  
