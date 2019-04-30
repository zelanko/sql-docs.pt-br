---
title: Estado de propriedade (ADO MD) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 812863395c2980f341ed2419eee1d9d661f19dd0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63308596"
---
# <a name="state-property-ado-md"></a>Propriedade State (ADO MD)
Indica o estado atual do conjunto de células.  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna um **longo** inteiro que indica a condição atual do [conjunto de células](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) object e é somente leitura. Os seguintes valores são válidos: **adStateClosed** (0) e **adStateOpen** (1).  
  
## <a name="remarks"></a>Comentários  
 Para usar o [ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md) nomes de constantes, você deve ter a biblioteca de tipos do ADO referenciada no seu projeto. Ver [usando o ADO com ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md) para obter mais informações.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Cellset (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte também  
 [Feche o método (ADO MD)](../../../ado/reference/ado-md-api/close-method-ado-md.md)   
 [Método Open (ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)
