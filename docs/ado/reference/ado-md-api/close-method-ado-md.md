---
title: Feche o método (ADO MD) | Microsoft Docs
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
- Close
- Cellset::Close
helpviewer_keywords:
- Close method [ADO MD]
ms.assetid: a3aa594d-f9d4-4654-8625-ec20153ff5d9
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 918cd96221d4d4e4c185bd1e09039069f9ce1128
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="close-method-ado-md"></a>Feche o método (ADO MD)
Fecha um conjunto de células aberto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Cellset.Close  
```  
  
## <a name="remarks"></a>Remarks  
 Usando o **fechar** método para fechar um [conjunto de células](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) objeto liberará os dados associados, inclusive dados em qualquer relacionadas [célula](../../../ado/reference/ado-md-api/cell-object-ado-md.md), [eixo](../../../ado/reference/ado-md-api/axis-object-ado-md.md), [Posição](../../../ado/reference/ado-md-api/position-object-ado-md.md), ou [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) objetos. Fechando uma **conjunto de células** não o remove da memória; você pode alterar suas configurações de propriedade e abri-lo novamente mais tarde. Para eliminar completamente um objeto da memória, defina a variável de objeto para **nada**.  
  
 Posteriormente, você pode chamar o [abrir](../../../ado/reference/ado-md-api/open-method-ado-md.md) método para reabrir o **conjunto de células** usando a mesma ou em outra cadeia de caracteres de origem. Enquanto o **conjunto de células** objeto é fechado, recuperar todas as propriedades ou chamar os métodos que fazem referência a dados subjacente ou metadados gera um erro.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Cellset (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte também  
 [Objeto de eixo (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)   
 [Objeto de célula (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [Membro de objeto (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)   
 [Método Open (ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)   
 [Objeto de posição (ADO MD)](../../../ado/reference/ado-md-api/position-object-ado-md.md)   
 [Propriedade State (ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)
