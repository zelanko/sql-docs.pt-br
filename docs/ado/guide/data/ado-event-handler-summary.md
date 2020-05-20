---
title: Resumo do manipulador de eventos do ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- events [ADO], about event handlers
- event handlers [ADO]
ms.assetid: b34f4472-5e04-4a2c-ab64-38d6eca31a69
author: rothja
ms.author: jroth
ms.openlocfilehash: 78c3b19c63025bc77862e7f88f6c4d83350c0313
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761362"
---
# <a name="ado-connection-and-recordset-events"></a>Eventos de conexão e conjunto de registros ADO
Dois objetos ADO podem gerar eventos: o objeto de [conexão](../../../ado/reference/ado-api/connection-object-ado.md) e o objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) . A família **ConnectionEvent** pertence a operações no objeto de **conexão** , e a família **RecordsetEvent** pertence a operações no objeto **Recordset** .

-   **Eventos de conexão**: os eventos são emitidos quando uma transação em uma conexão é iniciada, é confirmada ou revertida; Quando um [comando](../../../ado/reference/ado-api/command-object-ado.md) é executado; Quando ocorre um aviso durante uma operação de **evento de conexão** ; ou quando uma **conexão** inicia ou termina.

-   **Eventos do conjunto de registros**: os eventos são emitidos em oposição a operações de busca assíncrona, bem como quando você navega pelas linhas de um objeto **Recordset** , altera um campo em uma linha de um **conjunto de registros**, altera uma linha em um **conjunto**de registros, abre um **conjunto de registros** com um cursor do lado do servidor, fecha um **conjunto**de registros ou faz qualquer alteração no **conjunto de registros**

 As tabelas a seguir resumem os eventos e suas descrições.

|ConnectionEvent|Descrição|
|---------------------|-----------------|
|[BeginTransComplete, CommitTransComplete, RollbackTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|**Gerenciamento de transações** -notificação de que a transação atual na conexão foi iniciada, confirmada ou revertida.|
|[WillConnect](../../../ado/reference/ado-api/willconnect-event-ado.md), [ConnectComplete, desconectar](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|**Gerenciamento de conexão** -notificação de que a conexão atual iniciará, foi iniciada ou terminou.|
|[WillExecute](../../../ado/reference/ado-api/willexecute-event-ado.md), [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md)|**Gerenciamento de execução de comando** -notificação de que a execução do comando atual na conexão será iniciada ou finalizada.|
|[InfoMessage](../../../ado/reference/ado-api/infomessage-event-ado.md)|**Informativo** -notificação de que há informações adicionais sobre a operação atual.|

|RecordsetEvent|Descrição|
|--------------------|-----------------|
|[FetchProgress](../../../ado/reference/ado-api/fetchprogress-event-ado.md), [FetchComplete](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|**Status de recuperação** -notificação do progresso de uma operação de recuperação de dados ou que a operação de recuperação foi concluída. Esses eventos só estarão disponíveis se o **conjunto de registros** tiver sido aberto usando um cursor do lado do cliente.|
|[WillChangeField, FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|**Gerenciamento de alterações de campo** -notificação de que o valor do campo atual será alterado ou alterado.|
|[WillMove, MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md), [EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|**Gerenciamento de navegação** -notificação de que a posição da linha atual em um **conjunto de registros** será alterada, foi alterada ou atingiu o final do **conjunto de registros**.|
|[WillChangeRecord, RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|**Gerenciamento de alterações de linha** -notificação de que algo na linha atual do **conjunto de registros** será alterado ou alterado.|
|[WillChangeRecordset, RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|**Gerenciamento de alterações do conjunto de registros** -notificação de que algo no **conjunto de registros** atual será alterado ou alterado.|

## <a name="see-also"></a>Consulte Também
 [Parâmetros de evento](../../../ado/guide/data/event-parameters.md) [de instanciação do evento ADO por linguagem](../../../ado/guide/data/ado-event-instantiation-by-language.md) [ADO Events](../../../ado/reference/ado-api/ado-events.md) [como manipuladores de eventos trabalham em conjunto](../../../ado/guide/data/how-event-handlers-work-together.md) com [tipos de eventos](../../../ado/guide/data/types-of-events.md)
