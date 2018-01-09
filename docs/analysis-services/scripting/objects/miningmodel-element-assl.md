---
title: Elemento MiningModel (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: MiningModel Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: MiningModel
helpviewer_keywords: MiningModel element
ms.assetid: a61d935f-c8f6-457d-ad0c-44f58bb286f5
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 3acf412e4f7e880e6ce1b76799f6990ce32bf905
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="miningmodel-element-assl"></a>Elemento MiningModel (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Define um modelo de mineração de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<MiningModels>  
      <MiningModel>  
      <Name>...</Name>  
            <ID>...</ID>  
      <Description>...</<Descrip  
            <Algorithm>...</Algorithm>  
      <CreatedTimestamp>...</CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <LastProcessed>...</LastProcessed>  
      <AlgorithmParameters>...</AlgorithmParameters>  
      <AllowDrillThrough>...</AllowDrillThrough>  
      <Translations>...</Translations>  
      <Columns>...</Columns>  
      <State>...</State>  
      <MiningModelPermissions>...</MiningModelPermissions>  
      <Language>...</Language>  
            <Collation>...</Collation>  
            <Annotations>...</Annotations>  
            <ddl100_100:FoldingParameters>   </FoldingParameters>  
   </MiningModel>  
</MiningModels>  
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
|Elementos pai|[MiningModels](../../../analysis-services/scripting/collections/miningmodels-element-assl.md)|  
|Elementos filho|[Algoritmo](../../../analysis-services/scripting/properties/algorithm-element-assl.md), [AlgorithmParameters](../../../analysis-services/scripting/objects/algorithmparameter-element-assl.md), [AllowDrillThrough](../../../analysis-services/scripting/properties/allowdrillthrough-element-assl.md), [anotações](../../../analysis-services/scripting/collections/annotations-element-assl.md), [agrupamento](../../../analysis-services/scripting/properties/collation-element-assl.md), [Colunas](../../../analysis-services/scripting/collections/columns-element-assl.md), [CreatedTimestamp](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md), [descrição](../../../analysis-services/scripting/properties/description-element-assl.md), [ID](../../../analysis-services/scripting/properties/id-element-assl.md), [idioma](../../../analysis-services/scripting/properties/language-element-assl.md), [ LastProcessed](../../../analysis-services/scripting/properties/lastprocessed-element-assl.md), [LastSchemaUpdate](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md), [MiningModelPermissions](../../../analysis-services/scripting/collections/miningmodelpermissions-element-assl.md), [nome](../../../analysis-services/scripting/properties/name-element-assl.md), [estado](../../../analysis-services/scripting/properties/state-element-assl.md), [ Traduções](../../../analysis-services/scripting/collections/translations-element-assl.md),<br /><br /> [FoldingParameters](../../../analysis-services/scripting/properties/foldingparameters-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 O elemento **FoldingParameters** do modelo de mineração destina-se a uso interno do servidor e não tem suporte para uso em instruções DDL.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.MiningModel>.  
  
## <a name="see-also"></a>Consulte Também  
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
