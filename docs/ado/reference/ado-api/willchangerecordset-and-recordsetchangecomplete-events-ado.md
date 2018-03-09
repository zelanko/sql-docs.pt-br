---
title: WillChangeRecordset e RecordsetChangeComplete eventos (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b720776cd7c230e55e77cb37f7a66de3ad6772b6
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="willchangerecordset-and-recordsetchangecomplete-events-ado"></a>WillChangeRecordset e RecordsetChangeComplete eventos (ADO)
O **WillChangeRecordset** evento é chamado antes de uma operação pendente altera o [registros](../../../ado/reference/ado-api/recordset-object-ado.md). O **RecordsetChangeComplete** evento é chamado após o **registros** foi alterado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
WillChangeRecordset adReason, adStatus, pRecordset  
RecordsetChangeComplete adReason, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *adReason*  
 Um [EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md) valor que especifica o motivo para esse evento. Seu valor pode ser **adRsnRequery**, **adRsnResynch**, **adRsnClose**, **adRsnOpen**.  
  
 *adStatus*  
 Um [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valor de status.  
  
 Quando **WillChangeRecordset** é chamado, esse parâmetro é definido como **adStatusOK** se a operação que causou o evento foi bem-sucedida. Ele é definido como **adStatusCantDeny** se esse evento não é possível solicitar o cancelamento da operação pendente.  
  
 Quando **RecordsetChangeComplete** é chamado, esse parâmetro é definido como **adStatusOK** se a operação que causou o evento foi bem-sucedida, **adStatusErrorsOccurred** se a operação falhou, ou **adStatusCancel** se a operação associados ao aceitas anteriormente **WillChangeRecordset** evento foi cancelado.  
  
 Antes de **WillChangeRecordset** retorna, defina este parâmetro como **adStatusCancel** para solicitar o cancelamento da operação pendente ou definir esse parâmetro como adStatusUnwantedEvent para evitar subsequentes notificações.  
  
 Antes de **WillChangeRecordset** ou **RecordsetChangeComplete** retorna, defina este parâmetro como **adStatusUnwantedEvent** para impedir que as notificações subsequentes.  
  
 *pError*  
 Um [erro](../../../ado/reference/ado-api/error-object.md) objeto. Descreve o erro ocorrido se o valor de *adStatus* é **adStatusErrorsOccurred**; caso contrário, ele não está definido.  
  
 *pRecordset*  
 Um **registros** objeto. O **registros** para que esse evento ocorreu.  
  
## <a name="remarks"></a>Remarks  
 Um **WillChangeRecordset** ou **RecordsetChangeComplete** evento pode ocorrer devido a **registros** [Requery](../../../ado/reference/ado-api/requery-method.md) ou [Abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md) métodos.  
  
 Se o provedor não oferece suporte a indicadores, um **RecordsetChange** notificação de evento ocorre toda vez que novas linhas são recuperadas do provedor. A frequência desse evento depende de **RecordsetCacheSize** propriedade.  
  
 Você deve definir o **adStatus** parâmetro **adStatusUnwantedEvent** para cada possível **adReason** valor pare completamente a notificação de eventos para qualquer evento que inclui um **adReason** parâmetro.  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de modelo de eventos do ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Resumo do manipulador de eventos ADO](../../../ado/guide/data/ado-event-handler-summary.md)
