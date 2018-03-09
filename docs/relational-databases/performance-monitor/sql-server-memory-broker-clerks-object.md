---
title: "SQL Server, objeto Administradores do Agente de Memória | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLServer:Memory Broker Clerks
ms.assetid: 47b9c236-66a3-4c42-97ee-da5555bdc046
caps.latest.revision: 
author: dagiro
ms.author: v-dagir
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9d86b986025348a829734d57625a0567041cd12d
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="sql-server-memory-broker-clerks-object"></a>SQL Server, Objeto Administradores do Agente de Memória
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] O objeto de desempenho **SQLServer:Memory Broker Clerks** fornece contadores para estatísticas relacionadas a administradores do agente de memória.

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

## <a name="see-also"></a>Consulte Também  
[Monitorar o uso de recursos (Monitor do Sistema)](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)
