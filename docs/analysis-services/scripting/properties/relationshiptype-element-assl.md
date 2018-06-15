---
title: Elemento RelationshipType (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: c74d8bc597eaee5ca6842d2c9545d399a16e21f7
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34038100"
---
# <a name="relationshiptype-element-assl"></a>Elemento RelationshipType (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
