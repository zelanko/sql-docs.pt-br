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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 743e36e379760cb2c148c5484bb7b49b08d1d27e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63070850"
---
# <a name="eventreasonenum"></a>EventReasonEnum
Especifica o motivo que causou um evento ocorra.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adRsnAddNew**|1|Uma operação adicionado um novo registro.|  
|**adRsnClose**|9|Uma operação fechado o **conjunto de registros**.|  
|**adRsnDelete**|2|Um registro excluído de uma operação.|  
|**adRsnFirstChange**|11|Uma operação feita a primeira alteração a um registro.|  
|**adRsnMove**|10|Uma operação movido o ponteiro de registro dentro de **conjunto de registros**.|  
|**adRsnMoveFirst**|12|Uma operação movido o ponteiro de registro para o primeiro registro a **conjunto de registros**.|  
|**adRsnMoveLast**|15|Uma operação movido o ponteiro de registro para o último registro a **conjunto de registros**.|  
|**adRsnMoveNext**|13|Uma operação movido o ponteiro de registro para o próximo registro na **conjunto de registros**.|  
|**adRsnMovePrevious**|14|Uma operação movido o ponteiro de registro para o registro anterior na **conjunto de registros**.|  
|**adRsnRequery**|7|Uma operação consultadas novamente o [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).|  
|**adRsnResynch**|8|Uma operação ressincronizados a **Recordset** com o banco de dados.|  
|**adRsnUndoAddNew**|5|Uma operação revertida a adição de um novo registro.|  
|**adRsnUndoDelete**|6|Uma operação revertida a exclusão de um registro.|  
|**adRsnUndoUpdate**|4|Uma operação revertida a atualização de um registro.|  
|**adRsnUpdate**|3|Uma operação atualizado um registro existente.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Package: **com.ms.wfc.data**  
  
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
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Eventos WillChangeRecord e RecordChangeComplete (ADO)](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|[Eventos WillChangeRecordset e RecordsetChangeComplete (ADO)](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|  
|[Eventos WillMove e MoveComplete (ADO)](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)||
