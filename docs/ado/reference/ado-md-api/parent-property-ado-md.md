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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2f6d6e03dd3288a5b0ca71bb9e129e1a57abf7c8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67949324"
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
