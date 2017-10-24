---
title: Eventos de ADO | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- events [ADO]
- ADO, events
ms.assetid: 0ded5ad9-8f83-4224-95af-38512783b972
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 59492bb63fd11aa1c60b3c45daed5a7431475cd9
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="ado-events"></a>Eventos de ADO
|||  
|-|-|  
|[BeginTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|Chamado após o **BeginTrans** operação.|  
|[CommitTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|Chamado após o **CommitTrans** operação.|  
|[ConnectComplete](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|Chamado após o início de uma conexão.|  
|[Desconectar](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|Chamado após o término de uma conexão.|  
|[EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|Chamado quando há uma tentativa de mover para uma linha após o término do **registros**.|  
|[ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md)|Chamado depois que um comando tiver concluído a execução.|  
|[FetchComplete](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|Chamado depois que todos os registros em uma operação assíncrona demorada foram recuperados para o **registros**.|  
|[FetchProgress](../../../ado/reference/ado-api/fetchprogress-event-ado.md)|Chamado periodicamente durante uma operação demorada assíncrona para informar quantas linhas foram recuperadas no momento no **registros**.|  
|[FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|Chamado após o valor de um ou mais **campo** objetos foi alterado.|  
|[InfoMessage](../../../ado/reference/ado-api/infomessage-event-ado.md)|Chamado sempre que ocorrer um aviso durante uma **ConnectionEvent** operação.|  
|[MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|Chamado após a posição atual no **registros** alterações.|  
|[RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|Chamado após alterar um ou mais registros.|  
|[RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|Chamado após o **registros** foi alterado.|  
|[RollbackTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|Chamado após o **RollbackTrans** operação.|  
|[WillChangeField](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|Chamado antes de uma operação pendente altera o valor de uma ou mais **campo** objetos no **registros**.|  
|[WillChangeRecord](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|Chamado antes de um ou mais registros (linhas) no **registros** alterar.|  
|[WillChangeRecordset](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|Chamado antes de uma operação pendente altera o **registros**.|  
|[WillConnect](../../../ado/reference/ado-api/willconnect-event-ado.md)|Chamado antes do início de uma conexão.|  
|[WillExecute](../../../ado/reference/ado-api/willexecute-event-ado.md)|Chamado logo antes de um comando pendente executa nessa conexão e dá ao usuário uma oportunidade para examinar e modificar os parâmetros de execução pendente.|  
|[WillMove](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|O **WillMove** é chamado de evento *antes de* uma operação pendente altera a posição atual no **registros**.|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ADO](../../../ado/reference/ado-api/ado-api-reference.md)   
 [Coleções de ADO](../../../ado/reference/ado-api/ado-collections.md)   
 [Propriedades dinâmicas do ADO](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [Constantes enumeradas do ADO](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [Apêndice b: erros de ADO](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [Manipulação de eventos de ADO](../../../ado/guide/data/handling-ado-events.md)   
 [Métodos de ADO](../../../ado/reference/ado-api/ado-methods.md)   
 [Modelo de objeto ADO](../../../ado/reference/ado-api/ado-object-model.md)   
 [Interfaces e ADO](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [Propriedades ADO](../../../ado/reference/ado-api/ado-properties.md)

