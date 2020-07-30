---
title: LockTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- LockTypeEnum
helpviewer_keywords:
- LockTypeEnum enumeration [ADO]
ms.assetid: d2894eaf-4450-4ace-aa51-c8b875fd3010
author: rothja
ms.author: jroth
ms.openlocfilehash: e609a51d6b9f42cb6101ff485633302193757fbd
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242646"
---
# <a name="locktypeenum"></a>LockTypeEnum
Especifica o tipo de bloqueio colocado nos registros durante a edição.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adLockBatchOptimistic**|4|Indica atualizações de lote otimistas. Necessário para o modo de atualização do lote.|  
|**adLockOptimistic**|3|Indica o bloqueio otimista, registro por registro. O provedor usa o bloqueio otimista, bloqueando registros somente quando você chama o método [Update](../../../ado/reference/ado-api/update-method.md) .|  
|**adLockPessimistic**|2|Indica o bloqueio pessimista, registro por registro. O provedor faz o que é necessário para garantir a edição bem-sucedida dos registros, geralmente bloqueando os registros na fonte de dados imediatamente após a edição.|  
|**adLockReadOnly**|1|Indica registros somente leitura. Você não pode alterar os dados.|  
|**adLockUnspecified**|-1|Não especifica um tipo de bloqueio. Para clones, o clone é criado com o mesmo tipo de bloqueio do original.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums.LockType.BATCHOPTIMISTIC|  
|AdoEnums. LockType. otimista|  
|AdoEnums. LockType. PESSIMISTA|  
|AdoEnums. LockType. READONLY|  
|AdoEnums. LockType. não especificado|  
  
## <a name="applies-to"></a>Aplica-se A  

:::row:::
    :::column:::
        [Método Clone (ADO)](../../../ado/reference/ado-api/clone-method-ado.md)  
        [Propriedade LockType (ADO)](../../../ado/reference/ado-api/locktype-property-ado.md)  
    :::column-end:::
    :::column:::
        [Método Open (Conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)  
        [Evento WillExecute (ADO)](../../../ado/reference/ado-api/willexecute-event-ado.md)  
    :::column-end:::
:::row-end:::
