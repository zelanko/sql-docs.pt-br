---
title: Propriedade ChildCount (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ChildCount
- Member::ChildCount
helpviewer_keywords:
- ChildCount property [ADO MD]
ms.assetid: 5463be22-ca50-43ea-9c92-468fc8eda280
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: da861dbc7648edbe93926e8f4df7b560fc4a415f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="childcount-property-ado-md"></a>Propriedade ChildCount (ADO MD)
Indica o número de membros para os quais o atual [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) objeto é o pai em uma hierarquia.  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna um **longo** inteiro e é somente leitura.  
  
## <a name="remarks"></a>Remarks  
 Use o **ChildCount** propriedade para retornar uma estimativa de quantos filhos um **membro** tem. Os filhos reais de um **membro** pode ser retornado pelo [filhos](../../../ado/reference/ado-md-api/children-property-ado-md.md) propriedade.  
  
 Para **membro** objetos de um [posição](../../../ado/reference/ado-md-api/position-object-ado-md.md) do objeto, o número máximo retornado é 65536. Se o número real de filhos excede 65536, o valor retornado será ainda 65536. Portanto, o aplicativo deve interpretar um **ChildCount** de 65536 como igual ou maior que 65536 filhos.  
  
 Para **membro** objetos de um [nível](../../../ado/reference/ado-md-api/level-object-ado-md.md) de objeto, use a coleção de ADO [contagem](../../../ado/reference/ado-api/count-property-ado.md) propriedade o **filhos** coleção para determinar o número exato de filhos. Determinar o número exato de filhos pode ser lento se o número de filhos da coleção for grande.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Member (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte também  
 [Propriedade Children (ADO MD)](../../../ado/reference/ado-md-api/children-property-ado-md.md)   
 [Propriedade Count (ADO)](../../../ado/reference/ado-api/count-property-ado.md)   
 [Coleção Members (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)
