---
title: EventReasonEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- EventReasonEnum
helpviewer_keywords:
- EventReasonEnum enumeration [ADO]
ms.assetid: 7d4a5496-ec2d-4936-b36a-7049a82be4b4
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b173fb6838b082b0600714f3756858dcc1615ba2
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35278435"
---
# <a name="eventreasonenum"></a>EventReasonEnum
Especifica o motivo que causou um evento ocorra.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adRsnAddNew**|1|Uma operação de adicionar um novo registro.|  
|**adRsnClose**|9|Uma operação fechados a **registros**.|  
|**adRsnDelete**|2|Uma operação de um registro excluído.|  
|**adRsnFirstChange**|11|Uma operação feita a primeira alteração para um registro.|  
|**adRsnMove**|10|Uma operação Mover o ponteiro do registro dentro do **registros**.|  
|**adRsnMoveFirst**|12|Uma operação de mover o ponteiro do registro para o primeiro registro no **registros**.|  
|**adRsnMoveLast**|15|Uma operação de mover o ponteiro de registro para o último registro no **registros**.|  
|**adRsnMoveNext**|13|Uma operação de mover o ponteiro do registro para o próximo registro no **registros**.|  
|**adRsnMovePrevious**|14|Uma operação de mover o ponteiro do registro para o registro anterior no **registros**.|  
|**adRsnRequery**|7|Uma operação de consulta feita a [registros](../../../ado/reference/ado-api/recordset-object-ado.md).|  
|**adRsnResynch**|8|Uma operação ressincronizar a **registros** com o banco de dados.|  
|**adRsnUndoAddNew**|5|Uma operação revertida a adição de um novo registro.|  
|**adRsnUndoDelete**|6|Uma operação revertida a exclusão de um registro.|  
|**adRsnUndoUpdate**|4|Uma operação revertida, a atualização de um registro.|  
|**adRsnUpdate**|3|Uma operação atualizar um registro existente.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC equivalente  
 Pacote: **com.ms.wfc.data**  
  
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
