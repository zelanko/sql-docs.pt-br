---
title: Medir o elemento (ASSL) | Microsoft Docs
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
- Measure Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Measure
helpviewer_keywords:
- Measure element
ms.assetid: 4c2c2ed1-7f78-4564-982a-132f13bea36f
caps.latest.revision: 38
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 80d59a5356bf1c0b5712e729f230fff9383603cc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37159327"
---
# <a name="measure-element-assl"></a>Elemento Measure (ASSL)
  Define uma medida.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Measures>  
   <Measure> <!-- ancestor: MeasureGroup -->  
      <Name>...</Name>  
      <ID>...</ID>  
      <Description>...</Description>  
      <AggregateFunction>...</AggregateFunction>  
            <DataType>...</DataType>  
            <Source>...</Source>  
      <Visible>...</Visible>  
      <MeasureExpression>...</MeasureExpression>  
      <DisplayFolder>...</DisplayFolder>  
      <FormatString>...</FormatString>  
      <BackColor>...</BackColor>  
      <ForeColor>...</ForeColor>  
            <FontName>...</FontName>  
            <FontSize>...</FontSize>  
            <FontFlags>...</FontFlags>  
            <Translations>...</Translations>  
      <Annotations>...</Annotations>  
   </Measure>  
   <!-- or  -->  
   <Measure xsi:type="AggregationInstanceMeasure">...</Measure> <!-- parent: AggregationInstance -->  
      <!-- or  -->  
   <Measure xsi:type="MeasureBinding">...</Measure> <!-- ancestor: MeasureGroupBinding (out-of-line) -->  
   <!-- or  -->  
   <Measure xsi:type="PerspectiveMeasure">...</Measure> <!-- ancestor: PerspectiveMeasureGroup -->  
</Measures>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
|Ancestral ou pai|Tipo de Dados|  
|------------------------|---------------|  
|[AggregationInstance](../data-type/binding-data-type-assl.md)|  
|[MeasureGroup](group-element-assl.md)|Nenhum|  
|[MeasureGroupBinding (fora de linha)](../data-type/measurebinding-data-type-assl.md)|  
|[PerspectiveMeasureGroup](../data-type/perspectivemeasure-data-type-assl.md)|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Medidas](../collections/measures-element-assl.md)|  
  
|Ancestral ou pai|Elementos filho|  
|------------------------|--------------------|  
|[MeasureGroup](../properties/aggregatefunction-element-assl.md), [anotações](../collections/annotations-element-assl.md), [BackColor](../properties/backcolor-element-assl.md), [DataType](../properties/datatype-element-assl.md), [descrição](../properties/description-element-assl.md), [DisplayFolder ](../properties/displayfolder-element-assl.md), [FontFlags](../properties/fontflags-element-assl.md), [FontName](../properties/name-element-assl.md), [FontSize](../properties/fontsize-element-assl.md), [ForeColor](../properties/forecolor-element-assl.md), [FormatString ](../properties/formatstring-element-assl.md), [ID](../properties/id-element-assl.md), [MeasureExpression](../properties/expression-element-assl.md), [nome](../properties/name-element-assl.md), [fonte](../properties/source-element-measure-assl.md), [traduções](../collections/translations-element-assl.md), [Visíveis](../properties/visible-element-assl.md)|  
|Todos os outros|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 Os detalhes da associação podem ser fornecidos para uma medida. Esses detalhes agem como os padrões por partição.  
  
 Em cubos maiores, pode haver centenas de medidas e hierarquias. A propriedade `DisplayFolder` define a aparência de usuário no cliente. O valor da propriedade `DisplayFolder` pode conter qualquer uma das opções a seguir:  
  
-   Estar vazia, indicando que a medida não pertence a uma pasta.  
  
-   Conter um único nome de pasta, indicando que a medida deve ser processada como pertencente a uma pasta com o mesmo nome.  
  
-   Conter vários nomes de pasta separados por uma barra invertida (\\), indicando uma hierarquia inserida na pasta.  
  
 A propriedade `DisplayFolder` também se aplica a medidas e hierarquias calculadas.  
  
 Os elementos correspondentes no modelo de objeto AMO (Objetos de Gerenciamento de Análise) são <xref:Microsoft.AnalysisServices.Measure> e <xref:Microsoft.AnalysisServices.PerspectiveMeasure>.  
  
## <a name="see-also"></a>Consulte também  
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
