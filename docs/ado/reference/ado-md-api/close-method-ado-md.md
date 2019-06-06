---
title: Método (ADO MD) Close | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Close
- Cellset::Close
helpviewer_keywords:
- Close method [ADO MD]
ms.assetid: a3aa594d-f9d4-4654-8625-ec20153ff5d9
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 4f01845752c0ee1f9187ea3d209a97509f87a5a9
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66709581"
---
# <a name="close-method-ado-md"></a>Método Close (ADO MD)
Fecha um conjunto de células aberto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Cellset.Close  
```  
  
## <a name="remarks"></a>Comentários  
 Usando o **feche** método para fechar um [conjunto de células](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) objeto liberará os dados associados, inclusive dados em qualquer um relacionado [célula](../../../ado/reference/ado-md-api/cell-object-ado-md.md), [eixo](../../../ado/reference/ado-md-api/axis-object-ado-md.md), [Posição](../../../ado/reference/ado-md-api/position-object-ado-md.md), ou [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) objetos. Fechando uma **conjunto de células** não o remove da memória; você pode alterar suas configurações de propriedade e abri-lo novamente mais tarde. Para eliminar completamente um objeto da memória, defina a variável de objeto para **nada**.  
  
 Posteriormente, você pode chamar o [aberto](../../../ado/reference/ado-md-api/open-method-ado-md.md) método para reabrir a **conjunto de células** usando a mesma ou em outra cadeia de caracteres de origem. Enquanto o **conjunto de células** objeto está fechado, recuperando todas as propriedades ou chamar métodos que fazem referência aos dados subjacentes ou metadados gera um erro.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Cellset (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte também  
 [Objeto Axis (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)   
 [Objeto Cell (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [Objeto de membro (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)   
 [Método Open (ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)   
 [Objeto Position (ADO MD)](../../../ado/reference/ado-md-api/position-object-ado-md.md)   
 [Propriedade State (ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)
