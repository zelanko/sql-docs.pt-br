---
title: Propriedade FilterAxis (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Cellset::FilterAxis
- FilterAxis
helpviewer_keywords:
- FilterAxis property [ADO MD]
ms.assetid: 9c656963-531e-4cd1-b698-d5f42a9b7ba3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d44ac908c04338f80c18699319f75a068370c3e0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67938453"
---
# <a name="filteraxis-property-ado-md"></a>Propriedade FilterAxis (ADO MD)
Indica informações de filtro sobre o [células](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)atual.  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna um objeto [Axis](../../../ado/reference/ado-md-api/axis-object-ado-md.md) e é somente leitura.  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **FilterAxis** para retornar informações sobre as dimensões que foram usadas para dividir os dados. A propriedade [DimensionCount](../../../ado/reference/ado-md-api/dimensioncount-property-ado-md.md) do **eixo** retorna o número de dimensões da segmentação. Esse eixo geralmente tem apenas uma linha.  
  
 O **eixo** retornado por **FilterAxis** não está contido na coleção de [eixos](../../../ado/reference/ado-md-api/axes-collection-ado-md.md) de um objeto [células](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) .  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Cellset (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto Axis (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)   
 [Objeto Dimension (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)   
 [Propriedade DimensionCount (ADO MD)](../../../ado/reference/ado-md-api/dimensioncount-property-ado-md.md)
