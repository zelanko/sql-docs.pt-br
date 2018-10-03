---
title: Elemento HoldoutSeed | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
topic_type:
- apiref
f1_keywords:
- HoldoutSeed
helpviewer_keywords:
- HoldoutSeed element
ms.assetid: 6b608bb3-c075-4744-9722-f5fb9fa1cc7e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b97d88ee83d92d22f72db13d20ce37bb6ea9da08
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48097588"
---
# <a name="holdoutseed-element"></a>Elemento HoldoutSeed
  Especifica a semente para uma partição de validação repetível que contém o conjunto de teste de um [MiningStructure](../objects/miningstructure-element-assl.md) elemento. Esta semente assegura que o conteúdo do modelo permaneça o mesmo durante o reprocessamento. Se não for especificado ou definido como 0, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] cria uma semente, usando um algoritmo de hash no nome da estrutura de mineração.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<MiningStructure>  
   ...  
   <ddl100_100:HoldoutSeed>...</ddl100_100:HoldoutSeed>  
   ...  
</MiningStructure>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Longo|  
|Valor padrão|0|  
|Cardinalidade|0-1: Elemento opcional que poderá ocorrer uma vez, e somente uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[MiningStructure](../objects/miningstructure-element-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 Quando você criar uma estrutura de mineração pela primeira vez, a ID e o nome serão os mesmos. Porém, você poderá alterar o nome da estrutura de mineração. Portanto, se você quiser assegurar que a partição é repetível, não deverá confiar na semente criada pelo nome, mas deverá definir explicitamente uma semente.  
  
 Além disso, quando você cria uma cópia de uma estrutura de mineração usando o `EXPORT` instrução, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] manterão o nome da nova estrutura de mineração, mas irá gerar automaticamente uma nova ID. Portanto, é possível ter duas estruturas de mineração que compartilhem o mesmo nome, porém, com IDs diferentes. Quaisquer duas estruturas de mineração que tenham o mesmo nome terão a mesma semente. No entanto, como o particionamento dos dados também depende dos dados de origem, o conteúdo real das partições poderá ser diferente em cada estrutura.  
  
 As novas propriedades `HoldoutMaxCases`, `HoldoutMaxPercent`, `HoldoutSeed`, ou `HoldoutActualSize` só estão disponíveis no [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] e versões posteriores. Portanto, você deve prefixar essas propriedades com o namespace conforme mostrado na descrição de sintaxe ou o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] retornará um erro.  
  
 **Observação** na [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] não oferecia suporte ao uso de partições de validação em uma estrutura de mineração. Portanto, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instruções de linguagem de script (ASSL) que contêm os parâmetros de validação `HoldoutMaxCases`, `HoldoutMaxPercent`, `HoldoutSeed`, ou `HoldoutActualSize` não pode ser usado em [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Se você utilizar um destes parâmetros de validação em uma instrução ASSL em [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] retornará um erro.  
  
 O elemento que corresponde ao pai de `HoldoutSeed` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.MiningStructure>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)   
 [Elemento HoldoutActualSize](holdoutactualsize-element.md)   
 [Elemento HoldoutMaxPercent](holdoutmaxpercent-element.md)   
 [Elemento HoldoutMaxCases](holdoutmaxcases-element.md)  
  
  
