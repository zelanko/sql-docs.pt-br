---
title: Elemento HoldoutMaxCases | Microsoft Docs
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
- HoldoutMaxCases
helpviewer_keywords:
- HoldoutMaxCases element
ms.assetid: 58d94d10-e11e-4368-b3b8-dff23e1947cd
caps.latest.revision: 21
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 083ff97f8d739f4f970a6fec8a5c7353b43b5763
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120886"
---
# <a name="holdoutmaxcases-element"></a>Elemento HoldoutMaxCases
  Especifica o número máximo de casos na fonte de dados a ser usado para a partição de controle que contém o conjunto de teste de um [MiningStructure](../objects/miningstructure-element-assl.md) elemento. As situações restantes no conjunto de dados serão utilizadas para treinamento. Um valor de 0 indica que não existe nenhum limite para o número de casos que podem ser exibidos como conjunto de testes.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<MiningStructure>  
   ...  
   <ddl100_100:HoldoutMaxCases>...</ddl100_100:HoldoutMaxCases>  
   ...  
</MiningStructure>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Inteiro maior que 0.|  
|Valor padrão|0|  
|Cardinalidade|0-1: Elemento opcional que poderá ocorrer uma vez, e somente uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[MiningStructure](../objects/miningstructure-element-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 Se você especificar valores tanto para o `HoldoutMaxPercent` quanto para o `HoldoutMaxCases`, o algoritmo limitará o conjunto de testes ao menor dos dois valores.  
  
 Se o `HoldoutMaxCases` for definido para o padrão de 0 e o valor não tiver sido definido para `HoldoutMaxPercent`, o algoritmo utilizará todo o conjunto de dados para treinamento.  
  
 As novas propriedades `HoldoutMaxCases`, `HoldoutMaxPercent`, `HoldoutSeed`, ou `HoldoutActualSize` estão disponíveis apenas no [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] e versões posteriores. Portanto, você deve prefixar essas propriedades com o namespace conforme mostrado na descrição de sintaxe ou o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] retornará um erro.  
  
> [!NOTE]  
>  No [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] não oferecia suporte ao uso de partições de validação em uma estrutura de mineração. Portanto, as instruções de Linguagem de Script (ASSL) do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] que contenham um dos parâmetros de exibição, `HoldoutMaxCases`, `HoldoutMaxPercent`, `HoldoutSeed` ou `HoldoutActualSize` não poderão ser utilizadas no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Se você utilizar um destes parâmetros de validação em uma instrução ASSL em [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] retornará um erro.  
  
 O elemento que corresponde ao pai do `HoldoutMaxCases` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.MiningStructure>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)   
 [Elemento HoldoutMaxPercent](holdoutmaxpercent-element.md)   
 [Elemento HoldoutSeed](holdoutseed-element.md)   
 [Elemento HoldoutActualSize](holdoutactualsize-element.md)  
  
  