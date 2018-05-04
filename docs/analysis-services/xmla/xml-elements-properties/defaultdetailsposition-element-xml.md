---
title: Elemento DefaultDetailsPosition (XML) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 851ad331-aefd-4277-a5e5-e32a8f5c5e22
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: efe899c6d7aacf2c8eadf8854c9abd233898697e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="defaultdetailsposition-element-xml"></a>Elemento DefaultDetailsPosition (XML)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contém informações sobre a posição do elemento em uma coleção de elementos.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<RelationshipEndVisualizationProperties>  
   ...  
   <DefaultDetailsPosition>...</DefaultDetailsPosition>  
   ...  
</RelationshipEndVisualizationProperties>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Integer|  
|Valor padrão|-1|  
|Cardinalidade|0-1: elemento opcional que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[RelationshipEndVisualizationProperties](../../../analysis-services/scripting/data-type/relationshipendvisualizationproperties-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 Para **RelationshipEndVisualizationProperties** elementos, o **DefaultDetailsPosition** elemento contém a posição do elemento de detalhes padrão em uma coleção de detalhes. O valor padrão de **false** indica que não há nenhum detalhe padrão a ser usado.  
  
  
