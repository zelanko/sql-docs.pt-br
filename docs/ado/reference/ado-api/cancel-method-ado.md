---
description: Método Cancel (ADO)
title: Método Cancel (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 75829400fbb1beb838b9254acf7db129980046c3
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975647"
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
|[Comando](./command-object-ado.md)|[Executar](./execute-method-ado-command.md)|  
|[Conexão](./connection-object-ado.md)|[Executar](./execute-method-ado-connection.md) ou [abrir](./open-method-ado-connection.md)|  
|[Registro](./record-object-ado.md)|[CopyRecord](./copyrecord-method-ado.md), [DeleteRecord](./deleterecord-method-ado.md), [MoveRecord](./moverecord-method-ado.md)ou [Open](./open-method-ado-record.md)|  
|[Recordset](./recordset-object-ado.md)|[Abrir](./open-method-ado-recordset.md)|  
|[Fluxo](./stream-object-ado.md)|[Abrir](./open-method-ado-stream.md)|  
  
## <a name="applies-to"></a>Aplica-se A  

:::row:::
    :::column:::
        [Objeto Command (ADO)](./command-object-ado.md)  
        [Objeto Connection (ADO)](./connection-object-ado.md)  
    :::column-end:::
    :::column:::
        [Objeto Record (ADO)](./record-object-ado.md)  
        [Objeto Recordset (ADO)](./recordset-object-ado.md)  
    :::column-end:::
    :::column:::
        [Objeto Stream (ADO)](./stream-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Consulte Também  
 [Exemplo do método Cancel (VB)](./cancel-method-example-vb.md)   
 [Exemplo do método Cancel (VBScript)](../rds-api/cancel-method-example-vbscript.md)   
 [Exemplo do método Cancel (VC + +)](./cancel-method-example-vc.md)   
 [Método Cancel (RDS)](../rds-api/cancel-method-rds.md)   
 [Método CancelBatch (ADO)](./cancelbatch-method-ado.md)   
 [Método CancelUpdate (ADO)](./cancelupdate-method-ado.md)   
 [Método CancelUpdate (RDS)](../rds-api/cancelupdate-method-rds.md)   
 [Método Execute (comando ADO)](./execute-method-ado-command.md)   
 [Método Execute (conexão ADO)](./execute-method-ado-connection.md)   
 [Método Open (conexão ADO)](./open-method-ado-connection.md)   
 [Método Open (Conjunto de registros ADO)](./open-method-ado-recordset.md)