---
title: Elemento ReadDefinition (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ReadDefinition Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ReadDefinition
helpviewer_keywords:
- ReadDefinition element
ms.assetid: 1f250129-13b2-41b9-b083-b5aacddf0060
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 176f1fa1f1a9f4fca3e773d65a5fda01c2f6752d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48218106"
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
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Nenhuma*|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[CubePermission](../objects/cubepermission-element-assl.md), [DatabasePermission](../objects/databasepermission-element-assl.md), [DimensionPermission](../objects/dimensionpermission-element-assl.md), [MiningModelPermission](../objects/miningmodelpermission-element-assl.md), [MiningStructurePermission ](../objects/miningstructurepermission-element-assl.md), [Permissão](../data-type/permission-data-type-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Nenhuma*|O acesso à definição de objeto não é permitido.|  
|*Básico*|O acesso básico à definição de objeto é permitido. **Observação:** essa permissão é necessária para a criação de cubos locais, vincular grupos de medidas e dimensões.|  
|*Permitido*|O acesso completo à definição de objeto é permitido. **Observação:** essa permissão é necessária para executar um [Discover](../../xmla/xml-elements-methods-discover.md) XML para chamada Analysis (XMLA) usando o parâmetro DISCOVER_XML_METADATA.|  
  
 Os elementos que correspondem aos pais de `ReadDefinition` no modelo de objeto AMO (Objetos de Gerenciamento de Análise) são <xref:Microsoft.AnalysisServices.CubePermission>, <xref:Microsoft.AnalysisServices.DatabasePermission>, <xref:Microsoft.AnalysisServices.DimensionPermission>, <xref:Microsoft.AnalysisServices.MiningModelPermission>, <xref:Microsoft.AnalysisServices.MiningStructurePermission> e <xref:Microsoft.AnalysisServices.Permission>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento de função &#40;ASSL&#41;](../objects/role-element-assl.md)   
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
