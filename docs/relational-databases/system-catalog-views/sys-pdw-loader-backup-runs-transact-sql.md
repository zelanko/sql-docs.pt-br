---
title: sys. pdw_loader_backup_runs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 2b72034c-6a11-46b9-a76c-7a88b2bea360
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: c8e7826e4dcefdbed65fb0fa1f3368411a9ef12a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68127466"
---
# <a name="syspdw_loader_backup_runs-transact-sql"></a>sys. pdw_loader_backup_runs (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contém informações sobre operações de backup e restauração em andamento e [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]concluídas no, e sobre operações de backup, restauração e carregamento em [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]andamento e concluídas no. As informações persistem entre os reinícios do sistema.  
  
|Nome da coluna|Tipo de Dados|DESCRIÇÃO|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|run_id|**int**|Identificador exclusivo para um backup, restauração ou execução de carregamento específico.<br /><br /> Chave para esta exibição.||  
|name|**nvarchar (255)**|Nulo para carregamento. Nome opcional para backup ou restauração.||  
|submit_time|**datetime**|Hora em que a solicitação foi enviada.||  
|start_time|**datetime**|Hora em que a operação foi iniciada.||  
|end_time|**datetime**|Hora em que a operação foi concluída, falhou ou foi cancelada.||  
|total_elapsed_time|**int**|Tempo total decorrido entre start_time e a hora atual, ou entre start_time e end_time para execuções concluídas, canceladas ou com falha.|Se total_elapsed_time exceder o valor máximo de um inteiro (24,8 dias em milissegundos), isso causará falha de materialização devido ao estouro.<br /><br /> O valor máximo em milissegundos é equivalente a 24,8 dias.|  
|operation_type|**nvarchar (16)**|O tipo de carga.|' BACKUP ', ' LOAD ', ' RESTORE '|  
|modo|**nvarchar (16)**|O modo dentro do tipo de execução.|Para operation_type = **backup**<br />**DIFFERENTIAL**<br />**FULL**<br /><br /> Para operation_type = **Load**<br />**ANEXAR**<br />**RECARREGAR**<br />**UPSERT**<br /><br /> Para operation_type = **restaurar**<br />**DATABASE**<br />**HEADER_ONLY**|  
|database_name|**nvarchar (255)**|Nome do banco de dados que é o contexto desta operação||  
|table_name|**nvarchar (255)**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|Principal_id|**int**|ID do usuário que está solicitando a operação.||  
|session_id|**nvarchar (32)**|ID da sessão que está executando a operação.|Consulte session_id em [Sys. dm_pdw_exec_sessions &#40;&#41;do Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md).|  
|request_id|**nvarchar (32)**|ID da solicitação que executa a operação. Para cargas, esta é a solicitação atual ou a última associada a essa carga.|Consulte request_id em [Sys. dm_pdw_exec_requests &#40;&#41;do Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|status|**nvarchar (16)**|Status da execução.|' CANCELADO ', ' CONCLUÍDO ', ' COM FALHA ', ' ENFILEIRADO ', ' EM EXECUÇÃO '|  
|progresso|**int**|Porcentagem concluída.|0 a 100|  
|command|**nvarchar(4000)**|Texto completo do comando enviado pelo usuário.|Será truncado se tiver mais de 4000 caracteres (contando espaços).|  
|rows_processed|**bigint**|Número de linhas processadas como parte desta operação.||  
|rows_rejected|**bigint**|Número de linhas rejeitadas como parte desta operação.||  
|rows_inserted|**bigint**|Número de linhas inseridas nas tabelas de banco de dados como parte desta operação.||  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de Catálogo do SQL Data Warehouse e Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
