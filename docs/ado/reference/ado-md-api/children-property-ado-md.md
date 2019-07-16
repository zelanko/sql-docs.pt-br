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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67911525"
---
# <a name="children-property-ado-md"></a>Propriedade Children (ADO MD)
Retorna um [membros](../../../ado/reference/ado-md-api/members-collection-ado-md.md) coleção para a qual atual [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) é o pai na hierarquia.  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna um **membros** coleção e é somente leitura.  
  
## <a name="remarks"></a>Comentários  
 O **filhos** propriedade contém uma **membros** coleção para a qual atual **membro** é o pai hierárquico. Nível de folha **membro** objetos não têm nenhum membro filho **membros** coleção. Essa propriedade só é compatível com **membro** objetos que pertencem a um [nível](../../../ado/reference/ado-md-api/level-object-ado-md.md) objeto. Ocorre um erro quando essa propriedade é referenciada a partir **membro** objetos que pertencem a um [posição](../../../ado/reference/ado-md-api/position-object-ado-md.md) objeto.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Member (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte também  
 [Propriedade ChildCount (ADO MD)](../../../ado/reference/ado-md-api/childcount-property-ado-md.md)
