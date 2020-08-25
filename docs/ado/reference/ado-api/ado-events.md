---
description: Eventos ADO
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
ms.openlocfilehash: 4644596d216bd459b19778607e309cb7713d6fc4
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776655"
---
# <a name="ado-events"></a>Eventos ADO

|Evento|Descrição|  
|-|-|  
|[BeginTransComplete](./begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|Chamado após a operação **BeginTrans** .|  
|[CommitTransComplete](./begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|Chamado após a operação de **CommitTrans** .|  
|[ConnectComplete](./connectcomplete-and-disconnect-events-ado.md)|Chamado depois que uma conexão é iniciada.|  
|[Desligar](./connectcomplete-and-disconnect-events-ado.md)|Chamado após o término de uma conexão.|  
|[EndOfRecordset](./endofrecordset-event-ado.md)|Chamado quando há uma tentativa de mover para uma linha após o final do conjunto de **registros**.|  
|[ExecuteComplete](./executecomplete-event-ado.md)|Chamado após a conclusão da execução de um comando.|  
|[FetchComplete](./fetchcomplete-event-ado.md)|Chamado depois que todos os registros em uma operação assíncrona demorada tiverem sido recuperados no **conjunto de registros**.|  
|[FetchProgress](./fetchprogress-event-ado.md)|Chamado periodicamente durante uma operação assíncrona demorada para relatar quantas linhas foram recuperadas no **conjunto de registros**.|  
|[FieldChangeComplete](./willchangefield-and-fieldchangecomplete-events-ado.md)|Chamado depois que o valor de um ou mais objetos de **campo** foi alterado.|  
|[InfoMessage](./infomessage-event-ado.md)|Chamado sempre que ocorrer um aviso durante uma operação de **ConnectionEvent** .|  
|[MoveComplete](./willmove-and-movecomplete-events-ado.md)|Chamado depois que a posição atual no **conjunto de registros** é alterada.|  
|[RecordChangeComplete](./willchangerecord-and-recordchangecomplete-events-ado.md)|Chamado após a alteração de um ou mais registros.|  
|[RecordsetChangeComplete](./willchangerecordset-and-recordsetchangecomplete-events-ado.md)|Chamado depois que o **conjunto de registros** é alterado.|  
|[RollbackTransComplete](./begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|Chamado após a operação **RollbackTrans** .|  
|[WillChangeField](./willchangefield-and-fieldchangecomplete-events-ado.md)|Chamado antes de uma operação pendente Alterar o valor de um ou mais objetos de **campo** no **conjunto de registros**.|  
|[WillChangeRecord](./willchangerecord-and-recordchangecomplete-events-ado.md)|Chamado antes que um ou mais registros (linhas) no **conjunto de registros** sejam alterados.|  
|[WillChangeRecordset](./willchangerecordset-and-recordsetchangecomplete-events-ado.md)|Chamado antes que uma operação pendente altere o **conjunto de registros**.|  
|[WillConnect](./willconnect-event-ado.md)|Chamado antes de iniciar uma conexão.|  
|[WillExecute](./willexecute-event-ado.md)|Chamado logo antes de um comando pendente ser executado nessa conexão e dá ao usuário uma oportunidade de examinar e modificar os parâmetros de execução pendentes.|  
|[WillMove](./willmove-and-movecomplete-events-ado.md)|O evento **WillMove** é chamado *antes* de uma operação pendente Alterar a posição atual no **conjunto de registros**.|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API do ADO](./ado-api-reference.md)   
 [Coleções ADO](./ado-collections.md)   
 [Propriedades dinâmicas do ADO](./ado-dynamic-properties.md)   
 [Constantes enumeradas do ADO](./ado-enumerated-constants.md)   
 [Apêndice B: erros do ADO](../../guide/appendixes/appendix-b-ado-errors.md)   
 [Manipulando eventos ADO](../../guide/data/handling-ado-events.md)   
 [Métodos do ADO](./ado-methods.md)   
 [Modelo de objeto ADO](./ado-object-model.md)   
 [Objetos e interfaces do ADO](./ado-objects-and-interfaces.md)   
 [Propriedades ADO](./ado-properties.md)