---
title: Eventos ConnectComplete e Disconnect (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Disconnect
- Connection::ConnectComplete
- ConnectComplete
- Connection::Disconnect
helpviewer_keywords:
- Disconnect event [ADO]
- ConnectComplete event [ADO]
ms.assetid: 568f5252-d069-4d99-a01b-2ada87ad1304
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 448270ddf0e8cd7efb5ec39a93d4ff993360730e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67919575"
---
# <a name="connectcomplete-and-disconnect-events-ado"></a>Eventos ConnectComplete e Disconnect (ADO)
O evento **ConnectComplete** é chamado depois que uma conexão é iniciada. O evento de **desconexão** é chamado após o término de uma conexão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ConnectComplete pError, adStatus, pConnection  
Disconnect adStatus, pConnection  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *pError*  
 Um objeto de [erro](../../../ado/reference/ado-api/error-object.md) . Ele descreve o erro que ocorreu se o valor de *adStatus* for **adStatusErrorsOccurred**; caso contrário, ele não será definido.  
  
 *adStatus*  
 Um valor [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) que sempre retorna **adStatusOK**.  
  
 Quando **ConnectComplete** for chamado, esse parâmetro será definido como **adStatusCancel** se um evento **WillConnect** tiver solicitado cancelamento da conexão pendente.  
  
 Antes de qualquer evento retornar, defina esse parâmetro como **adStatusUnwantedEvent** para evitar notificações subsequentes. No entanto, fechar e reabrir a [conexão](../../../ado/reference/ado-api/connection-object-ado.md) faz com que esses eventos ocorram novamente.  
  
 *pConnection*  
 O objeto de **conexão** ao qual esse evento se aplica.  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do modelo de eventos ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Resumo do manipulador de eventos ADO](../../../ado/guide/data/ado-event-handler-summary.md)
