---
title: SQL Server, objeto de Estatísticas do pool de recursos | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
s.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Reosurce Pool Stats object
- 'SQLServer: Resource Pool Stats object'
ms.assetid: bb46e029-fcf9-4aeb-a066-be41e7668fb9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 73e24df827b07303afa8d24eff2babc7a0072271
ms.sourcegitcommit: ca038f1ef180e4e1b27910bbc5d87822cd1ed176
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2018
ms.locfileid: "52159145"
---
# <a name="sql-server-resource-pool-stats-object"></a>SQL Server, objeto de estatísticas do pool de recursos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O objeto SQLServer:Estatísticas de Pool de Recursos contém contadores de desempenho que fornecem informações sobre as estatísticas de pool de recursos do Administrador de Recursos.  
  
 Cada pool de recursos ativo cria uma instância do objeto de desempenho SQLServer:Estatísticas de Pool de Recursos que tem o mesmo nome de instância do pool de recursos do Administrador de Recursos. A tabela a seguir descreve os contadores suportados nesta instância.  
  
|Nome do contador|Descrição|  
|------------------|-----------------|  
|**Quantidade de memória ativa concedida (KB)**|A quantidade total atual, em kilobytes (KB), de memória concedida. Essas informações também estão disponíveis em [sys.dm_exec_query_resource_semaphores](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-resource-semaphores-transact-sql.md).| 
|**Contagem de concessões de memória ativa**|A contagem total atual de concessões de memória. Essas informações também estão disponíveis em [sys.dm_exec_query_memory_grants](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md).|  
|**Média de E/S de leitura de disco (ms)**|Tempo médio, em milissegundos, de uma operação de leitura do disco.|  
|**Base média de E/S de leitura de disco (ms)**|Somente para uso interno.|
|**Média de E/S de gravação em disco (ms)**|Tempo médio, em milissegundos, de uma operação de gravação no disco.|  
|**Base média de E/S de gravação de disco (ms)**|Somente para uso interno.|
|**Meta da memória cache (KB)**|A meta do agente de memória atual, em kilobytes (KB), para cache.|  
|**Meta da memória de compilação (KB)**|A meta do agente de memória atual, em kilobytes (KB), para compilações de consulta.|  
|**% de efeito do controle de CPU**|O efeito do Administrador de Recursos no pool de recursos. Calculado como (% de uso de CPU) / (% de uso de CPU sem o Administrador de Recursos).|  
|**% de CPU atrasada**|CPU do sistema atrasada para todas as solicitações na instância especificada do objeto de desempenho como uma porcentagem do tempo total ativo.|
|**% base de CPU atrasada**|Somente para uso interno.|
|**% de CPU efetiva**|Uso de CPU do sistema por todas as solicitações na instância especificada do objeto de desempenho como uma porcentagem do tempo total ativo.|
|**% base de CPU efetiva**|Somente para uso interno.|
|**% de uso de CPU**|O uso da largura de banda da CPU por todas as solicitações em todos os grupos de cargas de trabalho pertencentes a este pool. Essa é a medida relativa ao computador e normalizada para todas as CPUs no sistema. Esse valor mudará à medida que a quantidade de CPU disponível para o processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for alterada. Ele não é normalizado de acordo com o que é recebido pelo processo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|**% base de uso de CPU**|Somente para uso interno.|
|**% de meta de uso de CPU**|O valor de meta da % de uso da CPU para o pool de recursos com base nas definições de configuração do pool de recursos e na carga do sistema.|  
|**% de CPU violada**|A diferença entre a reserva de CPU e a porcentagem de agendamento efetiva.|
|**Leitura do disco/s**|Número de bytes lidos do disco no último segundo.|  
|**Leitura E/S de disco limitada/s**|Número de operações de leitura limitadas no último segundo.|  
|**E/S de leitura do disco/s**|Número de operações de leitura do disco no último segundo.| 
|**Gravação em disco bytes/s**|Número de bytes gravados no disco no último segundo.|  
|**Gravação E/S de disco limitada/s**|Número de operações de gravação limitadas no último segundo.| 
|**E/S de gravação em disco/s**|Número de operações de gravação no disco no último segundo.|
|**Memória máxima (KB)**|A quantidade máxima, em kilobytes (KB), de memória que o pool de recursos pode ter com base nas configurações do pool de recursos e no estado do servidor.| 
|**Tempos limite de concessão de memória/s**|O número de tempos limite de concessões de memória por segundo.|
|**Concessões de memória/s**|O número de concessões de memória por segundo que ocorrem neste pool de recursos.| 
|**Contagem de concessão de memória pendente**|O número de solicitações de concessões de memória pendentes nas filas. Essas informações também estão disponíveis em [sys.dm_exec_query_resource_semaphores](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-resource-semaphores-transact-sql.md).|
|**Meta da memória de execução de consultas (KB)**|A meta do agente de memória atual, em kilobytes (KB), para concessão de memória de execução de consultas. Essas informações também estão disponíveis em [sys.dm_exec_query_memory_grants](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md).|  
|**Meta de memória (KB)**|A meta de quantidade, em kilobytes (KB), de memória que o pool de recursos está tentando obter com base nas configurações do pool de recursos e no estado do servidor.|   
|**Memória usada (KB)**|A quantidade de memória usada, em kilobytes (KB), para o pool de recursos.|  

  
## <a name="see-also"></a>Consulte Também  
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server, objeto de estatísticas de grupo de cargas de trabalho](../../relational-databases/performance-monitor/sql-server-workload-group-stats-object.md)   
 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)  
  
  
