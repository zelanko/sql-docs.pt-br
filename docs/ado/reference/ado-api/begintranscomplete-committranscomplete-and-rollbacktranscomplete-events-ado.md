---
title: Eventos do BeginTrans, CommitTrans e RollbackTrans (ADO) | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 8239a5f9069212b9413216bc3535e3c90e2d5316
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66696359"
---
# <a name="begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado"></a>BeginTransComplete, CommitTransComplete e RollbackTransComplete eventos (ADO)
Esses eventos serão chamados após a operação associada na [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto termina a execução.  
  
-   **BeginTransComplete** é chamado após o [BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) operação.  
  
-   **CommitTransComplete** é chamado após o [CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) operação.  
  
-   **RollbackTransComplete** é chamado após o [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) operação.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
BeginTransComplete TransactionLevel, pError, adStatus, pConnection  
CommitTransComplete pError, adStatus, pConnection  
RollbackTransComplete pError, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *TransactionLevel*  
 Um **longo** que contém o novo nível de transação do valor de **BeginTrans** que causou este evento.  
  
 *pError*  
 Uma [erro](../../../ado/reference/ado-api/error-object.md) objeto. Ele descreve o erro que ocorreu, se for o valor de EventStatusEnum **adStatusErrorsOccurred**; caso contrário, ele não está definido.  
  
 *adStatus*  
 Uma [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valor de status. Quando qualquer um desses eventos é chamado, esse parâmetro é definido como **adStatusOK** se a operação que causou o evento foi bem-sucedida, ou para **adStatusErrorsOccurred** se a operação falhou.  
  
 Esses eventos podem impedir que as notificações subsequentes ao definir esse parâmetro **adStatusUnwantedEvent** antes de retorna o evento.  
  
 *pConnection*  
 O **Conexão** de objeto para o qual esse evento ocorreu.  
  
## <a name="remarks"></a>Comentários  
 No Visual C++, vários **conexões** podem compartilhar o mesmo método de manipulação de eventos. O método usa retornado **Conexão** objeto para determinar qual objeto causou o evento.  
  
 Se o [atributos](../../../ado/reference/ado-api/attributes-property-ado.md) estiver definida como **adXactCommitRetaining** ou **adXactAbortRetaining**, uma nova transação é iniciado depois de confirmar ou reverter uma transação. Use o **BeginTransComplete** evento para Ignorar tudo, mas o primeiro evento de início da transação.  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de modelo de eventos ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [BeginTrans, CommitTrans e RollbackTrans exemplo dos métodos (VB)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-example-vb.md)   
 [Resumo do manipulador de eventos ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Métodos BeginTrans, CommitTrans e RollbackTrans (ADO)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)
