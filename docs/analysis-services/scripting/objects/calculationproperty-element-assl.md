---
title: Elemento CalculationProperty (ASSL) | Microsoft Docs
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
apiname:
- CalculationProperty Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- CalculationProperty
helpviewer_keywords:
- CalculationProperty element
ms.assetid: 5f0b4cfc-7d25-4c01-a517-cc2e89859be3
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 499f002694022d737b7711c0d69891a5b08059eb
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="calculationproperty-element-assl"></a>Elemento CalculationProperty (ASSL)
  Contém uma coleção de propriedades de interface de usuário para um cálculo usado em uma [MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<CalculationProperties>  
   <CalculationProperty>  
      <CalculationReference>...</CalculationReference>  
      <CalculationType>...</CalculationType>  
      <Translations>...</Translations>  
      <Description>...</Description>  
      <Visible>...</Visible>  
      <SolveOrder>...</SolveOrder>  
      <FormatString>...</FormatString>  
      <ForeColor>...</ForeColor>  
      <BackColor>...</BackColor>  
            <FontName>...</FontName>  
            <FontSize>...</FontSize>  
            <FontFlags>...</FontFlags>  
            <NonEmptyBehavior>...</NonEmptyBehavior>  
      <AssociatedMeasureGroupID>...</AssociatedMeasureGroupID>  
      <DisplayFolder>...</DisplayFolder>  
   </CalculationProperty>  
</CalculationProperties>  
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
|Elementos pai|[CalculationProperties](../../../analysis-services/scripting/collections/calculationproperties-element-assl.md)|  
|Elementos filho|[AssociatedMeasureGroupID](../../../analysis-services/scripting/properties/associatedmeasuregroupid-element-assl.md), [BackColor](../../../analysis-services/scripting/properties/backcolor-element-assl.md), [CalculationReference](../../../analysis-services/scripting/properties/calculationreference-element-assl.md), [CalculationType](../../../analysis-services/scripting/properties/calculationtype-element-assl.md), [descrição](../../../analysis-services/scripting/properties/description-element-assl.md), [DisplayFolder](../../../analysis-services/scripting/properties/displayfolder-element-assl.md), [FontFlags](../../../analysis-services/scripting/properties/fontflags-element-assl.md), [FontName](../../../analysis-services/scripting/properties/fontname-element-assl.md), [FontSize](../../../analysis-services/scripting/properties/fontsize-element-assl.md), [ForeColor](../../../analysis-services/scripting/properties/forecolor-element-assl.md), [FormatString](../../../analysis-services/scripting/properties/formatstring-element-assl.md), [NonEmptyBehavior](../../../analysis-services/scripting/properties/nonemptybehavior-element-assl.md), [SolveOrder](../../../analysis-services/scripting/properties/solveorder-element-assl.md), [traduções](../../../analysis-services/scripting/collections/translations-element-assl.md), [visíveis](../../../analysis-services/scripting/properties/visible-element-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.CalculationProperty>.  
  
## <a name="see-also"></a>Consulte também  
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
