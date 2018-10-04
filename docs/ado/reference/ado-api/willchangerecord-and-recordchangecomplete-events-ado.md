---
title: Eventos WillChangeRecord e Recordchangecomplete (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- RecordChangeComplete
- Recordset::WillChangeRecord
- WillChangeRecord
- Recordset::RecordChangeComplete
helpviewer_keywords:
- WillChangeRecord event [ADO]
- recordchangecomplete event [ADO]
ms.assetid: cbc369fd-63af-4a7d-96ae-efa91b78ca69
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dd31a75a45bd38bda04655bbb47daca09714803c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47822005"
---
# <a name="willchangerecord-and-recordchangecomplete-events-ado"></a>Eventos WillChangeRecord e RecordChangeComplete (ADO)
O **eventos WillChangeRecord** evento é chamado antes de um ou mais registros (linhas) [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) alterar. O **RecordChangeComplete** evento é chamado depois que um ou mais registros de alteração.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
WillChangeRecord adReason, cRecords, adStatus, pRecordset  
RecordChangeCompleteadReason, cRecords, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *adReason*  
 Uma [EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md) valor que especifica o motivo para esse evento. Seu valor pode ser **adRsnAddNew**, **adRsnDelete**, **adRsnUpdate**, **adRsnUndoUpdate**, **adRsnUndoAddNew**, **adRsnUndoDelete**, ou **adRsnFirstChange**.  
  
 *cRecords*  
 Um **longo** valor que indica o número de registros de alteração (afetado).  
  
 *pError*  
 Uma [erro](../../../ado/reference/ado-api/error-object.md) objeto. Ele descreve o erro ocorrido se o valor de *adStatus* é **adStatusErrorsOccurred**; caso contrário, ele não está definido.  
  
 *adStatus*  
 Uma [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valor de status.  
  
 Quando **eventos WillChangeRecord** é chamado, esse parâmetro é definido como **adStatusOK** se a operação que causou o evento foi bem-sucedida. Ele é definido como **adStatusCantDeny** se esse evento não é possível solicitar o cancelamento da operação pendente.  
  
 Quando **RecordChangeComplete** é chamado, esse parâmetro é definido como **adStatusOK** se a operação que causou o evento foi bem-sucedida, ou ao **adStatusErrorsOccurred** se a operação falhou.  
  
 Antes de **eventos WillChangeRecord** retorna, defina esse parâmetro como **adStatusCancel** ao cancelamento de solicitação da operação que causou este evento ou definir esse parâmetro como  **adStatusUnwantedEvent** para evitar notificações subsequentes.  
  
 Antes de **RecordChangeComplete** retorna, defina esse parâmetro como **adStatusUnwantedEvent** para evitar notificações subsequentes.  
  
 *pRecordset*  
 Um **Recordset** objeto. O **Recordset** para que esse evento ocorreu.  
  
## <a name="remarks"></a>Comentários  
 Um **eventos WillChangeRecord** ou **RecordChangeComplete** evento pode ocorrer para o primeiro campo alterado em uma linha devido ao seguinte **conjunto de registros** operações: [ Atualização](../../../ado/reference/ado-api/update-method.md), [exclua](../../../ado/reference/ado-api/delete-method-ado-recordset.md), [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md), [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), e [ CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md). O valor da **conjunto de registros** [CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md) determina quais operações fazem com que a ocorrência de eventos.  
  
 Durante o **eventos WillChangeRecord** evento, o **conjunto de registros** [filtro](../../../ado/reference/ado-api/filter-property.md) propriedade é definida como **adFilterAffectedRecords**. Você não pode alterar essa propriedade ao processar o evento.  
  
 Você deve definir a **adStatus** parâmetro **adStatusUnwantedEvent** para cada possível **adReason** valor pare completamente a notificação de eventos para qualquer evento, que inclui uma **adReason** parâmetro.  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de modelo de eventos ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Resumo do manipulador de eventos ADO](../../../ado/guide/data/ado-event-handler-summary.md)
