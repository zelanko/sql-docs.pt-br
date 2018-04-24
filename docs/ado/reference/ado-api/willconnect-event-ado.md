---
title: Evento WillConnect (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- WillConnect
- Connection::WillConnect
helpviewer_keywords:
- WillConnect event [ADO]
ms.assetid: da561d58-eb58-446c-a4fd-1838c76073c0
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e6cbf1f81a692fd7dd2b751a516ff2ad99a79ef8
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="willconnect-event-ado"></a>Evento WillConnect (ADO)
O **WillConnect** evento é chamado antes do início de uma conexão.  
  
 **Aplica-se a:** [o objeto de Conexão (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
WillConnect ConnectionString, UserID, Password, Options, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *ConnectionString*  
 Um **cadeia de caracteres** que contém informações de conexão para a conexão pendente.  
  
 *UserID*  
 Um **cadeia de caracteres** que contém um nome de usuário para a conexão pendente.  
  
 *Senha*  
 Um **cadeia de caracteres** que contém uma senha para a conexão pendente.  
  
 *Opções*  
 Um **longo** valor que indica como o provedor deve avaliar o *ConnectionString*. A única opção é **adAsyncOpen**.  
  
 *adStatus*  
 Um [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valor de status.  
  
 Quando esse evento é chamado, esse parâmetro é definido como **adStatusOK** por padrão. Ele é definido como **adStatusCantDeny** se o evento não é possível solicitar o cancelamento da operação pendente.  
  
 Antes desse evento retorna, defina este parâmetro como **adStatusUnwantedEvent** para impedir que as notificações subsequentes. Definir esse parâmetro como **adStatusCancel** para solicitar a operação de conexão que causou o cancelamento dessa notificação.  
  
 *pConnection*  
 O [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) de objeto para o qual esta notificação de evento se aplica. Altera para os parâmetros do **Conexão** pelo **WillConnect** manipulador de eventos não terá efeito o **Conexão**.  
  
## <a name="remarks"></a>Remarks  
 Quando **WillConnect** é chamado, o *ConnectionString*, *UserID*, *senha*, e *opções* os parâmetros são definidos para os valores estabelecidos pela operação que causou este evento (a conexão pendente) e pode ser alterada antes do evento retorna. **WillConnect** pode retornar uma solicitação que a conexão pendente ser cancelada.  
  
 Quando esse evento é cancelado, **ConnectComplete** será chamada com seu *adStatus* parâmetro definido como **adStatusErrorsOccurred**.  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de modelo de eventos do ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Resumo do manipulador de eventos ADO](../../../ado/guide/data/ado-event-handler-summary.md)
