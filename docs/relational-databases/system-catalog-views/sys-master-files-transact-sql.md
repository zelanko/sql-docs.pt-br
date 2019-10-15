---
title: sys. master_files (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/10/2016
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.master_files
- master_files_TSQL
- sys.master_files_TSQL
- master_files
dev_langs:
- TSQL
helpviewer_keywords:
- sys.master_files catalog view
ms.assetid: 803b22f2-0016-436b-a561-ce6f023d6b6a
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2aa7c30f132f0c0e8774dcb39f31e1a254e8689c
ms.sourcegitcommit: c7a202af70fd16467a498688d59637d7d0b3d1f3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72313715"
---
# <a name="sysmaster_files-transact-sql"></a>sys.master_files (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  Contém uma fila por arquivo de um banco de dados, como armazenado no banco de dados mestre. Essa é uma exibição única que abrange todo o sistema.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|database_id|**int**|ID do banco de dados ao qual este arquivo se aplica. O masterdatabase_id é sempre 1.|  
|file_id|**int**|ID do arquivo no banco de dados. O file_id primário sempre é 1.|  
|file_guid|**uniqueidentifier**|Identificador exclusivo do arquivo.<br /><br /> NULL = o banco de dados foi atualizado de uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (válido para SQL Server 2005 e anterior).|  
|type|**tinyint**|Tipo de arquivo:<br /><br /> 0 = linhas.<br /><br /> 1 = Log<br /><br /> 2 = FILESTREAM<br /><br /> 3 = [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> 4 = texto completo (catálogos de texto completo anteriores ao [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]; catálogos de texto completo atualizados para ou criados no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou superior informarão um tipo de arquivo 0.)|  
|type_desc|**nvarchar(60)**|Descrição do tipo de arquivo:<br /><br /> ROWS<br /><br /> LOG<br /><br /> FILESTREAM<br /><br /> FULLTEXT (catálogos de texto completo anteriores ao [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].)|  
|data_space_id|**int**|ID do espaço de dados ao qual pertence o arquivo. Espaço de dados é um grupo de arquivos.<br /><br /> 0 = Arquivos de log|  
|name|**sysname**|Nome lógico do arquivo no banco de dados.|  
|physical_name|**nvarchar(260)**|Nome de arquivo do sistema operacional.|  
|state|**tinyint**|Estado do arquivo:<br /><br /> 0 = ONLINE<br /><br /> 1 = RESTORING<br /><br /> 2 = RECOVERING<br /><br /> 3 = RECOVERY_PENDING<br /><br /> 4 = SUSPECT<br /><br /> 5 = [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> 6 = OFFLINE<br /><br /> 7 = DEFUNCT|  
|state_desc|**nvarchar(60)**|Descrição do estado do arquivo:<br /><br /> ONLINE<br /><br /> RESTORING<br /><br /> RECOVERING<br /><br /> RECOVERY_PENDING<br /><br /> SUSPECT<br /><br /> OFFLINE<br /><br /> DEFUNCT<br /><br /> Para obter mais informações, consulte [Estados de arquivo](../../relational-databases/databases/file-states.md).|  
|size|**int**|Tamanho de arquivo atual, em páginas de 8 KB. Para um instantâneo do banco de dados, tamanho reflete o espaço máximo que o instantâneo poderá usar para o arquivo.<br /><br /> Observação: Este campo é preenchido como zero para contêineres FILESTREAM. Consulte a exibição do catálogo *Sys. database_files* para obter o tamanho real dos contêineres FileStream.|  
|max_size|**int**|Tamanho de arquivo máximo, em páginas de 8 KB:<br /><br /> 0 = Crescimento não é permitido.<br /><br /> -1 = Arquivo crescerá até que o disco esteja completo.<br /><br /> 268435456 = Arquivo de log crescerá a um tamanho máximo de 2 TB.<br /><br /> Observação: Os bancos de dados que são atualizados com um tamanho de arquivo de log ilimitado relatarão-1 para o tamanho máximo do arquivo de log.|  
|growth|**int**|0 = Arquivo tem tamanho fixo e não crescerá.<br /><br /> > 0 = o arquivo aumentará automaticamente.<br /><br /> Se is_percent_growth = 0, incremento de crescimento está em unidades de páginas de 8 KB, arredondado ao mais próximo de 64 KB.<br /><br /> Se is_percent_growth = 1, o incremento de crescimento será expresso em porcentagem de número inteiro.|  
|is_media_read_onlyF|**bit**|1 = O arquivo está em mídia somente leitura.<br /><br /> 0 = Arquivo está em mídia leitura/gravação.|  
|is_read_only|**bit**|1 = Arquivo está marcado como somente leitura.<br /><br /> 0 = Arquivo está marcado como leitura/gravação.|  
|is_sparse|**bit**|1 = O arquivo é um arquivo esparso.<br /><br /> 0 = O arquivo não é um arquivo esparso.<br /><br /> Para obter mais informações, consulte [Exibir o tamanho do arquivo esparso de um instantâneo de banco de dados &#40;Transact-SQL&#41;](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md).|  
|is_percent_growth|**bit**|1 = Crescimento do arquivo é uma porcentagem.<br /><br /> 0 = Tamanho de crescimento absoluto em páginas.|  
|is_name_reserved|**bit**|1 = Nome de arquivo descartado é reutilizável. Um backup de log deve ser usado antes que o nome (name ou physical_name) seja usado de novo para um nome de arquivo novo.<br /><br /> 0 = O nome de arquivo está indisponível para ser usado novamente.|  
|create_lsn|**numeric(25,0)**|Número de sequência de log (LSN) no qual o arquivo foi criado.|  
|drop_lsn|**numeric(25,0)**|LSN no qual o arquivo foi descartado.|  
|read_only_lsn|**numeric(25,0)**|LSN do grupo de arquivos que contém o arquivo alterado de leitura/gravação para somente leitura (a mudança mais recente).|  
|read_write_lsn|**numeric(25,0)**|LSN no qual o grupo de arquivos que contém o arquivo foi alterado de somente leitura para leitura/gravação (a mudança mais recente).|  
|differential_base_lsn|**numeric(25,0)**|Base para backups diferenciais. Extensões de dados alteradas depois desse LSN serão incluídas em um backup diferencial.|  
|differential_base_guid|**uniqueidentifier**|Identificador exclusivo do backup de base no qual um backup diferencial será baseado.|  
|differential_base_time|**datetime**|Hora que corresponde a differential_base_lsn.|  
|redo_start_lsn|**numeric(25,0)**|LSN no qual o próximo roll forward deve ser iniciado.<br /><br /> Será NULL a menos que estado = RESTORING ou estado = RECOVERY_PENDING.|  
|redo_start_fork_guid|**uniqueidentifier**|O identificador exclusivo da bifurcação da recuperação. O first_fork_guid do próximo backup de log restaurado deve corresponder a este valor. Isso representa o estado atual do contêiner.|  
|redo_target_lsn|**numeric(25,0)**|LSN no qual a rolagem para frente online neste arquivo pode ser interrompida.<br /><br /> Será NULL a menos que estado = RESTORING ou estado = RECOVERY_PENDING.|  
|redo_target_fork_guid|**uniqueidentifier**|O ponto de bifurcação de recuperação no qual o contêiner pode ser recuperado. Associado a redo_target_lsn.|  
|backup_lsn|**numeric(25,0)**|O LSN do backup de dados ou diferencial mais recente do arquivo.|  
|credential_id|**int**|O `credential_id` de `sys.credentials` usado para armazenar o arquivo. Por exemplo, quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está em execução em uma máquina virtual do Azure e os arquivos de banco de dados são armazenados no armazenamento de BLOBs do Azure, uma credencial é configurada com as credenciais de acesso para o local de armazenamento.|  
  
> [!NOTE]  
>  Quando você descarta ou reconstrói índices grandes, ou descarta ou trunca tabelas grandes, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] adia as desalocações de página atuais e seus bloqueios associados, até depois que a transação confirme. Operações de cancelamento adiadas não libertam espaço alocado imediatamente. Então, os valores retornados por sys.master_files, imediatamente depois de descartar ou truncar um objeto grande podem não refletir o espaço de disco real disponível.  
  
## <a name="permissions"></a>Permissões  
 As permissões mínimas exigidas para ver a linha correspondente são CREATE DATABASE, ALTER ANY DATABASE ou VIEW ANY DEFINITION.  
  
## <a name="see-also"></a>Consulte também  
 [Exibição de catálogo do bancos de dados e de arquivos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [Estados de arquivo](../../relational-databases/databases/file-states.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [Arquivos e grupos de arquivos do banco de dados](../../relational-databases/databases/database-files-and-filegroups.md)  
  
  
