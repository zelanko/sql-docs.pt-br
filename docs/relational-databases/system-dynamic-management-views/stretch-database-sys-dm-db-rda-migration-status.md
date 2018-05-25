---
title: sys.dm_db_rda_migration_status (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_rda_migration_status
- sys.dm_db_rda_migration_status_TSQL
- dm_db_rda_migration_status
- dm_db_rda_migration_status_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_rda_migration_status dynamic management view
ms.assetid: faf3901c-a0e0-4e0c-8b1b-86d9f15f34dd
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7a8778c09acc143bc6384f9b82ff03fa25603334
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2018
---
# <a name="stretch-database---sysdmdbrdamigrationstatus"></a>Stretch Database - sys.DM db_rda_migration_status
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada lote de dados migrados de cada tabela habilitada para ampliação na instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Lotes são identificados por sua hora de início e a hora de término.  
  
 **sys.DM db_rda_migration_status** voltada para o contexto de banco de dados atual. Verifique se que você está no contexto de banco de dados das tabelas de habilitar a ampliação para o qual você deseja ver o status da migração.  
  
 Em [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], a saída de **sys.DM db_rda_migration_status** é limitada a 200 linhas.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**table_id**|**Int**|A ID da tabela da qual as linhas foram migradas.|  
|**database_id**|**Int**|A ID do banco de dados do qual as linhas foram migradas.|  
|**migrated_rows**|**bigint**|O número de linhas migradas nesse lote.|  
|**start_time_utc**|**datetime**|A hora UTC em que o lote foi iniciado.|  
|**end_time_utc**|**datetime**|A hora UTC em que o lote concluído.|  
|**error_number**|**Int**|Se o lote falhar, o número do erro do erro que ocorreu; Caso contrário, nulo.|  
|**error_severity**|**Int**|Se o lote falhar, a severidade do erro que ocorreu; Caso contrário, nulo.|  
|**error_state**|**Int**|Se o lote falhar, o estado do erro que ocorreu; Caso contrário, nulo.<br /><br /> O **error_state** indica a condição ou um local em que ocorreu o erro.|  
  
## <a name="see-also"></a>Consulte também  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
