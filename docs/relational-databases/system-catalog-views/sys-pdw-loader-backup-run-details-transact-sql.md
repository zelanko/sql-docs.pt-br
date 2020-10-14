---
description: sys.pdw_loader_backup_run_details (Transact-SQL)
title: sys.pdw_loader_backup_run_details (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 04fc004f-ee15-4d7a-be08-78357aa99b55
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 243bbff033bfa3b9327227da6fdbf200d28e1ee5
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92034799"
---
# <a name="syspdw_loader_backup_run_details-transact-sql"></a>sys.pdw_loader_backup_run_details (Transact-SQL)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Contém informações detalhadas adicionais, além das informações em [sys.pdw_loader_backup_runs &#40;&#41;de Transact-SQL ](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md), sobre operações de backup e restauração em andamento e concluídas no [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e sobre operações de backup, restauração e carregamento em andamento e concluídas no [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] . As informações persistem entre os reinícios do sistema.  
  
|Nome da coluna|Tipo de Dados|DESCRIÇÃO|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|run_id|**int**|Identificador exclusivo para uma execução de backup ou restauração específica.<br /><br /> run_id e pdw_node_id formate a chave para essa exibição.||  
|pdw_node_id|**int**|Identificador exclusivo de um nó de dispositivo para o qual este registro contém detalhes.<br /><br /> run_id e pdw_node_id formate a chave para essa exibição.|Consulte node_id em [sys.dm_pdw_nodes &#40;&#41;do Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|status|**nvarchar (16)**|O status atual da execução.|' CANCELADO ', ' CONCLUÍDO ', ' COM FALHA ', ' ENFILEIRADO ', ' EM EXECUÇÃO '|  
|start_time|**datetime**|Hora em que a operação foi iniciada neste nó em particular.||  
|end_time|**datetime**|Hora em que a operação foi encerrada neste nó específico, se houver.||  
|total_elapsed_time|**int**|Tempo total de execução da operação neste nó em particular.|Se total_elapsed_time exceder o valor máximo de um inteiro (24,8 dias em milissegundos), isso causará falha de materialização devido ao estouro.<br /><br /> O valor máximo em milissegundos é equivalente a 24,8 dias.|  
|progress|**int**|Progresso da operação expressa como uma porcentagem.|0 a 100|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de Catálogo do Azure Synapse Analytics e do Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
