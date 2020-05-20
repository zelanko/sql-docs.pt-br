---
title: Propriedade State (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command25::State
helpviewer_keywords:
- State property [ADO]
ms.assetid: 0b993bac-2653-40b1-bcbb-5b57b6aae2bf
author: rothja
ms.author: jroth
ms.openlocfilehash: 68a0e6fe0c595a79447cbf79155914606415df89
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759752"
---
# <a name="state-property-ado"></a>Propriedade State (ADO)
Indica para todos os objetos aplicáveis se o estado do objeto está aberto ou fechado. Se o objeto estiver executando um método assíncrono, indicará se o estado atual do objeto está se conectando, executando ou recuperando.  
  
## <a name="return-value"></a>Valor Retornado  
 Retorna um valor **longo** que pode ser um valor [ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md) . O valor padrão é **adStateClosed**.  
  
## <a name="remarks"></a>Comentários  
 Você pode usar a propriedade **State** para determinar o estado atual de um determinado objeto a qualquer momento.  
  
 A propriedade de **estado** do objeto pode ter uma combinação de valores. Por exemplo, se uma instrução estiver em execução, essa propriedade terá um valor combinado de **adStateOpen** e **adStateExecuting**.  
  
 A propriedade **State** é somente leitura.  
  
## <a name="applies-to"></a>Aplica-se A  
  
||||  
|-|-|-|  
|[Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|  
|[Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)||  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades ConnectionString, ConnectionTimeout e State (VB)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [Exemplo das propriedades ConnectionString, ConnectionTimeout e State (VC + +)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vc.md)   
