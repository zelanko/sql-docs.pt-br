---
title: Propriedade (ADO MD) pai | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Parent
- Member::Parent
helpviewer_keywords:
- Parent property [ADO MD]
ms.assetid: 32c278c1-d8e1-4bb7-9ecd-2fbfdffee34b
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f37e6cf355e035044e25979f4e76256936b7e240
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66708801"
---
# <a name="parent-property-ado-md"></a>Propriedade Parent (ADO MD)
Indica o membro que é o pai do atual [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) em uma hierarquia.  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna um [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) do objeto e é somente leitura.  
  
## <a name="remarks"></a>Comentários  
 Um membro que está no nível superior de uma hierarquia (raiz) não tem pai. Essa propriedade é suportada apenas no **membro** objetos que pertencem a um [nível](../../../ado/reference/ado-md-api/level-object-ado-md.md) objeto. Ocorre um erro quando essa propriedade é referenciada a partir **membro** objetos que pertencem a um [posição](../../../ado/reference/ado-md-api/position-object-ado-md.md) objeto.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Member (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte também  
 [Propriedade Children (ADO MD)](../../../ado/reference/ado-md-api/children-property-ado-md.md)
