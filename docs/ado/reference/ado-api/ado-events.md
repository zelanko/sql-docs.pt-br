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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 35169313ae487514403f62c8e6d1ba2c262cb8a7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67921004"
---
# <a name="ado-events"></a>Eventos ADO

|||  
|-|-|  
|[BeginTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|Chamado após o **BeginTrans** operação.|  
|[CommitTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|Chamado após o **CommitTrans** operação.|  
|[ConnectComplete](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|Chamado depois que uma conexão é iniciado.|  
|[Desconectar](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|Chamado após o término de uma conexão.|  
|[EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|Chamado quando há uma tentativa de mover para uma linha após o término do **conjunto de registros**.|  
|[ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md)|Chamado depois que um comando tiver concluído a execução.|  
|[FetchComplete](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|Chamado depois que todos os registros em uma operação assíncrona demorada foram recuperados para o **conjunto de registros**.|  
|[FetchProgress](../../../ado/reference/ado-api/fetchprogress-event-ado.md)|Chamado periodicamente durante uma operação assíncrona demorada para relatar o número de linhas atualmente foram recuperado na **conjunto de registros**.|  
|[FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|Chamado após o valor de um ou mais **campo** objetos foi alterado.|  
|[InfoMessage](../../../ado/reference/ado-api/infomessage-event-ado.md)|Chamado sempre que ocorrer um aviso durante um **ConnectionEvent** operação.|  
|[MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|Chamado após a posição atual na **Recordset** alterações.|  
|[RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|Chamado após alterar um ou mais registros.|  
|[RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|Chamado após o **Recordset** foi alterado.|  
|[RollbackTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|Chamado após o **RollbackTrans** operação.|  
|[WillChangeField](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|Chamado antes que uma operação pendente altera o valor de um ou mais **campo** objetos na **conjunto de registros**.|  
|[WillChangeRecord](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|Chamado antes de um ou mais registros (linhas) na **Recordset** alterar.|  
|[WillChangeRecordset](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|Chamado antes que uma operação pendente é alterado de **conjunto de registros**.|  
|[WillConnect](../../../ado/reference/ado-api/willconnect-event-ado.md)|Chamado antes do início de uma conexão.|  
|[WillExecute](../../../ado/reference/ado-api/willexecute-event-ado.md)|Chamado pouco antes de um comando pendente executa nessa conexão e permite que o usuário a oportunidade de examinar e modificar os parâmetros de execução pendente.|  
|[WillMove](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|O **eventos WillMove** evento é chamado *antes* uma operação pendente altera a posição atual no **conjunto de registros**.|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ADO](../../../ado/reference/ado-api/ado-api-reference.md)   
 [Coleções ADO](../../../ado/reference/ado-api/ado-collections.md)   
 [Propriedades dinâmicas do ADO](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [Constantes enumeradas do ADO](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [Apêndice b: Erros ADO](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [Manipulando eventos ADO](../../../ado/guide/data/handling-ado-events.md)   
 [Métodos ADO](../../../ado/reference/ado-api/ado-methods.md)   
 [Modelo de objeto ADO](../../../ado/reference/ado-api/ado-object-model.md)   
 [Interfaces e os objetos do ADO](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [Propriedades ADO](../../../ado/reference/ado-api/ado-properties.md)
