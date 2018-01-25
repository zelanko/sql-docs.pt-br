---
title: SQL Server, objeto Scripts Externos | Microsoft Docs
ms.custom: 
ms.date: 03/21/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- External Scripts object
- SQLServer:External Scripts
ms.assetid: 8a75ccce-b174-4937-bc92-8e413b55afe1
caps.latest.revision: "7"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fa53d84e29b23d73f73c93641306b11a328fc2e1
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="sql-server-external-scripts-object"></a>SQL Server, objeto Scripts Externos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  O objeto **SQLServer:External Scripts** no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece contadores para monitorar as ações associadas à execução de scripts externos. Para obter informações sobre a execução de scripts externos, veja [sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).  
  
 Esta tabela descreve os contadores [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Scripts Externos** .  
  
|Contadores de Scripts Externos do SQL Server|Description|  
|------------------------------------------|-----------------|  
|**Erros de Execução**|O número de erros na execução de scripts externos.|  
|**Logons de autenticação implícita**|O número de logons dos processos satélites autenticados usando a autenticação implícita.|  
|**Execuções paralelas**|O número de scripts externos executados com @parallel = 1.|  
|**Execuções de CC do SQL**|O número de scripts externos executados usando o Contexto de Computação do SQL.|  
|**Execuções de streaming**|O número de scripts externos executados com o parâmetro @r_rowsPerRead.|  
|**Tempo total de execução (ms)**|O tempo total gasto na execução de scripts externos.|  
|**Total de Execuções**|O número de scripts externos executados.|  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [sys.resource_governor_external_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)   
 [sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)  
  
  
