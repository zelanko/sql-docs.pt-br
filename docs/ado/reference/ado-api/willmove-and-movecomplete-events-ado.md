---
description: Eventos WillMove e MoveComplete (ADO)
title: Eventos WillMove e MoveComplete (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset::MoveComplete
- WillMove
- MoveComplete
- Recordset::WillMove
helpviewer_keywords:
- MoveComplete event [ADO]
- WillMove event [ADO]
ms.assetid: 1a3d1042-4f30-4526-a0c7-853c242496db
author: rothja
ms.author: jroth
ms.openlocfilehash: 27d86dc84960399be6b5738f72c69430c6834c7e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88987757"
---
# <a name="willmove-and-movecomplete-events-ado"></a>Eventos WillMove e MoveComplete (ADO)
O evento **WillMove** é chamado antes de uma operação pendente Alterar a posição atual no [conjunto de registros](./recordset-object-ado.md). O evento **MoveComplete** é chamado depois que a posição atual no **conjunto de registros** é alterada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
WillMove adReason, adStatus, pRecordset  
MoveComplete adReason, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *adReason*  
 Um valor [EventReasonEnum](./eventreasonenum.md) que especifica o motivo para esse evento. Seu valor pode ser **adRsnMoveFirst**, **adRsnMoveLast**, **adRsnMoveNext**, **adRsnMovePrevious**, **adRsnMove**ou **adRsnRequery**.  
  
 *pError*  
 Um objeto de [erro](./error-object.md) . Ele descreve o erro que ocorreu se o valor de *adStatus* for **adStatusErrorsOccurred**; caso contrário, o parâmetro não será definido.  
  
 *adStatus*  
 Um valor de status de [EventStatusEnum](./eventstatusenum.md) .  
  
 Quando **WillMove** for chamado, esse parâmetro será definido como **adStatusOK** se a operação que causou o evento tiver sido bem-sucedida. Ele será definido como **adStatusCantDeny** se esse evento não puder solicitar o cancelamento da operação pendente.  
  
 Quando **MoveComplete** for chamado, esse parâmetro será definido como **adStatusOK** se a operação que causou o evento foi bem-sucedida ou para **adStatusErrorsOccurred** se a operação falhar.  
  
 Antes de **WillMove** retornar, defina esse parâmetro como **adStatusCancel** para o cancelamento de solicitação da operação pendente ou defina esse parâmetro como **adStatusUnwantedEvent** para evitar notificações subsequentes.  
  
 Antes de **MoveComplete** retornar, defina esse parâmetro como **adStatusUnwantedEvent** para evitar notificações subsequentes.  
  
 *pRecordset*  
 Um objeto [Recordset](./recordset-object-ado.md) . O **conjunto de registros** para o qual esse evento ocorreu.  
  
## <a name="remarks"></a>Comentários  
 Um evento **WillMove** ou **MoveComplete** pode ocorrer devido às seguintes operações de **conjunto de registros** : [Open](./open-method-ado-recordset.md), [move](./move-method-ado.md), [MoveFirst](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md), [MoveLast](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md), [MoveNext](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md), [MovePrevious](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md), [AddNew](./addnew-method-ado.md)e [Requery](./requery-method.md). Esses eventos podem ocorrer devido às seguintes propriedades: [filtro](./filter-property.md), [índice](./index-property.md), [indicador](./bookmark-property-ado.md), [AbsolutePage](./absolutepage-property-ado.md)e [AbsolutePosition](./absoluteposition-property-ado.md). Esses eventos também ocorrerão se um **conjunto de registros** filho tiver eventos do **conjunto** de registros conectados e o **conjunto de registros** pai for movido.  
  
 Você deve definir o parâmetro *adStatus* como **adStatusUnwantedEvent** para cada valor de *adReason* possível a fim de parar completamente a notificação de eventos para qualquer evento que inclua um parâmetro *adReason* .  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do modelo de eventos ADO (VC + +)](./ado-events-model-example-vc.md)   
 [Resumo do manipulador de eventos do ADO](../../guide/data/ado-event-handler-summary.md)   
 [Objeto Recordset (ADO)](./recordset-object-ado.md)