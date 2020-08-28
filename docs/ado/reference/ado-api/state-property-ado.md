---
description: Propriedade State (ADO)
title: Propriedade State (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: d118ed6d695f8f047640f0ef16c139204ae36277
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988837"
---
# <a name="state-property-ado"></a>Propriedade State (ADO)
Indica para todos os objetos aplicáveis se o estado do objeto está aberto ou fechado. Se o objeto estiver executando um método assíncrono, indicará se o estado atual do objeto está se conectando, executando ou recuperando.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um valor **longo** que pode ser um valor [ObjectStateEnum](./objectstateenum.md) . O valor padrão é **adStateClosed**.  
  
## <a name="remarks"></a>Comentários  
 Você pode usar a propriedade **State** para determinar o estado atual de um determinado objeto a qualquer momento.  
  
 A propriedade de **estado** do objeto pode ter uma combinação de valores. Por exemplo, se uma instrução estiver em execução, essa propriedade terá um valor combinado de **adStateOpen** e **adStateExecuting**.  
  
 A propriedade **State** é somente leitura.  
  
## <a name="applies-to"></a>Aplica-se A  

:::row:::
    :::column:::
        [Objeto Command (ADO)](./command-object-ado.md)  
        [Objeto Connection (ADO)](./connection-object-ado.md)  
    :::column-end:::
    :::column:::
        [Objeto Record (ADO)](./record-object-ado.md)  
        [Objeto Recordset (ADO)](./recordset-object-ado.md)  
    :::column-end:::
    :::column:::
        [Objeto Stream (ADO)](./stream-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades ConnectionString, ConnectionTimeout e State (VB)](./connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [Exemplo das propriedades ConnectionString, ConnectionTimeout e State (VC + +)](./connectionstring-connectiontimeout-and-state-properties-example-vc.md)