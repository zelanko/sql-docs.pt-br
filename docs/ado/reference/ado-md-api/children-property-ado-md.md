---
description: Propriedade Children (ADO MD)
title: Propriedade Children (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Member::Children
- Children
helpviewer_keywords:
- Children property [ADO MD]
ms.assetid: 61d36468-1ccd-467a-9cb5-17d0bfacc766
author: rothja
ms.author: jroth
ms.openlocfilehash: 7f6af5f18de07a3d9eb2f74ace77a9b4032303f1
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88987117"
---
# <a name="children-property-ado-md"></a>Propriedade Children (ADO MD)
Retorna uma coleção de [Membros](./members-collection-ado-md.md) para a qual o [membro](./member-object-ado-md.md) atual é o pai na hierarquia.  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna uma coleção de **Membros** e é somente leitura.  
  
## <a name="remarks"></a>Comentários  
 A propriedade **Children** contém uma coleção **Members** para a qual o **membro** atual é o pai hierárquico. Os objetos de **membro** de nível folha não têm membros filho na coleção de **Membros** . Só há suporte para essa propriedade em objetos **Membros** que pertencem a um objeto de [nível](./level-object-ado-md.md) . Um erro ocorre quando essa propriedade é referenciada de objetos **Membros** que pertencem a um objeto [Position](./position-object-ado-md.md) .  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Member (ADO MD)](./member-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedade ChildCount (ADO MD)](./childcount-property-ado-md.md)