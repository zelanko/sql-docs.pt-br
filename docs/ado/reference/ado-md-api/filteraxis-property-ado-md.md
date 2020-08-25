---
description: Propriedade FilterAxis (ADO MD)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 0100363a013dc3ea3435ca205822a4f88b56735b
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88778135"
---
# <a name="filteraxis-property-ado-md"></a>Propriedade FilterAxis (ADO MD)
Indica informações de filtro sobre o [células](./cellset-object-ado-md.md)atual.  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna um objeto [Axis](./axis-object-ado-md.md) e é somente leitura.  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **FilterAxis** para retornar informações sobre as dimensões que foram usadas para dividir os dados. A propriedade [DimensionCount](./dimensioncount-property-ado-md.md) do **eixo** retorna o número de dimensões da segmentação. Esse eixo geralmente tem apenas uma linha.  
  
 O **eixo** retornado por **FilterAxis** não está contido na coleção de [eixos](./axes-collection-ado-md.md) de um objeto [células](./cellset-object-ado-md.md) .  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Cellset (ADO MD)](./cellset-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto Axis (ADO MD)](./axis-object-ado-md.md)   
 [Objeto Dimension (ADO MD)](./dimension-object-ado-md.md)   
 [Propriedade DimensionCount (ADO MD)](./dimensioncount-property-ado-md.md)