---
title: Propriedade Children (ADO MD) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Member::Children
- Children
helpviewer_keywords:
- Children property [ADO MD]
ms.assetid: 61d36468-1ccd-467a-9cb5-17d0bfacc766
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 39c1ba30aab6f6a972241c0e564a7a0680165828
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
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
