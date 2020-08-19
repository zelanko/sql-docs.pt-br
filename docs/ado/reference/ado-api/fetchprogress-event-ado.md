---
description: Evento FetchProgress (ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 53f22936f17e70c02a7640355250cdb5f2bcea95
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443808"
---
# <a name="fetchprogress-event-ado"></a>Evento FetchProgress (ADO)
O evento **FetchProgress**é chamado periodicamente durante uma operação assíncrona demorada para relatar quantas linhas foram recuperadas no [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
FetchProgress Progress, MaxProgress, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Progresso*  
 Um valor **longo** que indica o número de registros que foram recuperados pela operação de busca no momento.  
  
 *MaxProgress*  
 Um valor **longo** que indica o número máximo de registros esperados a serem recuperados.  
  
 *adStatus*  
 Um valor de status de [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) .  
  
 *pRecordset*  
 Um objeto **Recordset** que é o objeto para o qual os registros estão sendo recuperados.  
  
## <a name="remarks"></a>Comentários  
 Ao usar **FetchProgress** com um **conjunto de registros**filho, lembre-se de que os valores de parâmetro *Progress* e *MaxProgress* são derivados do conjunto de linhas de [serviço de cursor](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) subjacente. Os valores retornados representam o número total de registros no conjunto de linhas subjacente, não apenas o número de registros no capítulo atual.  
  
> [!NOTE]
>  Para usar o **FetchProgress** com o Microsoft Visual Basic, é necessário ter o Visual Basic 6,0 ou posterior.  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do modelo de eventos ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Resumo do manipulador de eventos ADO](../../../ado/guide/data/ado-event-handler-summary.md)
