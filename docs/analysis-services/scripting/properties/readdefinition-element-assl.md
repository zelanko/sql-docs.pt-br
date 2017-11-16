---
title: Elemento ReadDefinition (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
apiname:
- ReadDefinition Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- ReadDefinition
helpviewer_keywords:
- ReadDefinition element
ms.assetid: 1f250129-13b2-41b9-b083-b5aacddf0060
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 50bf45c70b3c49be547d3c1ff5568acbb6e891e2
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="readdefinition-element-assl"></a>Elemento ReadDefinition (ASSL)
  Determina se os membros podem ler a definição do banco de dados ou a definição de objetos no banco de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Permission> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <ReadDefinition>...</ReadDefinition>  
   ...  
</Permission>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Nenhuma*|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[CubePermission](../../../analysis-services/scripting/objects/cubepermission-element-assl.md), [DatabasePermission](../../../analysis-services/scripting/objects/databasepermission-element-assl.md), [DimensionPermission](../../../analysis-services/scripting/objects/dimensionpermission-element-assl.md), [MiningModelPermission](../../../analysis-services/scripting/objects/miningmodelpermission-element-assl.md), [MiningStructurePermission ](../../../analysis-services/scripting/objects/miningstructurepermission-element-assl.md), [Permissão](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Nenhuma*|O acesso à definição de objeto não é permitido.|  
|*Básico*|O acesso básico à definição de objeto é permitido.<br /><br /> Observação: Essa permissão é necessária para a criação de cubos locais, vincular grupos de medidas e dimensões.|  
|*Permitido*|O acesso completo à definição de objeto é permitido.<br /><br /> Observação: Essa permissão é necessária para executar um [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) XML para chamada Analysis (XMLA) usando o parâmetro DISCOVER_XML_METADATA.|  
  
 Os elementos que correspondem aos pais de **ReadDefinition** no modelo de objeto de Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.CubePermission>, <xref:Microsoft.AnalysisServices.DatabasePermission>, <xref:Microsoft.AnalysisServices.DimensionPermission>, <xref:Microsoft.AnalysisServices.MiningModelPermission>, <xref:Microsoft.AnalysisServices.MiningStructurePermission>e <xref:Microsoft.AnalysisServices.Permission>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento Role &#40; ASSL &#41;](../../../analysis-services/scripting/objects/role-element-assl.md)   
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

