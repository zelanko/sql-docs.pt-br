---
title: Elemento HoldoutActualSize | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
f1_keywords:
- HoldoutActualSize
helpviewer_keywords:
- HoldoutActualSize element
ms.assetid: 606a6674-cedb-4cee-82d0-26589f084dd9
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: fe781b9e3381a97d9ad75440dac40e281881419f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36020567"
---
# <a name="holdoutactualsize-element"></a>Elemento HoldoutActualSize
  Indica o tamanho real, após o processamento da partição de exibição que contém o conjunto de teste de um [MiningStructure](../objects/miningstructure-element-assl.md) elemento. As situações restantes no conjunto de dados serão utilizadas para treinamento. Esta propriedade é somente leitura.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<MiningStructure>  
   ...  
   <ddl100_100:HoldoutActualSize>...</ddl100_100:HoldoutActualSize>  
   ...  
</MiningStructure  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Valor de inteiro somente leitura.|  
|Valor padrão|Não aplicável|  
|Cardinalidade|0-1: Elemento opcional que pode ocorrer uma vez, e somente uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[MiningStructure](../objects/miningstructure-element-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O valor de `HoldoutActualSize` depende dos dados de origem e os valores para [HoldoutMaxCases](holdoutmaxcases-element.md), [HoldoutMaxPercent](holdoutmaxpercent-element.md), e [HoldoutSeed](holdoutseed-element.md). Portanto, o valor do `HoldoutActualSize` não estará disponível até que o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] processe a estrutura de mineração.  
  
 O elemento que corresponde ao pai do `HoldoutActualSize` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.MiningStructure>.  
  
> [!NOTE]  
>  No [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] não oferecia suporte ao uso de partições de validação em uma estrutura de mineração. Portanto, as instruções de Linguagem de Script (ASSL) do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] que contenham um dos parâmetros de exibição, `HoldoutMaxCases`, `HoldoutMaxPercent`, `HoldoutSeed` ou `HoldoutActualSize` não poderão ser utilizadas no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Se você utilizar um destes parâmetros de validação em uma instrução ASSL em [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] retornará um erro.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)   
 [Elemento HoldoutMaxCases](holdoutmaxcases-element.md)   
 [Elemento HoldoutMaxPercent](holdoutmaxpercent-element.md)   
 [Elemento HoldoutSeed](holdoutseed-element.md)  
  
  