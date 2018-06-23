---
title: Referência técnica para anotações de BI para CSDL | Microsoft Docs
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
ms.assetid: 63b3e069-6ba5-474e-b769-47b7cc87b7dd
caps.latest.revision: 15
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 27ed1339d64dd3c4035288a96b31ae163a304733
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36010295"
---
# <a name="technical-reference-for-bi-annotations-to-csdl"></a>Referência técnica para anotações de BI em CSDL
  Esta seção lista os elementos, o atributo e as propriedades em CSDL usadas para representar modelos tabulares do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Alguns elementos são novos; outros foram anotados ou estendidos para oferecer suporte à modelagem de business intelligence.  
  
 Para obter uma visão geral de modelos de tabela e como as entidades, relações e fórmulas são representadas na CSDL, consulte [anotações CSDL para Business Intelligence &#40;CSDLBI&#41;](../csdl-annotations-for-business-intelligence-csdlbi.md).  
  
## <a name="extended-csdl-elements-complex-types"></a>Elementos de CSDL estendidos: tipos complexos  
 Os elementos de CSDL a seguir foram adicionados ou estendidos para oferecer suporte aos modelos de dados de business intelligence, de tabela e multidimensionais.  
  
-   [Elemento AssociationSet &#40;CSDLBI&#41;](associationset-element-csdlbi.md)  
  
-   [Elemento BaseProperty &#40;CSDLBI&#41;](property-element-csdlbi.md)  
  
-   [Elemento DefaultDetails &#40;CSDLBI&#41;](defaultdetails-element-csdlbi.md)  
  
-   [Elemento DisplayKey &#40;CSDLBI&#41;](displaykey-element-csdlbi.md)  
  
-   [Elemento EntityContainer &#40;CSDLBI&#41;](entitycontainer-element-csdlbi.md)  
  
-   [Elemento EntitySet &#40;CSDLBI&#41;](entityset-element-csdlbi.md)  
  
-   [Elemento EntityType &#40;CSDLBI&#41;](entitytype-element-csdlbi.md)  
  
-   [Elemento Hierarchy &#40;CSDLBI&#41;](hierarchy-element-csdlbi.md)  
  
-   [Elemento KPI &#40;CSDLBI&#41;](kpi-element-csdlbi.md)  
  
-   [Elemento KpiGoal &#40;CSDLBI&#41;](kpigoal-element-csdlbi.md)  
  
-   [Elemento KpiStatus &#40;CSDLBI&#41;](kpistatus-element-csdlbi.md)  
  
-   [Elemento de nível &#40;CSDLBI&#41;](level-element-csdlbi.md)  
  
-   [Elemento de medidas &#40;CSDLBI&#41;](measure-element-csdlbi.md)  
  
-   [Elemento Member &#40;CSDLBI&#41;](member-element-csdlbi.md)  
  
-   [Elemento MemberRef &#40;CSDLBI&#41;](memberref-element-csdlbi.md)  
  
-   [Elemento NavigationProperty &#40;CSDLBI&#41;](navigationproperty-element-csdlbi.md)  
  
-   [Elemento de propriedade &#40;CSDLBI&#41;](property-element-csdlbi.md)  
  
-   [Elemento PropertyRef &#40;CSDLBI&#41;](propertyref-element-csdlbi.md)  
  
## <a name="simple-type-and-subtypes"></a>Tipo e subtipos simples  
 A tabela a seguir lista alguns tipos simples e alguns tipos complexos menores que são incluídos nas definições de tipos complexos listados acima. A documentação para cada tipo ou subtipo simples listado na coluna à esquerda é fornecida em elementos pai listados na coluna à direita.  
  
|Tipo simples|Encontrado no tópico|  
|-----------------|--------------------|  
|Alinhamento|[Elemento BaseProperty &#40;CSDLBI&#41;](property-element-csdlbi.md)|  
|CompareOptions|[Elemento EntityContainer &#40;CSDLBI&#41;](entitycontainer-element-csdlbi.md)|  
|Sumário|[Elemento EntityType &#40;CSDLBI&#41;](entitytype-element-csdlbi.md)|  
|ContextualNameRule|[Elemento Member &#40;CSDLBI&#41;](member-element-csdlbi.md)|  
|DefaultAggregationFunction|[Elemento de propriedade &#40;CSDLBI&#41;](property-element-csdlbi.md)|  
|DirectQueryMode|[Elemento EntityContainer &#40;CSDLBI&#41;](entitycontainer-element-csdlbi.md)|  
|GroupingBehavior|[Elemento de propriedade &#40;CSDLBI&#41;](property-element-csdlbi.md)|  
|MemberRefs|[Elemento MemberRef &#40;CSDLBI&#41;](memberref-element-csdlbi.md)|  
|PropertyRefs|[Elemento PropertyRef &#40;CSDLBI&#41;](propertyref-element-csdlbi.md)|  
|SortDirection|[Elemento BaseProperty &#40;CSDLBI&#41;](property-element-csdlbi.md)|  
|Estado|[Elemento AssociationSet &#40;CSDLBI&#41;](associationset-element-csdlbi.md)|  
|Stability|[Elemento de propriedade &#40;CSDLBI&#41;](property-element-csdlbi.md)|  
|SortDirection|[Elemento BaseProperty &#40;CSDLBI&#41;](property-element-csdlbi.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Conceitos da CSDLBI](../csdlbi-concepts.md)  
  
  