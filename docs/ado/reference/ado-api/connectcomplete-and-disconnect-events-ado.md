---
title: ConnectComplete e desconectar eventos (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
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
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ebd4363f166a67a6e48fee41c2585b68de93bc98
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

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

