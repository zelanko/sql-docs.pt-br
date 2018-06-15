---
title: Elemento Perspective (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d84b369134c55a09317ae8812f2d511e147605bf
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34031937"
---
# <a name="perspective-element-assl"></a>Elemento Perspective (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
## <a name="remarks"></a>Remarks  
 Uma perspectiva fornece um subconjunto de um cubo, selecionando as dimensões, as hierarquias, os atributos e outros detalhes que devem ser incluídos e definindo a fatia de dados a ser incluída. Uma perspectiva pertence a um único cubo. Não é possível substituir nem adicionar objetos em uma perspectiva; todas as dimensões, hierarquias e outros detalhes devem existir no cubo subjacente. Não é possível incluir objetos e marcá-los como visível.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.Perspective>.  
  
## <a name="see-also"></a>Consulte também  
 [Objetos de & #40; ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
