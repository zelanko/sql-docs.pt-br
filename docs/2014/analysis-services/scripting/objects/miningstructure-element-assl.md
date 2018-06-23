---
title: Elemento Miningstructures (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- MiningStructure Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MiningStructure
helpviewer_keywords:
- MiningStructure element
ms.assetid: b943cd92-0ed8-4bd8-8fbc-7dab0534aede
caps.latest.revision: 48
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 5298c78f1902ee9a8fb1ed12ecf066092a02d938
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36121358"
---
# <a name="miningstructure-element-assl"></a>Elemento MiningStructures (ASSL)
  Define a estrutura para um conjunto de modelos de mineração.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<MiningStructures>  
   <MiningStructure>  
      <Name>...</Name>  
      <ID>...</ID>  
      <Description>...</<Description>  
      <Source>...</Source>  
      <CreatedTimestamp>...</<CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <LastProcessed>...</LastProcessed>  
      <Translations>...</Translations>  
      <Language>...</Language>  
            <Collation>...</Collation>  
      <ErrorConfiguration>...</ErrorConfiguration>  
      <CacheMode>...</CacheMode>  
            <Columns>...</Columns>  
      <State>...</State>  
      <HoldoutActualSize>...</HoldoutActualSize>  
      <HoldoutMaxCases>...</HoldoutMaxCases>  
      <HoldoutMaxPercent>...</HoldoutMaxPercent>  
      <HoldoutSeed>...</HoldoutSeed>        
            <MiningStructurePermissions>...</<MiningStructurePermissions>  
            <MiningModels>...</MiningModels>  
            <Annotations>...</Annotations>  
   </MiningStructure>  
</MiningStructures>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[MiningStructures](../collections/miningstructures-element-assl.md)|  
|Elementos filho|[Anotações](../collections/annotations-element-assl.md), [CacheMode](../properties/cachemode-element-assl.md), [agrupamento](../properties/collation-element-assl.md), [colunas](../collections/columns-element-assl.md), [CreatedTimestamp](../properties/createdtimestamp-element-assl.md), [descrição ](../properties/description-element-assl.md), [ErrorConfiguration](errorconfiguration-element-assl.md),<br /><br /> [HoldoutActualSize](../properties/holdoutactualsize-element.md),<br /><br /> [HoldoutMaxCases](../properties/holdoutmaxcases-element.md),<br /><br /> [HoldoutMaxPercent](../properties/holdoutmaxpercent-element.md),<br /><br /> [HoldoutSeed](../properties/holdoutseed-element.md),<br /><br /> [ID](../properties/id-element-assl.md), [idioma](../properties/language-element-assl.md), [LastProcessed](../properties/lastprocessed-element-assl.md), [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md), [MiningModels](../collections/miningmodels-element-assl.md), [ MiningStructurePermissions](../collections/miningstructurepermissions-element-assl.md), [nome](../properties/name-element-assl.md), [fonte](../properties/source-element-binding-assl.md), [estado](../properties/state-element-assl.md), [traduções](../collections/translations-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 A estrutura de mineração define as colunas e as associações. Depois de definir uma estrutura de mineração, você pode usar aquela estrutura para definir muitos modelos de mineração. A estrutura de mineração e cada modelo de mineração que contém, pode ser processada independentemente.  
  
> [!NOTE]  
>  Foram introduzidas as propriedades holdout, `HoldoutMaxCases`, `HoldoutMaxPercent`, `HoldoutSeed` e `HoldoutActualSize`, no [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]. Elas permitem que você defina uma partição em uma estrutura de mineração que atua como o conjunto de testes para todos os modelos de mineração que estão associados com a estrutura. O [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] não oferece suporte a essas propriedades. Então, se você tentar usar estas propriedades em uma instância do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] retornará um erro.  
  
## <a name="drillthrough-to-structure-columns"></a>Detalhamento para colunas de estrutura  
 Em [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], foi adicionado um novo elemento de permissão para o [elemento MiningStructurePermissions &#40;ASSL&#41; ](../collections/miningstructurepermissions-element-assl.md) coleção. Se você adicionar `AllowDrillthrough` permissão para ambos os [MiningStructurePermissions](../collections/miningstructurepermissions-element-assl.md) e [MiningModelPermission](miningmodelpermission-element-assl.md) coleções, o detalhamento está habilitado do modelo de mineração à estrutura, de forma que os membros de uma função que tenha `AllowDrillthrough` permissões no modelo podem consultar o modelo de mineração de dados e retornar colunas de estrutura que não foram incluídas no modelo.  
  
 Portanto, para proteger dados confidenciais ou informações pessoais, você deve construir sua exibição da fonte de dados para mascarar informações confidenciais e conceder permissão `AllowDrillthrough` em uma estrutura de mineração somente quando for necessário. Para obter mais informações, consulte [elemento AllowDrillThrough &#40;ASSL&#41;](../properties/allowdrillthrough-element-assl.md).  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.MiningStructure>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento MiningModel &#40;ASSL&#41;](miningmodel-element-assl.md)   
 [Objetos &#40;ASSL&#41;](objects-assl.md)   
 [SELECIONE &AMP;#40;DMX&AMP;#41;](/sql/dmx/select-dmx)  
  
  
