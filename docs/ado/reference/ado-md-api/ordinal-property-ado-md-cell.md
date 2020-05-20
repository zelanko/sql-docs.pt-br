---
title: Propriedade ordinal (célula ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Cell::Ordinal
- Ordinal
helpviewer_keywords:
- Ordinal property [ADO MD]
ms.assetid: a6001168-b954-47f0-ba0d-c05c4cc40c58
author: rothja
ms.author: jroth
ms.openlocfilehash: b0563912d49ba6baff085fd83be88693e8f8ba1f
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82765067"
---
# <a name="ordinal-property-ado-md-cell"></a>Propriedade Ordinal (Célula do ADO MD)
Identifica exclusivamente uma [célula](../../../ado/reference/ado-md-api/cell-object-ado-md.md) pela sua posição em um células.  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna um inteiro **longo** e é somente leitura.  
  
## <a name="remarks"></a>Comentários  
 O valor ordinal da célula identifica exclusivamente a célula em um células. Conceitualmente, as células são numeradas em um células como se o células fosse uma matriz *p*-dimensional, em que *p* é o número de [eixos](../../../ado/reference/ado-md-api/axes-collection-ado-md.md). As células são numeradas a partir de zero na ordem de linha principal. Aqui está a fórmula para calcular o número ordinal de uma célula:  
  
 O valor ordinal da célula pode ser usado com a propriedade [Item](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md) do objeto [células](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) para recuperar rapidamente a [célula](../../../ado/reference/ado-md-api/cell-object-ado-md.md).  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Cell (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de eixo (VBScript)](../../../ado/reference/ado-md-api/axis-example-vbscript.md)   
 [Objeto células (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)   
 [Propriedade Item (ADO MD células)](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)   
 [Propriedade Ordinal (Posição do ADO MD)](../../../ado/reference/ado-md-api/ordinal-property-ado-md-position.md)
