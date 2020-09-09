---
description: sys.tables (Transact-SQL)
title: sys. Tables (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- tables_TSQL
- sys.tables_TSQL
- sys.tables
- tables
dev_langs:
- TSQL
helpviewer_keywords:
- sys.tables catalog view
ms.assetid: 8c42eba1-c19f-4045-ac82-b97a5e994090
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d87bd3ec1361cbe3c038ff57bdde31c5593a4dbb
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543996"
---
# <a name="systables-transact-sql"></a>sys.tables (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Retorna uma linha para cada tabela de usuário no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|\<inherited columns>||Para obter uma lista de colunas que essa exibição herda, consulte [Sys. objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).|  
|lob_data_space_id|**int**|O valor diferente de zero é a ID do espaço de dados (esquema de partição ou grupo de arquivos) que armazena os dados de objeto binário grande (LOB) dessa tabela. Exemplos de tipos de dados LOB incluem **varbinary (max)**, **varchar (max)**, **geography**ou **XML**.<br /><br /> 0 = A tabela não contém dados LOB.|  
|filestream_data_space_id|**int**|É a ID do espaço de dados de um grupo de arquivos FILESTREAM ou de um esquema de partição que consiste em grupos de arquivos FILESTREAM.<br /><br /> Para relatar o nome de um grupo de arquivos FILESTREAM, execute a consulta `SELECT FILEGROUP_NAME (filestream_data_space_id) FROM sys.tables` .<br /><br /> sys.tables pode ser unido às seguintes exibições em filestream_data_space_id = data_space_id.<br /><br /> -sys. FileGroups<br /><br /> -sys. partition_schemes<br /><br /> -sys. Indexes<br /><br /> -sys. allocation_units<br /><br /> -sys. fulltext_catalogs<br /><br /> -sys. data_spaces<br /><br /> -sys. destination_data_spaces<br /><br /> -sys. master_files<br /><br /> -sys. database_files<br /><br /> -backupfilegroup (junção em filegroup_id)|  
|max_column_id_used|**int**|ID máxima de coluna já usada por esta tabela.|  
|lock_on_bulk_load|**bit**|A tabela é bloqueada em carregamento em massa. Para obter mais informações, veja [sp_tableoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md).|  
|uses_ansi_nulls|**bit**|A tabela foi criada com a opção de banco de dados SET ANSI_NULLS definida como ON.|  
|is_replicated|**bit**|1 = A tabela é publicada usando replicação de instantâneo ou replicação transacional.|  
|has_replication_filter|**bit**|1 = A tabela tem um filtro de replicação.|  
|is_merge_published|**bit**|1 = A tabela é publicada usando replicação de mesclagem.|  
|is_sync_tran_subscribed|**bit**|1 = A tabela é inscrita usando uma assinatura de atualização imediata.|  
|has_unchecked_assembly_data|**bit**|1 = A tabela contém dados persistentes que dependem de um assembly cuja definição foi alterada durante o último ALTER ASSEMBLY. Será redefinida como 0 depois do próximo DBCC CHECKDB ou DBCC CHECKTABLE bem-sucedido.|  
|text_in_row_limit|**int**|O máximo de bytes permitidos para texto em linha.<br /><br /> 0 = Texto em opção de linha não é definido. Para obter mais informações, veja [sp_tableoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md).|  
|large_value_types_out_of_row|**bit**|1 = Tipos de valor grande são armazenados fora de linha. Para obter mais informações, veja [sp_tableoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md).|  
|is_tracked_by_cdc|**bit**|1 = A tabela está habilitada para Change Data Capture. Para obter mais informações, consulte [Sys. sp_cdc_enable_table &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md).|  
|lock_escalation|**tinyint**|O valor da opção LOCK_ESCALATION da tabela:<br /><br /> 0 = TABLE<br /><br /> 1 = DISABLE<br /><br /> 2 = AUTO|  
|lock_escalation_desc|**nvarchar(60)**|Uma descrição de texto da opção lock_escalation da tabela. Os valores possíveis são: TABLE, AUTO e DISABLE.|  
|is_filetable|**bit**|**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior e [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)].<br /><br /> 1 = A tabela é uma FileTable.<br /><br /> Para obter mais informações sobre FileTables, veja [FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md).|  
|durabilidade|**tinyint**|**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior e [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)].<br /><br /> O valores possíveis são os seguintes:<br /><br /> 0 = SCHEMA_AND_DATA<br /><br /> 1 = SCHEMA_ONLY<br /><br /> O valor de 0 é o valor padrão.|  
|durability_desc|**nvarchar(60)**|**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior e [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)].<br /><br /> O valores possíveis são os seguintes:<br /><br /> SCHEMA_ONLY<br /><br /> SCHEMA_AND_DATA<br /><br /> O valor de SCHEMA_AND_DATA indica que a tabela é uma tabela na memória e durável. SCHEMA_AND_DATA é o valor padrão para tabelas com otimização de memória. O valor de SCHEMA_ONLY indica que os dados da tabela não serão mantidos na reinicialização do banco de dados com objetos com otimização de memória.|  
|is_memory_optimized|**bit**|**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior e [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)].<br /><br /> O valores possíveis são os seguintes:<br /><br /> 0 = sem otimização de memória.<br /><br /> 1 = com otimização de memória.<br /><br /> Um valor de 0 é o valor padrão.<br /><br /> As tabelas com otimização de memória são tabelas de usuário na memória, o esquema que é persistido em disco semelhante a outras tabelas de usuário. As tabelas otimizadas em memória podem ser acessadas de procedimentos armazenados compilados nativamente.|  
|temporal_type|**tinyint**|**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior e [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)].<br /><br /> O valor numérico que representa o tipo de tabela:<br /><br /> 0 = NON_TEMPORAL_TABLE<br /><br /> 1 = HISTORY_TABLE<br /><br /> 2 = SYSTEM_VERSIONED_TEMPORAL_TABLE|  
|temporal_type_desc|**nvarchar(60)**|**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior e [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)].<br /><br /> A descrição de texto do tipo de tabela:<br /><br /> NON_TEMPORAL_TABLE<br /><br /> HISTORY_TABLE<br /><br /> SYSTEM_VERSIONED_TEMPORAL_TABLE|  
|history_table_id|**int**|**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior e [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)].<br /><br /> Quando temporal_type em (2, 4) retorna object_id da tabela que mantém os dados históricos; caso contrário, retorna NULL.|  
|is_remote_data_archive_enabled|**bit**|**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior e [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)]<br /><br /> Indica se a tabela está habilitada para Stretch.<br /><br /> 0 = a tabela não está habilitada para Stretch.<br /><br /> 1 = a tabela é habilitada para Stretch.<br /><br /> Para obter mais informações, consulte [Stretch Database](../../sql-server/stretch-database/stretch-database.md).|  
|is_external|**bit**|**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior, [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)] e [!INCLUDE[sssdwfull](../../includes/sssdwfull-md.md)] .<br /><br /> Indica que a tabela é uma tabela externa.<br /><br /> 0 = a tabela não é uma tabela externa.<br /><br /> 1 = a tabela é uma tabela externa.| 
|history_retention_period|**int**|**Aplica-se a**: [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)]. <br/><br/>O valor numérico que representa a duração do período de retenção do histórico temporal em unidades especificadas com history_retention_period_unit. |  
|history_retention_period_unit|**int**|**Aplica-se a**: [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)]. <br/><br/>O valor numérico que representa o tipo de unidade de período de retenção do histórico temporal. <br /><br />-1: INFINITO <br /><br />3: DIA <br /><br />4: SEMANA <br /><br />5: MÊS <br /><br />6: ANO |  
|history_retention_period_unit_desc|**nvarchar (10)**|**Aplica-se a**: [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)]. <br/><br/>A descrição de texto do tipo de unidade do período de retenção do histórico temporal. <br /><br />INFINITE <br /><br />DAY <br /><br />WEEK <br /><br />MONTH <br /><br />YEAR |  
|is_node|**bit**|**Aplica-se a**: [!INCLUDE[sssql17-md.md](../../includes/sssql17-md.md)] e [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)]. <br/><br/>1 = Esta é uma tabela de nó de gráfico. <br /><br />0 = esta não é uma tabela de nó de gráfico. |  
|is_edge|**bit**|**Aplica-se a**: [!INCLUDE[sssql17-md.md](../../includes/sssql17-md.md)] e [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)]. <br/><br/>1 = Esta é uma tabela de borda do gráfico. <br /><br />0 = esta não é uma tabela de borda do gráfico. |  

## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna todas as tabelas de usuário que não possuem uma chave primária.  
  
```  
SELECT SCHEMA_NAME(schema_id) AS schema_name  
    ,name AS table_name   
FROM sys.tables   
WHERE OBJECTPROPERTY(object_id,'TableHasPrimaryKey') = 0  
ORDER BY schema_name, table_name;  
GO  
  
```  
  
O exemplo a seguir mostra como os dados temporais relacionados podem ser expostos.  
   
**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior e [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)].
  
```  
SELECT T1.object_id, T1.name as TemporalTableName, SCHEMA_NAME(T1.schema_id) AS TemporalTableSchema,  
T2.name as HistoryTableName, SCHEMA_NAME(T2.schema_id) AS HistoryTableSchema,  
T1.temporal_type_desc  
FROM sys.tables T1  
LEFT JOIN sys.tables T2   
ON T1.history_table_id = T2.object_id  
ORDER BY T1.temporal_type desc  
```  

O exemplo a seguir mostra como as informações sobre a retenção de histórico temporal podem ser expostas.  

**Aplica-se a**: [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)].  
  
```  
SELECT DB.is_temporal_history_retention_enabled, SCHEMA_NAME(T1.schema_id) AS TemporalTableSchema, 
T1.name as TemporalTableName, SCHEMA_NAME(T2.schema_id) AS HistoryTableSchema, T2.name as HistoryTableName,
T1.history_retention_period, T1.history_retention_period_unit_desc
FROM sys.tables T1  
OUTER APPLY (select is_temporal_history_retention_enabled from sys.databases where name = DB_NAME()) DB
LEFT JOIN sys.tables T2   
ON T1.history_table_id = T2.object_id WHERE T1.temporal_type = 2 
```  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)   
 [DBCC CHECKtable &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)   
 [Consultando as perguntas frequentes sobre o catálogo do sistema SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [OLTP in-memory &#40;Otimização na memória&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
