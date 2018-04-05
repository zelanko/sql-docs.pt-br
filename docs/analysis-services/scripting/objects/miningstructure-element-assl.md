---
title: Elemento Miningstructures (ASSL) | Microsoft Docs
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
apiname:
- MiningStructure Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- MiningStructure
helpviewer_keywords:
- MiningStructure element
ms.assetid: b943cd92-0ed8-4bd8-8fbc-7dab0534aede
caps.latest.revision: 48
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 455d874cf279e44e8381c5183d2d376e40e2a351
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="miningstructure-element-assl"></a>Elemento MiningStructures (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Define a estrutura para um conjunto de modelos de mineração.  
  
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
|Elementos pai|[MiningStructures](../../../analysis-services/scripting/collections/miningstructures-element-assl.md)|  
|Elementos filho|[Anotações](../../../analysis-services/scripting/collections/annotations-element-assl.md), [CacheMode](../../../analysis-services/scripting/properties/cachemode-element-assl.md), [agrupamento](../../../analysis-services/scripting/properties/collation-element-assl.md), [colunas](../../../analysis-services/scripting/collections/columns-element-assl.md), [CreatedTimestamp](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md), [ Descrição](../../../analysis-services/scripting/properties/description-element-assl.md), [ErrorConfiguration](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md),<br /><br /> [HoldoutActualSize](../../../analysis-services/scripting/properties/holdoutactualsize-element.md),<br /><br /> [HoldoutMaxCases](../../../analysis-services/scripting/properties/holdoutmaxcases-element.md),<br /><br /> [HoldoutMaxPercent](../../../analysis-services/scripting/properties/holdoutmaxpercent-element.md),<br /><br /> [HoldoutSeed](../../../analysis-services/scripting/properties/holdoutseed-element.md),<br /><br /> [ID](../../../analysis-services/scripting/properties/id-element-assl.md), [idioma](../../../analysis-services/scripting/properties/language-element-assl.md), [LastProcessed](../../../analysis-services/scripting/properties/lastprocessed-element-assl.md), [LastSchemaUpdate](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md), [MiningModels](../../../analysis-services/scripting/collections/miningmodels-element-assl.md), [ MiningStructurePermissions](../../../analysis-services/scripting/collections/miningstructurepermissions-element-assl.md), [nome](../../../analysis-services/scripting/properties/name-element-assl.md), [fonte](../../../analysis-services/scripting/properties/source-element-binding-assl.md), [estado](../../../analysis-services/scripting/properties/state-element-assl.md), [traduções](../../../analysis-services/scripting/collections/translations-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 A estrutura de mineração define as colunas e as associações. Depois de definir uma estrutura de mineração, você pode usar aquela estrutura para definir muitos modelos de mineração. A estrutura de mineração e cada modelo de mineração que contém, pode ser processada independentemente.  
  
> [!NOTE]  
>  As propriedades holdout, **HoldoutMaxCases**, **HoldoutMaxPercent**, **HoldoutSeed**, e **HoldoutActualSize**, foram introduzidos no [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]. Elas permitem que você defina uma partição em uma estrutura de mineração que atua como o conjunto de testes para todos os modelos de mineração que estão associados com a estrutura. O [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] não oferece suporte a essas propriedades. Então, se você tentar usar estas propriedades em uma instância do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] retornará um erro.  
  
## <a name="drillthrough-to-structure-columns"></a>Detalhamento para colunas de estrutura  
 Em [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], foi adicionado um novo elemento de permissão para o [elemento MiningStructurePermissions &#40; ASSL &#41; ](../../../analysis-services/scripting/collections/miningstructurepermissions-element-assl.md) coleção. Se você adicionar **AllowDrillthrough** permissão para ambos os [MiningStructurePermissions](../../../analysis-services/scripting/collections/miningstructurepermissions-element-assl.md) e [MiningModelPermission](../../../analysis-services/scripting/objects/miningmodelpermission-element-assl.md) coleções, o detalhamento estiver habilitado das modelo de mineração à estrutura, de forma que os membros de uma função que tenha **AllowDrillthrough** permissões no modelo podem consultar o modelo de mineração de dados e retornar colunas de estrutura que não foram incluídas no modelo.  
  
 Portanto, para proteger dados confidenciais ou informações pessoais, você deve construir sua exibição da fonte de dados para mascarar informações confidenciais e conceder permissão **AllowDrillthrough** em uma estrutura de mineração somente quando for necessário. Para obter mais informações, consulte [elemento AllowDrillThrough &#40; ASSL &#41; ](../../../analysis-services/scripting/properties/allowdrillthrough-element-assl.md).  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.MiningStructure>.  
  
## <a name="see-also"></a>Consulte Também  
 [Elemento MiningModel &#40; ASSL &#41;](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)   
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)   
 [SELECIONAR &#40; DMX &#41;](../../../dmx/select-dmx.md)  
  
  
