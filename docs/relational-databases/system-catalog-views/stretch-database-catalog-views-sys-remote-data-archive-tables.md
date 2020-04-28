---
title: sys. remote_data_archive_tables (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.remote_data_archive_tables
- sys.remote_data_archive_tables_TSQL
- remote_data_archive_tables
- remote_data_archive_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.remote_data_archive_tables catalog view
ms.assetid: 765069b7-60fd-414c-875f-3455460b75cd
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: 65e42e6303b467abd38ddadb6be0c0d0fece46e5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68018196"
---
# <a name="stretch-database-catalog-views---sysremote_data_archive_tables"></a>Stretch Database exibições do catálogo-sys. remote_data_archive_tables
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada tabela remota que armazena dados de uma tabela local habilitada para Stretch.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|A ID de objeto da tabela local habilitada para Stretch.|  
|**remote_database_id**|**int**|O identificador local gerado automaticamente do banco de dados remoto.|  
|**remote_table_name**|**sysname**|O nome da tabela no banco de dados remoto que corresponde à tabela local habilitada para Stretch.|  
|**filter_predicate**|**nvarchar(max)**|O predicado de filtro, se houver, que identifica linhas na tabela a ser migrada. Se o valor for nulo, a tabela inteira poderá ser migrada.<br /><br /> Para obter mais informações, consulte [habilitar Stretch Database para uma tabela](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md) e [selecionar linhas para migrar usando um predicado de filtro](~/sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md).|  
|**migration_direction**|**tinyint**|A direção na qual os dados estão sendo migrados no momento. Os valores disponíveis são os seguintes.<br/>1 (saída)<br/>2 (entrada)|  
|**migration_direction_desc**|**nvarchar(60)**|A descrição da direção na qual os dados estão sendo migrados no momento. Os valores disponíveis são os seguintes.<br/>saída (1)<br/>entrada (2)|  
|**is_migration_paused**|**bit**|Indica se a migração está em pausa no momento.|  
|**is_reconciled**|**bit**| Indica se a tabela remota e a tabela de SQL Server estão em sincronia.<br/><br/>Quando o valor de **is_reconciled** é 1 (true), a tabela remota e a tabela de SQL Server estão em sincronia, e você pode executar consultas que incluem os dados remotos.<br/><br/>Quando o valor de **is_reconciled** é 0 (false), a tabela remota e a tabela de SQL Server não estão em sincronia. As linhas migradas recentemente precisam ser migradas novamente. Isso ocorre quando você restaura o banco de dados remoto do Azure ou quando você exclui as linhas manualmente da tabela remota. Até que você reconcilie as tabelas, não será possível executar consultas que incluam os dados remotos. Para reconciliar as tabelas, execute [Sys. sp_rda_reconcile_batch](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-batch-transact-sql.md). |  
  
## <a name="see-also"></a>Consulte Também  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  

