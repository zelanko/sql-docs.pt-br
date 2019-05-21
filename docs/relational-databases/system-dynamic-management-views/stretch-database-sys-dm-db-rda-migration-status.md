---
title: sys.dm_db_rda_migration_status (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
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
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 257d83e522b398cce8358c1e30f4966dd951739e
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65945457"
---
# <a name="stretch-database---sysdmdbrdamigrationstatus"></a>Stretch Database - DM db_rda_migration_status
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada lote de dados migrados de cada tabela habilitada para Stretch na instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Lotes são identificados por sua hora de início e a hora de término.  
  
 **DM db_rda_migration_status** tem como escopo o contexto de banco de dados atual. Verifique se que você está no contexto de banco de dados das tabelas de habilitar a ampliação para o qual você deseja ver o status da migração.  
  
 Na [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], a saída de **DM db_rda_migration_status** é limitada a 200 linhas.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**table_id**|**int**|A ID da tabela da qual as linhas foram migradas.|  
|**database_id**|**int**|A ID do banco de dados do qual as linhas foram migradas.|  
|**migrated_rows**|**bigint**|O número de linhas migradas nesse lote.|  
|**start_time_utc**|**datetime**|A hora UTC em que o lote foi iniciado.|  
|**end_time_utc**|**datetime**|A hora UTC em que o lote concluído.|  
|**error_number**|**int**|Se o lote falhar, o número do erro do erro que ocorreu; Caso contrário, nulo.|  
|**error_severity**|**int**|Se o lote falhar, a severidade do erro ocorrido; Caso contrário, nulo.|  
|**error_state**|**int**|Se o lote falhar, o estado do erro que ocorreu; Caso contrário, nulo.<br /><br /> O **error_state** indica o local em que ocorreu o erro ou condição.|  
  
## <a name="see-also"></a>Consulte também  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
