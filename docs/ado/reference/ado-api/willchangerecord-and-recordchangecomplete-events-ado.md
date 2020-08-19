---
description: Eventos WillChangeRecord e RecordChangeComplete (ADO)
title: Eventos WillChangeRecord e RecordChangeComplete (ADO) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 0a6cb124e51c232b0a3a26e9eb84316e3bde7ecd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441518"
---
# <a name="willchangerecord-and-recordchangecomplete-events-ado"></a>Eventos WillChangeRecord e RecordChangeComplete (ADO)
O evento **WillChangeRecord** é chamado antes de um ou mais registros (linhas) serem alterados no [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) . O evento **RecordChangeComplete** é chamado após a alteração de um ou mais registros.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
WillChangeRecord adReason, cRecords, adStatus, pRecordset  
RecordChangeCompleteadReason, cRecords, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *adReason*  
 Um valor [EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md) que especifica o motivo para esse evento. Seu valor pode ser **adRsnAddNew**, **adRsnDelete**, **adRsnUpdate**, **adRsnUndoUpdate**, **adRsnUndoAddNew**, **adRsnUndoDelete**ou **adRsnFirstChange**.  
  
 *cRecords*  
 Um valor **longo** que indica o número de registros alterados (afetados).  
  
 *pError*  
 Um objeto de [erro](../../../ado/reference/ado-api/error-object.md) . Ele descreve o erro que ocorreu se o valor de *adStatus* for **adStatusErrorsOccurred**; caso contrário, ele não será definido.  
  
 *adStatus*  
 Um valor de status de [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) .  
  
 Quando **WillChangeRecord** for chamado, esse parâmetro será definido como **adStatusOK** se a operação que causou o evento tiver sido bem-sucedida. Ele será definido como **adStatusCantDeny** se esse evento não puder solicitar o cancelamento da operação pendente.  
  
 Quando **RecordChangeComplete** for chamado, esse parâmetro será definido como **adStatusOK** se a operação que causou o evento foi bem-sucedida ou para **adStatusErrorsOccurred** se a operação falhar.  
  
 Antes de **WillChangeRecord** retornar, defina esse parâmetro como **adStatusCancel** para o cancelamento de solicitação da operação que causou esse evento ou defina esse parâmetro como **adStatusUnwantedEvent** para evitar notificações subsequentes.  
  
 Antes de **RecordChangeComplete** retornar, defina esse parâmetro como **adStatusUnwantedEvent** para evitar notificações subsequentes.  
  
 *pRecordset*  
 Um objeto **Recordset** . O **conjunto de registros** para o qual esse evento ocorreu.  
  
## <a name="remarks"></a>Comentários  
 Um evento **WillChangeRecord** ou **RecordChangeComplete** pode ocorrer para o primeiro campo alterado em uma linha devido às seguintes operações de **conjunto de registros** : [Update](../../../ado/reference/ado-api/update-method.md), [delete](../../../ado/reference/ado-api/delete-method-ado-recordset.md), [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md), [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)e [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md). O valor de [CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md) do **conjunto de registros** determina quais operações fazem com que os eventos ocorram.  
  
 Durante o evento **WillChangeRecord** , a propriedade de [filtro](../../../ado/reference/ado-api/filter-property.md) **Recordset** é definida como **adFilterAffectedRecords**. Você não pode alterar essa propriedade durante o processamento do evento.  
  
 Você deve definir o parâmetro **adStatus** como **adStatusUnwantedEvent** para cada valor de **adReason** possível parar completamente a notificação de eventos para qualquer evento que inclua um parâmetro **adReason** .  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do modelo de eventos ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Resumo do manipulador de eventos ADO](../../../ado/guide/data/ado-event-handler-summary.md)
