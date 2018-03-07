---
title: RESTORE HEADERONLY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/07/2016
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- HEADERONLY
- RESTORE HEADERONLY
- RESTORE_HEADERONLY_TSQL
- HEADERONLY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backup sets [SQL Server], header information
- headers [SQL Server]
- RESTORE HEADERONLY statement
- backup header information [SQL Server]
ms.assetid: 4b88e98c-49c4-4388-ab0e-476cc956977c
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 840793c4bbfee8282676cf90d42d6e7a6c4d6b42
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="restore-statements---headeronly-transact-sql"></a>Instruções - de RESTORE HEADERONLY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna um conjunto de resultados que contém todas as informações do cabeçalho de backup de todos os conjuntos de backup em um determinado dispositivo de backup no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Para obter as descrições dos argumentos, consulte [argumentos RESTORE &#40; Transact-SQL &#41; ](../../t-sql/statements/restore-statements-arguments-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
RESTORE HEADERONLY   
FROM <backup_device>   
[ WITH   
 {  
--Backup Set Options  
   FILE = { backup_set_file_number | @backup_set_file_number }   
 | PASSWORD = { password | @password_variable }   
  
--Media Set Options  
 | MEDIANAME = { media_name | @media_name_variable }   
 | MEDIAPASSWORD = { mediapassword | @mediapassword_variable }  
  
--Error Management Options  
 | { CHECKSUM | NO_CHECKSUM }   
 | { STOP_ON_ERROR | CONTINUE_AFTER_ERROR }  
  
--Tape Options  
 | { REWIND | NOREWIND }   
 | { UNLOAD | NOUNLOAD }    
 } [ ,...n ]  
]  
[;]  
  
<backup_device> ::=  
{   
   { logical_backup_device_name |  
      @logical_backup_device_name_var }  
   | { DISK | TAPE } = { 'physical_backup_device_name' |  
       @physical_backup_device_name_var }   
}  
  
```  
  
## <a name="arguments"></a>Argumentos  
 Para obter descrições dos argumentos RESTORE HEADERONLY, consulte [argumentos RESTORE &#40; Transact-SQL &#41; ](../../t-sql/statements/restore-statements-arguments-transact-sql.md).  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Para cada backup em um determinado dispositivo, o servidor envia uma linha de informações de cabeçalho com as seguintes colunas:  
  
> [!NOTE]  
>  RESTORE HEADERONLY examina todos os conjuntos de backup na mídia. Por esse motivo, a produção desse conjunto de resultados quando se utilizam unidades de fita de alta capacidade pode levar algum tempo. Para obter uma visão geral de mídia sem obter informações sobre cada conjunto de backup, use RESTORE LABELONLY ou especifique o arquivo  **=**  *backup_set_file_number*.  
  
> [!NOTE]  
>  Devido à natureza de [!INCLUDE[msCoName](../../includes/msconame-md.md)] formato de fita, é possível para conjuntos de backup de outros programas conseguem ocupar espaço na mesma mídia [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjuntos de backup. O conjunto de resultados retornado por RESTORE HEADERONLY inclui uma linha para cada um desses conjuntos de backup.  
  
|Nome da coluna|Tipo de dados|Descrição dos conjuntos de backup do SQL Server|  
|-----------------|---------------|--------------------------------------------|  
|**BackupName**|**nvarchar(128)**|Nome do conjunto de backup.|  
|**BackupDescription**|**nvarchar(255)**|Descrição do conjunto de backup.|  
|**BackupType**|**smallint**|Tipo de backup:<br /><br /> **1** = banco de dados<br /><br /> **2** = log de transações<br /><br /> **4** = arquivo<br /><br /> **5** = banco de dados diferencial<br /><br /> **6** = arquivo diferencial<br /><br /> **7** = Partial<br /><br /> **8** = parcial diferencial|  
|**ExpirationDate**|**datetime**|Data de vencimento do conjunto de backup.|  
|**Compactado**|**BYTE(1)**|Se o conjunto de backup é compactado com compactação de software:<br /><br /> **0** = No<br /><br /> **1** = Sim|  
|**Posição**|**smallint**|Posição do conjunto de backup no volume (para uso com o FILE = opção).|  
|**DeviceType**|**tinyint**|Número que corresponde ao dispositivo usado na operação de backup.<br /><br /> Disco:<br /><br /> **2** = Logical<br /><br /> **102** = físico<br /><br /> Fita:<br /><br /> **5** = Logical<br /><br /> **105** = Physical<br /><br /> Dispositivo virtual:<br /><br /> **7** = Logical<br /><br /> **107** = Physical<br /><br /> Nomes de dispositivo lógico e números de dispositivo estão em **backup_devices**; para obter mais informações, consulte [backup_devices &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-backup-devices-transact-sql.md).|  
|**UserName**|**nvarchar(128)**|Nome do usuário que realizou a operação de backup.|  
|**ServerName**|**nvarchar(128)**|Nome do servidor que gravou o conjunto de backup.|  
|**DatabaseName**|**nvarchar(128)**|Nome do banco de dados cujo backup foi feito.|  
|**DatabaseVersion**|**Int**|Versão do banco de dados a partir do qual o backup foi criado.|  
|**DatabaseCreationDate**|**datetime**|Date e hora em que o banco de dados foi criado.|  
|**BackupSize**|**numeric(20,0)**|Tamanho do backup em bytes.|  
|**FirstLSN**|**numeric(25,0)**|Número de sequência do primeiro registro de log no conjunto de backup.|  
|**LastLSN**|**numeric(25,0)**|Número de sequência de log do próximo registro de log após o conjunto de backup.|  
|**CheckpointLSN**|**numeric(25,0)**|Número de sequência de log do ponto de verificação mais recente no momento em que o backup foi criado.|  
|**DatabaseBackupLSN**|**numeric(25,0)**|Número de sequência de log do backup de banco de dados completo mais recente.<br /><br /> **DatabaseBackupLSN** é o "início do ponto de verificação" que é disparado quando o backup é iniciado. Esse LSN coincidirá com **FirstLSN** se o backup é feito quando o banco de dados estiver ocioso e nenhuma replicação for configurada.|  
|**BackupStartDate**|**datetime**|Date e hora em que a operação de backup começou.|  
|**BackupFinishDate**|**datetime**|Data e hora em que a operação de backup foi concluída.|  
|**SortOrder**|**smallint**|Ordem de classificação do servidor. Esta coluna só é válida para backups de banco de dados. Fornecido para compatibilidade com versões anteriores.|  
|**CodePage**|**smallint**|Página de código de servidor ou conjunto de caracteres usado pelo servidor.|  
|**UnicodeLocaleId**|**Int**|Opção de configuração de ID de localidade Unicode do servidor usada para classificar dados de caracteres Unicode. Fornecido para compatibilidade com versões anteriores.|  
|**UnicodeComparisonStyle**|**Int**|Opção de configuração de estilo de comparação Unicode do servidor que oferece controle adicional sobre a classificação dos dados Unicode. Fornecido para compatibilidade com versões anteriores.|  
|**CompatibilityLevel**|**tinyint**|Configuração do nível de compatibilidade do banco de dados a partir do qual o backup foi criado.|  
|**SoftwareVendorId**|**Int**|Número de conta de identificação do fornecedor de software. Para o SQL Server, esse número é **4608** (ou hexadecimal **0x1200**).|  
|**SoftwareVersionMajor**|**Int**|Número de versão principal do servidor que criou o conjunto de backup.|  
|**SoftwareVersionMinor**|**Int**|Número de versão secundário do servidor que criou o conjunto de backup.|  
|**SoftwareVersionBuild**|**Int**|Número de versão do servidor que criou o conjunto de backup.|  
|**MachineName**|**nvarchar(128)**|Nome do computador que realizou a operação de backup.|  
|**Flags**|**Int**|Significados dos bits de sinalizadores individuais se definido como **1**:<br /><br /> **1** = log de backup contém operações bulk-logged.<br /><br /> **2** = backup de instantâneo.<br /><br /> **4** = banco de dados era somente leitura quando o backup.<br /><br /> **8** = banco de dados estava no modo de usuário único quando o backup.<br /><br /> **16** = backup contém somas de verificação de backup.<br /><br /> **32** = banco de dados foi danificado durante o backup, mas a operação de backup foi solicitada a continuar apesar dos erros.<br /><br /> **64** = backup do final do log.<br /><br /> **128** = backup de log de final com metadados incompletos.<br /><br /> **256** = backup de log de final com NORECOVERY.<br /><br /> **Importante:** é recomendável que, em vez de **sinalizadores** você usar colunas de booliano individuais (listadas abaixo iniciando com **HasBulkLoggedData** e terminando com  **IsCopyOnly**).|  
|**BindingID**|**uniqueidentifier**|ID de associação do banco de dados. Isso corresponde à **sys.database_recovery_status***database_guid**. Quando o banco de dados é restaurado, um valor novo é atribuído. Consulte também **FamilyGUID** (abaixo).|  
|**RecoveryForkID**|**uniqueidentifier**|ID do ponto de bifurcação da recuperação final. Essa coluna corresponde a **last_recovery_fork_guid** no [backupset](../../relational-databases/system-tables/backupset-transact-sql.md) tabela.<br /><br /> Para backups de dados, **RecoveryForkID** é igual a **FirstRecoveryForkID**.|  
|**Agrupamento**|**nvarchar(128)**|Agrupamento usado pelo banco de dados.|  
|**FamilyGUID**|**uniqueidentifier**|ID do banco de dados original quando criado. Esse valor fica igual quando o banco de dados é restaurado.|  
|**HasBulkLoggedData**|**bit**|**1** = backup de log que contém operações bulk-logged.|  
|**IsSnapshot**|**bit**|**1** = backup de instantâneo.|  
|**IsReadOnly**|**bit**|**1** = banco de dados era somente leitura quando o backup.|  
|**IsSingleUser**|**bit**|**1** = banco de dados era de usuário único quando o backup.|  
|**HasBackupChecksums**|**bit**|**1** = backup contém somas de verificação de backup.|  
|**IsDamaged**|**bit**|**1** = banco de dados foi danificado durante o backup, mas a operação de backup foi solicitada a continuar apesar dos erros.|  
|**BeginsLogChain**|**bit**|**1** = este é o primeiro em uma cadeia contínua de backups de log. Uma cadeia de logs é iniciada com o primeiro backup de log feito após a criação do banco de dados ou quando é alternado do modelo de recuperação simples para completo ou bulk-logged.|  
|**HasIncompleteMetaData**|**bit**|**1** = backup da parte final do log com metadados incompletos.<br /><br /> Para obter informações sobre backups da parte final do log com backup incompleto de metadados, consulte [Backups da parte final do Log &#40; SQL Server &#41; ](../../relational-databases/backup-restore/tail-log-backups-sql-server.md).|  
|**IsForceOffline**|**bit**|**1** = backup feito com NORECOVERY; o banco de dados foi colocado offline pelo backup.|  
|**IsCopyOnly**|**bit**|**1** = um backup somente cópia.<br /><br /> Um backup somente cópia não causa impactos ao backup global e restaura procedimentos do banco de dados. Para obter mais informações, veja [Backups somente cópia &#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md).|  
|**FirstRecoveryForkID**|**uniqueidentifier**|ID da bifurcação da recuperação inicial. Essa coluna corresponde a **first_recovery_fork_guid** no [backupset](../../relational-databases/system-tables/backupset-transact-sql.md) tabela.<br /><br /> Para backups de dados, **FirstRecoveryForkID** é igual a **RecoveryForkID**.|  
|**ForkPointLSN**|**numeric(25,0)** NULL|Se **FirstRecoveryForkID** não é igual a **RecoveryForkID**, este é o número de sequência de log do ponto de bifurcação. Caso contrário, esse valor será NULL.|  
|**RecoveryModel**|**nvarchar(60)**|Modelo de recuperação do banco de dados, sendo:<br /><br /> FULL<br /><br /> BULK-LOGGED<br /><br /> SIMPLE|  
|**DifferentialBaseLSN**|**numeric(25,0)** NULL|Para um único backup diferencial de base, o valor é igual a **FirstLSN** da base diferencial; alterações com LSNs maiores que ou iguais a **DifferentialBaseLSN** são incluídas no diferencial.<br /><br /> Para um diferencial com várias bases, o valor é NULL e o LSN base deve ser determinado no nível de arquivo. Para obter mais informações, veja [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md).<br /><br /> Para tipos de backup não diferenciais, o valor é sempre NULL.<br /><br /> Para obter mais informações, veja [Backups diferenciais &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md).|  
|**DifferentialBaseGUID**|**uniqueidentifier**|Para um backup diferencial de base única, o valor é o identificador exclusivo da base diferencial.<br /><br /> Para diferenciais com várias bases, o valor é NULL, e a base do diferencial deve ser determinada por arquivo.<br /><br /> Para tipos de backup não diferenciais, o valor é NULL.|  
|**BackupTypeDescription**|**nvarchar(60)**|Tipo de backup como cadeia de caracteres, sendo:<br /><br /> DATABASE<br /><br /> TRANSACTION LOG<br /><br /> FILE OR FILEGROUP<br /><br /> DATABASE DIFFERENTIAL<br /><br /> FILE DIFFERENTIAL PARTIAL<br /><br /> PARTIAL DIFFERENTIAL|  
|**BackupSetGUID**|**uniqueidentifier** nulo|Número de identificação exclusivo do conjunto de backup pelo qual ele é identificado na mídia.|  
|**CompressedBackupSize**|**bigint**|Contagem de bytes do conjunto de backup. Para backups não compactados, esse valor é o mesmo que **BackupSize**.<br /><br /> Para calcular a taxa de compactação, use **CompressedBackupSize** e **BackupSize**.<br /><br /> Durante uma **msdb** atualização, esse valor é definido para corresponder ao valor da **BackupSize** coluna.|  
|**containment**|**tinyint** não NULL|**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Indica o status de contenção do banco de dados.<br /><br /> 0 = a contenção do banco de dados está desativada<br /><br /> 1 = o banco de dados está em contenção parcial|  
|**KeyAlgorithm**|**nvarchar(32)**|**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (CU1) até a versão atual.<br /><br /> O algoritmo de criptografia usado para criptografar o backup. NO_Encryption indica que o backup não foi criptografado. Quando não for possível determinar o valor correto, o valor deve ser NULL.|  
|**EncryptorThumbprint**|**varbinary(20)**|**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (CU1) até a versão atual.<br /><br /> A impressão digital do criptografador que pode ser usada para localizar o certificado ou chave assimétrica no banco de dados. Quando o backup não tiver sido criptografado, esse valor é NULL.|  
|**EncryptorType**|**nvarchar(32)**|**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (CU1) até a versão atual.<br /><br /> O tipo de criptografador usado: certificado ou chave assimétrica. Quando o backup não tiver sido criptografado, esse valor é NULL.|  
  
> [!NOTE]  
>  Se as senhas forem definidas para os conjuntos de backup, RESTORE HEADERONLY mostrará informações completas apenas para o conjunto de backup cuja senha corresponda à opção PASSWORD especificada do comando. RESTORE HEADERONLY também mostra informações completas de conjuntos de backup desprotegidos. O **BackupName** coluna para os outros protegido por senha conjuntos de backup na mídia é definida como ' * protegido por senha\*\*\*', e todas as outras colunas são NULL.  
  
## <a name="general-remarks"></a>Comentários gerais  
 Um cliente pode usar RESTORE HEADERONLY para recuperar todas as informações do cabeçalho de todos os backups em um dispositivo de backup particular. Para cada backup no dispositivo de backup, o servidor envia as informações de cabeçalho como uma linha.  
  
## <a name="security"></a>Segurança  
 Uma operação de backup pode, opcionalmente, especificar senhas para um conjunto de mídias, um conjunto de backup ou ambos. Quando uma senha tiver sido definida em um conjunto de backup ou de mídias, será preciso especificar a senha ou as senhas corretas na instrução RESTORE. Essas senhas impedem operações de restauração não autorizadas e Anexações não autorizadas de conjuntos de backup à mídia usando [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ferramentas. Porém, uma senha não impede a substituição da mídia usando a opção FORMAT da instrução BACKUP.  
  
> [!IMPORTANT]  
>  A proteção fornecida por esta senha é fraca. Destina-se a evitar uma restauração incorreta com o uso de ferramentas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por usuários autorizados ou não autorizados. Não impede a leitura dos dados de backup por outros meios ou a substituição da senha. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]A prática recomendada para proteger backups é armazenar as fitas de backup em um local seguro ou fazer backup de arquivos de disco que são protegidos por listas de controle de acesso adequadas (ACLs). As ACLs devem ser definidas no diretório raiz em que os backups são criados.  
  
### <a name="permissions"></a>Permissões  
 Obter informações sobre um conjunto de backups ou dispositivo de backup, é necessário ter a permissão CREATE DATABASE. Para obter mais informações, veja [GRANT Database Permissions &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo seguinte retorna as informações no cabeçalho do arquivo em disco `C:\AdventureWorks-FullBackup.bak`.  
  
```  
RESTORE HEADERONLY   
FROM DISK = N'C:\AdventureWorks-FullBackup.bak'   
WITH NOUNLOAD;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [conjunto de backup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [RESTORE REWINDONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)   
 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Informações de histórico e cabeçalho de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)   
 [Habilitar ou desabilitar as somas de verificação de Backup durante Backup ou restauração &#40; SQL Server &#41;](../../relational-databases/backup-restore/enable-or-disable-backup-checksums-during-backup-or-restore-sql-server.md)   
 [Conjuntos de mídias, famílias de mídia e conjuntos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [Modelos de recuperação &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)  
  
  
