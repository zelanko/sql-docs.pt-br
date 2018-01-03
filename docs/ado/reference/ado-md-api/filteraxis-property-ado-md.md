---
title: Propriedade FilterAxis (ADO MD) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Cellset::FilterAxis
- FilterAxis
helpviewer_keywords: FilterAxis property [ADO MD]
ms.assetid: 9c656963-531e-4cd1-b698-d5f42a9b7ba3
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 90f4edb021af562a20eb5b78695fce208ea785d2
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="filteraxis-property-ado-md"></a>Propriedade FilterAxis (ADO MD)
Indica as informações de filtro sobre atual [conjunto de células](../../../ado/reference/ado-md-api/cellset-object-ado-md.md).  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna um [eixo](../../../ado/reference/ado-md-api/axis-object-ado-md.md) do objeto e é somente leitura.  
  
## <a name="remarks"></a>Remarks  
 Use o **FilterAxis** propriedade para retornar informações sobre as dimensões que foram usadas para segmentar os dados. O [DimensionCount](../../../ado/reference/ado-md-api/dimensioncount-property-ado-md.md) propriedade o **eixo** retorna o número de dimensões de slicer. Normalmente, este eixo tem apenas uma linha.  
  
 O **eixo** retornado por **FilterAxis** não está contida no [eixos](../../../ado/reference/ado-md-api/axes-collection-ado-md.md) coleção para um [conjunto de células](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) objeto.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Cellset (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto de eixo (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)   
 [Objeto de dimensão (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)   
 [Propriedade DimensionCount (ADO MD)](../../../ado/reference/ado-md-api/dimensioncount-property-ado-md.md)
