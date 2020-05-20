---
title: sys. database_files (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/19/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.database_files
- sys.database_files_TSQL
- database_files
- database_files_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_files catalog view
ms.assetid: 0f5b0aac-c17d-4e99-b8f7-d04efc9edf44
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f51c090baea876c662b3fa31210d1eec59139bf4
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82823479"
---
# <a name="sysdatabase_files-transact-sql"></a>sys.database_files (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Contém uma fila por arquivo de um banco de dados, conforme armazenado no próprio banco de dados. Esta é uma exibição por banco de dados.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**file_id**|**int**|ID do arquivo no banco de dados.|  
|**file_guid**|**uniqueidentifier**|GUID do arquivo.<br /><br /> NULL = o banco de dados foi atualizado de uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (válido para SQL Server 2005 e anterior).|  
|**tipo**|**tinyint**|Tipo de arquivo:<br/><br /> 0 = linhas<br /><br/> 1 = Log<br/><br /> 2 = FILESTREAM<br /><br /> 3 =[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> 4 = texto completo|  
|**type_desc**|**nvarchar(60)**|Descrição do tipo de arquivo:<br /><br /> ROWS <br /><br /> LOG<br /><br /> FILESTREAM<br /><br /> FULLTEXT|  
|**data_space_id**|**int**|O valor pode ser 0 ou maior que 0. Um valor igual a 0 representa o arquivo de log do banco de dados, e um valor maior que 0 representa a ID do grupo de arquivos no qual os dados estão armazenados.|  
|**name**|**sysname**|Nome lógico do arquivo no banco de dados.|  
|**physical_name**|**nvarchar(260)**|Nome de arquivo do sistema operacional. Se o banco de dados for hospedado por uma [réplica secundária legível](../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)AlwaysOn, **physical_name** indicará o local do arquivo do banco de dados de réplica primária. Para o local de arquivo correto de um banco de dados secundário legível, consulte [Sys. sysaltfiles](../../relational-databases/system-compatibility-views/sys-sysaltfiles-transact-sql.md).|  
|**state**|**tinyint**|Estado do arquivo:<br /><br /> 0 = ONLINE<br /><br /> 1 = RESTORING<br /><br /> 2 = RECOVERING<br /><br /> 3 = RECOVERY_PENDING<br /><br /> 4 = SUSPECT<br /><br /> 5 = [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> 6 = OFFLINE<br /><br /> 7 = DEFUNCT|  
|**state_desc**|**nvarchar(60)**|Descrição do estado do arquivo:<br /><br /> ONLINE<br /><br /> RESTORING<br /><br /> RECOVERING<br /><br /> RECOVERY_PENDING<br /><br /> SUSPECT<br /><br /> OFFLINE<br /><br /> DEFUNCT<br /><br /> Para obter mais informações, consulte [Estados de arquivo](../../relational-databases/databases/file-states.md).|  
|**size**|**int**|Tamanho atual do arquivo, em páginas de 8 KB.<br /><br /> 0 = Não aplicável<br /><br /> Para um instantâneo do banco de dados, tamanho reflete o espaço máximo que o instantâneo poderá usar para o arquivo.<br /><br /> Para contêineres de grupo de arquivos FILESTREAM, o tamanho reflete o tamanho atual usado do contêiner.|  
|**max_size**|**int**|Tamanho de arquivo máximo, em páginas de 8 KB:<br /><br /> 0 = Crescimento não é permitido.<br /><br /> -1 = Arquivo crescerá até que o disco esteja completo.<br /><br /> 268435456 = Arquivo de log crescerá a um tamanho máximo de 2 TB.<br /><br /> Para contêineres de grupo de arquivos FILESTREAM, max_size reflete o tamanho máximo do contêiner.<br /><br /> Observe que os bancos de dados que são atualizados com um tamanho de arquivo de log ilimitado relatarão-1 para o tamanho máximo do arquivo de log.|  
|**growth**|**int**|0 = Arquivo tem tamanho fixo e não crescerá.<br /><br /> >0 = o arquivo aumentará automaticamente.<br /><br /> Se is_percent_growth = 0, o incremento de crescimento estará em unidades de 8 KB de páginas, arredondado para o 64 KB mais próximo.<br /><br /> Se is_percent_growth = 1, o incremento de crescimento será expresso em porcentagem de número inteiro.|  
|**is_media_read_only**|**bit**|1 = O arquivo está em mídia somente leitura.<br /><br /> 0 = O arquivo está em mídia de leitura/gravação.|  
|**is_read_only**|**bit**|1 = Arquivo está marcado como somente leitura.<br /><br /> 0 = O arquivo está marcado como leitura/gravação.|  
|**is_sparse**|**bit**|1 = O arquivo é um arquivo esparso.<br /><br /> 0 = O arquivo não é um arquivo esparso.<br /><br /> Para obter mais informações, consulte [Exibir o tamanho do arquivo esparso de um instantâneo de banco de dados &#40;Transact-SQL&#41;](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md).|  
|**is_percent_growth**|**bit**|1 = Crescimento do arquivo é uma porcentagem.<br /><br /> 0 = Tamanho de crescimento absoluto em páginas.|  
|**is_name_reserved**|**bit**|1 = Nome de arquivo descartado (name ou physical_name) só é reutilizável após o backup de log seguinte. Quando arquivos são descartados de um banco de dados, os nomes lógicos ficam em um estado reservado até o próximo backup de log. Essa coluna é relevante apenas no modelo de recuperação completa ou no modelo de recuperação bulk-logged.|  
|**create_lsn**|**numeric(25,0)**|Número de sequência de log (LSN) no qual o arquivo foi criado.|  
|**drop_lsn**|**numeric(25,0)**|LSN no qual o arquivo foi descartado.<br /><br /> 0 = O nome do arquivo não está disponível para ser usado novamente.|  
|**read_only_lsn**|**numeric(25,0)**|LSN do grupo de arquivos que contém o arquivo alterado de leitura/gravação para somente leitura (a mudança mais recente).|  
|**read_write_lsn**|**numeric(25,0)**|LSN no qual o grupo de arquivos que contém o arquivo foi alterado de somente leitura para leitura/gravação (a mudança mais recente).|  
|**differential_base_lsn**|**numeric(25,0)**|Base para backups diferenciais. Extensões de dados alteradas depois desse LSN serão incluídas em um backup diferencial.|  
|**differential_base_guid**|**uniqueidentifier**|Identificador exclusivo do backup de base no qual um backup diferencial será baseado.|  
|**differential_base_time**|**datetime**|Hora que corresponde a differential_base_lsn.|  
|**redo_start_lsn**|**numeric(25,0)**|LSN no qual o próximo roll forward deve ser iniciado.<br /><br /> Será NULL a menos que estado = RESTORING ou estado = RECOVERY_PENDING.|  
|**redo_start_fork_guid**|**uniqueidentifier**|O identificador exclusivo da bifurcação da recuperação. O first_fork_guid do próximo backup de log restaurado deve corresponder a este valor. Isso representa o estado atual do arquivo.|  
|**redo_target_lsn**|**numeric(25,0)**|LSN no qual a rolagem para frente online neste arquivo pode ser interrompida.<br /><br /> Será NULL a menos que estado = RESTORING ou estado = RECOVERY_PENDING.|  
|**redo_target_fork_guid**|**uniqueidentifier**|A bifurcação de recuperação na qual o arquivo pode ser recuperado. Associado a redo_target_lsn.|  
|**backup_lsn**|**numeric(25,0)**|O LSN do backup de dados ou diferencial mais recente do arquivo.|  
  
> [!NOTE]  
>  Quando você descarta ou reconstrói índices grandes, ou descarta ou trunca tabelas grandes, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] adia as desalocações de página atuais e seus bloqueios associados, até depois que a transação confirme. Operações de cancelamento adiadas não libertam espaço alocado imediatamente. Portanto, os valores retornados por sys.database_files, imediatamente depois de descartar ou truncar um objeto grande podem não refletir o espaço de disco real disponível.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  

## <a name="examples"></a>Exemplos  
A instrução a seguir retorna o nome, o tamanho do arquivo e a quantidade de espaço vazio para cada arquivo de banco de dados.

```
SELECT name, size/128.0 FileSizeInMB,
size/128.0 - CAST(FILEPROPERTY(name, 'SpaceUsed') AS int)/128.0 
   AS EmptySpaceInMB
FROM sys.database_files;
```
Para obter mais informações ao usar o [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] , consulte [determinando o tamanho do banco de dados no banco de dados SQL do Azure V12](https://blogs.msdn.microsoft.com/sqlcat/2016/09/21/determining-database-size-in-azure-sql-database-v12/) no blog da equipe do SQL Customer Advisory.
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo de bancos de dados e arquivos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [Estados de arquivo](../../relational-databases/databases/file-states.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys. master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [Arquivos de banco de dados e grupos de arquivo](../../relational-databases/databases/database-files-and-filegroups.md)   
 [sys.data_spaces &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)  
  
  
