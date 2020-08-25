---
description: Propriedade Parent (ADO MD)
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
ms.openlocfilehash: 208fce5328f76f35cdd562ca82bb989851f366cb
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777905"
---
# <a name="parent-property-ado-md"></a>Propriedade Parent (ADO MD)
Indica o membro que é o pai do [membro](./member-object-ado-md.md) atual em uma hierarquia.  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna um objeto de [membro](./member-object-ado-md.md) e é somente leitura.  
  
## <a name="remarks"></a>Comentários  
 Um membro que está no nível superior de uma hierarquia (a raiz) não tem nenhum pai. Essa propriedade tem suporte apenas em objetos **Membros** que pertencem a um objeto de [nível](./level-object-ado-md.md) . Um erro ocorre quando essa propriedade é referenciada de objetos **Membros** que pertencem a um objeto [Position](./position-object-ado-md.md) .  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Member (ADO MD)](./member-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedade Children (ADO MD)](./children-property-ado-md.md)