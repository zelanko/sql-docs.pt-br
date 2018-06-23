---
title: Tipo de dados DimensionAttributeBinding (fora de linha) (ASSL) | Microsoft Docs
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
- DimensionAttributeBinding Data Type (out-of-line)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- DimensionAttributeBinding data type
ms.assetid: d8ec77a9-749f-4b08-8d56-8b6514a70248
caps.latest.revision: 8
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 6f72755c02c6b8b07cdf67c4d5464d1f3b2d9e55
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117045"
---
# <a name="dimensionattributebinding-data-type-out-of-line-assl"></a>Tipo de dados DimensionAttributeBinding (fora de linha) (ASSL)
  Define um tipo de dados derivado que representa uma associação fora de linha para um atributo em uma dimensão.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DimensionAttributeBinding>  
   <!-- The following elements extend Binding -->  
   <DatabaseID>...</DatabaseID>  
   <DimensionID>...</DimensionID>  
   <AttributeID>...</AttributeID>  
   <KeyColumns>...</KeyColumns>  
   <NameColumn>...</NameColumn>  
   <Translations>...</Translations>  
</DimensionAttributeBinding>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipos de dados base|[Associação](binding-data-type-assl.md)|  
|Tipos de dados derivados|Nenhum|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhum|  
|Elementos filho|[AttributeID](../properties/id-element-assl.md), [DatabaseID](../../xmla/xml-elements-properties/id-element-xmla.md), [DimensionID](../properties/dimensionid-element-assl.md), [KeyColumns](../collections/columns-element-assl.md), [NameColumn](../objects/column-element-assl.md), [traduções](../collections/translations-element-assl.md)|  
|Elementos derivados|[Associação](../../xmla/xml-elements-properties/binding-element-xmla.md) ([associações](../collections/attributes-element-assl.md) coleção do XML for Analysis (XMLA) [lote](../../xmla/xml-elements-commands/batch-element-xmla.md) e [processo](../../xmla/xml-elements-commands/process-element-xmla.md) comandos)|  
  
## <a name="remarks"></a>Remarks  
 Para obter mais informações sobre associações fora de linha, consulte [fontes de dados e associações &#40;multidimensionais do SSAS&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  