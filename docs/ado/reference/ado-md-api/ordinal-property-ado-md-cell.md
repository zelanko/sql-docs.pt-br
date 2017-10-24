---
title: "Propriedade ordinal (ADO MD célula) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Cell::Ordinal
- Ordinal
helpviewer_keywords:
- Ordinal property [ADO MD]
ms.assetid: a6001168-b954-47f0-ba0d-c05c4cc40c58
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b6928eeeb7450b2edbd244d70d3c6a8aa999343a
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="ordinal-property-ado-md-cell"></a>Propriedade ordinal (ADO MD célula)
Identifica exclusivamente um [célula](../../../ado/reference/ado-md-api/cell-object-ado-md.md) por sua posição dentro de um conjunto de células.  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna um **longo** inteiro e é somente leitura.  
  
## <a name="remarks"></a>Comentários  
 O valor da célula ordinal identifica exclusivamente a célula em um conjunto de células. Conceitualmente, as células são numeradas em um conjunto de células como se fosse o conjunto de células um *p*-matriz dimensional, onde *p* é o número de [eixos](../../../ado/reference/ado-md-api/axes-collection-ado-md.md). As células são numeradas a partir do zero na ordem de linhas principais. Aqui está a fórmula para calcular o número ordinal de uma célula:  
  
 Valor ordinal da célula pode ser usado com o [Item](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md) propriedade o [conjunto de células](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) objeto para recuperar rapidamente o [célula](../../../ado/reference/ado-md-api/cell-object-ado-md.md).  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Cell (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de eixo (VBScript)](../../../ado/reference/ado-md-api/axis-example-vbscript.md)   
 [Objeto de conjunto de células (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)   
 [Propriedade item (conjunto de células do ADO MD)](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)   
 [Propriedade Ordinal (Posição do ADO MD)](../../../ado/reference/ado-md-api/ordinal-property-ado-md-position.md)

