---
title: sys.dm_db_rda_schema_update_status (Transact-SQL) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 85c12ae224203def43c9f9953cada0c336e9ebbd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65947386"
---
# <a name="stretch-database---sysdmdbrdaschemaupdatestatus"></a>Stretch Database - sys.dm_db_rda_schema_update_status
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada tarefa de atualização de esquema para o arquivo de dados remotos de cada tabela habilitada para Stretch no banco de dados atual. As tarefas são identificadas por suas ids de tarefa.  
  
 **dm_db_rda_schema_update_status** tem como escopo o contexto de banco de dados atual. Verifique se que você está no contexto da tabela habilitados para Stretch para a qual você deseja ver o status de atualização do esquema de banco de dados.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**table_id**|**int**|A ID local habilitado para ampliação da tabela de esquema de arquivar cujos dados remotos está sendo atualizada.|  
|**database_id**|**int**|A ID do banco de dados que contém a tabela local habilitada para Stretch.|  
|**task_id**|**bigint**|A ID da tarefa de atualização de esquema de arquivo morto de dados remotos.|  
|**task_type**|**int**|O tipo da tarefa de atualização de esquema de arquivo morto de dados remotos.|  
|**task_type_desc**|**nvarchar**|A descrição do tipo da tarefa de atualização de esquema de arquivo morto de dados remotos.|  
|**task_state**|**int**|O estado da tarefa de atualização de esquema de arquivo morto de dados remotos.|  
|**task_state_des**|**nvarchar**|A descrição do estado da tarefa de atualização de esquema de arquivo morto de dados remotos.|  
|**start_time_utc**|**datetime**|A hora UTC em que os dados remotos arquivar iniciada de atualização de esquema.|  
|**end_time_utc**|**datetime**|A hora UTC em que os dados remotos arquivar a atualização do esquema foi concluída.|  
|**error_number**|**int**|Se a atualização de esquema de arquivo morto de dados remotos falhar, o número do erro do erro que ocorreu; Caso contrário, nulo.|  
|**error_severity**|**int**|Se a atualização de esquema de arquivo morto de dados remotos falhar, a severidade do erro ocorrido; Caso contrário, nulo.|  
|**error_state**|**int**|Se a atualização de esquema de arquivo morto de dados remotos falhar, o estado do erro que ocorreu; Caso contrário, nulo. O error_state indica o local em que ocorreu o erro ou condição.|  
  
## <a name="see-also"></a>Consulte também  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
