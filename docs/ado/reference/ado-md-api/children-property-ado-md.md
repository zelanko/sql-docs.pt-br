---
title: Propriedade Children (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Member::Children
- Children
helpviewer_keywords:
- Children property [ADO MD]
ms.assetid: 61d36468-1ccd-467a-9cb5-17d0bfacc766
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 872d9d125cc1f397d0f9b6e8cbd66c32308b5072
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="children-property-ado-md"></a>Propriedade Children (ADO MD)
Retorna um [membros](../../../ado/reference/ado-md-api/members-collection-ado-md.md) coleção para a qual atual [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) é o pai na hierarquia.  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna um **membros** coleção e é somente leitura.  
  
## <a name="remarks"></a>Remarks  
 O **filhos** propriedade contém um **membros** coleção para a qual atual **membro** é o pai hierárquico. Nível de folha **membro** objetos não têm nenhum membro filho **membros** coleção. Essa propriedade só é suportada em **membro** objetos que pertencem a um [nível](../../../ado/reference/ado-md-api/level-object-ado-md.md) objeto. Ocorre um erro quando essa propriedade é referenciada em **membro** objetos que pertencem a um [posição](../../../ado/reference/ado-md-api/position-object-ado-md.md) objeto.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Member (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte também  
 [Propriedade ChildCount (ADO MD)](../../../ado/reference/ado-md-api/childcount-property-ado-md.md)
