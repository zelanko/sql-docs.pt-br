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
author: rothja
ms.author: jroth
ms.openlocfilehash: ae8b426a0e4b95498cb0d4f9a4590c3aaf30196d
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760132"
---
# <a name="executecomplete-event-ado"></a>Evento ExecuteComplete (ADO)
O evento **ExecuteComplete** é chamado após a conclusão da execução de um comando.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ExecuteComplete RecordsAffected, pError, adStatus, pCommand, pRecordset, pConnection  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *RecordsAffected*  
 Um valor **longo** que indica o número de registros afetados pelo comando.  
  
 *pError*  
 Um objeto de [erro](../../../ado/reference/ado-api/error-object.md) . Ele descreve o erro que ocorreu se o valor de **adStatus** for **adStatusErrorsOccurred**; caso contrário, ele não será definido.  
  
 *adStatus*  
 Um valor de status de [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) . Quando esse evento for chamado, esse parâmetro será definido como **adStatusOK** se a operação que causou o êxito do evento ou **adStatusErrorsOccurred** se a operação falhou.  
  
 Antes desse evento retornar, defina esse parâmetro como **adStatusUnwantedEvent** para evitar notificações subsequentes.  
  
 *pCommand*  
 O objeto de [comando](../../../ado/reference/ado-api/command-object-ado.md) que foi executado. Contém um objeto **Command** mesmo ao chamar **Connection. Execute** ou **Recordset. Open** sem criar explicitamente um **comando**, em que casos o objeto **Command** é criado internamente pelo ADO.  
  
 *pRecordset*  
 Um objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) que é o resultado do comando executado. Este **conjunto de registros** pode estar vazio. Você nunca deve destruir este objeto Recordset de dentro deste manipulador de eventos. Isso resultará em uma violação de acesso quando o ADO tentar acessar um objeto que não existe mais.  
  
 *pConnection*  
 Um objeto de [conexão](../../../ado/reference/ado-api/connection-object-ado.md) . A conexão sobre a qual a operação foi executada.  
  
## <a name="remarks"></a>Comentários  
 Um evento **ExecuteComplete** pode ocorrer devido à **conexão.** [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md), **Command.** [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md), **Recordset.** [Abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md), **conjunto de registros.** [Requery](../../../ado/reference/ado-api/requery-method.md)ou **Recordset.** Métodos [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md) .  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do modelo de eventos ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Resumo do manipulador de eventos ADO](../../../ado/guide/data/ado-event-handler-summary.md)
