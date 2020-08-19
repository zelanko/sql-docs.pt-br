---
description: Eventos WillMove e MoveComplete (ADO)
title: Eventos WillMove e MoveComplete (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
ms.openlocfilehash: 4c992f95ae9caf96708f5fcde0c255ff8c7c6f11
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441498"
---
# <a name="willmove-and-movecomplete-events-ado"></a>Eventos WillMove e MoveComplete (ADO)
O evento **WillMove** é chamado antes de uma operação pendente Alterar a posição atual no [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md). O evento **MoveComplete** é chamado depois que a posição atual no **conjunto de registros** é alterada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
WillMove adReason, adStatus, pRecordset  
MoveComplete adReason, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *adReason*  
 Um valor [EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md) que especifica o motivo para esse evento. Seu valor pode ser **adRsnMoveFirst**, **adRsnMoveLast**, **adRsnMoveNext**, **adRsnMovePrevious**, **adRsnMove**ou **adRsnRequery**.  
  
 *pError*  
 Um objeto de [erro](../../../ado/reference/ado-api/error-object.md) . Ele descreve o erro que ocorreu se o valor de *adStatus* for **adStatusErrorsOccurred**; caso contrário, o parâmetro não será definido.  
  
 *adStatus*  
 Um valor de status de [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) .  
  
 Quando **WillMove** for chamado, esse parâmetro será definido como **adStatusOK** se a operação que causou o evento tiver sido bem-sucedida. Ele será definido como **adStatusCantDeny** se esse evento não puder solicitar o cancelamento da operação pendente.  
  
 Quando **MoveComplete** for chamado, esse parâmetro será definido como **adStatusOK** se a operação que causou o evento foi bem-sucedida ou para **adStatusErrorsOccurred** se a operação falhar.  
  
 Antes de **WillMove** retornar, defina esse parâmetro como **adStatusCancel** para o cancelamento de solicitação da operação pendente ou defina esse parâmetro como **adStatusUnwantedEvent** para evitar notificações subsequentes.  
  
 Antes de **MoveComplete** retornar, defina esse parâmetro como **adStatusUnwantedEvent** para evitar notificações subsequentes.  
  
 *pRecordset*  
 Um objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) . O **conjunto de registros** para o qual esse evento ocorreu.  
  
## <a name="remarks"></a>Comentários  
 Um evento **WillMove** ou **MoveComplete** pode ocorrer devido às seguintes operações de **conjunto de registros** : [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md), [move](../../../ado/reference/ado-api/move-method-ado.md), [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), [MoveLast](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), [MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), [MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)e [Requery](../../../ado/reference/ado-api/requery-method.md). Esses eventos podem ocorrer devido às seguintes propriedades: [filtro](../../../ado/reference/ado-api/filter-property.md), [índice](../../../ado/reference/ado-api/index-property.md), [indicador](../../../ado/reference/ado-api/bookmark-property-ado.md), [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)e [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md). Esses eventos também ocorrerão se um **conjunto de registros** filho tiver eventos do **conjunto** de registros conectados e o **conjunto de registros** pai for movido.  
  
 Você deve definir o parâmetro *adStatus* como **adStatusUnwantedEvent** para cada valor de *adReason* possível a fim de parar completamente a notificação de eventos para qualquer evento que inclua um parâmetro *adReason* .  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do modelo de eventos ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Resumo do manipulador de eventos do ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
