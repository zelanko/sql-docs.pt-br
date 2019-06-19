---
title: Evento ExecuteComplete (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection::ExecuteComplete
- ExecuteComplete
helpviewer_keywords:
- ExecuteComplete event [ADO]
ms.assetid: 62470d42-e511-494c-bec4-ad4591734b7b
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: df6437e80ab746a7d6aa219fb3299cb54712b5c3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66697909"
---
# <a name="executecomplete-event-ado"></a>Evento ExecuteComplete (ADO)
O **ExecuteComplete** evento é chamado depois que um comando tiver concluído a execução.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ExecuteComplete RecordsAffected, pError, adStatus, pCommand, pRecordset, pConnection  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *RecordsAffected*  
 Um **longo** valor que indica o número de registros afetados pelo comando.  
  
 *pError*  
 Uma [erro](../../../ado/reference/ado-api/error-object.md) objeto. Ele descreve o erro ocorrido se o valor de **adStatus** é **adStatusErrorsOccurred**; caso contrário, ele não está definido.  
  
 *adStatus*  
 Uma [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valor de status. Quando esse evento é chamado, esse parâmetro é definido como **adStatusOK** se a operação que causou o evento foi bem-sucedida, ou para **adStatusErrorsOccurred** se a operação falhou.  
  
 Antes de retorna a este evento, defina esse parâmetro como **adStatusUnwantedEvent** para evitar notificações subsequentes.  
  
 *pCommand*  
 O [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto que foi executado. Contém uma **comando** do objeto, mesmo quando chamar **Connection.Execute** ou **Recordset.Open** sem criar explicitamente uma **comando** , em quais casos os **comando** objeto é criado internamente pelo ADO.  
  
 *pRecordset*  
 Um [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto que é o resultado do comando executado. Isso **Recordset** pode estar vazia. Você nunca deve destruir a este objeto de conjunto de registros de dentro do manipulador de eventos. Ao fazer isso resultará em uma violação de acesso ao ADO tenta acessar um objeto que não existe mais.  
  
 *pConnection*  
 Um [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto. A conexão na qual a operação foi executada.  
  
## <a name="remarks"></a>Comentários  
 Uma **ExecuteComplete** evento pode ocorrer devido ao **Conexão.** [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md), **comando.** [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md), **conjunto de registros.** [Aberto](../../../ado/reference/ado-api/open-method-ado-recordset.md), **conjunto de registros.** [Requery](../../../ado/reference/ado-api/requery-method.md), ou **conjunto de registros.** [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md) métodos.  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de modelo de eventos ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Resumo do manipulador de eventos ADO](../../../ado/guide/data/ado-event-handler-summary.md)
