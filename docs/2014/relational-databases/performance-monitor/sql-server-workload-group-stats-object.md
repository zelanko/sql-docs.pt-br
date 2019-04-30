---
title: SQL Server, objeto Estatísticas de grupo de cargas de trabalho | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Workload Group Stats object
- 'SQLServer: Workload Group Stats'
ms.assetid: ca20e4f6-50ec-4456-900d-87d280fde2b3
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 06651ffcfee30d538c8ede09914133a2ed818b3b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63151099"
---
# <a name="sql-server-workload-group-stats-object"></a>SQL Server, objeto de estatísticas de grupo de cargas de trabalho
  O objeto SQLServer:Estatísticas de Grupo de Cargas de Trabalho contém contadores de desempenho que dão informações sobre estatísticas de grupo de cargas de trabalho do Administrador de Recursos.  
  
 Cada grupo de cargas de trabalho ativo cria uma instância do objeto de desempenho SQLServer:Estatísticas de Grupo de Cargas de Trabalho que tem o mesmo nome de instância do grupo de cargas de trabalho do Administrador de Recursos. A tabela a seguir descreve os contadores suportados nesta instância.  
  
|Nome do contador|Descrição|  
|------------------|-----------------|  
|Solicitações em fila|O número atual de solicitações em fila que estão esperando para serem selecionadas. Esta contagem poderá ser diferente de zero se a aceleração ocorrer depois que o limite GROUP_MAX_REQUESTS for atingido.|  
|Solicitações ativas|O número de solicitações que estão sendo executadas neste grupo de cargas de trabalho. Deverá ser equivalente à contagem de linhas de sys.dm_exec_requests filtradas pela ID de grupo.|  
|Solicitações concluídas/s|O número de solicitações que foram concluídas neste grupo de cargas de trabalho. Este número é cumulativo.|  
|% de uso de CPU|O uso da largura de banda da CPU por todas as solicitações neste grupo de cargas de trabalho calculado em relação ao computador e normalizado para todas as CPUs do sistema. Esse valor mudará à medida que a quantidade de CPU disponível para o processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for alterada. Ele não é normalizado de acordo com o que é recebido pelo processo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|Tempo máximo de CPU da solicitação (ms)|O tempo máximo de CPU, em milissegundos, usado por uma solicitação que está sendo executada no grupo de cargas de trabalho.|  
|Solicitações bloqueadas|O número atual de solicitações bloqueadas no grupo de cargas de trabalho. Esse número pode ser usado para determinar características de carga de trabalho.|  
|Concessões de memória reduzidas/s|O número de consultas que estão obtendo menos do que a quantidade ideal de concessões de memória por segundo.|  
|Concessão máxima de memória da solicitação (KB)|O valor máximo da concessão de memória, em kilobytes (KB), para uma consulta.|  
|Otimizações de consultas/seg|O número de otimizações de consulta por segundo ocorridas neste grupo de cargas de trabalho. Esse número pode ser usado para determinar características de carga de trabalho.|  
|Planos de qualidade inferior/s|O número de planos de qualidade inferior que são gerados por segundo neste grupo de cargas de trabalho.|  
|Threads paralelos ativos|A contagem atual de uso de threads paralelos.|  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](monitor-resource-usage-system-monitor.md)   
 [SQL Server, objeto de estatísticas do pool de recursos](sql-server-resource-pool-stats-object.md)   
 [Resource Governor](../resource-governor/resource-governor.md)  
  
  
