---
title: Método Close (ADO MD) | Microsoft Docs
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
ms.openlocfilehash: 09e83fd8645a5c0ab604a640478c4cced4870742
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67949817"
---
# <a name="close-method-ado-md"></a>Método Close (ADO MD)
Fecha um células aberto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Cellset.Close  
```  
  
## <a name="remarks"></a>Comentários  
 Usar o **método Close** para fechar um [objeto células](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) liberará os dados associados, incluindo dados em qualquer [célula](../../../ado/reference/ado-md-api/cell-object-ado-md.md), [eixo](../../../ado/reference/ado-md-api/axis-object-ado-md.md), [posição](../../../ado/reference/ado-md-api/position-object-ado-md.md)ou objetos de [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) relacionados. Fechar um **células** não o Remove da memória; Você pode alterar suas configurações de propriedade e abri-las novamente mais tarde. Para eliminar completamente um objeto da memória, defina a variável de objeto como **Nothing**.  
  
 Posteriormente, você pode chamar o método [Open](../../../ado/reference/ado-md-api/open-method-ado-md.md) para reabrir o **células** usando a mesma cadeia de caracteres de origem ou outra. Enquanto o objeto **células** é fechado, a recuperação de qualquer propriedade ou a chamada de qualquer método que referencie os dados subjacentes ou os metadados gera um erro.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Cellset (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto Axis (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)   
 [Objeto Cell (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [Objeto member (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)   
 [Método Open (ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)   
 [Objeto Position (ADO MD)](../../../ado/reference/ado-md-api/position-object-ado-md.md)   
 [Propriedade State (ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)
