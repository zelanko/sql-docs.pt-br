---
title: Evento FetchComplete (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset::ExecuteComplete
- ExecuteComplete
helpviewer_keywords:
- FetchComplete event [ADO]
ms.assetid: a28d3858-566c-468d-b070-d1de4339fbea
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a8332a6332f27a8e2022975a80814be9c28cf4da
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="fetchcomplete-event-ado"></a>Evento FetchComplete (ADO)
O **FetchComplete** eventos é chamado depois que todos os registros em uma operação assíncrona demorada foram recuperados para o [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
FetchComplete pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *pError*  
 Um [erro](../../../ado/reference/ado-api/error-object.md) objeto. Descreve o erro ocorrido se o valor de **adStatus** é **adStatusErrorsOccurred**; caso contrário, ele não está definido.  
  
 *adStatus*  
 Um [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valor de status. Quando esse evento é chamado, esse parâmetro é definido como **adStatusOK** se a operação que causou o evento foi bem-sucedida, ou para **adStatusErrorsOccurred** se a operação falhou.  
  
 Antes desse evento retorna, defina este parâmetro como **adStatusUnwantedEvent** para impedir que as notificações subsequentes.  
  
 *pRecordset*  
 Um **registros** objeto. O objeto para o qual os registros foram recuperados.  
  
## <a name="remarks"></a>Remarks  
 Para usar **FetchComplete** com o Microsoft Visual Basic, Visual Basic 6.0 ou posterior é necessário.  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de modelo de eventos do ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Resumo do manipulador de eventos ADO](../../../ado/guide/data/ado-event-handler-summary.md)
