---
title: Propriedade Children (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cbec9733044127d23e75364697a41ccd7e8910e4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67911525"
---
# <a name="children-property-ado-md"></a>Propriedade Children (ADO MD)
Retorna uma coleção de [Membros](../../../ado/reference/ado-md-api/members-collection-ado-md.md) para a qual o [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) atual é o pai na hierarquia.  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna uma coleção de **Membros** e é somente leitura.  
  
## <a name="remarks"></a>Comentários  
 A propriedade **Children** contém uma coleção **Members** para a qual o **membro** atual é o pai hierárquico. Os objetos de **membro** de nível folha não têm membros filho na coleção de **Membros** . Só há suporte para essa propriedade em objetos **Membros** que pertencem a um objeto de [nível](../../../ado/reference/ado-md-api/level-object-ado-md.md) . Um erro ocorre quando essa propriedade é referenciada de objetos **Membros** que pertencem a um objeto [Position](../../../ado/reference/ado-md-api/position-object-ado-md.md) .  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Member (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedade ChildCount (ADO MD)](../../../ado/reference/ado-md-api/childcount-property-ado-md.md)
