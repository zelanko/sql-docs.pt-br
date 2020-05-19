---
title: Eventos ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- events [ADO]
- ADO, events
ms.assetid: 0ded5ad9-8f83-4224-95af-38512783b972
author: rothja
ms.author: jroth
ms.openlocfilehash: e1b69ced6c5d55b3b393ec30247c1a9f35f9fc57
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82747331"
---
# <a name="ado-events"></a>Eventos ADO

|||  
|-|-|  
|[BeginTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|Chamado após a operação **BeginTrans** .|  
|[CommitTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|Chamado após a operação de **CommitTrans** .|  
|[ConnectComplete](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|Chamado depois que uma conexão é iniciada.|  
|[Desligar](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|Chamado após o término de uma conexão.|  
|[EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|Chamado quando há uma tentativa de mover para uma linha após o final do conjunto de **registros**.|  
|[ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md)|Chamado após a conclusão da execução de um comando.|  
|[FetchComplete](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|Chamado depois que todos os registros em uma operação assíncrona demorada tiverem sido recuperados no **conjunto de registros**.|  
|[FetchProgress](../../../ado/reference/ado-api/fetchprogress-event-ado.md)|Chamado periodicamente durante uma operação assíncrona demorada para relatar quantas linhas foram recuperadas no **conjunto de registros**.|  
|[FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|Chamado depois que o valor de um ou mais objetos de **campo** foi alterado.|  
|[InfoMessage](../../../ado/reference/ado-api/infomessage-event-ado.md)|Chamado sempre que ocorrer um aviso durante uma operação de **ConnectionEvent** .|  
|[MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|Chamado depois que a posição atual no **conjunto de registros** é alterada.|  
|[RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|Chamado após a alteração de um ou mais registros.|  
|[RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|Chamado depois que o **conjunto de registros** é alterado.|  
|[RollbackTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|Chamado após a operação **RollbackTrans** .|  
|[WillChangeField](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|Chamado antes de uma operação pendente Alterar o valor de um ou mais objetos de **campo** no **conjunto de registros**.|  
|[WillChangeRecord](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|Chamado antes que um ou mais registros (linhas) no **conjunto de registros** sejam alterados.|  
|[WillChangeRecordset](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|Chamado antes que uma operação pendente altere o **conjunto de registros**.|  
|[WillConnect](../../../ado/reference/ado-api/willconnect-event-ado.md)|Chamado antes de iniciar uma conexão.|  
|[WillExecute](../../../ado/reference/ado-api/willexecute-event-ado.md)|Chamado logo antes de um comando pendente ser executado nessa conexão e dá ao usuário uma oportunidade de examinar e modificar os parâmetros de execução pendentes.|  
|[WillMove](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|O evento **WillMove** é chamado *antes* de uma operação pendente Alterar a posição atual no **conjunto de registros**.|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API do ADO](../../../ado/reference/ado-api/ado-api-reference.md)   
 [Coleções ADO](../../../ado/reference/ado-api/ado-collections.md)   
 [Propriedades dinâmicas do ADO](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [Constantes enumeradas do ADO](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [Apêndice B: erros do ADO](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [Manipulando eventos ADO](../../../ado/guide/data/handling-ado-events.md)   
 [Métodos do ADO](../../../ado/reference/ado-api/ado-methods.md)   
 [Modelo de objeto ADO](../../../ado/reference/ado-api/ado-object-model.md)   
 [Objetos e interfaces do ADO](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [Propriedades ADO](../../../ado/reference/ado-api/ado-properties.md)
