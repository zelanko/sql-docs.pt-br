---
title: Evento EndOfRecordset (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- EndOfRecordset
- Recordset::EndOfRecordset
helpviewer_keywords: EndOfRecordset event [ADO]
ms.assetid: 475de5e2-f634-4954-9edf-0027a6ba38d6
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c9bedfab5204ec93f5f3de8e0f574640e2b04429
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="endofrecordset-event-ado"></a>Evento EndOfRecordset (ADO)
O **EndOfRecordset** evento é chamado quando há uma tentativa de mover para uma linha após o término do [registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
EndOfRecordset fMoreData, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *fMoreData*  
 Um **VARIANT_BOOL** valor que, se definido como VARIANT_TRUE, indica que mais linhas foram adicionadas para o **registros**.  
  
 *adStatus*  
 Um [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valor de status.  
  
 Quando **EndOfRecordset** é chamado, esse parâmetro é definido como **adStatusOK** se a operação que causou o evento foi bem-sucedida. Ele é definido como **adStatusCantDeny** se esse evento não é possível solicitar o cancelamento da operação que causou este evento.  
  
 Antes de **EndOfRecordset** retorna, defina este parâmetro como **adStatusUnwantedEvent** para impedir que as notificações subsequentes.  
  
 *pRecordset*  
 Um **registros** objeto. O **registros** para que esse evento ocorreu.  
  
## <a name="remarks"></a>Remarks  
 Um **EndOfRecordset** evento pode ocorrer se o [MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) Falha na operação.  
  
 Este manipulador de eventos é chamado quando é feita uma tentativa de mover após o término do **registros** objeto, talvez como resultado da chamada **MoveNext**. No entanto, enquanto esse evento, você pode recuperar mais registros de um banco de dados e anexá-la ao final do **registros**. Nesse caso, defina *fMoreData* VARIANT_TRUE e o retorno de **EndOfRecordset**. Em seguida, chame **MoveNext** novamente para acessar os registros recuperados recentemente.  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de modelo de eventos do ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Resumo do manipulador de eventos ADO](../../../ado/guide/data/ado-event-handler-summary.md)
