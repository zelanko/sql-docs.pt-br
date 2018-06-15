---
title: Elemento Annotation (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 303ed41b27538d5e21541e2912e892d91fd0f3d0
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34034469"
---
# <a name="annotation-element-assl"></a>Elemento Annotation (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Contém elementos que são usados para estender o esquema ASSL (Analysis Services Scripting Language).  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Annotations>  
   <Annotation>  
      <Name>...</Name>  
      <Visibility>...</Visibility>  
      <Value>...</Value>  
   </Annotation>  
</Annotations >  
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
|Elementos pai|[Anotações](../../../analysis-services/scripting/collections/annotations-element-assl.md)|  
|Elementos filho|[Nome](../../../analysis-services/scripting/properties/name-element-assl.md), [valor](../../../analysis-services/scripting/properties/value-element-assl.md), [visibilidade](../../../analysis-services/scripting/properties/visibility-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 O **anotação** elemento fornece a extensibilidade do esquema ASSL para todos os objetos diferentes dos usados unicamente para definir um tipo de dados complexos. O **valor** elemento o **anotação** elemento pode conter um XML válido de qualquer namespace XML diferente de ASSL, sujeito às seguintes regras:  
  
-   O XML pode conter somente elementos.  
  
-   Cada elemento deve ter um nome exclusivo. É recomendável que o valor da **nome** elemento o **anotação** elemento referência ao namespace de destino.  
  
 Essas regras são impostas para permitir que o conteúdo do **anotação** pares de elemento deve ser exposta como um conjunto de nome/valor por meio de outras interfaces, como Decision Support Objects (DSO).  
  
 Comentários e espaços em branco dentro do **anotação** elemento que não são incluídos em um elemento filho não pode ser preservado. Além disso, todos os elementos devem ter permissão de leitura/gravação; os elementos somente leitura serão ignorados.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.Annotation>.  
  
## <a name="see-also"></a>Consulte também  
 [Objetos de & #40; ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
