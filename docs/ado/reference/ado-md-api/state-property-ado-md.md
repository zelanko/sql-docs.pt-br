---
description: Propriedade State (ADO MD)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: efc3b140b2864aec7151e1235010c4a14b0b3a64
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777855"
---
# <a name="state-property-ado-md"></a>Propriedade State (ADO MD)
Indica o estado atual do células.  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna um inteiro **longo** indicando a condição atual do objeto [células](./cellset-object-ado-md.md) e é somente leitura. Os seguintes valores são válidos: **adStateClosed** (0) e **adStateOpen** (1).  
  
## <a name="remarks"></a>Comentários  
 Para usar os nomes de constantes do [ObjectStateEnum](../ado-api/objectstateenum.md) , você deve ter a biblioteca de tipos do ADO referenciada em seu projeto. Consulte [usando o ADO com ADO MD](../../guide/multidimensional/using-ado-with-ado-md.md) para obter mais informações.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Cellset (ADO MD)](./cellset-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Método Close (ADO MD)](./close-method-ado-md.md)   
 [Método Open (ADO MD)](./open-method-ado-md.md)