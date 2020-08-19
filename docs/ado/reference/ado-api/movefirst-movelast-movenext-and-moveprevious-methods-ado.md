---
description: Métodos MoveFirst, MoveLast, MoveNext e MovePrevious (ADO)
title: Métodos MoveFirst, MoveLast, MoveNext e MovePrevious (ADO) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 440b2dec1ce045604456c38672c8c53e5c514df2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443198"
---
# <a name="movefirst-movelast-movenext-and-moveprevious-methods-ado"></a>Métodos MoveFirst, MoveLast, MoveNext e MovePrevious (ADO)
Move para o primeiro, último, próximo ou registro anterior em um objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) especificado e torna esse registro o registro atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
recordset.{MoveFirst | MoveLast | MoveNext | MovePrevious}  
```  
  
## <a name="remarks"></a>Comentários  
 Use o método **MoveFirst** para mover a posição atual do registro para o primeiro registro no **conjunto de registros**.  
  
 Use o método **MoveLast** para mover a posição atual do registro para o último registro no **conjunto de registros**. O objeto **Recordset** deve dar suporte a indicadores ou movimento de cursor para trás; caso contrário, a chamada do método gerará um erro.  
  
 Uma chamada para o **MoveFirst** ou **MoveLast** quando o **conjunto de registros** está vazio ( **BOF** e **EOF** são verdadeiros) gera um erro.  
  
 Use o método **MoveNext** para mover a posição do registro atual um registro para frente (na direção da parte inferior do **conjunto de registros**). Se o último registro for o registro atual e você chamar o método **MoveNext** , o ADO definirá o registro atual como a posição após o último registro no **conjunto de registros** ([EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) é **true**). Uma tentativa de avançar quando a propriedade **EOF** já é **verdadeira** gera um erro.  
  
 No ADO 2,5 e posterior, quando o **conjunto de registros** tiver sido filtrado ou classificado e os dados do registro atual forem alterados, chamar o método **MoveNext** moverá o cursor dois registros para frente do registro atual. Isso ocorre porque, quando o registro atual é alterado, o próximo registro se torna o novo registro atual. Chamar **MoveNext** depois que a alteração move o cursor um registro para frente do novo registro atual. Isso é diferente do comportamento no ADO 2,1 e anterior. Nessas versões anteriores, alterar os dados de um registro atual no **conjunto de registros** classificado ou filtrado não altera a posição do registro atual e **MoveNext** move o cursor para o próximo registro imediatamente após o registro atual.  
  
 Use o método **MovePrevious** para mover a posição do registro atual um registro para trás (em direção à parte superior do **conjunto de registros**). O objeto **Recordset** deve dar suporte a indicadores ou movimento de cursor para trás; caso contrário, a chamada do método gerará um erro. Se o primeiro registro for o registro atual e você chamar o método **MovePrevious** , o ADO definirá o registro atual como a posição anterior ao primeiro registro no **conjunto de registros** ([BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) é **true**). Uma tentativa de retroceder quando a propriedade **BOF** já é **verdadeira** gera um erro. Se o objeto **Recordset** não oferecer suporte a indicadores ou movimento de cursor para trás, o método **MovePrevious** gerará um erro.  
  
 Se o **conjunto de registros** for somente encaminhamento e você quiser dar suporte à rolagem para frente e para trás, você poderá usar a propriedade [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) para criar um cache de registros que dará suporte à movimentação de cursor para trás por meio do método [move](../../../ado/reference/ado-api/move-method-ado.md) . Como os registros armazenados em cache são carregados na memória, você deve evitar armazenar em cache mais registros do que o necessário. Você pode chamar o método **MoveFirst** em um objeto **Recordset** somente de encaminhamento; Isso pode fazer com que o provedor execute novamente o comando que gerou o objeto **Recordset** .  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo dos métodos MoveFirst, MoveLast, MoveNext e MovePrevious (VB)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vb.md)   
 [Exemplo dos métodos MoveFirst, MoveLast, MoveNext e MovePrevious (VBScript)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vbscript.md)   
 [Exemplo dos métodos MoveFirst, MoveLast, MoveNext e MovePrevious (VC + +)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vc.md)   
 [Método Move (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [Métodos MoveFirst, MoveLast, MoveNext e MovePrevious (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)   
 [Método MoveRecord (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)
