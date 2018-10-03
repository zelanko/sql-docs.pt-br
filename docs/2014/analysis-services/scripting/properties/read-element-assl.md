---
title: Ler o elemento (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Read Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Read element
ms.assetid: 2e2c1173-72ca-4e8a-a6cd-fd348ef96d78
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2f950d35e74a64b75ec239c7d35ba31660ec8f08
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48157376"
---
# <a name="read-element-assl"></a>Elemento Read (ASSL)
  Determina se os dados ou metadados podem ser lidos para um determinado [CubeDimensionPermission](../data-type/permission-data-type-assl.md) ou [permissão](../data-type/permission-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<CubeDimensionPermission> <!-- or Permission -->  
   ...  
   <Read>...</Read>  
   ...  
</CubeDimensionPermission>  
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
|Elementos pai|[CubeDimensionPermission](../objects/cubepermission-element-assl.md), [permissão](../data-type/permission-data-type-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Nenhuma*|Nenhum acesso é permitido para dados ou metadados do objeto pai.|  
|*Permitido*|O acesso de leitura é permitido para dados e metadados do objeto pai.|  
  
## <a name="remarks"></a>Comentários  
 Os elementos que correspondem aos pais de `Read` no modelo de objeto Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.CubeDimensionPermission> e <xref:Microsoft.AnalysisServices.Permission>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento de cubo &#40;ASSL&#41;](../objects/cube-element-assl.md)   
 [Elemento de dimensão &#40;ASSL&#41;](../objects/dimension-element-assl.md)   
 [Elemento CubePermission &#40;ASSL&#41;](../objects/cubepermission-element-assl.md)   
 [Tipo de dados Permission &#40;ASSL&#41;](../data-type/permission-data-type-assl.md)   
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
