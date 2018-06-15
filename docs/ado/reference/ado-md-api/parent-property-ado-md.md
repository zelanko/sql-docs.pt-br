---
title: Propriedade (ADO MD) pai | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Parent
- Member::Parent
helpviewer_keywords:
- Parent property [ADO MD]
ms.assetid: 32c278c1-d8e1-4bb7-9ecd-2fbfdffee34b
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d07d330aaa7497679524caab2a8a9543d64370be
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35284628"
---
# <a name="parent-property-ado-md"></a>Propriedade pai (ADO MD)
Indica o membro que é o pai do atual [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) em uma hierarquia.  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna um [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) do objeto e é somente leitura.  
  
## <a name="remarks"></a>Remarks  
 Um membro que está no nível superior de uma hierarquia (raiz) não tem nenhum pai. Essa propriedade é suportada apenas em **membro** objetos que pertencem a um [nível](../../../ado/reference/ado-md-api/level-object-ado-md.md) objeto. Ocorre um erro quando essa propriedade é referenciada em **membro** objetos que pertencem a um [posição](../../../ado/reference/ado-md-api/position-object-ado-md.md) objeto.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Member (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte também  
 [Propriedade Children (ADO MD)](../../../ado/reference/ado-md-api/children-property-ado-md.md)
