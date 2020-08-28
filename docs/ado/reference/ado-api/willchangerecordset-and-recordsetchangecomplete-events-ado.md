---
description: Eventos WillChangeRecordset e RecordsetChangeComplete (ADO)
title: Eventos WillChangeRecordset e RecordsetChangeComplete (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: c3066ebce2f1f3e96404e933af1c39ad0fdd2659
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88987797"
---
# <a name="willchangerecordset-and-recordsetchangecomplete-events-ado"></a>Eventos WillChangeRecordset e RecordsetChangeComplete (ADO)
O evento **WillChangeRecordset** é chamado antes de uma operação pendente Alterar o [conjunto de registros](./recordset-object-ado.md). O evento **RecordsetChangeComplete** é chamado depois que o **conjunto de registros** é alterado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
WillChangeRecordset adReason, adStatus, pRecordset  
RecordsetChangeComplete adReason, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *adReason*  
 Um valor [EventReasonEnum](./eventreasonenum.md) que especifica o motivo para esse evento. Seu valor pode ser **adRsnRequery**, **adRsnResynch**, **adRsnClose**, **adRsnOpen**.  
  
 *adStatus*  
 Um valor de status de [EventStatusEnum](./eventstatusenum.md) .  
  
 Quando **WillChangeRecordset** for chamado, esse parâmetro será definido como **adStatusOK** se a operação que causou o evento tiver sido bem-sucedida. Ele será definido como **adStatusCantDeny** se esse evento não puder solicitar o cancelamento da operação pendente.  
  
 Quando **RecordsetChangeComplete** for chamado, esse parâmetro será definido como **adStatusOK** se a operação que causou o êxito do evento, **adStatusErrorsOccurred** se a operação falhou ou **AdStatusCancel** se a operação associada ao evento **WillChangeRecordset** anteriormente aceito foi cancelada.  
  
 Antes de **WillChangeRecordset** retornar, defina esse parâmetro como **adStatusCancel** para solicitar cancelamento da operação pendente ou defina esse parâmetro como adStatusUnwantedEvent para evitar notificações subsequentes.  
  
 Antes de **WillChangeRecordset** ou **RecordsetChangeComplete** retornar, defina esse parâmetro como **adStatusUnwantedEvent** para evitar notificações subsequentes.  
  
 *pError*  
 Um objeto de [erro](./error-object.md) . Ele descreve o erro que ocorreu se o valor de *adStatus* for **adStatusErrorsOccurred**; caso contrário, ele não será definido.  
  
 *pRecordset*  
 Um objeto **Recordset** . O **conjunto de registros** para o qual esse evento ocorreu.  
  
## <a name="remarks"></a>Comentários  
 Um evento **WillChangeRecordset** ou **RecordsetChangeComplete** pode ocorrer devido à [repetição](./requery-method.md) do **conjunto de registros** ou aos métodos [abertos](./open-method-ado-recordset.md) .  
  
 Se o provedor não oferecer suporte a indicadores, uma notificação de evento **RecordsetChange** ocorrerá toda vez que novas linhas forem recuperadas do provedor. A frequência desse evento depende da propriedade **RecordsetCacheSize** .  
  
 Você deve definir o parâmetro **adStatus** como **adStatusUnwantedEvent** para cada valor de **adReason** possível parar completamente a notificação de eventos para qualquer evento que inclua um parâmetro **adReason** .  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do modelo de eventos ADO (VC + +)](./ado-events-model-example-vc.md)   
 [Resumo do manipulador de eventos ADO](../../guide/data/ado-event-handler-summary.md)