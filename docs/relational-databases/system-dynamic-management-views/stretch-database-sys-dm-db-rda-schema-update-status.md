---
title: sys. dm_db_rda_schema_update_status (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.dm_db_rda_schema_update_status
- sys.dm_db_rda_schema_update_status_TSQL
- dm_db_rda_schema_update_status
- dm_db_rda_schema_update_status_TSQL
helpviewer_keywords:
- sys.dm_db_rda_schema_update_status dynamic management view
ms.assetid: 364e3caa-a7c6-4be5-a029-0b19da34de3e
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 611fe9d5bea47204b655f2defe5072d2dd17be92
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67937013"
---
# <a name="stretch-database---sysdm_db_rda_schema_update_status"></a>Stretch Database-sys. dm_db_rda_schema_update_status
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada tarefa de atualização de esquema para o arquivo de dados remoto de cada tabela habilitada para o Stretch no banco de dado atual. As tarefas são identificadas por suas IDs de tarefa.  
  
 **dm_db_rda_schema_update_status** está no escopo do contexto do banco de dados atual. Verifique se você está no contexto do banco de dados da tabela habilitada para Stretch para a qual você deseja ver o status de atualização do esquema.  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**table_id**|**int**|A ID da tabela local habilitada para Stretch cujo esquema de arquivo de dados remoto está sendo atualizado.|  
|**database_id**|**int**|A ID do banco de dados que contém a tabela local habilitada para Stretch.|  
|**task_id**|**bigint**|A ID da tarefa de atualização do esquema de arquivo de dados remoto.|  
|**task_type**|**int**|O tipo da tarefa de atualização do esquema de arquivo de dados remoto.|  
|**task_type_desc**|**nvarchar**|A descrição do tipo da tarefa de atualização do esquema de arquivo de dados remoto.|  
|**task_state**|**int**|O estado da tarefa de atualização do esquema de arquivo de dados remoto.|  
|**task_state_des**|**nvarchar**|A descrição do estado da tarefa de atualização do esquema de arquivo de dados remoto.|  
|**start_time_utc**|**datetime**|A hora UTC em que a atualização do esquema do arquivo de dados remoto foi iniciada.|  
|**end_time_utc**|**datetime**|A hora UTC em que a atualização do esquema do arquivo de dados remoto foi concluída.|  
|**error_number**|**int**|Se a atualização do esquema do arquivo de dados remoto falhar, o número do erro que ocorreu; caso contrário, NULL.|  
|**error_severity**|**int**|Se a atualização do esquema do arquivo de dados remoto falhar, a severidade do erro que ocorreu; caso contrário, NULL.|  
|**error_state**|**int**|Se a atualização do esquema do arquivo de dados remoto falhar, o estado do erro que ocorreu; caso contrário, NULL. O error_state indica a condição ou o local em que o erro ocorreu.|  
  
## <a name="see-also"></a>Consulte Também  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
