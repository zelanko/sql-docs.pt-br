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
ms.openlocfilehash: 4c599bd75388dc0b2ea7e4a5c16f495817f917ba
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88440788"
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
