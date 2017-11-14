---
title: Eventos de RollbackTrans BeginTrans, CommitTrans e (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 26062971810fcc46fdcd3ab95c8edc0701784860
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado"></a>BeginTransComplete, CommitTransComplete e RollbackTransComplete eventos (ADO)
Esses eventos ser chamados após a operação associada no [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto conclui a execução.  
  
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
 Um **longo** valor que contém o novo nível de transação do **BeginTrans** que causou este evento.  
  
 *pError*  
 Um [erro](../../../ado/reference/ado-api/error-object.md) objeto. Descreve o erro ocorrido se o valor de EventStatusEnum é **adStatusErrorsOccurred**; caso contrário, ele não está definido.  
  
 *adStatus*  
 Um [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valor de status. Quando qualquer um desses eventos é chamado, esse parâmetro é definido como **adStatusOK** se a operação que causou o evento foi bem-sucedida, ou para **adStatusErrorsOccurred** se a operação falhou.  
  
 Esses eventos podem impedir que as notificações subsequentes ao definir esse parâmetro **adStatusUnwantedEvent** antes de retorna o evento.  
  
 *pConnection*  
 O **Conexão** de objeto para que esse evento ocorreu.  
  
## <a name="remarks"></a>Comentários  
 No Visual C++, vários **conexões** podem compartilhar o mesmo método de manipulação de eventos. O método usa retornado **Conexão** objeto para determinar qual objeto causou o evento.  
  
 Se o [atributos](../../../ado/reference/ado-api/attributes-property-ado.md) está definida como **adXactCommitRetaining** ou **adXactAbortRetaining**, inicia uma nova transação depois de confirmar ou reverter uma transação. Use o **BeginTransComplete** evento para Ignorar tudo, mas o primeiro evento de início da transação.  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de modelo de eventos do ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [BeginTrans, CommitTrans e exemplo de métodos RollbackTrans (VB)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-example-vb.md)   
 [Resumo de manipulador de eventos de ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Métodos BeginTrans, CommitTrans e RollbackTrans (ADO)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)

