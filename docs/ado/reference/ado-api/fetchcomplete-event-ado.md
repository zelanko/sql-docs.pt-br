---
description: Evento FetchComplete (ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: a4fd58f7783b8fdf2b98d8e295bbf96137cfa5ff
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443818"
---
# <a name="fetchcomplete-event-ado"></a>Evento FetchComplete (ADO)
O evento **FetchComplete** é chamado depois que todos os registros em uma operação assíncrona demorada tiverem sido recuperados no [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
FetchComplete pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *pError*  
 Um objeto de [erro](../../../ado/reference/ado-api/error-object.md) . Ele descreve o erro que ocorreu se o valor de **adStatus** for **adStatusErrorsOccurred**; caso contrário, ele não será definido.  
  
 *adStatus*  
 Um valor de status de [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) . Quando esse evento for chamado, esse parâmetro será definido como **adStatusOK** se a operação que causou o êxito do evento ou **adStatusErrorsOccurred** se a operação falhou.  
  
 Antes desse evento retornar, defina esse parâmetro como **adStatusUnwantedEvent** para evitar notificações subsequentes.  
  
 *pRecordset*  
 Um objeto **Recordset** . O objeto para o qual os registros foram recuperados.  
  
## <a name="remarks"></a>Comentários  
 Para usar o **FetchComplete** com o Microsoft Visual Basic, é necessário ter o Visual Basic 6,0 ou posterior.  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do modelo de eventos ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Resumo do manipulador de eventos ADO](../../../ado/guide/data/ado-event-handler-summary.md)
