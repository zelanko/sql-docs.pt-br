---
description: Propriedade ChildCount (ADO MD)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 713958259b274e779802828d1940cabf25c5c222
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441198"
---
# <a name="childcount-property-ado-md"></a>Propriedade ChildCount (ADO MD)
Indica o número de membros para os quais o objeto de [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) atual é o pai em uma hierarquia.  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna um inteiro **longo** e é somente leitura.  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **ChildCount** para retornar uma estimativa de quantos filhos um **membro** tem. Os filhos reais de um **membro** podem ser retornados pela propriedade [Children](../../../ado/reference/ado-md-api/children-property-ado-md.md) .  
  
 Para objetos de **membro** de um objeto [Position](../../../ado/reference/ado-md-api/position-object-ado-md.md) , o número máximo retornado é 65536. Se o número real de filhos exceder 65536, o valor retornado ainda será 65536. Portanto, o aplicativo deve interpretar um **ChildCount** de 65536 como igual ou maior que 65536 filhos.  
  
 Para objetos de **membro** de um objeto de [nível](../../../ado/reference/ado-md-api/level-object-ado-md.md) , use a propriedade de [contagem](../../../ado/reference/ado-api/count-property-ado.md) de coleção ADO na coleção de **filhos** para determinar o número exato de filhos. Determinar o número exato de filhos pode ser lento se o número de filhos na coleção for grande.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Member (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedade Children (ADO MD)](../../../ado/reference/ado-md-api/children-property-ado-md.md)   
 [Propriedade Count (ADO)](../../../ado/reference/ado-api/count-property-ado.md)   
 [Coleção Members (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)
