---
title: sys. dm_db_rda_migration_status (Transact-SQL) | Microsoft Docs
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
ms.openlocfilehash: 21e5230e4f3efd86fe90382202f0b21a0187a214
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67937060"
---
# <a name="stretch-database---sysdm_db_rda_migration_status"></a>Stretch Database-sys. dm_db_rda_migration_status
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada lote de dados migrados de cada tabela habilitada para Stretch na instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os lotes são identificados por sua hora de início e hora de término.  
  
 **Sys. dm_db_rda_migration_status** está no escopo do contexto do banco de dados atual. Verifique se você está no contexto de banco de dados das tabelas de habilitação de ampliação para as quais você deseja ver o status de migração.  
  
 No [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], a saída de **Sys. dm_db_rda_migration_status** é limitada a 200 linhas.  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**table_id**|**int**|A ID da tabela da qual as linhas foram migradas.|  
|**database_id**|**int**|A ID do banco de dados do qual as linhas foram migradas.|  
|**migrated_rows**|**bigint**|O número de linhas migradas neste lote.|  
|**start_time_utc**|**datetime**|A hora UTC em que o lote foi iniciado.|  
|**end_time_utc**|**datetime**|A hora UTC em que o lote foi concluído.|  
|**error_number**|**int**|Se o lote falhar, o número de erro do erro que ocorreu; caso contrário, NULL.|  
|**error_severity**|**int**|Se o lote falhar, a severidade do erro que ocorreu; caso contrário, NULL.|  
|**error_state**|**int**|Se o lote falhar, o estado do erro que ocorreu; caso contrário, NULL.<br /><br /> O **ERROR_STATE** indica a condição ou o local em que o erro ocorreu.|  
  
## <a name="see-also"></a>Consulte Também  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
