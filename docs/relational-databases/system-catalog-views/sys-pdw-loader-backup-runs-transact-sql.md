---
title: sys.pdw_loader_backup_runs (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 2b72034c-6a11-46b9-a76c-7a88b2bea360
caps.latest.revision: "10"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5ebdadbeeba70444eda300f44480e49fa9992d29
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="syspdwloaderbackupruns-transact-sql"></a>sys.pdw_loader_backup_runs (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contém informações sobre backup em andamento e concluído e operações de restauração em [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]e sobre backup em andamento e concluído, restauração e operações de carregamento em [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. As informações persistem entre as reinicializações do sistema.  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|run_id|**int**|Identificador exclusivo de um backup específico, restaure ou carga executar.<br /><br /> Chave para este modo de exibição.||  
|name|**nvarchar(255)**|NULL para carregamento. Nome opcional para backup ou restauração.||  
|submit_time|**datetime**|Hora em que a solicitação foi enviada.||  
|start_time|**datetime**|Hora em que a operação iniciada.||  
|end_time|**datetime**|Tempo a operação foi concluída, falhou ou foi cancelada.||  
|total_elapsed_time|**int**|Tempo total decorrido entre start_time e a hora atual, ou entre start_time e end_time for concluída, cancelada ou com falha de execução.|Se total_elapsed_time excede o valor máximo para um inteiro (24.8 dias em milissegundos), isso causará falha materialização devido ao estouro.<br /><br /> O valor máximo em milissegundos é equivalente a 24.8 dias.|  
|operation_type|**nvarchar(16)**|O tipo de carga.|'BACKUP', 'CARREGAR', 'RESTORE'|  
|mode|**nvarchar(16)**|O modo de dentro do tipo de execução.|Para operation_type = **BACKUP**<br />**DIFERENCIAL**<br />**FULL**<br /><br /> Para operation_type = **carga**<br />**ACRESCENTAR**<br />**RECARREGAR**<br />**UPSERT**<br /><br /> Para operation_type = **RESTAURAR**<br />**DATABASE**<br />**HEADER_ONLY**|  
|database_name|**nvarchar(255)**|Nome do banco de dados que é o contexto desta operação||  
|table_name|**nvarchar(255)**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|Principal_id|**int**|ID do usuário que está solicitando a operação.||  
|session_id|**nvarchar (32)**|ID da sessão que está executando a operação.|Consulte session_id [sys.dm_pdw_exec_sessions &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md).|  
|request_id|**nvarchar (32)**|ID da solicitação de executar a operação. Para cargas, esta é a solicitação atual ou última associada a esse tipo de carga.|Consulte request_id em [sys.dm_pdw_exec_requests &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|status|**nvarchar(16)**|Status da execução.|'CANCELADO', 'CONCLUIR', 'COM FALHA', 'ENFILEIRADO', 'EM EXECUÇÃO'|  
|progresso|**int**|Porcentagem concluída.|0 a 100|  
|command|**nvarchar(4000)**|Texto completo do comando enviado pelo usuário.|Será truncado se mais de 4000 caracteres (contando espaços).|  
|rows_processed|**bigint**|Número de linhas processadas como parte dessa operação.||  
|rows_rejected|**bigint**|Número de linhas rejeitadas como parte dessa operação.||  
|rows_inserted|**bigint**|Número de linhas inseridas em tabelas de banco de dados como parte dessa operação.||  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse e exibições de catálogo do Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
