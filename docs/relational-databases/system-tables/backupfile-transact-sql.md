---
title: backupfile (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- backupfile
- backupfile_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- file backups [SQL Server], backupfile system table
- backupfile system table
ms.assetid: f1a7fc0a-f4b4-47eb-9138-eebf930dc9ac
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c5c304cfafc04d9f7c0ec77dc5faedc75ada79df
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85890693"
---
# <a name="backupfile-transact-sql"></a>backupfile (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contém uma linha para cada arquivo de dados ou de log do banco de dados. As colunas descrevem a configuração de arquivo no momento em que o backup foi feito. Se o arquivo está ou não incluído no backup é determinado pela coluna **is_present** . Essa tabela é armazenada no banco de dados **msdb** .  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**backup_set_id**|**int**|Número de identificação exclusivo do arquivo que contém o conjunto de backup. Faz referência a **backupset (backup_set_id)**.|  
|**first_family_number**|**tinyint**|Número de família da primeira mídia que contém este arquivo de backup. Pode ser NULL.|  
|**first_media_number**|**smallint**|Número de mídia da primeira mídia que contém este arquivo de backup. Pode ser NULL.|  
|**filegroup_name**|**nvarchar(128)**|Nome do grupo de arquivos que contém um arquivo de banco de dados do qual foi feito backup. Pode ser NULL.|  
|**page_size**|**int**|Tamanho da página em bytes.|  
|**file_number**|**numeric (10, 0)**|Número de identificação do arquivo exclusivo em um banco de dados (corresponde a **Sys. database_files**.** file_id**).|  
|**backed_up_page_count**|**numeric (10, 0)**|Número de páginas das quais foi feito backup. Pode ser NULL.|  
|**file_type**|**Char (1)**|Arquivo do qual foi feito backup, um dos seguintes:<br /><br /> D = Arquivo de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> L = Arquivo de log do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> F = Catálogo de texto completo.<br /><br /> Pode ser NULL.|  
|**source_file_block_size**|**numeric (10, 0)**|Dispositivo no qual os dados originais ou o arquivo de log residiram durante o backup. Pode ser NULL.|  
|**file_size**|**numeric(20,0)**|Comprimento do arquivo do qual é feito backup em bytes. Pode ser NULL.|  
|**logical_name**|**nvarchar(128)**|Nome lógico do arquivo do qual é feito backup. Pode ser NULL.|  
|**physical_drive**|**nvarchar(260)**|Unidade física ou nome de partição. Pode ser NULL.|  
|**physical_name**|**nvarchar(260)**|Lembrete do nome de arquivo físico (sistema operacional). Pode ser NULL.|  
|**state**|**tinyint**|Estado do arquivo, um dos seguintes:<br /><br /> 0 = ONLINE<br /><br /> 1 = RESTORING<br /><br /> 2 = RECOVERING<br /><br /> 3 = RECOVERY PENDING<br /><br /> 4 = SUSPECT<br /><br /> 6 = OFFLINE<br /><br /> 7 = DEFUNCT<br /><br /> 8 = REMOVIDO<br /><br /> Observação: o valor 5 é ignorado para que esses valores correspondam aos valores dos Estados de banco de dados.|  
|**state_desc**|**nvarchar (64)**|Descrição do estado do arquivo, uma das seguintes:<br /><br /> ONLINE RESTORING<br /><br /> RECOVERING<br /><br /> RECOVERY_PENDING<br /><br /> SUSPECT OFFLINE DEFUNCT|  
|**create_lsn**|**numeric(25,0)**|Número da sequência de log na qual o arquivo foi criado.|  
|**drop_lsn**|**numeric(25,0)**|Número de sequência de log no qual o arquivo foi descartado. Pode ser NULL.<br /><br /> Se o arquivo não tiver sido descartado, esse valor será NULL.|  
|**file_guid**|**uniqueidentifier**|Identificador exclusivo do arquivo.|  
|**read_only_lsn**|**numeric(25,0)**|Número da sequência de log em que o grupo de arquivos que contém o arquivo alterado de leitura/gravação para somente leitura (a alteração mais recente). Pode ser NULL.|  
|**read_write_lsn**|**numeric(25,0)**|Número da sequência de log em que o grupo de arquivos que contém o arquivo alterado de somente leitura para leitura/gravação (a alteração mais recente). Pode ser NULL.|  
|**differential_base_lsn**|**numeric(25,0)**|LSN base para backups diferenciais. Um backup diferencial inclui apenas extensões de dados que têm um número de sequência de log igual ou maior que **differential_base_lsn**.<br /><br /> Para outros tipos de backup, o valor é NULL.|  
|**differential_base_guid**|**uniqueidentifier**|Para um backup diferencial, é o identificador exclusivo do backup de dados mais recente que forma a base diferencial do arquivo; se o valor for NULL, o arquivo foi incluído no backup diferencial, mas foi adicionado após a criação da base.<br /><br /> Para outros tipos de backup, o valor é NULL.|  
|**backup_size**|**numeric(20,0)**|Tamanho do backup do arquivo em bytes.|  
|**filegroup_guid**|**uniqueidentifier**|ID do grupo de arquivos. Para localizar informações de grupo de arquivos na tabela backupfilegroup, use **filegroup_guid** com **backup_set_id**.|  
|**is_readonly**|**bit**|1 = Arquivo somente leitura.|  
|**is_present**|**bit**|1 = Arquivo contido no conjunto de backup.|  
  
## <a name="remarks"></a>Comentários  
 RESTOre VERIFYONLY de *backup_device* com LOADHISTORY popula as colunas da tabela **backupmediaset** com os valores apropriados do cabeçalho conjunto de mídias.  
  
 Para reduzir o número de linhas nesta tabela e em outras tabelas de backup e histórico, execute o procedimento armazenado [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) .  
  
## <a name="see-also"></a>Consulte Também  
 [Backup e restauração de tabelas &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [backupfilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)   
 [backupmediafamily &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)   
 [backupmediaset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediaset-transact-sql.md)   
 [conjunto de backup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [Tabelas do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
