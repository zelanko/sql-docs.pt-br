---
title: conjunto de backup (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- backupset
- backupset_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backupset system table
- backup media [SQL Server], backupset system table
- backup sets [SQL Server]
ms.assetid: 6ff79bbf-4acf-4f75-926f-38637ca8a943
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b138a299edbb1e9f3a2314e92b7e77418594a711
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68119328"
---
# <a name="backupset-transact-sql"></a>backupset (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  Contém uma linha para cada conjunto de backup. Um *conjunto de backup* contém o backup de uma única operação de backup bem-sucedida. As instruções RESTORE, RESTORE FILELISTONLY, RESTORE HEADERONLY e RESTORE VERIFYONLY funcionam em um único conjunto de backups dentro do conjunto de mídias no dispositivo de backup ou dispositivos especificados.  
  
 Essa tabela é armazenada no banco de dados **msdb** .  

  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**backup_set_id**|**int**|Número de identificação exclusivo de conjunto de backup que o identifica. Identidade, chave primária.|  
|**backup_set_uuid**|**uniqueidentifier**|Número de identificação exclusivo de conjunto de backup que o identifica.|  
|**media_set_id**|**int**|Número de identificação exclusivo de conjunto de mídia que identifica o conjunto de mídia contendo o conjunto de backup. Faz referência a **backupmediaset (media_set_id)**.|  
|**first_family_number**|**tinyint**|Número de família da mídia em que conjunto de backup é iniciado. Pode ser NULL.|  
|**first_media_number**|**smallint**|Número de mídia da mídia em que conjunto de backup é iniciado. Pode ser NULL.|  
|**last_family_number**|**tinyint**|Número de família da mídia em que conjunto de backup é encerrado. Pode ser NULL.|  
|**last_media_number**|**smallint**|Número de mídia da mídia em que conjunto de backup é encerrado. Pode ser NULL.|  
|**catalog_family_number**|**tinyint**|Número de família da mídia que contém o início do diretório de conjunto de backup. Pode ser NULL.|  
|**catalog_media_number**|**smallint**|Número de mídia da mídia que contém o início do diretório de conjunto de backup. Pode ser NULL.|  
|**propostas**|**int**|Posição de backup usada na operação de restauração para localizar o conjunto de backup e arquivos apropriados. Pode ser NULL. Para obter mais informações, consulte arquivo em [BACKUP &#40;&#41;Transact-SQL ](../../t-sql/statements/backup-transact-sql.md).|  
|**expiration_date**|**datetime**|Data e hora de vencimento do conjunto de backup. Pode ser NULL.|  
|**software_vendor_id**|**int**|Número de identificação do fornecedor de software que escreve o cabeçalho de mídia de backup. Pode ser NULL.|  
|**name**|**nvarchar(128)**|Nome do conjunto de backup. Pode ser NULL.|  
|**ndescrição**|**nvarchar (255)**|Descrição do conjunto de backup. Pode ser NULL.|  
|**user_name**|**nvarchar(128)**|Nome do usuário que realizou a operação de backup. Pode ser NULL.|  
|**software_major_version**|**tinyint**|[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] número de versão principal. Pode ser NULL.|  
|**software_minor_version**|**tinyint**|Número de versão secundário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Pode ser NULL.|  
|**software_build_version**|**smallint**|Número de compilação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Pode ser NULL.|  
|**time_zone**|**smallint**|Diferença entre a hora local (onde a operação de backup está acontecendo) e o UTC (Tempo Universal Coordenado) em intervalos de 15 minutos. Os valores podem ser de -48 a +48, inclusive. Um valor de 127 indica que é desconhecido. Por exemplo, -20 é Hora Padrão do Leste dos EUA ou cinco horas após o UTC. Pode ser NULL.|  
|**mtf_minor_version**|**tinyint**|Número de versão secundário de formato de fita da [!INCLUDE[msCoName](../../includes/msconame-md.md)]. Pode ser NULL.|  
|**first_lsn**|**numeric(25,0)**|Número de sequência de log do primeiro ou mais antigo registro de log no conjunto de backup. Pode ser NULL.|  
|**last_lsn**|**numeric(25,0)**|Número de sequência de log do próximo registro de log após o conjunto de backup. Pode ser NULL.|  
|**checkpoint_lsn**|**numeric(25,0)**|Número de sequência de log do registro de log em que a operação de refazer deve ser iniciada. Pode ser NULL.|  
|**database_backup_lsn**|**numeric(25,0)**|Número de sequência de log do backup de banco de dados completo mais recente. Pode ser NULL.<br /><br /> **database_backup_lsn** é o "início do ponto de verificação" que é disparado quando o backup é iniciado. Esse LSN coincidirá com **first_lsn** se o backup for feito quando o banco de dados estiver ocioso e nenhuma replicação for configurada.|  
|**database_creation_date**|**datetime**|Data e hora em que o banco de dados foi originalmente criado. Pode ser NULL.|  
|**backup_start_date**|**datetime**|Data e hora em que a operação de backup foi iniciada. Pode ser NULL.|  
|**backup_finish_date**|**datetime**|Data e hora em que a operação de backup foi concluída. Pode ser NULL.|  
|**type**|**Char (1)**|Tipo de backup. Pode ser:<br /><br /> D = Banco de dados<br /><br /> I = Banco de dados diferencial<br /><br /> L = Log<br /><br /> G = Arquivo ou grupo de arquivos<br /><br /> G = Arquivo diferencial<br /><br /> P = Parcial<br /><br /> Q = Parcial diferencial<br /><br /> Pode ser NULL.|  
|**sort_order**|**smallint**|Ordem de classificação do servidor que está executando a operação de backup. Pode ser NULL. Para obter mais informações sobre ordens de classificação e agrupamentos, consulte [suporte a agrupamentos e a Unicode](../../relational-databases/collations/collation-and-unicode-support.md).|  
|**code_page**|**smallint**|Página de código do servidor que está executando a operação de backup. Pode ser NULL. Para obter mais informações sobre páginas de código, consulte [agrupamento e suporte a Unicode](../../relational-databases/collations/collation-and-unicode-support.md).|  
|**compatibility_level**|**tinyint**|Configuração de nível de compatibilidade para o banco de dados. Pode ser:<br /><br /> 90 = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]<br /><br /> 100 = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]<br /><br /> 110 = [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]<br /><br /> 120 = [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]<br /><br /> Pode ser NULL.<br /><br /> Para obter mais informações sobre níveis de compatibilidade, veja [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).|  
|**database_version**|**int**|Número de versão de banco de dados. Pode ser NULL.|  
|**backup_size**|**numeric(20,0)**|Tamanho do conjunto de backup, em bytes. Pode ser NULL. Para backups VSS, backup_size é um valor estimado.|  
|**database_name**|**nvarchar(128)**|Nome do banco de dados envolvido na operação de backup. Pode ser NULL.|  
|**server_name**|**nvarchar(128)**|Nome do servidor que está executando a operação de backup do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Pode ser NULL.|  
|**machine_name**|**nvarchar(128)**|Nome do computador que executa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Pode ser NULL.|  
|**sinalizadores**|**int**|No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a coluna **sinalizadores** foi preterida e está sendo substituída pelas seguintes colunas de bits:<br /><br /> **has_bulk_logged_data** <br /> **is_snapshot** <br /> **is_readonly** <br /> **is_single_user** <br /> **has_backup_checksums** <br /> **is_damaged** <br /> **begins_log_chain** <br /> **has_incomplete_metadata** <br /> **is_force_offline** <br /> **is_copy_only**<br /><br /> Pode ser NULL.<br /><br /> Em conjuntos de backup de versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], os bits de sinalizador:<br />1 = Backup contém dados registrados minimamente. <br />2 = WITH SNAPSHOT foi usado. <br />4 = Banco de dados era somente leitura na hora do backup.<br />8 = Banco de dados estava no modo de usuário único na hora do backup.|  
|**unicode_locale**|**int**|Localidade Unicode. Pode ser NULL.|  
|**unicode_compare_style**|**int**|Estilo de comparação Unicode. Pode ser NULL.|  
|**collation_name**|**nvarchar(128)**|Nome da ordenação. Pode ser NULL.|  
|**Is_password_protected**|**bit**|É o conjunto de backup<br /><br /> protegido por senha:<br /><br /> 0 = Não protegido<br /><br /> 1 = Protegido|  
|**recovery_model**|**nvarchar(60)**|Modelo de recuperação do banco de dados:<br /><br /> FULL<br /><br /> BULK-LOGGED<br /><br /> SIMPLES|  
|**has_bulk_logged_data**|**bit**|1 = Backup contém dados bulk-logged.|  
|**is_snapshot**|**bit**|1 = Backup usado com a opção SNAPSHOT.|  
|**is_readonly**|**bit**|1 = Banco de dados era somente leitura na hora do backup.|  
|**is_single_user**|**bit**|1 = Banco de dados era de usuário único na hora do backup.|  
|**has_backup_checksums**|**bit**|1 = Backup contém somas de verificação de backup.|  
|**is_damaged**|**bit**|1 = Dano no banco de dados foi detectado quando esse backup foi criado. A operação de backup foi solicitada a continuar apesar dos erros.|  
|**begins_log_chain**|**bit**|1 = Este é o primeiro em uma cadeia contínua de backups de log. Uma cadeia de logs é iniciada com o primeiro backup de log usado depois que o banco de dados é criado ou quando é alternado do modelo de recuperação simples para o completo ou bulk-logged.|  
|**has_incomplete_metadata**|**bit**|1 = Um backup da parte final do log com metadados incompletos. Para obter mais informações, veja [Backups da parte final do log &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md).|  
|**is_force_offline**|**bit**|1 = Banco de dados usado offline que usou a opção NORECOVERY quando o backup foi feito.|  
|**is_copy_only**|**bit**|1 = Um backup somente cópia. Para obter mais informações, veja [Backups somente cópia &#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md).|  
|**first_recovery_fork_guid**|**uniqueidentifier**|ID da bifurcação de recuperação inicial. Isso corresponde a **FirstRecoveryForkID** de HEADERONLY de restauração.<br /><br /> Para backups de dados, **first_recovery_fork_guid** é igual a **last_recovery_fork_guid**.|  
|**last_recovery_fork_guid**|**uniqueidentifier**|ID da bifurcação de recuperação final. Isso corresponde a **RecoveryForkID** de HEADERONLY de restauração.<br /><br /> Para backups de dados, **first_recovery_fork_guid** é igual a **last_recovery_fork_guid**.|  
|**fork_point_lsn**|**numeric(25,0)**|Se **first_recovery_fork_guid** não for igual a **last_recovery_fork_guid**, esse será o número de sequência de log do ponto de bifurcação. Caso contrário, o valor será NULL.|  
|**database_guid**|**uniqueidentifier**|ID exclusiva para o banco de dados. Isso corresponde a **BindingId** de RESTORE HEADERONLY. Quando o banco de dados é restaurado, um valor novo é atribuído.|  
|**family_guid**|**uniqueidentifier**|ID exclusiva do banco de dados original na criação. Este valor permanece o mesmo quando o banco de dados é restaurado, mesmo para um nome diferente.|  
|**differential_base_lsn**|**numeric(25,0)**|LSN base para backups diferenciais. Para um backup diferencial com base em um único; as alterações com LSNs maior ou igual a **differential_base_lsn** são incluídas no backup diferencial.<br /><br /> Para um diferencial multibase, o valor é NULL e o LSN base deve ser determinado no nível do arquivo (consulte [backupfile &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)).<br /><br /> Para tipos de backup não diferencial, o valor é sempre NULL.|  
|**differential_base_guid**|**uniqueidentifier**|Para um backup diferencial de base única, o valor é o identificador exclusivo da base diferencial.<br /><br /> Para diferenciais com várias bases, o valor é NULL, e a base diferencial deve ser determinada em nível de arquivo.<br /><br /> Para tipos de backup não diferencial, o valor é NULL.|  
|**compressed_backup_size**|**Numeric (20, 0)**|Contagem total de bytes do backup armazenado em disco.<br /><br /> Para calcular a taxa de compactação, use **compressed_backup_size** e **backup_size**.<br /><br /> Durante uma atualização do **msdb** , esse valor é definido como nulo. o que indica um backup não compactado.|  
|**key_algorithm**|**nvarchar(32)**|O algoritmo de criptografia usado para criptografar o backup. O valor de NO_Encryption indica que o backup não foi criptografado.|  
|**encryptor_thumbprint**|**varbinary(20)**|A impressão digital do criptografador que pode ser usada para localizar o certificado ou chave assimétrica no banco de dados. Quando o backup não tiver sido criptografado, esse valor será NULL.|  
|**encryptor_type**|**nvarchar(32)**|O tipo de criptografador usado: certificado ou chave assimétrica. . Quando o backup não tiver sido criptografado, esse valor será NULL.|  
  
## <a name="remarks"></a>Comentários  
 RESTOre VERIFYONLY de *backup_device* com LOADHISTORY popula a coluna da tabela **backupmediaset** com os valores apropriados do cabeçalho conjunto de mídias.  
  
 Para reduzir o número de linhas nesta tabela e em outras tabelas de backup e histórico, execute o procedimento armazenado [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) .  
  
## <a name="see-also"></a>Consulte Também  
 [Backup e restauração de tabelas &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [backupfile &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)   
 [&#41;backupfilegroup &#40;Transact-SQL](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)   
 [&#41;backupmediafamily &#40;Transact-SQL](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)   
 [&#41;backupmediaset &#40;Transact-SQL](../../relational-databases/system-tables/backupmediaset-transact-sql.md)   
 [Erros de mídia possíveis durante backup e restauração &#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md)   
 [Conjuntos de mídias, famílias de mídia e conjuntos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [Modelos de recuperação &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)   
 [RESTAURAR HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)   
 [Backup e restauração de tabelas &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)  
  
  
