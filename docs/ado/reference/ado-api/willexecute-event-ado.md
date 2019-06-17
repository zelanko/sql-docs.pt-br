---
title: Evento WillExecute (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- WillExecute
- Connection::WillExecute
helpviewer_keywords:
- WillExecute event [ADO]
ms.assetid: dd755e46-f589-48a3-93a9-51ff998d44b5
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 571c63e0b8e06c08fb066c3bb6b2d42a019895e5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66710039"
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
 Um [CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md) que contém o tipo de cursor para o **Recordset** que será aberta. Com esse parâmetro, você pode alterar o cursor em qualquer tipo durante um **conjunto de registros**[método Open (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md) operação. *CursorType* será ignorada para qualquer outra operação.  
  
 *LockType*  
 Um [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) que contém o tipo de bloqueio para o **Recordset** que será aberta. Com esse parâmetro, você pode alterar o bloqueio para qualquer tipo durante um **RecordsetOpen** operação. *LockType* será ignorada para qualquer outra operação.  
  
 *Opções*  
 Um **longo** valor que indica as opções que podem ser usadas para executar o comando ou abrir o **conjunto de registros**.  
  
 *adStatus*  
 Uma [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valor de status que pode ser **adStatusCantDeny** ou **adStatusOK** quando esse evento é chamado. Se ele estiver **adStatusCantDeny**, esse evento não pode solicitar o cancelamento da operação pendente.  
  
 *pCommand*  
 O [o objeto de comando (ADO)](../../../ado/reference/ado-api/command-object-ado.md) de objeto para o qual esta notificação de evento se aplica.  
  
 *pRecordset*  
 O [objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) de objeto para o qual esta notificação de evento se aplica.  
  
 *pConnection*  
 O [o objeto de Conexão (ADO)](../../../ado/reference/ado-api/connection-object-ado.md) de objeto para o qual esta notificação de evento se aplica.  
  
## <a name="remarks"></a>Comentários  
 Um **WillExecute** evento pode ocorrer devido a uma Conexão.  [Executar método (Conexão ADO)](../../../ado/reference/ado-api/execute-method-ado-connection.md), [método Execute (comando ADO)](../../../ado/reference/ado-api/execute-method-ado-command.md), ou [método Open (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md) método de *pConnection* deve de parâmetro sempre contém uma referência válida para um **Conexão** objeto. Se o evento for devido à **Connection.Execute**, o *pRecordset* e *pCommand* parâmetros são definidos como **nada**. Se o evento for devido à **Recordset.Open**, o *pRecordset* parâmetro fará referência a **conjunto de registros** objeto e o *pCommand* parâmetro for definido como **nada**. Se o evento for devido à **Command.Execute**, o *pCommand* parâmetro fará referência a **comando** objeto e o *pRecordset* parâmetro for definido como **nada**.  
  
 **WillExecute** permite que você examine e modifique os parâmetros de execução pendente. Esse evento pode retornar uma solicitação que o comando pendente a ser cancelada.  
  
> [!NOTE]
>  Se original da fonte para um **comando** é um fluxo especificadas pelo [propriedade CommandStream (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md) propriedade, atribuir uma nova cadeia de caracteres para o **WillExecute** _Código-fonte_ parâmetro altera a origem do **comando**. O **CommandStream** propriedade será limpa e o [propriedade CommandText (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md) propriedade será atualizada com a nova fonte. O fluxo original especificado pelo **CommandStream** será liberado e não pode ser acessado.  
  
 Se o dialeto da nova cadeia de caracteres de origem é diferente da configuração original do [propriedade Dialect](../../../ado/reference/ado-api/dialect-property.md) propriedade (que correspondessem ao **CommandStream**), o dialeto correto deve ser especificado definindo o **dialeto** propriedade do objeto de comando referenciada por *pCommand*.  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de modelo de eventos ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Resumo do manipulador de eventos ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
