---
title: ConnectComplete e desconectar eventos (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a7b708126c7187a47ee1c9e4c49f6595cc5b3ae4
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="connectcomplete-and-disconnect-events-ado"></a>ConnectComplete e desconectar eventos (ADO)
O **ConnectComplete** evento é chamado após o início de uma conexão. O **Disconnect** evento é chamado após o término de uma conexão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ConnectComplete pError, adStatus, pConnection  
Disconnect adStatus, pConnection  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *pError*  
 Um [erro](../../../ado/reference/ado-api/error-object.md) objeto. Descreve o erro ocorrido se o valor de *adStatus* é **adStatusErrorsOccurred**; caso contrário, ele não está definido.  
  
 *adStatus*  
 Um [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valor que sempre retorna **adStatusOK**.  
  
 Quando **ConnectComplete** é chamado, esse parâmetro é definido como **adStatusCancel** se um **WillConnect** evento solicitou o cancelamento de conexão pendente.  
  
 Antes de qualquer evento retorna, defina este parâmetro como **adStatusUnwantedEvent** para impedir que as notificações subsequentes. No entanto, fechar e reabrir o [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) faz com que esses eventos ocorra novamente.  
  
 *pConnection*  
 O **Conexão** de objeto para o qual este evento se aplica.  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de modelo de eventos do ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Resumo do manipulador de eventos ADO](../../../ado/guide/data/ado-event-handler-summary.md)
