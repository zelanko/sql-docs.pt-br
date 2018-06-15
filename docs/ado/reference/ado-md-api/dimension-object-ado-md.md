---
title: Dimensão de objeto (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Dimension
helpviewer_keywords:
- Dimension object [ADO MD]
ms.assetid: 66adbbd2-23a3-4c19-a91b-84c31309aa1b
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 10378c62ec05008529e1d271208f3e5657d6a140
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35283905"
---
# <a name="dimension-object-ado-md"></a>Objeto de dimensão (ADO MD)
Representa uma das dimensões de um cubo multidimensional, que contém uma ou mais hierarquias de membros.  
  
## <a name="remarks"></a>Remarks  
 Com as coleções e propriedades de um **dimensão** do objeto, você pode fazer o seguinte:  
  
-   Identificar o **dimensão** com o [nome](../../../ado/reference/ado-md-api/name-property-ado-md.md) e [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) propriedades.  
  
-   Retorna uma cadeia de caracteres significativa que descreve o **dimensão** com o [descrição](../../../ado/reference/ado-md-api/description-property-ado-md.md) propriedade.  
  
-   Retornar o [hierarquia](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md) objetos que compõem o **dimensão** com o [hierarquias](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md) coleção.  
  
-   Usar o ADO padrão [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção para obter informações adicionais sobre o **dimensão** objeto.  
  
 O **propriedades** coleção contém propriedades fornecidos pelo provedor. A tabela a seguir lista as propriedades que podem estar disponíveis. A lista de propriedade real pode ser diferente dependendo da implementação do provedor. Consulte a documentação do provedor para obter uma lista mais completa de propriedades disponíveis.  
  
|Nome|Description|  
|----------|-----------------|  
|CatalogName|O nome do catálogo ao qual pertence este cubo.|  
|CubeName|O nome do cubo.|  
|DefaultHierarchy|O nome exclusivo da hierarquia padrão.|  
|Description|Uma descrição significativa do cubo.|  
|DimensionCaption|Um rótulo ou legenda associada à dimensão.|  
|DimensionCardinality|O número de membros na dimensão.|  
|DimensionGUID|O GUID da dimensão.|  
|DimensionName|O nome da dimensão.|  
|DimensionOrdinal|O número ordinal da dimensão entre o grupo de dimensões que formam o cubo.|  
|DimensionType|O tipo de dimensão.|  
|DimensionUniqueName|O nome ambíguo de dimensão.|  
|SchemaName|O nome do esquema ao qual pertence este cubo.|  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos](../../../ado/reference/ado-md-api/dimension-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de CubeDef (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [Objeto CubeDef (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)   
 [Coleção de dimensões (ADO MD)](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)   
 [Coleção hierarquias (ADO MD)](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)   
 [Coleção Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
