---
title: Resumo do manipulador de eventos ADO | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 93790b3df8cb1d78ab2e0988cdc43cbd9af0718c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63063012"
---
# <a name="ado-connection-and-recordset-events"></a>Conexão do ADO e o conjunto de registros eventos
Dois objetos do ADO podem gerar eventos: o [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto e o [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto. O **ConnectionEvent** família pertence às operações na **Conexão** objeto e o **RecordsetEvent** família pertence às operações no  **Conjunto de registros** objeto.

-   **Eventos de Conexão**: Eventos são emitidos quando começa uma transação em uma conexão, é confirmada ou é revertida; Quando um [comando](../../../ado/reference/ado-api/command-object-ado.md) executa; quando ocorrer um aviso durante uma **eventos de Conexão** operação; ou quando um **Conexão** inicia ou termina.

-   **Conjunto de registros eventos**: Eventos são emitidos em torno de operações de busca assíncrono, bem como quando você navega pelas linhas de uma **conjunto de registros** do objeto, altere um campo em uma linha de uma **conjunto de registros**, alterar uma linha em um  **Conjunto de registros**, abra uma **conjunto de registros** com um cursor do lado do servidor, feche uma **conjunto de registros**, ou fazer qualquer alteração nada no **Recordset**.

 As tabelas a seguir resumem os eventos e suas descrições.

|ConnectionEvent|Descrição|
|---------------------|-----------------|
|[BeginTransComplete, CommitTransComplete, RollbackTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|**Gerenciamento de transações** -notificação de que a transação atual na conexão foi iniciada, confirmada ou revertida.|
|[WillConnect](../../../ado/reference/ado-api/willconnect-event-ado.md), [ConnectComplete, Disconnect](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|**Gerenciamento de Conexão** -notificação de que a conexão atual será iniciado, começou ou terminou.|
|[WillExecute](../../../ado/reference/ado-api/willexecute-event-ado.md), [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md)|**Gerenciamento de execução de comando** -notificação de que a execução do comando atual em que a conexão será iniciado ou terminou.|
|[InfoMessage](../../../ado/reference/ado-api/infomessage-event-ado.md)|**Informativo** -notificação de que há informações adicionais sobre a operação atual.|

|RecordsetEvent|Descrição|
|--------------------|-----------------|
|[FetchProgress](../../../ado/reference/ado-api/fetchprogress-event-ado.md), [FetchComplete](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|**Status de recuperação** -notificação do progresso de uma operação de recuperação de dados, ou que a operação de recuperação foi concluída. Esses eventos estão disponíveis apenas se o **Recordset** foi aberto usando um cursor do lado do cliente.|
|[WillChangeField, FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|**Gerenciamento de alterações de campo** -notificação de que o valor do campo atual será alterado ou foi alterada.|
|[WillMove, MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md), [EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|**Gerenciamento de navegação** -notificação de que a linha atual se posicionar em uma **conjunto de registros** mudará, foi alterado ou atingiu o fim da **conjunto de registros**.|
|[WillChangeRecord, RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|**Gerenciamento de alterações de linha** -notificação de que algo na linha atual do **Recordset** será alterado, ou foi alterada.|
|[WillChangeRecordset, RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|**Gerenciamento de alterações do conjunto de registros** -notificação de que algo no atual **Recordset** será alterado, ou foi alterada.|

## <a name="see-also"></a>Consulte também
 [Instanciação de evento ADO por linguagem](../../../ado/guide/data/ado-event-instantiation-by-language.md) [eventos ADO](../../../ado/reference/ado-api/ado-events.md) [parâmetros de evento](../../../ado/guide/data/event-parameters.md) [como manipuladores de eventos funcionam juntos](../../../ado/guide/data/how-event-handlers-work-together.md) [tipos de eventos](../../../ado/guide/data/types-of-events.md)
