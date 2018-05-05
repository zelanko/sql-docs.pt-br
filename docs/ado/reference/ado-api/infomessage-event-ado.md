---
title: Evento do InfoMessage (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection::InfoMessage
- InfoMessage
helpviewer_keywords:
- InfoMessage event [ADO]
ms.assetid: 468c87dd-e3bc-4084-9941-94d10743d4e9
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e4e0df8393f7f6e6b7c7eefccf8f60c18a242679
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="infomessage-event-ado"></a>Evento do InfoMessage (ADO)
O **InfoMessage** evento é chamado sempre que ocorrer um aviso durante uma **ConnectionEvent** operação.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
InfoMessage pError, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *pError*  
 Um [erro](../../../ado/reference/ado-api/error-object.md) objeto. Este parâmetro contém erros que são retornados. Se vários erros são retornados, enumerar o **erros** coleção encontrá-las.  
  
 *adStatus*  
 Um [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valor de status. Se ocorrer um aviso, *adStatus* é definido como **adStatusOK** e *pError* contém o aviso.  
  
 Antes desse evento retorna, defina este parâmetro como **adStatusUnwantedEvent** para impedir que as notificações subsequentes.  
  
 *pConnection*  
 Um [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto. A conexão para a qual o aviso ocorreu. Por exemplo, os avisos podem ocorrer ao abrir um **Conexão** objeto ou executar um [comando](../../../ado/reference/ado-api/command-object-ado.md) em uma **Conexão**.  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de modelo de eventos do ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Resumo de manipulador de eventos de ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
