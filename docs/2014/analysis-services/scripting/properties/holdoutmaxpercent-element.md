---
title: Elemento HoldoutMaxPercent | Microsoft Docs
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
- HoldoutMaxPercent
helpviewer_keywords:
- HoldoutMaxPercent element
ms.assetid: e375cc51-5f9d-4252-98a1-326ca0dbbf83
caps.latest.revision: 19
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 53689f28351a4a5505f1c1bc1d4c8a9586074704
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37278142"
---
# <a name="holdoutmaxpercent-element"></a>Elemento HoldoutMaxPercent
  Especifica o percentual máximo de casos na fonte de dados que será usado para a partição de exibição que contém o conjunto de teste de um [MiningStructure](../objects/miningstructure-element-assl.md) elemento. Os casos restantes serão usados para treinar. Um valor de 0 indica que não existe nenhum limite para o número de casos que podem ser exibidos como conjunto de testes.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<MiningStructure>  
   ...  
   <ddl100_100:HoldoutMaxPercent>...</ddl100_100:HoldoutMaxPercent>  
   ...  
</MiningStructure>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Inteiro entre 0 e 99.|  
|Valor padrão|30|  
|Cardinalidade|0-1: Elemento opcional que poderá ocorrer uma vez, e somente uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[MiningStructure](../objects/miningstructure-element-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 Se você especificar valores tanto para o `HoldoutMaxPercent` quanto para o `HoldoutMaxCases`, o algoritmo limitará o conjunto de testes ao menor dos dois valores.  
  
 Se o `HoldoutMaxCases` for definido para o padrão de 0 e o valor não tiver sido definido para `HoldoutMaxPercent`, o algoritmo utilizará o conjunto de dados completo para treinamento.  
  
 As novas propriedades `HoldoutMaxCases`, `HoldoutMaxPercent`, `HoldoutSeed`, ou `HoldoutActualSize` só estão disponíveis no [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] e versões posteriores. Portanto, deve-se prefixar estas propriedades utilizando o novo namespace conforme mostrado na descrição de sintaxe ou o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] retornará um erro.  
  
> [!NOTE]  
>  No [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] não oferecia suporte ao uso de partições de validação em uma estrutura de mineração. Portanto, as instruções de Linguagem de Script (ASSL) do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] que contenham um dos parâmetros de exibição, `HoldoutMaxCases`, `HoldoutMaxPercent`, `HoldoutSeed` ou `HoldoutActualSize` não poderão ser utilizadas no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Se você utilizar um destes parâmetros de validação em uma instrução ASSL em [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] retornará um erro.  
  
 O elemento que corresponde ao pai de `HoldoutMaxPercent` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.MiningStructure>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)   
 [Elemento HoldoutMaxCases](holdoutmaxcases-element.md)   
 [Elemento HoldoutSeed](holdoutseed-element.md)   
 [Elemento HoldoutActualSize](holdoutactualsize-element.md)  
  
  
