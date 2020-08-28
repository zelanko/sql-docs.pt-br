---
description: Eventos BeginTransComplete, CommitTransComplete e RollbackTransComplete (ADO)
title: BeginTrans, CommitTrans, eventos RollbackTrans (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 91f5d573d62ef5000cdd6ed85a52866a0ee7f544
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975867"
---
# <a name="begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado"></a>Eventos BeginTransComplete, CommitTransComplete e RollbackTransComplete (ADO)
Esses eventos serão chamados depois que a operação associada no objeto de [conexão](./connection-object-ado.md) terminar a execução.  
  
-   **BeginTransComplete** é chamado após a operação [BeginTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md) .  
  
-   **CommitTransComplete** é chamado após a operação de [CommitTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md) .  
  
-   **RollbackTransComplete** é chamado após a operação [RollbackTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md) .  
  
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
 Um objeto de [erro](./error-object.md) . Ele descreve o erro que ocorreu se o valor de EventStatusEnum for **adStatusErrorsOccurred**; caso contrário, ele não será definido.  
  
 *adStatus*  
 Um valor de status de [EventStatusEnum](./eventstatusenum.md) . Quando qualquer um desses eventos for chamado, esse parâmetro será definido como **adStatusOK** se a operação que causou o êxito do evento ou **adStatusErrorsOccurred** se a operação falhou.  
  
 Esses eventos podem impedir notificações subsequentes definindo esse parâmetro como **adStatusUnwantedEvent** antes que o evento seja retornado.  
  
 *pConnection*  
 O objeto de **conexão** para o qual esse evento ocorreu.  
  
## <a name="remarks"></a>Comentários  
 No Visual C++, várias **conexões** podem compartilhar o mesmo método de manipulação de eventos. O método usa o objeto de **conexão** retornado para determinar qual objeto causou o evento.  
  
 Se a propriedade [Attributes](./attributes-property-ado.md) for definida como **adXactCommitRetaining** ou **adXactAbortRetaining**, uma nova transação será iniciada depois de confirmar ou reverter uma transação. Use o evento **BeginTransComplete** para ignorar tudo, exceto o primeiro evento de início de transação.  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do modelo de eventos ADO (VC + +)](./ado-events-model-example-vc.md)   
 [Exemplo dos métodos BeginTrans, CommitTrans e RollbackTrans (VB)](./begintrans-committrans-and-rollbacktrans-methods-example-vb.md)   
 [Resumo do manipulador de eventos do ADO](../../guide/data/ado-event-handler-summary.md)   
 [Métodos BeginTrans, CommitTrans e RollbackTrans (ADO)](./begintrans-committrans-and-rollbacktrans-methods-ado.md)