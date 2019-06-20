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
manager: jroth
ms.openlocfilehash: cd7300a493067ced23a38e423befe0e77e6f0512
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66709331"
---
# <a name="filteraxis-property-ado-md"></a>Propriedade FilterAxis (ADO MD)
Indica as informações de filtro sobre o atual [conjunto de células](../../../ado/reference/ado-md-api/cellset-object-ado-md.md).  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna um [eixo](../../../ado/reference/ado-md-api/axis-object-ado-md.md) de objeto e é somente leitura.  
  
## <a name="remarks"></a>Comentários  
 Use o **FilterAxis** propriedade para retornar informações sobre as dimensões que foram usados para dividir os dados. O [DimensionCount](../../../ado/reference/ado-md-api/dimensioncount-property-ado-md.md) propriedade da **eixo** retorna o número de dimensões de segmentação de dados. Esse eixo normalmente tem apenas uma linha.  
  
 O **eixo** retornado pela **FilterAxis** não está contido no [eixos](../../../ado/reference/ado-md-api/axes-collection-ado-md.md) coleção para uma [conjunto de células](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) objeto.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Cellset (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte também  
 [Objeto Axis (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)   
 [Objeto de dimensão (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)   
 [Propriedade DimensionCount (ADO MD)](../../../ado/reference/ado-md-api/dimensioncount-property-ado-md.md)
