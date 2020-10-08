---
title: Habilitar o rastreamento de eventos no SqlClient
description: Descreve como habilitar o rastreamento de eventos no SqlClient implementando um ouvinte de eventos e como acessar os dados do evento.
ms.date: 06/15/2020
dev_langs:
- csharp
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: johnnypham
ms.author: v-jopha
ms.reviewer: ''
ms.openlocfilehash: 4eac1ab519549ccace092cfc175c735dd4537269
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725737"
---
# <a name="enabling-event-tracing-in-sqlclient"></a>Habilitar o rastreamento de eventos no SqlClient

[!INCLUDE [appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE [Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

O [ETW (Rastreamento de Eventos para Windows)](/windows/win32/etw/event-tracing-portal) é um recurso de rastreamento eficiente no nível de kernel que permite registrar eventos definidos pelo driver para fins de depuração e teste. O SqlClient dá suporte à captura de eventos ETW em diferentes níveis informativos. Para começar a capturar esses rastreamentos de eventos, os aplicativos cliente devem escutar eventos da implementação EventSource do SqlClient:

```
Microsoft.Data.SqlClient.EventSource
```

A implementação atual dá suporte às seguintes palavras-chave de evento:

| Nome da palavra-chave | Valor | DESCRIÇÃO |
| ------------ | ----- | ----------- |
| ExecutionTrace | 1 | Ativa a captura de eventos Iniciar/Parar antes e depois da execução do comando. |
| Trace | 2 | Ativa a captura de eventos básicos de rastreamento de fluxo de aplicativo. |
| Escopo | 4 | Ativa a captura de eventos de entrada e saída |
| NotificationTrace | 8 | Ativa a captura de eventos de rastreamento de `SqlNotification` |
| NotificationScope | 16 | Ativa a captura de eventos de entrada e saída de escopo de `SqlNotification` |
| PoolerTrace | 32 | Ativa a captura de eventos de rastreamento de fluxo do pool de conexões. |
| PoolerScope | 64 | Ativa a captura de eventos de rastreamento do escopo do pool de conexões. |
| AdvancedTrace | 128 | Ativa a captura de eventos de rastreamento de fluxo avançado. |
| AdvancedTraceBin  | 256 | Ativa a captura de eventos de rastreamento de fluxo avançado com informações adicionais. |
| CorrelationTrace | 512 | Ativa a captura de eventos de rastreamento de fluxo de correlação. |
| StateDump | 1024 | Ativa a captura do despejo de estado completo de `SqlConnection` |
| SNITrace | 2\.048 | Ativa a captura de eventos de rastreamento de fluxo da implementação de Rede Gerenciada (aplicável somente no .NET Core) |
| SNIScope | 4096 | Ativa a captura de eventos de escopo da implementação de Rede Gerenciada (aplicável somente no .NET Core) |
|||

## <a name="example"></a>Exemplo
O exemplo a seguir habilita o rastreamento de eventos para uma operação de dados no banco de dados de exemplo **AdventureWorks** e exibe os eventos na janela do console.

[!code-csharp [SqlClientEventSource#1](~/../sqlclient/doc/samples/SqlClientEventSource.cs#1)]

## <a name="external-resources"></a>Recursos externos  
Para obter mais informações, consulte os recursos a seguir.  
  
|Recurso|Descrição|  
|--------------|-----------------|  
|[EventSource Class](/dotnet/api/system.diagnostics.tracing.eventsource)|Fornece a capacidade de criar eventos ETW.| 
|[Classe EventListener](/dotnet/api/system.diagnostics.tracing.eventlistener)|Fornece métodos para habilitar e desabilitar eventos de origens do evento.|