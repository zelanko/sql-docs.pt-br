---
title: Propriedade State (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- State
- Cellset::State
helpviewer_keywords:
- State property [ADO MD]
ms.assetid: 06d480ca-9eb6-4570-a45d-a73539bddd32
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0c11bb74b62d54b1e2489cba5dd7cd35ee376a41
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67949153"
---
# <a name="state-property-ado-md"></a>Propriedade State (ADO MD)
Indica o estado atual do células.  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna um inteiro **longo** indicando a condição atual do objeto [células](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) e é somente leitura. Os seguintes valores são válidos: **adStateClosed** (0) e **adStateOpen** (1).  
  
## <a name="remarks"></a>Comentários  
 Para usar os nomes de constantes do [ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md) , você deve ter a biblioteca de tipos do ADO referenciada em seu projeto. Consulte [usando o ADO com ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md) para obter mais informações.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Cellset (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Método Close (ADO MD)](../../../ado/reference/ado-md-api/close-method-ado-md.md)   
 [Método Open (ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)
