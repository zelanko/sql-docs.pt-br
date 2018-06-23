---
title: Elemento Annotation (ASSL) | Microsoft Docs
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
- Annotation Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Annotation
helpviewer_keywords:
- Annotation element
ms.assetid: 7d75291a-47b4-498a-8ba4-3d093b8513b2
caps.latest.revision: 43
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 5dfe8ea881948de8ed53cea0ddcff1e1325a96d3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36019936"
---
# <a name="annotation-element-assl"></a>Elemento Annotation (ASSL)
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
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Anotações](../collections/annotations-element-assl.md)|  
|Elementos filho|[Nome](../properties/name-element-assl.md), [valor](../properties/value-element-assl.md), [visibilidade](../properties/visibility-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 O elemento `Annotation` fornece a extensibilidade do esquema ASSL para todos os objetos diferentes dos usados unicamente para definir um tipo de dados complexo. O elemento `Value` do elemento `Annotation` pode conter um XML válido de qualquer namespace XML diferente de ASSL, sujeito às seguintes regras:  
  
-   O XML pode conter somente elementos.  
  
-   Cada elemento deve ter um nome exclusivo. É recomendado que o valor do elemento `Name` do elemento `Annotation` faça referência ao namespace de destino.  
  
 Essas regras são impostas para permitir que o conteúdo do elemento `Annotation` seja exposto como um conjunto de pares nome/valor em outras interfaces, como DSO (Decision Support Objects).  
  
 Os comentários e o espaço em branco no elemento `Annotation` que não são incluídos em um elemento filho não podem ser preservados. Além disso, todos os elementos devem ter permissão de leitura/gravação; os elementos somente leitura serão ignorados.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.Annotation>.  
  
## <a name="see-also"></a>Consulte também  
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  