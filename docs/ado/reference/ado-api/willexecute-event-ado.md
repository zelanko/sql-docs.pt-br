---
description: Evento WillExecute (ADO)
title: Evento WillExecute (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: f56e864efd37b927ae657edc2ef2e8307d839104
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88987767"
---
# <a name="willexecute-event-ado"></a>Evento WillExecute (ADO)
O evento **WillExecute** é chamado logo antes de um comando pendente ser executado em uma conexão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
WillExecute Source, CursorType, LockType, Options, adStatus, pCommand, pRecordset, pConnection  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Origem*  
 Uma **cadeia de caracteres** que contém um comando SQL ou um nome de procedimento armazenado.  
  
 *CursorType*  
 Um [CursorTypeEnum](./cursortypeenum.md) que contém o tipo de cursor para o **conjunto de registros** que será aberto. Com esse parâmetro, você pode alterar o cursor para qualquer tipo durante uma **Recordset**operação de[método Open do conjunto de registros (ADO Recordset)](./open-method-ado-recordset.md) . O *CursorType* será ignorado para qualquer outra operação.  
  
 *LockType*  
 Um [LockTypeEnum](./locktypeenum.md) que contém o tipo de bloqueio para o **conjunto de registros** que será aberto. Com esse parâmetro, você pode alterar o bloqueio para qualquer tipo durante uma operação **RecordsetOpen** . *LockType* será ignorado para qualquer outra operação.  
  
 *Opções*  
 Um valor **longo** que indica opções que podem ser usadas para executar o comando ou abrir o **conjunto de registros**.  
  
 *adStatus*  
 Um valor de status de [EventStatusEnum](./eventstatusenum.md) que pode ser **adStatusCantDeny** ou **adStatusOK** quando esse evento é chamado. Se for **adStatusCantDeny**, esse evento poderá não solicitar o cancelamento da operação pendente.  
  
 *pCommand*  
 O objeto do [objeto de comando (ADO)](./command-object-ado.md) para o qual essa notificação de evento se aplica.  
  
 *pRecordset*  
 O objeto [Recordset (ADO)](./recordset-object-ado.md) para o qual essa notificação de evento se aplica.  
  
 *pConnection*  
 O objeto do [objeto de conexão (ADO)](./connection-object-ado.md) para o qual essa notificação de evento se aplica.  
  
## <a name="remarks"></a>Comentários  
 Um evento **WillExecute** pode ocorrer devido a uma conexão.  Método [Execute (conexão ADO)](./execute-method-ado-connection.md), [método Execute (comando ADO)](./execute-method-ado-command.md)ou método [Open Method (ADO Recordset)](./open-method-ado-recordset.md) o parâmetro *pConnection* deve sempre conter uma referência válida para um objeto **Connection** . Se o evento for devido a **Connection.Exegraciosos**, os parâmetros *precaboset* e *pCommand* serão definidos como **Nothing**. Se o evento for devido a **Recordset. Open**, o parâmetro *precaboset* fará referência ao objeto **Recordset** e o parâmetro *pCommand* será definido como **Nothing**. Se o evento for devido a **Command.Exegraciosos**, o parâmetro *pCommand* fará referência ao objeto **Command** e o parâmetro *precaboset* será definido como **Nothing**.  
  
 O **WillExecute** permite que você examine e modifique os parâmetros de execução pendentes. Esse evento pode retornar uma solicitação que o comando pendente seja cancelado.  
  
> [!NOTE]
>  Se a origem original de um **comando** for um fluxo especificado pela propriedade [CommandStream (ADO)](./commandstream-property-ado.md) , atribuir uma nova cadeia de caracteres ao parâmetro_Source_ **WillExecute**alterará a origem do **comando**. A propriedade **CommandStream** será desmarcada e a propriedade [CommandText (ADO)](./commandtext-property-ado.md) será atualizada com a nova origem. O fluxo original especificado por **CommandStream** será liberado e não poderá ser acessado.  
  
 Se o dialeto da nova cadeia de caracteres de origem for diferente da configuração original da propriedade de [Propriedade do dialeto](./dialect-property.md) (que correspondeu a **CommandStream**), o dialeto correto deverá ser especificado definindo a propriedade **Dialect** do objeto Command referenciado por *pCommand*.  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do modelo de eventos ADO (VC + +)](./ado-events-model-example-vc.md)   
 [Resumo do manipulador de eventos do ADO](../../guide/data/ado-event-handler-summary.md)   
 [Objeto Connection (ADO)](./connection-object-ado.md)