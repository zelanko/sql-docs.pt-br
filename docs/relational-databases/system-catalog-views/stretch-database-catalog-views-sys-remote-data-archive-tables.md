---
title: sys. remote_data_archive_tables (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: ''
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
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5d71c317ef36f254f83af70b3b4a2b2428fcbfa4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32974641"
---
# <a name="stretch-database-catalog-views---sysremotedataarchivetables"></a>Ampliar as exibições do catálogo de banco de dados - remote_data_archive_tables
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada tabela remota que armazena dados de uma tabela local habilitada para ampliação.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**Int**|A ID de objeto da tabela local habilitada para ampliação.|  
|**remote_database_id**|**Int**|O identificador de local gerado automaticamente do banco de dados remoto.|  
|**remote_table_name**|**sysname**|O nome da tabela no banco de dados remoto que corresponde à tabela local habilitada para ampliação.|  
|**filter_predicate**|**nvarchar(max)**|O predicado de filtro, se houver, que identifica as linhas na tabela a ser migrado. Se o valor for nulo, a tabela inteira será qualificada para ser migrada.<br /><br /> Para obter mais informações, consulte [Enable Stretch Database para uma tabela](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md) e [selecionar linhas a serem migradas usando um predicado de filtro](~/sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md).|  
|**migration_direction**|**tinyint**|A direção na qual os dados no momento está sendo migrados. Os valores disponíveis são os seguintes.<br/>1 (saída)<br/>2 (entrada)|  
|**migration_direction_desc**|**nvarchar(60)**|A descrição da direção na qual os dados no momento está sendo migrados. Os valores disponíveis são os seguintes.<br/>saída (1)<br/>entrada (2)|  
|**is_migration_paused**|**bit**|Indica se a migração está em pausa.|  
|**is_reconciled**|**bit**| Indica se a tabela remota e a tabela do SQL Server estão em sincronia.<br/><br/>Quando o valor de **is_reconciled** é 1 (true), a tabela remota e a tabela do SQL Server estão em sincronia e você pode executar consultas que incluem os dados remotos.<br/><br/>Quando o valor de **is_reconciled** é 0 (false), a tabela remota e a tabela do SQL Server não estão em sincronia. Recentemente linhas migradas precisam ser migrado novamente. Isso ocorre quando você restaura o banco de dados remoto do Azure, ou quando você excluir manualmente linhas da tabela remota. Até que você reconciliar as tabelas, você não pode executar consultas que incluem os dados remotos. Para reconciliar as tabelas, executar [sp_rda_reconcile_batch](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-batch-transact-sql.md). |  
  
## <a name="see-also"></a>Consulte também  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  

