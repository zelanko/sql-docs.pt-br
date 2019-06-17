---
title: EndOfRecordset Event (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- EndOfRecordset
- Recordset::EndOfRecordset
helpviewer_keywords:
- EndOfRecordset event [ADO]
ms.assetid: 475de5e2-f634-4954-9edf-0027a6ba38d6
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 414094da95076a7fb3781877645c5d43a03e6a7f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66698214"
---
# <a name="endofrecordset-event-ado"></a>EndOfRecordset Event (ADO)
O **EndOfRecordset** evento é chamado quando há uma tentativa de mover para uma linha após o término da [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
EndOfRecordset fMoreData, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *fMoreData*  
 Um **VARIANT_BOOL** valor que, se definido como VARIANT_TRUE, indica que mais linhas foram adicionadas para o **conjunto de registros**.  
  
 *adStatus*  
 Uma [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valor de status.  
  
 Quando **EndOfRecordset** é chamado, esse parâmetro é definido como **adStatusOK** se a operação que causou o evento foi bem-sucedida. Ele é definido como **adStatusCantDeny** se esse evento não é possível solicitar o cancelamento da operação que causou este evento.  
  
 Antes de **EndOfRecordset** retorna, defina esse parâmetro como **adStatusUnwantedEvent** para evitar notificações subsequentes.  
  
 *pRecordset*  
 Um **Recordset** objeto. O **Recordset** para que esse evento ocorreu.  
  
## <a name="remarks"></a>Comentários  
 Uma **EndOfRecordset** evento pode ocorrer se o [MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) operação falhará.  
  
 Esse manipulador de eventos é chamado quando é feita uma tentativa de mover após o término do **conjunto de registros** objeto, talvez como resultado da chamada **MoveNext**. No entanto, enquanto esse evento, você pode recuperar registros de mais de um banco de dados e acrescentá-los ao final dos **conjunto de registros**. Nesse caso, defina *fMoreData* VARIANT_TRUE e o retorno da **EndOfRecordset**. Em seguida, chame **MoveNext** novamente para acessar os registros recuperados recentemente.  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de modelo de eventos ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Resumo do manipulador de eventos ADO](../../../ado/guide/data/ado-event-handler-summary.md)
