---
title: MoveFirst, MoveLast, MoveNext e MovePrevious métodos (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::MoveLast
- Recordset15::MoveNext
- Recordset15::raw_MoveNext
- Recordset15::raw_MovePrevious
- Recordset15::MoveFirst
- Recordset15::raw_MoveLast
- Recordset15::MovePrevious
- Recordset15::raw_MoveFirst
helpviewer_keywords:
- MoveNext method [ADO]
- MoveLast method [ADO]
- MoveFirst method [ADO]
- MovePrevious method [ADO]
ms.assetid: a61a01a7-5b33-4150-9126-21dfa63654cb
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 83e216f15da49150481af18ee98aac1f604b2394
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66707476"
---
# <a name="movefirst-movelast-movenext-and-moveprevious-methods-ado"></a>MoveFirst, MoveLast, MoveNext e MovePrevious métodos (ADO)
Move para a primeira, última, registro anterior ou seguinte em um especificado [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto e torna esse registro o registro atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
recordset.{MoveFirst | MoveLast | MoveNext | MovePrevious}  
```  
  
## <a name="remarks"></a>Comentários  
 Use o **MoveFirst** método para mover a posição do registro atual para o primeiro registro na **conjunto de registros**.  
  
 Use o **MoveLast** método para mover a posição do registro atual para o último registro na **conjunto de registros**. O **Recordset** objeto deve dar suporte a indicadores ou movimento do cursor com versões anteriores; caso contrário, a chamada de método irá gerar um erro.  
  
 Uma chamada para a **MoveFirst** ou **MoveLast** quando o **conjunto de registros** está vazia (ambos **BOF** e **EOF** são True) gera um erro.  
  
 Use o **MoveNext** método para mover o registro atual posicionar um registro para a frente (na parte inferior do **Recordset**). Se o último registro é o registro atual e você chamar o **MoveNext** método, ADO define o registro atual para a posição após o último registro na **conjunto de registros** ([EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) é **Verdadeira**). Tentativa de mover o encaminhamento quando o **EOF** propriedade já está **verdadeiro** gera um erro.  
  
 No ADO 2.5 e posterior, quando o **conjunto de registros** foi filtrada ou classificada e os dados do registro atual são alterados, chamar o **MoveNext** método move os registros de cursor dois encaminham do registro atual . Isso ocorre porque quando o registro atual é alterado, o próximo registro se torna o novo registro atual. Chamando **MoveNext** depois que a alteração move o cursor um registro para a frente do novo registro atual. Isso é diferente do comportamento no ADO 2.1 e anteriores. Nessas versões anteriores, alterando os dados de um registro atual em classificados ou filtrados **conjunto de registros** não altera a posição do registro atual, e **MoveNext** move o cursor para o próximo registro imediatamente após o registro atual.  
  
 Use o **MovePrevious** método para mover o registro atual posicionar um registro com versões anteriores (na parte superior do **Recordset**). O **Recordset** objeto deve dar suporte a indicadores ou movimento do cursor com versões anteriores; caso contrário, a chamada de método irá gerar um erro. Se o primeiro registro é o registro atual e você chamar o **MovePrevious** método, o ADO define o registro atual para a posição antes do primeiro registro na **conjunto de registros** ([BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)está **verdadeira**). Tentativa de mover quando com versões anteriores a **BOF** propriedade já está **verdadeiro** gera um erro. Se o **conjunto de registros** objeto não oferece suporte a indicadores ou movimento do cursor com versões anteriores, o **MovePrevious** método irá gerar um erro.  
  
 Se o **conjunto de registros** é somente encaminhamento e você deseja oferecer suporte de rolagem para frente e para trás, você pode usar o [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) propriedade para criar um cache de registro que oferecerá suporte ao movimento do cursor com versões anteriores por meio de [mover](../../../ado/reference/ado-api/move-method-ado.md) método. Porque registros armazenados em cache são carregados na memória, você deve evitar o armazenamento em cache os registros que não é necessário. Você pode chamar o **MoveFirst** método em um somente de avanço **conjunto de registros** objeto; fazer isso pode provocar o provedor executar novamente o comando que gerou o **Recordset** objeto .  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [MoveFirst, MoveLast, MoveNext e MovePrevious exemplo dos métodos (VB)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vb.md)   
 [MoveFirst, MoveLast, MoveNext e MovePrevious exemplo dos métodos (VBScript)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vbscript.md)   
 [MoveFirst, MoveLast, MoveNext e MovePrevious exemplo dos métodos (VC + +)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vc.md)   
 [Método Move (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [MoveFirst, MoveLast, MoveNext e MovePrevious métodos (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)   
 [Método MoveRecord (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)
