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
author: rothja
ms.author: jroth
ms.openlocfilehash: ef47b4bac626d82754ce01685504b4a48303a4b4
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764447"
---
# <a name="willexecute-event-ado"></a>Evento WillExecute (ADO)
O evento **WillExecute** é chamado logo antes de um comando pendente ser executado em uma conexão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
WillExecute Source, CursorType, LockType, Options, adStatus, pCommand, pRecordset, pConnection  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Fonte*  
 Uma **cadeia de caracteres** que contém um comando SQL ou um nome de procedimento armazenado.  
  
 *CursorType*  
 Um [CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md) que contém o tipo de cursor para o **conjunto de registros** que será aberto. Com esse parâmetro, você pode alterar o cursor para qualquer tipo durante uma **Recordset**operação de[método Open do conjunto de registros (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md) . O *CursorType* será ignorado para qualquer outra operação.  
  
 *LockType*  
 Um [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) que contém o tipo de bloqueio para o **conjunto de registros** que será aberto. Com esse parâmetro, você pode alterar o bloqueio para qualquer tipo durante uma operação **RecordsetOpen** . *LockType* será ignorado para qualquer outra operação.  
  
 *Opções*  
 Um valor **longo** que indica opções que podem ser usadas para executar o comando ou abrir o **conjunto de registros**.  
  
 *adStatus*  
 Um valor de status de [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) que pode ser **adStatusCantDeny** ou **adStatusOK** quando esse evento é chamado. Se for **adStatusCantDeny**, esse evento poderá não solicitar o cancelamento da operação pendente.  
  
 *pCommand*  
 O objeto do [objeto de comando (ADO)](../../../ado/reference/ado-api/command-object-ado.md) para o qual essa notificação de evento se aplica.  
  
 *pRecordset*  
 O objeto [Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) para o qual essa notificação de evento se aplica.  
  
 *pConnection*  
 O objeto do [objeto de conexão (ADO)](../../../ado/reference/ado-api/connection-object-ado.md) para o qual essa notificação de evento se aplica.  
  
## <a name="remarks"></a>Comentários  
 Um evento **WillExecute** pode ocorrer devido a uma conexão.  Método [Execute (conexão ADO)](../../../ado/reference/ado-api/execute-method-ado-connection.md), [método Execute (comando ADO)](../../../ado/reference/ado-api/execute-method-ado-command.md)ou método [Open Method (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md) o parâmetro *pConnection* deve sempre conter uma referência válida para um objeto **Connection** . Se o evento for devido a **Connection. Execute**, os parâmetros *precaboset* e *pCommand* serão definidos como **Nothing**. Se o evento for devido a **Recordset. Open**, o parâmetro *precaboset* fará referência ao objeto **Recordset** e o parâmetro *pCommand* será definido como **Nothing**. Se o evento for devido a **Command. Execute**, o parâmetro *pCommand* fará referência ao objeto **Command** e o parâmetro *precaboset* será definido como **Nothing**.  
  
 O **WillExecute** permite que você examine e modifique os parâmetros de execução pendentes. Esse evento pode retornar uma solicitação que o comando pendente seja cancelado.  
  
> [!NOTE]
>  Se a origem original de um **comando** for um fluxo especificado pela propriedade [CommandStream (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md) , atribuir uma nova cadeia de caracteres ao parâmetro_Source_ **WillExecute**alterará a origem do **comando**. A propriedade **CommandStream** será desmarcada e a propriedade [CommandText (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md) será atualizada com a nova origem. O fluxo original especificado por **CommandStream** será liberado e não poderá ser acessado.  
  
 Se o dialeto da nova cadeia de caracteres de origem for diferente da configuração original da propriedade de [Propriedade do dialeto](../../../ado/reference/ado-api/dialect-property.md) (que correspondeu a **CommandStream**), o dialeto correto deverá ser especificado definindo a propriedade **Dialect** do objeto Command referenciado por *pCommand*.  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do modelo de eventos ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Resumo do manipulador de eventos do ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
