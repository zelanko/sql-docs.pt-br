---
title: sys.pdw_loader_backup_run_details (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 04fc004f-ee15-4d7a-be08-78357aa99b55
caps.latest.revision: 9
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: eb30aed9807e183904f68bd4ae3ceb76345dce63
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="syspdwloaderbackuprundetails-transact-sql"></a>sys.pdw_loader_backup_run_details (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contém mais informações detalhadas, além das informações no [sys.pdw_loader_backup_runs &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md), sobre em andamento e concluído operações de backup e restauração em [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e sobre em andamento e concluir o backup, restauração e operações de carregamento em [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. As informações persistem entre os reinícios do sistema.  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|run_id|**Int**|Identificador exclusivo de um backup específico ou executar a restauração.<br /><br /> run_id e pdw_node_id formam a chave para este modo de exibição.||  
|pdw_node_id|**Int**|Identificador exclusivo de um nó de dispositivo para o qual este registro contém detalhes.<br /><br /> run_id e pdw_node_id formam a chave para este modo de exibição.|Consulte node_id em [sys.dm_pdw_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|status|**nvarchar(16)**|O status atual da execução.|'CANCELLED', 'COMPLETED', 'FAILED', 'QUEUED', 'RUNNING'|  
|start_time|**datetime**|Hora em que a operação iniciada neste nó específico.||  
|end_time|**datetime**|Hora em que a operação foi concluída neste nó específico, se houver.||  
|total_elapsed_time|**Int**|Tempo total que a operação está em execução neste nó específico.|Se total_elapsed_time excede o valor máximo para um inteiro (24.8 dias em milissegundos), isso causará falha materialização devido ao estouro.<br /><br /> O valor máximo em milissegundos é equivalente a 24.8 dias.|  
|progresso|**Int**|Progresso da operação expressada como uma porcentagem.|0 a 100|  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse e exibições de catálogo do Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
