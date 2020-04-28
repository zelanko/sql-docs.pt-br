---
title: Evento WillConnect (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- WillConnect
- Connection::WillConnect
helpviewer_keywords:
- WillConnect event [ADO]
ms.assetid: da561d58-eb58-446c-a4fd-1838c76073c0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9fc1ac74e7e3d521bae587957f5f95771e5a5268
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67945853"
---
# <a name="willconnect-event-ado"></a>Evento WillConnect (ADO)
O evento **WillConnect** é chamado antes de iniciar uma conexão.  
  
 **Aplica-se a:** [objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
WillConnect ConnectionString, UserID, Password, Options, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *ConnectionString*  
 Uma **cadeia de caracteres** que contém informações de conexão para a conexão pendente.  
  
 *ID*  
 Uma **cadeia de caracteres** que contém um nome de usuário para a conexão pendente.  
  
 *Senha*  
 Uma **cadeia de caracteres** que contém uma senha para a conexão pendente.  
  
 *Opções*  
 Um valor **longo** que indica como o provedor deve avaliar o *ConnectionString*. Sua única opção é **adAsyncOpen**.  
  
 *adStatus*  
 Um valor de status de [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) .  
  
 Quando esse evento é chamado, esse parâmetro é definido como **adStatusOK** por padrão. Ele será definido como **adStatusCantDeny** se o evento não puder solicitar o cancelamento da operação pendente.  
  
 Antes desse evento retornar, defina esse parâmetro como **adStatusUnwantedEvent** para evitar notificações subsequentes. Defina esse parâmetro como **adStatusCancel** para solicitar a operação de conexão que causou o cancelamento dessa notificação.  
  
 *pConnection*  
 O objeto de [conexão](../../../ado/reference/ado-api/connection-object-ado.md) ao qual essa notificação de evento se aplica. As alterações nos parâmetros da **conexão** pelo manipulador de eventos **WillConnect** não terão nenhum efeito na **conexão**.  
  
## <a name="remarks"></a>Comentários  
 Quando **WillConnect** é chamado, os parâmetros *ConnectionString*, *userid*, *password*e *Options* são definidos para os valores estabelecidos pela operação que causou esse evento (a conexão pendente) e podem ser alterados antes que o evento seja retornado. **WillConnect** pode retornar uma solicitação que a conexão pendente seja cancelada.  
  
 Quando esse evento for cancelado, **ConnectComplete** será chamado com seu parâmetro *AdStatus* definido como **adStatusErrorsOccurred**.  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do modelo de eventos ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Resumo do manipulador de eventos ADO](../../../ado/guide/data/ado-event-handler-summary.md)
