---
title: EventReasonEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- EventReasonEnum
helpviewer_keywords:
- EventReasonEnum enumeration [ADO]
ms.assetid: 7d4a5496-ec2d-4936-b36a-7049a82be4b4
author: rothja
ms.author: jroth
ms.openlocfilehash: 94b36cbab5ffe7c22f4d1941e61af8fabc8b9973
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242726"
---
# <a name="eventreasonenum"></a>EventReasonEnum
Especifica o motivo que causou a ocorrência de um evento.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adRsnAddNew**|1|Uma operação adicionou um novo registro.|  
|**adRsnClose**|9|Uma operação fechou o **conjunto de registros**.|  
|**adRsnDelete**|2|Uma operação excluiu um registro.|  
|**adRsnFirstChange**|11|Uma operação fez a primeira alteração em um registro.|  
|**adRsnMove**|10|Uma operação moveu o ponteiro de registro dentro do **conjunto de registros**.|  
|**adRsnMoveFirst**|12|Uma operação moveu o ponteiro de registro para o primeiro registro no **conjunto de registros**.|  
|**adRsnMoveLast**|15|Uma operação moveu o ponteiro de registro para o último registro no **conjunto de registros**.|  
|**adRsnMoveNext**|13|Uma operação moveu o ponteiro de registro para o próximo registro no **conjunto de registros**.|  
|**adRsnMovePrevious**|14|Uma operação moveu o ponteiro de registro para o registro anterior no **conjunto de registros**.|  
|**adRsnRequery**|7|Uma operação reconsultou o [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).|  
|**adRsnResynch**|8|Uma operação sincronizou novamente o **conjunto de registros** com o banco de dados.|  
|**adRsnUndoAddNew**|5|Uma operação reverteu a adição de um novo registro.|  
|**adRsnUndoDelete**|6|Uma operação reverteu a exclusão de um registro.|  
|**adRsnUndoUpdate**|4|Uma operação reverteu a atualização de um registro.|  
|**adRsnUpdate**|3|Uma operação atualizou um registro existente.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums.EventReason.ADDNEW|  
|AdoEnums.EventReason.CLOSE|  
|AdoEnums.EventReason.DELETE|  
|AdoEnums.EventReason.FIRSTCHANGE|  
|AdoEnums.EventReason.MOVE|  
|AdoEnums.EventReason.MOVEFIRST|  
|AdoEnums.EventReason.MOVELAST|  
|AdoEnums.EventReason.MOVENEXT|  
|AdoEnums.EventReason.MOVEPREVIOUS|  
|AdoEnums.EventReason.REQUERY|  
|AdoEnums.EventReason.RESYNCH|  
|AdoEnums.EventReason.UNDOADDNEW|  
|AdoEnums.EventReason.UNDODELETE|  
|AdoEnums.EventReason.UNDOUPDATE|  
|AdoEnums.EventReason.UPDATE|  
  
## <a name="applies-to"></a>Aplica-se A  

:::row:::
    :::column:::
        [Eventos WillChangeRecord e RecordChangeComplete (ADO)](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)  

        [Eventos WillChangeRecordset e RecordsetChangeComplete (ADO)](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)  
    :::column-end:::
    :::column:::
        [Eventos WillMove e MoveComplete (ADO)](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)  
    :::column-end:::
:::row-end:::
