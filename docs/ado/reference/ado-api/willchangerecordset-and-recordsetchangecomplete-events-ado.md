---
title: Eventos WillChangeRecordset e Recordsetchangecomplete (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset::RecordsetChangeComplete
- RecordsetChangeComplete
- Recordset::WillChangeRecordset
- WillChangeRecordset
helpviewer_keywords:
- RecordsetChangeComplete event [ADO]
- WillChangeRecordset event [ADO]
ms.assetid: d5d44659-e0d9-46d9-a297-99c43555082f
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c5ca84c5759523bf17c4e047b22cafbd48dce547
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66710070"
---
# <a name="willchangerecordset-and-recordsetchangecomplete-events-ado"></a>Eventos WillChangeRecordset e RecordsetChangeComplete (ADO)
O **eventos WillChangeRecordset** evento é chamado antes de uma operação pendente altera o [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md). O **RecordsetChangeComplete** eventos é chamado após o **Recordset** foi alterado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
WillChangeRecordset adReason, adStatus, pRecordset  
RecordsetChangeComplete adReason, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *adReason*  
 Uma [EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md) valor que especifica o motivo para esse evento. Seu valor pode ser **adRsnRequery**, **adRsnResynch**, **adRsnClose**, **adRsnOpen**.  
  
 *adStatus*  
 Uma [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valor de status.  
  
 Quando **eventos WillChangeRecordset** é chamado, esse parâmetro é definido como **adStatusOK** se a operação que causou o evento foi bem-sucedida. Ele é definido como **adStatusCantDeny** se esse evento não é possível solicitar o cancelamento da operação pendente.  
  
 Quando **RecordsetChangeComplete** é chamado, esse parâmetro é definido como **adStatusOK** se a operação que causou o evento foi bem-sucedida, **adStatusErrorsOccurred** se a operação falhou, ou **adStatusCancel** se a operação associada com aceitos anteriormente **eventos WillChangeRecordset** evento tiver sido cancelado.  
  
 Antes de **eventos WillChangeRecordset** retorna, defina esse parâmetro como **adStatusCancel** para solicitar o cancelamento da operação pendente ou definir esse parâmetro como adStatusUnwantedEvent para evitar subsequentes notificações.  
  
 Antes de **eventos WillChangeRecordset** ou **RecordsetChangeComplete** retorna, defina esse parâmetro como **adStatusUnwantedEvent** para evitar notificações subsequentes.  
  
 *pError*  
 Uma [erro](../../../ado/reference/ado-api/error-object.md) objeto. Ele descreve o erro ocorrido se o valor de *adStatus* é **adStatusErrorsOccurred**; caso contrário, ele não está definido.  
  
 *pRecordset*  
 Um **Recordset** objeto. O **Recordset** para que esse evento ocorreu.  
  
## <a name="remarks"></a>Comentários  
 Um **eventos WillChangeRecordset** ou **RecordsetChangeComplete** evento pode ocorrer devido a **conjunto de registros** [Requery](../../../ado/reference/ado-api/requery-method.md) ou [Abra](../../../ado/reference/ado-api/open-method-ado-recordset.md) métodos.  
  
 Se o provedor não dá suporte a indicadores, uma **RecordsetChange** notificação de evento ocorre sempre que novas linhas são recuperadas do provedor. A frequência desse evento depende do **RecordsetCacheSize** propriedade.  
  
 Você deve definir a **adStatus** parâmetro **adStatusUnwantedEvent** para cada possível **adReason** valor pare completamente a notificação de eventos para qualquer evento, que inclui uma **adReason** parâmetro.  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de modelo de eventos ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Resumo do manipulador de eventos ADO](../../../ado/guide/data/ado-event-handler-summary.md)
