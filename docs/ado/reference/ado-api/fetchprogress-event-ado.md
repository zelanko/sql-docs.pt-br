---
title: Evento FetchProgress (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FetchProgress
- Recordset::FetchProgress
helpviewer_keywords:
- FetchProgress event [ADO]
ms.assetid: 301716fd-81fc-40eb-8a04-221ef7ab410e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f47fb473d0120c124fd07fbb0b30bdecf991926f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63258972"
---
# <a name="fetchprogress-event-ado"></a>Evento FetchProgress (ADO)
O **FetchProgress**evento é chamado periodicamente durante uma operação assíncrona demorada para relatar o número de linhas mais atualmente foram recuperado na [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
FetchProgress Progress, MaxProgress, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Andamento*  
 Um **longo** valor que indica o número de registros que foram recuperados pela operação de busca no momento.  
  
 *MaxProgress*  
 Um **longo** esperado do valor que indica o número máximo de registros a serem recuperados.  
  
 *adStatus*  
 Uma [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valor de status.  
  
 *pRecordset*  
 Um **Recordset** objeto que é o objeto para o qual os registros estão sendo recuperados.  
  
## <a name="remarks"></a>Comentários  
 Ao usar **FetchProgress** com um filho **conjunto de registros**, lembre-se que o *progresso* e *MaxProgress* valores de parâmetro são derivados de subjacente [Cursor Service](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) conjunto de linhas. Os valores retornados representam o número total de registros no conjunto de linhas subjacente, não apenas o número de registros no capítulo atual.  
  
> [!NOTE]
>  Para usar **FetchProgress** com o Microsoft Visual Basic, Visual Basic 6.0 ou posterior é necessário.  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de modelo de eventos ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Resumo do manipulador de eventos ADO](../../../ado/guide/data/ado-event-handler-summary.md)
