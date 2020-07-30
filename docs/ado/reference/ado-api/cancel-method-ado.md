---
title: Método Cancel (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::Cancel
- _Record::Cancel
- _Connection::Cancel
- Command25::Cancel
- _Stream::Cancel
helpviewer_keywords:
- Cancel method [ADO]
ms.assetid: e0db4e15-6787-41e2-8f13-9e9b524d620a
author: rothja
ms.author: jroth
ms.openlocfilehash: 25b6de609d286847fe7458353203dd7f4b9c7b4b
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242422"
---
# <a name="cancel-method-ado"></a>Método Cancel (ADO)
Cancela a execução de uma chamada de método assíncrona pendente.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.Cancel  
```  
  
## <a name="remarks"></a>Comentários  
 Use o método **Cancel** para encerrar a execução de uma chamada de método assíncrono: ou seja, um método invocado com a opção **adAsyncConnect**, **adAsyncExecute**ou **adAsyncFetch** .  
  
 A tabela a seguir mostra qual tarefa é encerrada quando você usa o método **Cancel** em um determinado tipo de objeto.  
  
|Se *Object* for um|A última chamada assíncrona para este método é encerrada|  
|----------------------|-------------------------------------------------------------|  
|[Comando](../../../ado/reference/ado-api/command-object-ado.md)|[Executados](../../../ado/reference/ado-api/execute-method-ado-command.md)|  
|[Conexão](../../../ado/reference/ado-api/connection-object-ado.md)|[Executar](../../../ado/reference/ado-api/execute-method-ado-connection.md) ou [abrir](../../../ado/reference/ado-api/open-method-ado-connection.md)|  
|[Registro](../../../ado/reference/ado-api/record-object-ado.md)|[CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md), [DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md), [MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md)ou [Open](../../../ado/reference/ado-api/open-method-ado-record.md)|  
|[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)|[Abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md)|  
|[Fluxo](../../../ado/reference/ado-api/stream-object-ado.md)|[Abrir](../../../ado/reference/ado-api/open-method-ado-stream.md)|  
  
## <a name="applies-to"></a>Aplica-se A  

:::row:::
    :::column:::
        [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
        [Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
    :::column-end:::
    :::column:::
        [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
        [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
    :::column-end:::
    :::column:::
        [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Consulte Também  
 [Exemplo do método Cancel (VB)](../../../ado/reference/ado-api/cancel-method-example-vb.md)   
 [Exemplo do método Cancel (VBScript)](../../../ado/reference/rds-api/cancel-method-example-vbscript.md)   
 [Exemplo do método Cancel (VC + +)](../../../ado/reference/ado-api/cancel-method-example-vc.md)   
 [Método Cancel (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [Método CancelBatch (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Método CancelUpdate (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Método CancelUpdate (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Método Execute (comando ADO)](../../../ado/reference/ado-api/execute-method-ado-command.md)   
 [Método Execute (conexão ADO)](../../../ado/reference/ado-api/execute-method-ado-connection.md)   
 [Método Open (conexão ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Método Open (Conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)
