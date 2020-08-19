---
description: EventStatusEnum
title: EventStatusEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- EventStatusEnum
helpviewer_keywords:
- EventStatusEnum enumeration [ADO]
ms.assetid: ebfd4cda-4017-4873-9d28-38b1c7db12a8
author: rothja
ms.author: jroth
ms.openlocfilehash: 3d696d7b971b5f6624a85addb3f023f2090ac90d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443898"
---
# <a name="eventstatusenum"></a>EventStatusEnum
Especifica o status atual da execução de um evento.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adStatusCancel**|4|Solicita o cancelamento da operação que causou a ocorrência do evento.|  
|**adStatusCantDeny**|3|Indica que a operação não pode solicitar o cancelamento da operação pendente.|  
|**adStatusErrorsOccurred**|2|Indica que a operação que causou o evento falhou devido a um erro ou erros.|  
|**adStatusOK**|1|Indica que a operação que causou o evento foi bem-sucedida.|  
|**adStatusUnwantedEvent**|5|Impede as notificações subsequentes antes da conclusão da execução do método de evento.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums. EventStatus. CANCEL|  
|AdoEnums. EventStatus. CANTDENY|  
|AdoEnums. EventStatus. ERRORSOCCURRED|  
|AdoEnums. EventStatus. OK|  
|AdoEnums. EventStatus. UNWANTEDEVENT|  
  
## <a name="applies-to"></a>Aplica-se A  

:::row:::
    :::column:::
        [Eventos BeginTransComplete, CommitTransComplete e RollbackTransComplete (ADO)](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)  

        [Eventos ConnectComplete e Disconnect (ADO)](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)  

        [EndOfRecordset Event (ADO)](../../../ado/reference/ado-api/endofrecordset-event-ado.md)  

        [Evento ExecuteComplete (ADO)](../../../ado/reference/ado-api/executecomplete-event-ado.md)  
    :::column-end:::
    :::column:::
        [Evento FetchComplete (ADO)](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)  

        [Evento InfoMessage (ADO)](../../../ado/reference/ado-api/infomessage-event-ado.md)  

        [Eventos WillChangeField e FieldChangeComplete (ADO)](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)  

        [Eventos WillChangeRecord e RecordChangeComplete (ADO)](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)  
    :::column-end:::
    :::column:::
        [Eventos WillChangeRecordset e RecordsetChangeComplete (ADO)](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)  

        [Evento WillConnect (ADO)](../../../ado/reference/ado-api/willconnect-event-ado.md)  

        [Evento WillExecute (ADO)](../../../ado/reference/ado-api/willexecute-event-ado.md)  

        [Eventos WillMove e MoveComplete (ADO)](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)  
    :::column-end:::
:::row-end:::
