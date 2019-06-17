---
title: Evento InfoMessage (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection::InfoMessage
- InfoMessage
helpviewer_keywords:
- InfoMessage event [ADO]
ms.assetid: 468c87dd-e3bc-4084-9941-94d10743d4e9
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: edc451ae2075a22c106f4e2395836e7d508a7808
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66694791"
---
# <a name="infomessage-event-ado"></a>Evento InfoMessage (ADO)
O **InfoMessage** eventos é chamado sempre que ocorrer um aviso durante uma **ConnectionEvent** operação.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
InfoMessage pError, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *pError*  
 Uma [erro](../../../ado/reference/ado-api/error-object.md) objeto. Este parâmetro conterá todos os erros que são retornados. Se vários erros forem retornados, enumerar os **erros** coleção encontrá-los.  
  
 *adStatus*  
 Uma [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valor de status. Se ocorrer um aviso, *adStatus* é definido como **adStatusOK** e o *pError* contém o aviso.  
  
 Antes de retorna a este evento, defina esse parâmetro como **adStatusUnwantedEvent** para evitar notificações subsequentes.  
  
 *pConnection*  
 Um [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto. A conexão para a qual o aviso ocorreu. Por exemplo, os avisos podem ocorrer ao abrir um **Conexão** objeto ou à execução de uma [comando](../../../ado/reference/ado-api/command-object-ado.md) em um **Conexão**.  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de modelo de eventos ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Resumo do manipulador de eventos ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
