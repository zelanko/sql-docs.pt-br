---
title: Evento FetchComplete (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset::ExecuteComplete
- ExecuteComplete
helpviewer_keywords:
- FetchComplete event [ADO]
ms.assetid: a28d3858-566c-468d-b070-d1de4339fbea
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f3e5f5ae1c886f8d08d522fac19cee563efbb86c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67932830"
---
# <a name="fetchcomplete-event-ado"></a>Evento FetchComplete (ADO)
O evento **FetchComplete** é chamado depois que todos os registros em uma operação assíncrona demorada tiverem sido recuperados no [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
FetchComplete pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>parâmetros  
 *pError*  
 Um objeto de [erro](../../../ado/reference/ado-api/error-object.md) . Ele descreve o erro que ocorreu se o valor de **adStatus** for **adStatusErrorsOccurred**; caso contrário, ele não será definido.  
  
 *adStatus*  
 Um valor de status de [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) . Quando esse evento for chamado, esse parâmetro será definido como **adStatusOK** se a operação que causou o êxito do evento ou **adStatusErrorsOccurred** se a operação falhou.  
  
 Antes desse evento retornar, defina esse parâmetro como **adStatusUnwantedEvent** para evitar notificações subsequentes.  
  
 *precaboset*  
 Um objeto **Recordset** . O objeto para o qual os registros foram recuperados.  
  
## <a name="remarks"></a>Comentários  
 Para usar o **FetchComplete** com o Microsoft Visual Basic, é necessário ter o Visual Basic 6,0 ou posterior.  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do modelo de eventos ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Resumo do manipulador de eventos ADO](../../../ado/guide/data/ado-event-handler-summary.md)
