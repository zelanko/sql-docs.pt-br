---
title: "SQL Server, Objeto Administradores do Agente de Mem&#243;ria | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SQLServer:Administradores do Agente de Memória"
ms.assetid: 47b9c236-66a3-4c42-97ee-da5555bdc046
caps.latest.revision: 4
author: "dagiro"
ms.author: "v-dagir"
manager: "jhubbard"
caps.handback.revision: 4
---
# SQL Server, Objeto Administradores do Agente de Mem&#243;ria
O objeto de desempenho **SQLServer:Administradores do Agente de Memória** fornece contadores para estatísticas relacionadas a administradores do agente de memória.

A tabela a seguir descreve os objetos de desempenho **Administradores do Agente de Memória** do SQL Server.

|**Contadores de Administradores do Agente de Memória do SQL Server**|Description|  
|-------------|-----------------|  
|**Benefício interno**|O valor interno de memória para pressão da contagem de entradas, em ms por página por ms, multiplicado por 10 bilhões e truncado para um inteiro.|
|**Tamanho do administrador do agente de memória**|O tamanho do administrador, em páginas.|
|**Remoções periódicas (páginas)**|O número de páginas removidas do administrador do agente pela última remoção periódica.|
|**Remoções de pressão (páginas/s)**|O número de páginas por segundo removidas do administrador do agente pela pressão de memória.|
|**Benefício de simulação**|O valor de memória para o administrador, em ms por página por ms, multiplicado por 10 bilhões e truncado para um inteiro.|
|**Tamanho de simulação**|O tamanho atual da simulação de administrador, em páginas.|

Há uma instância do contador para o pool de buffers e para o pool de objetos de repositório de coluna.

## Consulte também  
[Monitorar o uso de recursos (Monitor do Sistema)](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)