---
title: Resumo de manipulador de eventos do ADO | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- events [ADO], about event handlers
- event handlers [ADO]
ms.assetid: b34f4472-5e04-4a2c-ab64-38d6eca31a69
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c00af6ce5dcdff509b04d25bc09a42a6e9e89fd7
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="ado-connection-and-recordset-events"></a>Conexão do ADO e o conjunto de registros eventos
Dois objetos ADO podem gerar eventos: o [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto e o [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto. O **ConnectionEvent** família pertence às operações no **Conexão** objeto e o **RecordsetEvent** família pertence às operações no  **Conjunto de registros** objeto.

-   **Eventos de Conexão**: eventos serão emitidos quando começa uma transação em uma conexão, é confirmada ou é revertida novamente; quando um [comando](../../../ado/reference/ado-api/command-object-ado.md) está sendo executado quando ocorre um aviso durante uma **eventos de Conexão**operação; ou, quando um **Conexão** inicia ou termina.

-   **Eventos de conjunto de registros**: eventos são emitidos em torno de operações de busca assíncrona, bem como quando você navega pelas linhas de um **registros** de objeto, alterar um campo em uma linha de um **Recordset**, alterar uma linha em um **Recordset**, abra um **Recordset** com um cursor do lado do servidor, feche um **Recordset**, ou fazer qualquer alteração qualquer no  **Conjunto de registros**.

 As tabelas a seguir resumem os eventos e suas descrições.

|ConnectionEvent|Description|
|---------------------|-----------------|
|[BeginTransComplete, CommitTransComplete, RollbackTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|**Gerenciamento de transações** — uma notificação de que a transação atual em que a conexão foi iniciado, confirmada ou revertida.|
|[WillConnect](../../../ado/reference/ado-api/willconnect-event-ado.md), [ConnectComplete, desconectar](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|**Gerenciamento de Conexão** — uma notificação de que a conexão atual será iniciado, começou ou terminou.|
|[WillExecute](../../../ado/reference/ado-api/willexecute-event-ado.md), [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md)|**Gerenciamento de execução do comando** — uma notificação de que a execução do comando atual em que a conexão será iniciado ou terminou.|
|[InfoMessage](../../../ado/reference/ado-api/infomessage-event-ado.md)|**Informação** — notificação de que há informações adicionais sobre a operação atual.|

|RecordsetEvent|Description|
|--------------------|-----------------|
|[FetchProgress](../../../ado/reference/ado-api/fetchprogress-event-ado.md), [FetchComplete](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|**Status de recuperação** — notificação do progresso de uma operação de recuperação de dados, ou que a operação de recuperação foi concluída. Esses eventos estão disponíveis somente se o **registros** foi aberto usando um cursor do lado do cliente.|
|[WillChangeField, FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|**Gerenciamento de alterações de campo** — uma notificação de que o valor do campo atual será alterado ou foi alterada.|
|[WillMove, MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md), [EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|**Gerenciamento de navegação** — notificação posicionar a linha atual em um **Recordset** será alterado, foi alterado ou atingiu o fim do **Recordset**.|
|[WillChangeRecord, RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|**Gerenciamento de alterações de linha** — notificação de que algo na linha atual do **registros** alterará ou foi alterada.|
|[WillChangeRecordset, RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|**Gerenciamento de alterações de conjunto de registros** — a notificação de que algo no atual **registros** alterará ou foi alterada.|

## <a name="see-also"></a>Consulte Também
 [Instanciação de evento ADO pela linguagem](../../../ado/guide/data/ado-event-instantiation-by-language.md) [ADO eventos](../../../ado/reference/ado-api/ado-events.md) [parâmetros de evento](../../../ado/guide/data/event-parameters.md) [como manipuladores de eventos funcionam juntos](../../../ado/guide/data/how-event-handlers-work-together.md) [tipos de eventos](../../../ado/guide/data/types-of-events.md)
