---
title: SQL Server, objeto Administradores do Agente de Memória | Microsoft Docs
description: Saiba mais sobre o objeto de desempenho SQLServer:Memory Broker Clerks, que fornece contadores para estatísticas relacionadas aos administradores do agente de memória.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Memory Broker Clerks
ms.assetid: 47b9c236-66a3-4c42-97ee-da5555bdc046
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 6e3a569e65d02af75e4b0195ed0795e097b96838
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505640"
---
# <a name="sql-server-memory-broker-clerks-object"></a>SQL Server, Objeto Administradores do Agente de Memória
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
O objeto de desempenho **SQLServer:Administradores do Agente de Memória** fornece contadores para estatísticas relacionadas a administradores do agente de memória.

A tabela a seguir descreve os objetos de desempenho **Administradores do Agente de Memória** do SQL Server.

|**Contadores de Administradores do Agente de Memória do SQL Server**|Descrição|  
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
