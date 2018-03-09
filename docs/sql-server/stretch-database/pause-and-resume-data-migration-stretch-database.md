---
title: "Pausar e retomar a migração de dados (Stretch Database) | Microsoft Docs"
ms.custom: 
ms.date: 06/14/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: stretch-database
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Stretch Database, pausing and resuming
- pausing Stretch Database
- resuming Stretch Database
ms.assetid: 65d6a990-b295-41b2-97f9-7b6bf3000e4d
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1a668af6406490e36584d9ad7754f4f783b8b0be
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="pause-and-resume-data-migration-stretch-database"></a>Pausar e retomar a migração de dados (Stretch Database)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  Para pausar ou retomar a migração de dados no Azure, escolha **Stretch** para uma tabela no SQL Server Management Studio e escolha **Pausar** para pausar a migração de dados ou **Retomar** para retomar a migração de dados. Você também pode usar o Transact-SQL para pausar ou retomar a migração de dados.  
  
 Pause a migração de dados em tabelas individuais quando quiser solucionar problemas no servidor local ou para maximizar a largura de banda de rede disponível.  

## <a name="pause-data-migration"></a>Pausar a migração de dados  
  
### <a name="use-sql-server-management-studio-to-pause-data-migration"></a>Usar o SQL Server Management Studio para pausar uma migração de dados  
  
1.  No SQL Server Management Studio, no Pesquisador de Objetos, selecione a tabela habilitada para o Stretch para a qual você deseja pausar a migração de dados.  
  
2.  Clique com o botão direito do mouse e selecione **Stretch**e selecione **Pausar**.  
  
### <a name="use-transact-sql-to-pause-data-migration"></a>Usar o Transact-SQL para pausar a migração de dados  
 Execute o comando a seguir.  
  
```sql  
USE <Stretch-enabled database name>;
GO
ALTER TABLE <Stretch-enabled table name>  
    SET ( REMOTE_DATA_ARCHIVE ( MIGRATION_STATE = PAUSED ) ) ;  
GO 
```  
  
## <a name="resume-data-migration"></a>Retomar a migração de dados  
  
### <a name="use-sql-server-management-studio-to-resume-data-migration"></a>Usar o SQL Server Management Studio para retomar uma migração de dados  
  
1.  No SQL Server Management Studio, no Pesquisador de Objetos, selecione a tabela habilitada para o Stretch para a qual você deseja retomar a migração de dados.  
  
2.  Clique com o botão direito do mouse e selecione **Stretch**e selecione **Retomar**.  
  
### <a name="use-transact-sql-to-resume-data-migration"></a>Usar o Transact-SQL para retomar a migração de dados  
 Execute o comando a seguir.  
  
```sql  
USE <Stretch-enabled database name>;
GO
ALTER TABLE <Stretch-enabled table name>   
    SET ( REMOTE_DATA_ARCHIVE ( MIGRATION_STATE = OUTBOUND ) ) ;  
 GO
```  

## <a name="check-whether-migration-is-active-or-paused"></a>Verificar se a migração está ativa ou em pausa

### <a name="use-sql-server-management-studio-to-check-whether-migration-is-active-or-paused"></a>Usar o SQL Server Management Studio para verificar se a migração está ativa ou em pausa
No SQL Server Management Studio, abra **Monitor do Stretch Database** e verifique o valor da coluna **Estado de Migração** . Para obter mais informações, veja [monitorar e solucionar problemas de migração de dados](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md).

### <a name="use-transact-sql-to-check-whether-migration-is-active-or-paused"></a>Usar o Transact-SQL para verificar se a migração está ativa ou em pausa
Consulte a exibição de catálogo **sys.remote_data_archive_tables** e verifique o valor da coluna **is_migration_paused** . Para obter mais informações, veja [sys.remote_data_archive_tables](../../relational-databases/system-catalog-views/stretch-database-catalog-views-sys-remote-data-archive-tables.md).

## <a name="see-also"></a>Consulte Também  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[monitorar e solucionar problemas de migração de dados](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md) 
  
