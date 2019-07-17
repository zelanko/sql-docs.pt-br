---
title: Propriedade ChildCount (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ChildCount
- Member::ChildCount
helpviewer_keywords:
- ChildCount property [ADO MD]
ms.assetid: 5463be22-ca50-43ea-9c92-468fc8eda280
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a8e6f6a7cb749ff2b22a1f7563b43ce07e060aab
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67911554"
---
# <a name="childcount-property-ado-md"></a>Propriedade ChildCount (ADO MD)
Indica o número de membros para os quais o atual [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) objeto é o pai em uma hierarquia.  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna um **longo** inteiro e é somente leitura.  
  
## <a name="remarks"></a>Comentários  
 Use o **ChildCount** propriedade para retornar uma estimativa de quantos filhos uma **membro** tem. Os filhos reais de um **membro** pode ser retornado pela [filhos](../../../ado/reference/ado-md-api/children-property-ado-md.md) propriedade.  
  
 Para **membro** objetos de uma [posição](../../../ado/reference/ado-md-api/position-object-ado-md.md) do objeto, o número máximo retornado é 65536. Se o número real de filhos excede 65536, o valor retornado ainda seja 65536. Portanto, o aplicativo deve interpretar um **ChildCount** de 65.536 como igual a ou maior que 65536 filhos.  
  
 Para **membro** objetos de uma [nível](../../../ado/reference/ado-md-api/level-object-ado-md.md) de objeto, use a coleção de ADO [contagem](../../../ado/reference/ado-api/count-property-ado.md) propriedade no **filhos** coleção para determinar o número exato de filhos. Determinar o número exato de filhos pode ser lento se o número de filhos na coleção for grande.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Member (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte também  
 [Propriedade Children (ADO MD)](../../../ado/reference/ado-md-api/children-property-ado-md.md)   
 [Propriedade Count (ADO)](../../../ado/reference/ado-api/count-property-ado.md)   
 [Coleção Members (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)
