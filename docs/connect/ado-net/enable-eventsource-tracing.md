---
title: Habilitar o rastreamento de eventos no SqlClient
description: Descreve como habilitar o rastreamento de eventos no SqlClient implementando um ouvinte de eventos e como acessar os dados do evento.
ms.date: 11/23/2020
dev_langs:
- csharp
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: johnnypham
ms.author: v-jopha
ms.reviewer: ''
ms.openlocfilehash: b45f6146f8b5e2f367281720b0fa1c3395d94256
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96123956"
---
# <a name="enable-event-tracing-in-sqlclient"></a>Habilitar o rastreamento de eventos no SqlClient

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

## <a name="event-tracing-support-in-native-sni"></a>Suporte ao rastreamento de eventos no SNI nativo

O **Microsoft.Data.SqlClient** versão 2.1.0 estende o suporte ao rastreamento de eventos em **Microsoft.Data.SqlClient.SNI** e **Microsoft.Data.SqlClient.SNI.runtime**. Com o envio de um EventCommand para `SqlClientEventSource`, os eventos no SNI.dll nativo podem ser coletados usando ferramentas [Xperf](https://docs.microsoft.com/windows-hardware/test/wpt/) e [PerfView](https://github.com/microsoft/perfview). Os valores de EventCommand válidos são listados como abaixo:

```cs
// Enables trace events:
EventSource.SendCommand(eventSource, (EventCommand)8192, null);

// Enables flow events:
EventSource.SendCommand(eventSource, (EventCommand)16384, null);

// Enables both trace and flow events:
EventSource.SendCommand(eventSource, (EventCommand)(8192 | 16384), null);
```

O exemplo a seguir habilita o rastreamento de eventos no SNI.dll nativo quando o aplicativo tem .NET Framework como destino. 

```cs
// Native SNI tracing example
// .NET Framework application
using System;
using System.Diagnostics.Tracing;
using Microsoft.Data.SqlClient;

public class SqlClientListener : EventListener
{
    protected override void OnEventSourceCreated(EventSource eventSource)
    {
        if (eventSource.Name.Equals("Microsoft.Data.SqlClient.EventSource"))
        {
            // Enables both trace and flow events
            EventSource.SendCommand(eventSource, (EventCommand)(8192 | 16384), null);
        }
    }
}

class Program
{
    static string connectionString = @"Data Source = localhost; Initial Catalog = AdventureWorks;Integrated Security=true;";

    static void Main(string[] args)
    {
        using (SqlClientListener listener = new SqlClientListener())
        using (SqlConnection connection = new SqlConnection(connectionString))
        {
            connection.Open();
        }        
    }
}
```

### <a name="use-xperf-to-collect-trace-log"></a>Usar Xperf para coletar o log de rastreamento

1. Inicie o rastreamento usando a linha de comando a seguir.

   ```
   xperf -start trace -f myTrace.etl -on *Microsoft.Data.SqlClient.EventSource
   ```
   
2. Execute o exemplo de rastreamento do SNI nativo para se conectar ao SQL Server.

3. Pare o rastreamento usando a linha de comando a seguir.

   ```
   xperf -stop trace
   ```
   
4. Use PerfView para abrir o arquivo myTrace.etl especificado na etapa 1. O log de rastreamento do SNI pode ser encontrado com os nomes de evento `Microsoft.Data.SqlClient.EventSource/SNIScope` e `Microsoft.Data.SqlClient.EventSource/SNITrace`. 

   ![Usar PerfView para exibir o arquivo de rastreamento do SNI](media/view-event-trace-native-sni.png)


### <a name="use-perfview-to-collect-trace-log"></a>Usar PerfView para coletar o log de rastreamento

1. Inicie o PerfView e execute `Collect > Collect` na barra de menus.

2. Configure o nome do arquivo de rastreamento, o caminho de saída e o nome do provedor.

   ![Configurar Prefview antes da coleta](media/collect-event-trace-native-sni.png)
   
3. Inicie a coleta.

4. Execute o exemplo de rastreamento do SNI nativo para se conectar ao SQL Server.

5. Interrompa a coleta no PerfView. Levará algum tempo para gerar o arquivo PerfViewData.etl de acordo com a configuração na etapa 2.

6. Abra o arquivo etl no PerfView. O log de rastreamento do SNI pode ser encontrado com os nomes de evento `Microsoft.Data.SqlClient.EventSource/SNIScope` e `Microsoft.Data.SqlClient.EventSource/SNITrace`. 


## <a name="external-resources"></a>Recursos externos  
Para obter mais informações, consulte os recursos a seguir.  
  
|Recurso|Descrição|  
|--------------|-----------------|  
|[EventSource Class](/dotnet/api/system.diagnostics.tracing.eventsource)|Fornece a capacidade de criar eventos ETW.| 
|[Classe EventListener](/dotnet/api/system.diagnostics.tracing.eventlistener)|Fornece métodos para habilitar e desabilitar eventos de origens do evento.|
