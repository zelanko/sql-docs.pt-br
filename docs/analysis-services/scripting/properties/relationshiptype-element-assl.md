---
title: Elemento RelationshipType (ASSL) | Microsoft Docs
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
- RelationshipType Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- RelationshipType
helpviewer_keywords:
- RelationshipType element
ms.assetid: 72e1ab0e-a95d-4ebe-857d-21de1bf9fe03
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2c851069422e2e2f89c9c00decae26a9b872d93d
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="relationshiptype-element-assl"></a>Elemento RelationshipType (ASSL)
  Indica se as relações de membro para um [AttributeRelationship](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md) pode ser alterado.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<AttributeRelationship>  
   ...  
   <RelationshipType>...</RelationshipType>  
   ...  
</AttributeRelationship>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Flexível*|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[AttributeRelationship](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Rígida*|As relações de membro entre um atributo e um atributo relacionado não podem ser alteradas.|  
|*Flexível*|As relações de membro entre um atributo e um atributo relacionado podem ser alteradas.|  
  
 Por exemplo, se **ZipCode** não puder ser alterado de uma **City** para outra, a relação de **ZipCode** com **City** será marcada como *Rigid*.  
  
 A enumeração que corresponde aos valores permitidos para **RelationshipType** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.RelationshipType>.  
  
## <a name="see-also"></a>Consulte também  
 [Atributos e hierarquias de atributo](../../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

