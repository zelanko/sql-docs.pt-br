---
title: Estado de propriedade (ADO MD) | Microsoft Docs
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
- State
- Cellset::State
helpviewer_keywords:
- State property [ADO MD]
ms.assetid: 06d480ca-9eb6-4570-a45d-a73539bddd32
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f10a12bd20d96c361cfa7b60738ba7d68586b1e0
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="state-property-ado-md"></a>Propriedade State (ADO MD)
Indica o estado atual do conjunto de células.  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna um **longo** inteiro que indica a condição atual do [conjunto de células](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) do objeto e é somente leitura. Os seguintes valores são válidos: **adStateClosed** (0) e **adStateOpen** (1).  
  
## <a name="remarks"></a>Remarks  
 Para usar o [ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md) nomes de constantes, você deve ter a biblioteca de tipos do ADO referenciada em seu projeto. Consulte [usando o ADO com ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md) para obter mais informações.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Cellset (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte também  
 [Feche o método (ADO MD)](../../../ado/reference/ado-md-api/close-method-ado-md.md)   
 [Método Open (ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)
