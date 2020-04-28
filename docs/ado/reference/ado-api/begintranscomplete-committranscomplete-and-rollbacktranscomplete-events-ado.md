---
title: BeginTrans, CommitTrans, eventos RollbackTrans (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CommitTransComplete
- Connection::BeginTransComplete
- Connection::RollbackTransComplete
- Connection::CommitTransComplete
- RollbackTransComplete
- BeginTransComplete
helpviewer_keywords:
- CommitTransComplete event [ADO]
- RollbackTransComplete event [ADO]
- BeginTransComplete event [ADO]
ms.assetid: ec4e4b38-e9c6-4757-b2ef-4e468ae5f1d8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 750e89e97eb916c7db23e71475b753a57a4d90e9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67920445"
---
# <a name="begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado"></a>Eventos BeginTransComplete, CommitTransComplete e RollbackTransComplete (ADO)
Esses eventos serão chamados depois que a operação associada no objeto de [conexão](../../../ado/reference/ado-api/connection-object-ado.md) terminar a execução.  
  
-   **BeginTransComplete** é chamado após a operação [BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) .  
  
-   **CommitTransComplete** é chamado após a operação de [CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) .  
  
-   **RollbackTransComplete** é chamado após a operação [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
BeginTransComplete TransactionLevel, pError, adStatus, pConnection  
CommitTransComplete pError, adStatus, pConnection  
RollbackTransComplete pError, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *TransactionLevel*  
 Um valor **longo** que contém o novo nível de transação do **BeginTrans** que causou esse evento.  
  
 *pError*  
 Um objeto de [erro](../../../ado/reference/ado-api/error-object.md) . Ele descreve o erro que ocorreu se o valor de EventStatusEnum for **adStatusErrorsOccurred**; caso contrário, ele não será definido.  
  
 *adStatus*  
 Um valor de status de [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) . Quando qualquer um desses eventos for chamado, esse parâmetro será definido como **adStatusOK** se a operação que causou o êxito do evento ou **adStatusErrorsOccurred** se a operação falhou.  
  
 Esses eventos podem impedir notificações subsequentes definindo esse parâmetro como **adStatusUnwantedEvent** antes que o evento seja retornado.  
  
 *pConnection*  
 O objeto de **conexão** para o qual esse evento ocorreu.  
  
## <a name="remarks"></a>Comentários  
 No Visual C++, várias **conexões** podem compartilhar o mesmo método de manipulação de eventos. O método usa o objeto de **conexão** retornado para determinar qual objeto causou o evento.  
  
 Se a propriedade [Attributes](../../../ado/reference/ado-api/attributes-property-ado.md) for definida como **adXactCommitRetaining** ou **adXactAbortRetaining**, uma nova transação será iniciada depois de confirmar ou reverter uma transação. Use o evento **BeginTransComplete** para ignorar tudo, exceto o primeiro evento de início de transação.  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do modelo de eventos ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Exemplo dos métodos BeginTrans, CommitTrans e RollbackTrans (VB)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-example-vb.md)   
 [Resumo do manipulador de eventos do ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Métodos BeginTrans, CommitTrans e RollbackTrans (ADO)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)
