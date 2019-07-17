---
title: sys.dm_io_virtual_file_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_io_virtual_file_stats
- sys.dm_io_virtual_file_stats_TSQL
- sys.dm_io_virtual_file_stats
- dm_io_virtual_file_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_io_virtual_file_stats dynamic management function
ms.assetid: fa3e321f-6fe5-45ff-b397-02a0dd3d6b7d
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 524f0d82b5f426ae41169b8358dd8ad8be66da03
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67900286"
---
# <a name="sysdmiovirtualfilestats-transact-sql"></a>sys.dm_io_virtual_file_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

  Retorna estatísticas de E/S para arquivos de dados e de log. Essa exibição de gerenciamento dinâmico substitui o [fn_virtualfilestats](../../relational-databases/system-functions/sys-fn-virtualfilestats-transact-sql.md) função.  
  
> [!NOTE]  
>  Chamá-lo partir [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], use o nome **sys.dm_pdw_nodes_io_virtual_file_stats**. 

## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server and Azure SQL Database

sys.dm_io_virtual_file_stats (   
    { database_id | NULL },  
    { file_id | NULL }  
)  
```  

```  
-- Syntax for Azure SQL Data Warehouse

sys.dm_pdw_nodes_io_virtual_file_stats
```
  
## <a name="arguments"></a>Argumentos  


 *database_id* | NULL

 **APLICA-SE A:** SQL Server (começando com o 2008), o Banco de Dados SQL do Azure

 ID do banco de dados. *database_id* é int, sem padrão. São entradas válidas o número de ID de um banco de dados ou NULL. Quando NULL for especificado, serão retornados todos os bancos de dados na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 A função interna [DB_ID](../../t-sql/functions/db-id-transact-sql.md) pode ser especificado.  
  
*file_id* | NULL

**APLICA-SE A:** SQL Server (começando com o 2008), o Banco de Dados SQL do Azure
 
ID do arquivo. *file_id* é int, sem padrão. São entradas válidas o número de ID de um arquivo ou NULL. Quando NULL for especificado, serão retornados todos os arquivos do banco de dados.  
  
 A função interna [FILE_IDEX](../../t-sql/functions/file-idex-transact-sql.md) podem ser especificados e se refere a um arquivo de banco de dados atual.  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**database_name**|**sysname**|Nome do banco de dados.</br></br>Para o SQL Data Warehouse, esse é o nome do banco de dados armazenado no nó que é identificado por pdw_node_id. Cada nó tem um banco de dados do tempdb que tem 13 arquivos. Cada nó também tem um banco de dados por distribuição, e cada banco de dados de distribuição tem 5 arquivos. Por exemplo, se cada nó contém 4 distribuições, os resultados mostram 20 arquivos de banco de dados de distribuição por pdw_node_id. 
|**database_id**|**smallint**|ID do banco de dados.|  
|**file_id**|**smallint**|ID de arquivo.|  
|**sample_ms**|**bigint**|Número de milissegundos desde que o computador foi iniciado. Essa coluna pode ser usada para comparar saídas diferentes dessa função.</br></br>O tipo de dados é **int** para [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|**num_of_reads**|**bigint**|Número de leituras emitidas no arquivo.|  
|**num_of_bytes_read**|**bigint**|Número total de bytes lidos no arquivo.|  
|**io_stall_read_ms**|**bigint**|Tempo total, em milissegundos, que os usuários aguardaram pelas leituras emitidas no arquivo.|  
|**num_of_writes**|**bigint**|Número de gravações feitas no arquivo.|  
|**num_of_bytes_written**|**bigint**|Número total de bytes gravados no arquivo.|  
|**io_stall_write_ms**|**bigint**|Tempo total, em milissegundos, que os usuários aguardaram até o término das gravações no arquivo.|  
|**io_stall**|**bigint**|Tempo total, em milissegundos, que os usuários aguardaram até o término de E/S no arquivo.|  
|**size_on_disk_bytes**|**bigint**|Número de bytes do disco usado por esse arquivo. No caso de arquivos esparsos, esse número é o número real de bytes do disco que é utilizado para os instantâneos do banco de dados.|  
|**file_handle**|**varbinary**|Identificador de arquivo do Windows desse arquivo.|  
|**io_stall_queued_read_ms**|**bigint**|**Não é aplicável a:** : [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)].<br /><br /> Latência total de E/S apresentada pela administração do recurso de E/S para leituras. Não permite valor nulo. Para obter mais informações, consulte [DM resource_governor_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md).|  
|**io_stall_queued_write_ms**|**bigint**|**Não é aplicável a:** : [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)].<br /><br />  Latência total de E/S apresentada pela administração do recurso de E/S para gravações. Não permite valor nulo.|
|**pdw_node_id**|**int**|**Aplica-se a:** [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]</br></br>Identificador do nó para a distribuição.
 
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW SERVER STAT. Para obter mais informações, consulte [funções e exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md).  
  
## <a name="examples"></a>Exemplos  

### <a name="a-return-statistics-for-a-log-file"></a>A. Retornar as estatísticas para um arquivo de log

**Aplica-se a:** SQL Server (começando com o 2008), o Banco de Dados SQL do Azure

 O exemplo a seguir retorna todas as estatísticas do arquivo de log no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```sql  
SELECT * FROM sys.dm_io_virtual_file_stats(DB_ID(N'AdventureWorks2012'), 2);  
GO  
```  
  
### <a name="b-return-statistics-for-file-in-tempdb"></a>B. Retornar as estatísticas para o arquivo em tempdb

**Aplica-se a:** Azure SQL Data Warehouse

```sql
SELECT * FROM sys.dm_pdw_nodes_io_virtual_file_stats 
WHERE database_name = 'tempdb' AND file_id = 2;

```

## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Eu O relacionadas a funções e exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/i-o-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  

