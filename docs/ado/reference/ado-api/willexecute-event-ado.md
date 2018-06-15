---
title: Evento WillExecute (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- WillExecute
- Connection::WillExecute
helpviewer_keywords:
- WillExecute event [ADO]
ms.assetid: dd755e46-f589-48a3-93a9-51ff998d44b5
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d0fd9c97018c5c15710067298a88b4996c5a699f
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35282875"
---
# <a name="willexecute-event-ado"></a>Evento WillExecute (ADO)
O **WillExecute** evento é chamado antes de um comando pendente é executado em uma conexão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
WillExecute Source, CursorType, LockType, Options, adStatus, pCommand, pRecordset, pConnection  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Origem*  
 Um **cadeia de caracteres** que contém um comando SQL ou um nome de procedimento armazenado.  
  
 *CursorType*  
 Um [CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md) que contém o tipo de cursor para o **registros** que será aberta. Com esse parâmetro, você pode alterar o cursor para qualquer tipo durante um **registros**[método Open (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md) operação. *CursorType* será ignorada para qualquer outra operação.  
  
 *LockType*  
 Um [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) que contém o tipo de bloqueio para o **registros** que será aberta. Com esse parâmetro, você pode alterar o bloqueio em qualquer tipo durante um **RecordsetOpen** operação. *LockType* será ignorada para qualquer outra operação.  
  
 *Opções*  
 Um **longo** valor que indica as opções que podem ser usadas para executar o comando ou abrir o **registros**.  
  
 *adStatus*  
 Um [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valor de status que pode ser **adStatusCantDeny** ou **adStatusOK** quando esse evento é chamado. Se for **adStatusCantDeny**, esse evento não pode solicitar o cancelamento da operação pendente.  
  
 *pCommand*  
 O [comando Object (ADO)](../../../ado/reference/ado-api/command-object-ado.md) de objeto para o qual esta notificação de evento se aplica.  
  
 *pRecordset*  
 O [Recordset Object (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) de objeto para o qual esta notificação de evento se aplica.  
  
 *pConnection*  
 O [Conexão Object (ADO)](../../../ado/reference/ado-api/connection-object-ado.md) de objeto para o qual esta notificação de evento se aplica.  
  
## <a name="remarks"></a>Remarks  
 Um **WillExecute** evento pode ocorrer devido a uma Conexão.  [Executar método (Conexão ADO)](../../../ado/reference/ado-api/execute-method-ado-connection.md), [executar método (comando ADO)](../../../ado/reference/ado-api/execute-method-ado-command.md), ou [método Open (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md) método o *pConnection* deve de parâmetro sempre contém uma referência válida para um **Conexão** objeto. Se o evento for devido a **Connection.Execute**, o *pRecordset* e *pCommand* parâmetros são definidos como **nada**. Se o evento for devido a **Recordset.Open**, o *pRecordset* parâmetro fará referência a **registros** objeto e o *pCommand* parâmetro está definido como **nada**. Se o evento for devido a **Command.Execute**, o *pCommand* parâmetro fará referência a **comando** objeto e o *pRecordset* parâmetro está definido como **nada**.  
  
 **WillExecute** permite que você examine e modifique os parâmetros de execução pendente. Esse evento pode retornar uma solicitação que o comando pendente ser cancelada.  
  
> [!NOTE]
>  Se a fonte original para uma **comando** é um fluxo especificado pelo [propriedade CommandStream (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md) propriedade, atribuir uma nova cadeia de caracteres para o **WillExecute * fonte* a origem do parâmetro é alterado de **comando**. O **CommandStream** propriedade será limpa e [propriedade CommandText (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md) propriedade será atualizada com a nova fonte. O fluxo original especificado por **CommandStream** serão liberados e não pode ser acessado.  
  
 Se o dialeto da nova cadeia de caracteres de origem é diferente da configuração original de [propriedade Dialect](../../../ado/reference/ado-api/dialect-property.md) propriedade (que correspondeu ao **CommandStream**), o dialeto correto deve ser especificado pela configuração o **dialeto** propriedade do objeto de comando referenciada por *pCommand*.  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de modelo de eventos do ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Resumo de manipulador de eventos de ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
