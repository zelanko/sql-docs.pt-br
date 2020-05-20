---
title: Evento InfoMessage (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection::InfoMessage
- InfoMessage
helpviewer_keywords:
- InfoMessage event [ADO]
ms.assetid: 468c87dd-e3bc-4084-9941-94d10743d4e9
author: rothja
ms.author: jroth
ms.openlocfilehash: c5fc0adfec791294bb6c680dab94078b8a63ec07
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82758682"
---
# <a name="infomessage-event-ado"></a>Evento InfoMessage (ADO)
O evento **InfoMessage** é chamado sempre que ocorrer um aviso durante uma operação de **ConnectionEvent** .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
InfoMessage pError, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *pError*  
 Um objeto de [erro](../../../ado/reference/ado-api/error-object.md) . Esse parâmetro contém todos os erros retornados. Se vários erros forem retornados, enumere a coleção de **erros** para encontrá-los.  
  
 *adStatus*  
 Um valor de status de [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) . Se ocorrer um aviso, *adStatus* será definido como **AdStatusOK** e o *perror* conterá o aviso.  
  
 Antes desse evento retornar, defina esse parâmetro como **adStatusUnwantedEvent** para evitar notificações subsequentes.  
  
 *pConnection*  
 Um objeto de [conexão](../../../ado/reference/ado-api/connection-object-ado.md) . A conexão para a qual o aviso ocorreu. Por exemplo, podem ocorrer avisos ao abrir um objeto de **conexão** ou executar um [comando](../../../ado/reference/ado-api/command-object-ado.md) em uma **conexão**.  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do modelo de eventos ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Resumo do manipulador de eventos do ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
