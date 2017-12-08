---
title: Elemento Perspective (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Perspective Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Perspective
helpviewer_keywords: Perspective element
ms.assetid: 0442334c-8b00-4451-ad81-02e58c735e8f
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 28368ffe071ae5139c4ea5245a0d9bea9222b7dc
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="perspective-element-assl"></a>Elemento Perspective (ASSL)
  Define os detalhes de uma perspectiva de um [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Perspectives>  
   <<Perspective>  
      <Name>...</Name>  
      <ID>...</ID>  
      <CreatedTimestamp>...</CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <Description>...</Description>  
      <Translations>...</Translations>  
      <DefaultMeasure>...</DefaultMeasure>  
      <Dimensions>...</Dimensions>  
            <MeasureGroups>...</MeasureGroups>  
      <Calculations>...</Calculations>  
      <Kpis>...</Kpis>  
            <Actions>...</Actions>  
      <Annotations>...</Annotations>  
   </Perspective>  
</Perspectives>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Perspectivas](../../../analysis-services/scripting/collections/perspectives-element-assl.md)|  
|Elementos filho|[Ações](../../../analysis-services/scripting/collections/actions-element-assl.md), [anotações](../../../analysis-services/scripting/collections/annotations-element-assl.md), [cálculos](../../../analysis-services/scripting/collections/calculations-element-assl.md), [CreatedTimestamp](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md), [DefaultMeasure](../../../analysis-services/scripting/properties/defaultmeasure-element-assl.md), [ Descrição](../../../analysis-services/scripting/properties/description-element-assl.md), [dimensões](../../../analysis-services/scripting/collections/dimensions-element-assl.md), [ID](../../../analysis-services/scripting/properties/id-element-assl.md), [Kpis](../../../analysis-services/scripting/collections/kpis-element-assl.md), [LastSchemaUpdate](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md), [ MeasureGroups](../../../analysis-services/scripting/collections/measuregroups-element-assl.md), [nome](../../../analysis-services/scripting/properties/name-element-assl.md), [traduções](../../../analysis-services/scripting/collections/translations-element-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 Uma perspectiva fornece um subconjunto de um cubo, selecionando as dimensões, as hierarquias, os atributos e outros detalhes que devem ser incluídos e definindo a fatia de dados a ser incluída. Uma perspectiva pertence a um único cubo. Não é possível substituir nem adicionar objetos em uma perspectiva; todas as dimensões, hierarquias e outros detalhes devem existir no cubo subjacente. Não é possível incluir objetos e marcá-los como visível.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.Perspective>.  
  
## <a name="see-also"></a>Consulte também  
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
