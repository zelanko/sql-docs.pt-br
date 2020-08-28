---
description: Eventos de conexão e conjunto de registros ADO
title: Resumo do manipulador de eventos do ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: ddec7c573c7d208d80fe05dc8f15ba2d0d02c428
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991717"
---
# <a name="ado-connection-and-recordset-events"></a>Eventos de conexão e conjunto de registros ADO
Dois objetos ADO podem gerar eventos: o objeto de [conexão](../../reference/ado-api/connection-object-ado.md) e o objeto [Recordset](../../reference/ado-api/recordset-object-ado.md) . A família **ConnectionEvent** pertence a operações no objeto de **conexão** , e a família **RecordsetEvent** pertence a operações no objeto **Recordset** .

-   **Eventos de conexão**: os eventos são emitidos quando uma transação em uma conexão é iniciada, é confirmada ou revertida; Quando um [comando](../../reference/ado-api/command-object-ado.md) é executado; Quando ocorre um aviso durante uma operação de **evento de conexão** ; ou quando uma **conexão** inicia ou termina.

-   **Eventos do conjunto de registros**: os eventos são emitidos em oposição a operações de busca assíncrona, bem como quando você navega pelas linhas de um objeto **Recordset** , altera um campo em uma linha de um **conjunto de registros**, altera uma linha em um **conjunto**de registros, abre um **conjunto de registros** com um cursor do lado do servidor, fecha um **conjunto**de registros ou faz qualquer alteração no **conjunto de registros**

 As tabelas a seguir resumem os eventos e suas descrições.

|ConnectionEvent|Descrição|
|---------------------|-----------------|
|[BeginTransComplete, CommitTransComplete, RollbackTransComplete](../../reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|**Gerenciamento de transações** -notificação de que a transação atual na conexão foi iniciada, confirmada ou revertida.|
|[WillConnect](../../reference/ado-api/willconnect-event-ado.md), [ConnectComplete, desconectar](../../reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|**Gerenciamento de conexão** -notificação de que a conexão atual iniciará, foi iniciada ou terminou.|
|[WillExecute](../../reference/ado-api/willexecute-event-ado.md), [ExecuteComplete](../../reference/ado-api/executecomplete-event-ado.md)|**Gerenciamento de execução de comando** -notificação de que a execução do comando atual na conexão será iniciada ou finalizada.|
|[InfoMessage](../../reference/ado-api/infomessage-event-ado.md)|**Informativo** -notificação de que há informações adicionais sobre a operação atual.|

|RecordsetEvent|Descrição|
|--------------------|-----------------|
|[FetchProgress](../../reference/ado-api/fetchprogress-event-ado.md), [FetchComplete](../../reference/ado-api/fetchcomplete-event-ado.md)|**Status de recuperação** -notificação do progresso de uma operação de recuperação de dados ou que a operação de recuperação foi concluída. Esses eventos só estarão disponíveis se o **conjunto de registros** tiver sido aberto usando um cursor do lado do cliente.|
|[WillChangeField, FieldChangeComplete](../../reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|**Gerenciamento de alterações de campo** -notificação de que o valor do campo atual será alterado ou alterado.|
|[WillMove, MoveComplete](../../reference/ado-api/willmove-and-movecomplete-events-ado.md), [EndOfRecordset](../../reference/ado-api/endofrecordset-event-ado.md)|**Gerenciamento de navegação** -notificação de que a posição da linha atual em um **conjunto de registros** será alterada, foi alterada ou atingiu o final do **conjunto de registros**.|
|[WillChangeRecord, RecordChangeComplete](../../reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|**Gerenciamento de alterações de linha** -notificação de que algo na linha atual do **conjunto de registros** será alterado ou alterado.|
|[WillChangeRecordset, RecordsetChangeComplete](../../reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|**Gerenciamento de alterações do conjunto de registros** -notificação de que algo no **conjunto de registros** atual será alterado ou alterado.|

## <a name="see-also"></a>Consulte Também
 [Parâmetros de evento](./event-parameters.md) [de instanciação do evento ADO por linguagem](./ado-event-instantiation-by-language.md) [ADO Events](../../reference/ado-api/ado-events.md) [como manipuladores de eventos trabalham em conjunto](./how-event-handlers-work-together.md) com [tipos de eventos](./types-of-events.md)