---
title: Elemento MembersWithData (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: MembersWithData Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: MembersWithData
helpviewer_keywords: MembersWithData element
ms.assetid: 845087a2-b12d-4344-a8be-85ca61155296
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d7bda746e07dd77b2d530b57091d3b303f06fdcd
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="memberswithdata-element-assl"></a>Elemento MembersWithData (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Determina se deve exibir membros de dados para membros não folha no atributo pai.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DimensionAttribute>  
   ...  
   <MembersWithData>...</MembersWithData>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Nonleafdatahidden*|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O valor da **MembersWithData** elemento é usado somente por atributos pai (em outras palavras, o valor da [uso](../../../analysis-services/scripting/properties/usage-element-dimensionattribute-assl.md) elemento do **DimensionAttribute** elemento pai é definido como *pai*) para determinar se deve exibir membros de dados para membros não folha no atributo pai. Para obter mais informações sobre membros de dados, consulte [Atributos em hierarquias pai-filho](../../../analysis-services/multidimensional-models/parent-child-dimension-attributes.md).  
  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*NonLeafDataHidden*|Dados não folha estão ocultos.|  
|*Nonleafdatahidden*|Dados não folha estão visíveis.|  
  
 A enumeração que corresponde aos valores permitidos para **MembersWithData** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.MembersWithData>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento MembersWithDataCaption &#40; ASSL &#41;](../../../analysis-services/scripting/properties/memberswithdatacaption-element-assl.md)   
 [Tipo de dados DimensionAttribute &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)   
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
