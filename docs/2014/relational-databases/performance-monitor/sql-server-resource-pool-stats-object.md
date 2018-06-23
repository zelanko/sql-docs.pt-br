---
title: SQL Server, objeto de Estatísticas do pool de recursos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Reosurce Pool Stats object
- 'SQLServer: Resource Pool Stats object'
ms.assetid: bb46e029-fcf9-4aeb-a066-be41e7668fb9
caps.latest.revision: 12
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 26d74ff671e55843b279d0609e8ee99a6b7b58b2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007684"
---
# <a name="sql-server-resource-pool-stats-object"></a>SQL Server, objeto de estatísticas do pool de recursos
  O objeto SQLServer:Estatísticas de Pool de Recursos contém contadores de desempenho que fornecem informações sobre as estatísticas de pool de recursos do Administrador de Recursos.  
  
 Cada pool de recursos ativo cria uma instância do objeto de desempenho SQLServer:Estatísticas de Pool de Recursos que tem o mesmo nome de instância do pool de recursos do Administrador de Recursos. A tabela a seguir descreve os contadores suportados nesta instância.  
  
|Nome do contador|Description|  
|------------------|-----------------|  
|% de uso de CPU|O uso da largura de banda da CPU por todas as solicitações em todos os grupos de cargas de trabalho pertencentes a este pool. Essa é a medida relativa ao computador e normalizada para todas as CPUs no sistema. Esse valor mudará à medida que a quantidade de CPU disponível para o processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for alterada. Ele não é normalizado de acordo com o que é recebido pelo processo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|% de meta de uso de CPU|O valor de meta da % de uso da CPU para o pool de recursos com base nas definições de configuração do pool de recursos e na carga do sistema.|  
|% de efeito do controle de CPU|O efeito do Administrador de Recursos no pool de recursos. Calculado como (% de uso de CPU) / (% de uso de CPU sem o Administrador de Recursos).|  
|Meta da memória de compilação (KB)|A meta do agente de memória atual, em kilobytes (KB), para compilações de consulta.|  
|Meta da memória cache (KB)|A meta do agente de memória atual, em kilobytes (KB), para cache.|  
|Meta da memória de execução de consultas (KB)|A meta do agente de memória atual, em kilobytes (KB), para concessão de memória de execução de consultas. Essas informações também estão disponíveis em [sys.dm_exec_query_memory_grants](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql).|  
|Concessões de memória/s|O número de concessões de memória por segundo que ocorrem neste pool de recursos.|  
|Contagem de concessões de memória ativa|A contagem total atual de concessões de memória. Essas informações também estão disponíveis em [sys.dm_exec_query_memory_grants](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql).|  
|Tempos limite de concessão de memória/s|O número de tempos limite de concessões de memória por segundo.|  
|Quantidade de memória ativa concedida (KB)|A quantidade total atual, em kilobytes (KB), de memória concedida. Essas informações também estão disponíveis em [sys.dm_exec_query_resource_semaphores](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-resource-semaphores-transact-sql).|  
|Contagem de concessão de memória pendente|O número de solicitações de concessões de memória pendentes nas filas. Essas informações também estão disponíveis em [sys.dm_exec_query_resource_semaphores](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-resource-semaphores-transact-sql).|  
|Memória máxima (KB)|A quantidade máxima, em kilobytes (KB), de memória que o pool de recursos pode ter com base nas configurações do pool de recursos e no estado do servidor.|  
|Memória usada (KB)|A quantidade de memória usada, em kilobytes (KB), para o pool de recursos.|  
|Meta de memória (KB)|A meta de quantidade, em kilobytes (KB), de memória que o pool de recursos está tentando obter com base nas configurações do pool de recursos e no estado do servidor.|  
|E/S de leitura do disco/s|Número de operações de leitura do disco no último segundo.|  
|Leitura E/S de disco limitada/s|Número de operações de leitura limitadas no último segundo.|  
|Leitura do disco/s|Número de bytes lidos do disco no último segundo.|  
|Média de E/S de leitura de disco (ms)|Tempo médio, em milissegundos, de uma operação de leitura do disco.|  
|E/S de gravação em disco/s|Número de operações de gravação no disco no último segundo.|  
|Gravação E/S de disco limitada/s|Número de operações de gravação limitadas no último segundo.|  
|Gravação em disco bytes/s|Número de bytes gravados no disco no último segundo.|  
|Média de E/S de gravação em disco (ms)|Tempo médio, em milissegundos, de uma operação de gravação no disco.|  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](monitor-resource-usage-system-monitor.md)   
 [SQL Server, objeto de estatísticas de grupo de cargas de trabalho](sql-server-workload-group-stats-object.md)   
 [Resource Governor](../resource-governor/resource-governor.md)  
  
  
