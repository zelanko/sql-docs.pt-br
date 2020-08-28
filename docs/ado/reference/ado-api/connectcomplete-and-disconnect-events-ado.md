---
description: Eventos ConnectComplete e Disconnect (ADO)
title: Eventos ConnectComplete e Disconnect (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 9fbea6991ca030f0f83e31dfdc26b3ac72a8697f
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974987"
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
 Um objeto de [erro](./error-object.md) . Ele descreve o erro que ocorreu se o valor de *adStatus* for **adStatusErrorsOccurred**; caso contrário, ele não será definido.  
  
 *adStatus*  
 Um valor [EventStatusEnum](./eventstatusenum.md) que sempre retorna **adStatusOK**.  
  
 Quando **ConnectComplete** for chamado, esse parâmetro será definido como **adStatusCancel** se um evento **WillConnect** tiver solicitado cancelamento da conexão pendente.  
  
 Antes de qualquer evento retornar, defina esse parâmetro como **adStatusUnwantedEvent** para evitar notificações subsequentes. No entanto, fechar e reabrir a [conexão](./connection-object-ado.md) faz com que esses eventos ocorram novamente.  
  
 *pConnection*  
 O objeto de **conexão** ao qual esse evento se aplica.  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do modelo de eventos ADO (VC + +)](./ado-events-model-example-vc.md)   
 [Resumo do manipulador de eventos ADO](../../guide/data/ado-event-handler-summary.md)