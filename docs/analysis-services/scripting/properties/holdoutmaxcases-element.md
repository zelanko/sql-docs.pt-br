---
title: Elemento HoldoutMaxCases | Microsoft Docs
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
- HoldoutMaxCases
helpviewer_keywords:
- HoldoutMaxCases element
ms.assetid: 58d94d10-e11e-4368-b3b8-dff23e1947cd
caps.latest.revision: 21
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1e49da22961d21088649b4eda4539e357998049e
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="holdoutmaxcases-element"></a>Elemento HoldoutMaxCases
  Especifica o número máximo de casos na fonte de dados a ser usado para a partição de controle que contém o conjunto de teste de um [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md) elemento. As situações restantes no conjunto de dados serão utilizadas para treinamento. Um valor de 0 indica que não existe nenhum limite para o número de casos que podem ser exibidos como conjunto de testes.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<MiningStructure>  
   ...  
   <ddl100_100:HoldoutMaxCases>...</ddl100_100:HoldoutMaxCases>  
   ...  
</MiningStructure>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Inteiro maior que 0.|  
|Valor padrão|0|  
|Cardinalidade|0-1: Elemento opcional que poderá ocorrer uma vez, e somente uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 Se você especificar valores para ambos **HoldoutMaxPercent** e **HoldoutMaxCases**, o algoritmo limitará o conjunto de testes ao menor dos dois valores.  
  
 Se **HoldoutMaxCases** é definido como o padrão de 0, e um valor não foi definido para **HoldoutMaxPercent**, o algoritmo usa todo o conjunto de dados para treinamento.  
  
 As novas propriedades **HoldoutMaxCases**, **HoldoutMaxPercent**, **HoldoutSeed**, ou **HoldoutActualSize** estão disponíveis apenas em [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] e versões posteriores. Portanto, você deve prefixar essas propriedades com o namespace conforme mostrado na descrição de sintaxe ou o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] retornará um erro.  
  
> [!NOTE]  
>  No [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] não oferecia suporte ao uso de partições de validação em uma estrutura de mineração. Portanto, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instruções de linguagem de script (ASSL) que contêm um dos parâmetros de validação, **HoldoutMaxCases**, **HoldoutMaxPercent**, **HoldoutSeed**, ou **HoldoutActualSize**, não pode ser usado em [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Se você utilizar um destes parâmetros de validação em uma instrução ASSL em [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] retornará um erro.  
  
 O elemento que corresponde ao pai do **HoldoutMaxCases** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.MiningStructure>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)   
 [Elemento HoldoutMaxPercent](../../../analysis-services/scripting/properties/holdoutmaxpercent-element.md)   
 [Elemento HoldoutSeed](../../../analysis-services/scripting/properties/holdoutseed-element.md)   
 [Elemento HoldoutActualSize](../../../analysis-services/scripting/properties/holdoutactualsize-element.md)  
  
  
