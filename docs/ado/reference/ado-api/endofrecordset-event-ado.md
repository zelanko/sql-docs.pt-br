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
ms.openlocfilehash: 0a83f101d46a94a4ea43a85424677fc1c8da08be
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67918946"
---
# <a name="endofrecordset-event-ado"></a>EndOfRecordset Event (ADO)
O evento **EndOfRecordset** é chamado quando há uma tentativa de mover para uma linha após o final do conjunto de [registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
EndOfRecordset fMoreData, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *fMoreData*  
 Um valor **VARIANT_BOOL** que, se definido como VARIANT_TRUE, indica que mais linhas foram adicionadas ao **conjunto de registros**.  
  
 *adStatus*  
 Um valor de status de [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) .  
  
 Quando **EndOfRecordset** for chamado, esse parâmetro será definido como **adStatusOK** se a operação que causou o evento tiver sido bem-sucedida. Ele será definido como **adStatusCantDeny** se esse evento não puder solicitar o cancelamento da operação que causou esse evento.  
  
 Antes de **EndOfRecordset** retornar, defina esse parâmetro como **adStatusUnwantedEvent** para evitar notificações subsequentes.  
  
 *pRecordset*  
 Um objeto **Recordset** . O **conjunto de registros** para o qual esse evento ocorreu.  
  
## <a name="remarks"></a>Comentários  
 Um evento **EndOfRecordset** pode ocorrer se a operação [MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) falhar.  
  
 Esse manipulador de eventos é chamado quando é feita uma tentativa de mover após o final do objeto **Recordset** , talvez como resultado da chamada a **MoveNext**. No entanto, embora, nesse caso, você possa recuperar mais registros de um banco de dados e acrescentá-los ao final do **conjunto de registros**. Nesse caso, defina *fMoreData* como VARIANT_TRUE e retorne de **EndOfRecordset**. Em seguida, chame **MoveNext** novamente para acessar os registros recuperados recentemente.  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do modelo de eventos ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Resumo do manipulador de eventos ADO](../../../ado/guide/data/ado-event-handler-summary.md)
