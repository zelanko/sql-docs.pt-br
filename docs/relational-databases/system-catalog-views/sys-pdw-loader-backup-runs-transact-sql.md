---
title: sys.pdw_loader_backup_runs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-objects
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 2b72034c-6a11-46b9-a76c-7a88b2bea360
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 8da926d5e3e12619a249fe593fac4b1be5df2bf6
ms.sourcegitcommit: abd71294ebc39695d403e341c4f77829cb4166a8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2018
ms.locfileid: "36875004"
---
# <a name="syspdwloaderbackupruns-transact-sql"></a>sys.pdw_loader_backup_runs (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contém informações sobre operações de restauração em e de backup em andamento e concluído [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]e sobre backup em andamento e concluído, restauração e operações de carregamento em [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. As informações persistem entre os reinícios do sistema.  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|run_id|**int**|Identificador exclusivo de um backup específico, a restauração ou a execução de carga.<br /><br /> A chave para este modo de exibição.||  
|nome|**nvarchar(255)**|NULL para a carga. Nome opcional para backup ou restauração.||  
|submit_time|**datetime**|Hora em que a solicitação foi enviada.||  
|start_time|**datetime**|Hora em que a operação iniciada.||  
|end_time|**datetime**|Tempo a operação concluída, falhou ou foi cancelada.||  
|total_elapsed_time|**int**|Tempo total decorrido entre start_time e a hora atual, ou entre start_time e end_time para concluído, cancelada ou com falha seja executada.|Se total_elapsed_time exceder o valor máximo para um inteiro (24,8 dias em milissegundos), ela causará falha de materialização devido a estouro.<br /><br /> O valor máximo em milissegundos é equivalente a 24,8 dias.|  
|operation_type|**nvarchar(16)**|O tipo de carga.|'BACKUP', 'LOAD', 'RESTORE'|  
|mode|**nvarchar(16)**|O modo de dentro do tipo de execução.|Para operation_type = **BACKUP**<br />**DIFERENCIAL**<br />**FULL**<br /><br /> Para operation_type = **carga**<br />**ACRESCENTAR**<br />**RELOAD**<br />**UPSERT**<br /><br /> Para operation_type = **RESTAURAR**<br />**DATABASE**<br />**HEADER_ONLY**|  
|database_name|**nvarchar(255)**|Nome do banco de dados que é o contexto desta operação||  
|table_name|**nvarchar(255)**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|Principal_id|**int**|ID do usuário que está solicitando a operação.||  
|session_id|**nvarchar(32)**|ID da sessão que está executando a operação.|Consulte session_id [DM pdw_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md).|  
|request_id|**nvarchar(32)**|ID da solicitação executando a operação. Para cargas, isso é a solicitação atual ou última associada com essa carga...|Consulte request_id na [DM pdw_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|status|**nvarchar(16)**|Status da execução.|'CANCELAR', 'CONCLUIR', 'FALHA', 'ENFILEIRADO', 'RUNNING'|  
|progresso|**int**|Porcentagem concluída.|0 a 100|  
|command|**nvarchar(4000)**|Texto completo do comando enviado pelo usuário.|Será truncado se for maior que 4000 caracteres (contando espaços).|  
|rows_processed|**bigint**|Número de linhas processadas como parte dessa operação.||  
|rows_rejected|**bigint**|Número de linhas rejeitadas como parte dessa operação.||  
|rows_inserted|**bigint**|Número de linhas inseridas nas tabelas de banco de dados como parte dessa operação.||  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse e Parallel Data Warehouse exibições do catálogo](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
