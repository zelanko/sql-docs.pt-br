---
title: SQL Server, objeto Scripts Externos | Microsoft Docs
description: Saiba mais sobre o objeto SQLServer:External Scripts, que fornece contadores para monitorar as ações associadas à execução de scripts externos.
ms.custom: ''
ms.date: 03/21/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- External Scripts object
- SQLServer:External Scripts
ms.assetid: 8a75ccce-b174-4937-bc92-8e413b55afe1
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: fb8ded658e80c3530b916ea81595ac5fa5c99f52
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2020
ms.locfileid: "86457405"
---
# <a name="sql-server-external-scripts-object"></a>SQL Server, objeto Scripts Externos
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  O objeto **SQLServer:External Scripts** no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece contadores para monitorar as ações associadas à execução de scripts externos. Para obter informações sobre a execução de scripts externos, veja [sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).  
  
 Esta tabela descreve os contadores **Scripts Externos** do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Contadores de Scripts Externos do SQL Server|Descrição|  
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
  
  
