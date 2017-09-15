---
title: Evento ExecuteComplete (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Connection::ExecuteComplete
- ExecuteComplete
helpviewer_keywords:
- ExecuteComplete event [ADO]
ms.assetid: 62470d42-e511-494c-bec4-ad4591734b7b
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e612e83e3c550c429b9ebcfe63c0641b61390b95
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="executecomplete-event-ado"></a>Evento ExecuteComplete (ADO)
O **ExecuteComplete** eventos é chamado depois que um comando tiver concluído a execução.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ExecuteComplete RecordsAffected, pError, adStatus, pCommand, pRecordset, pConnection  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *RecordsAffected*  
 Um **longo** valor que indica o número de registros afetados pelo comando.  
  
 *pError*  
 Um [erro](../../../ado/reference/ado-api/error-object.md) objeto. Descreve o erro ocorrido se o valor de **adStatus** é **adStatusErrorsOccurred**; caso contrário, ele não está definido.  
  
 *adStatus*  
 Um [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valor de status. Quando esse evento é chamado, esse parâmetro é definido como **adStatusOK** se a operação que causou o evento foi bem-sucedida, ou para **adStatusErrorsOccurred** se a operação falhou.  
  
 Antes desse evento retorna, defina este parâmetro como **adStatusUnwantedEvent** para impedir que as notificações subsequentes.  
  
 *pCommand*  
 O [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto que foi executado. Contém uma **comando** objeto mesmo ao chamar **Connection.Execute** ou **Recordset.Open** sem criar explicitamente uma **comando** , em quais casos o **comando** objeto é criado internamente pelo ADO.  
  
 *pRecordset*  
 Um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto que é o resultado do comando executado. Isso **registros** pode estar vazia. Você nunca deve destruir este objeto de conjunto de registros de dentro deste manipulador de eventos. Isso resulta em uma violação de acesso quando ADO tenta acessar um objeto que não existe mais.  
  
 *pConnection*  
 Um [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto. A conexão através da qual a operação foi executada.  
  
## <a name="remarks"></a>Comentários  
 Um **ExecuteComplete** evento pode ocorrer devido ao **Conexão.** [Executar](../../../ado/reference/ado-api/execute-method-ado-connection.md), **comando.** [Executar](../../../ado/reference/ado-api/execute-method-ado-command.md), **Recordset.** [Abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md), **Recordset.** [Requery](../../../ado/reference/ado-api/requery-method.md), ou **Recordset.** [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md) métodos.  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de modelo de eventos do ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Resumo do manipulador de eventos ADO](../../../ado/guide/data/ado-event-handler-summary.md)
