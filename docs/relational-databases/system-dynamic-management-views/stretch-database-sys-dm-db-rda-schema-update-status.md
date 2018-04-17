---
title: sys.dm_db_rda_schema_update_status (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_rda_schema_update_status
- sys.dm_db_rda_schema_update_status_TSQL
- dm_db_rda_schema_update_status
- dm_db_rda_schema_update_status_TSQL
helpviewer_keywords:
- sys.dm_db_rda_schema_update_status dynamic management view
ms.assetid: 364e3caa-a7c6-4be5-a029-0b19da34de3e
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: eb96dc574363190b7d31915df3bf19a7d1e85bf1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="stretch-database---sysdmdbrdaschemaupdatestatus"></a>Stretch Database - sys.dm_db_rda_schema_update_status
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada tarefa de atualização de esquema para o arquivo de dados remotos de cada tabela habilitada para Stretch no banco de dados atual. Tarefas são identificadas por suas ids de tarefa.  
  
 **dm_db_rda_schema_update_status** voltada para o contexto de banco de dados atual. Verifique se que você está no contexto de banco de dados da tabela habilitada para ampliação para o qual você deseja ver o status de atualização de esquema.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**table_id**|**Int**|A ID local habilitada para ampliação da tabela de esquema de arquivos cujos dados remotos está sendo atualizada.|  
|**database_id**|**Int**|A ID do banco de dados que contém a tabela local habilitada para ampliação.|  
|**task_id**|**bigint**|A ID da tarefa de atualização de esquema de arquivo morto de dados remotos.|  
|**task_type**|**Int**|O tipo da tarefa de atualização de esquema de arquivo morto de dados remotos.|  
|**task_type_desc**|**nvarchar**|A descrição do tipo da tarefa de atualização de esquema de arquivo morto de dados remotos.|  
|**task_state**|**Int**|O estado da tarefa de atualização de esquema de arquivo morto de dados remotos.|  
|**task_state_des**|**nvarchar**|A descrição do estado da tarefa de atualização de esquema de arquivo morto de dados remotos.|  
|**start_time_utc**|**datetime**|A hora UTC em que os dados remotos arquivar o início da atualização de esquema.|  
|**end_time_utc**|**datetime**|A hora UTC em que os dados remotos arquivar a atualização de esquema concluída.|  
|**error_number**|**Int**|Se a atualização de esquema de arquivo morto de dados remotos falhar, o número do erro do erro que ocorreu; Caso contrário, nulo.|  
|**error_severity**|**Int**|Se a atualização de esquema de arquivo morto de dados remotos falhar, a severidade do erro que ocorreu; Caso contrário, nulo.|  
|**error_state**|**Int**|Se a atualização de esquema de arquivo morto de dados remotos falhar, o estado do erro que ocorreu; Caso contrário, nulo. O error_state indica a condição ou um local em que ocorreu o erro.|  
  
## <a name="see-also"></a>Consulte também  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
