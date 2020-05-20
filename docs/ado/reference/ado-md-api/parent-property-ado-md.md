---
title: Propriedade Parent (ADO MD) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 94e6e920d6ab44265c42b9ca26e2410c43c3659e
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82765047"
---
# <a name="parent-property-ado-md"></a>Propriedade Parent (ADO MD)
Indica o membro que é o pai do [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) atual em uma hierarquia.  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna um objeto de [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) e é somente leitura.  
  
## <a name="remarks"></a>Comentários  
 Um membro que está no nível superior de uma hierarquia (a raiz) não tem nenhum pai. Essa propriedade tem suporte apenas em objetos **Membros** que pertencem a um objeto de [nível](../../../ado/reference/ado-md-api/level-object-ado-md.md) . Um erro ocorre quando essa propriedade é referenciada de objetos **Membros** que pertencem a um objeto [Position](../../../ado/reference/ado-md-api/position-object-ado-md.md) .  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Member (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedade Children (ADO MD)](../../../ado/reference/ado-md-api/children-property-ado-md.md)
