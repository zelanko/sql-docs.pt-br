---
title: MoveFirst, MoveLast, MoveNext e MovePrevious métodos (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 5803eb0c9c10c0bb4e62cc32b0f341b7ba06c32f
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="movefirst-movelast-movenext-and-moveprevious-methods-ado"></a>MoveFirst, MoveLast, MoveNext e MovePrevious métodos (ADO)
Move para a primeira, última, registro anterior ou seguinte em um especificado [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto e torna esse registro o registro atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
recordset.{MoveFirst | MoveLast | MoveNext | MovePrevious}  
```  
  
## <a name="remarks"></a>Remarks  
 Use o **MoveFirst** método para mover a posição do registro atual para o primeiro registro o **registros**.  
  
 Use o **MoveLast** método para mover a posição do registro atual para o último registro no **registros**. O **registros** objeto deve dar suporte a indicadores ou movimento do cursor com versões anteriores; caso contrário, a chamada do método gerará um erro.  
  
 Uma chamada para a **MoveFirst** ou **MoveLast** quando o **registros** está vazia (ambos **BOF** e **EOF** são True) gera um erro.  
  
 Use o **MoveNext** método para mover o registro atual posicionar um registro para a frente (na parte inferior do **registros**). Se o último registro é o registro atual e você chamar o **MoveNext** método ADO define o registro atual para a posição após o último registro de **conjunto de registros** ([EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) é **True**). Tentativa de mover quando encaminhar o **EOF** propriedade já está **True** gera um erro.  
  
 No ADO 2.5 e superior, quando o **registros** foram filtrados ou classificados e os dados do registro atual são alterados, chamando o **MoveNext** método move os cursor dois registros na frente registro atual . Isso ocorre porque quando o registro atual é alterado, o próximo registro se torna o novo registro atual. Chamando **MoveNext** após a alteração move o cursor um registro para a frente do novo registro atual. Isso é diferente do comportamento no ADO 2.1 e anteriores. Nessas versões anteriores, alterando os dados de um registro atual no classificados ou filtrados **registros** não altera a posição do registro atual, e **MoveNext** move o cursor para o próximo registro imediatamente após o registro atual.  
  
 Use o **MovePrevious** método para mover o registro atual posicionar um registro com versões anteriores (na parte superior do **registros**). O **registros** objeto deve dar suporte a indicadores ou movimento do cursor com versões anteriores; caso contrário, a chamada do método gerará um erro. Se o primeiro registro é o registro atual e você chamar o **MovePrevious** método, o ADO define o registro atual para a posição antes do primeiro registro no **registros** ([BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)é **True**). Tentativa de mover para trás quando o **BOF** propriedade já está **True** gera um erro. Se o **registros** objeto não oferece suporte a indicadores ou movimento do cursor com versões anteriores, o **MovePrevious** método gerará um erro.  
  
 Se o **registros** é encaminhar apenas e você deseja dar suporte a rolagem para frente e para trás, você pode usar o [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) propriedade para criar um cache de registro que oferecerá suporte ao movimento do cursor com versões anteriores por meio de [mover](../../../ado/reference/ado-api/move-method-ado.md) método. Porque os registros armazenados em cache são carregados na memória, você deve evitar cache mais registros do que é necessário. Você pode chamar o **MoveFirst** método em um e somente de encaminhamento **registros** objeto; fazer isso pode provocar o provedor executar novamente o comando que gerou o **registros** objeto .  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [MoveFirst, MoveLast, MoveNext e MovePrevious métodos exemplo (VB)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vb.md)   
 [MoveFirst, MoveLast, MoveNext e MovePrevious métodos exemplo (VBScript)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vbscript.md)   
 [MoveFirst, MoveLast, MoveNext e MovePrevious métodos exemplo (VC + +)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vc.md)   
 [Método Move (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [MoveFirst, MoveLast, MoveNext e MovePrevious métodos (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)   
 [Método MoveRecord (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)
