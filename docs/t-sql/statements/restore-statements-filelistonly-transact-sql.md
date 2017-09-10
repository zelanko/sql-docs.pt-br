---
title: RESTORE FILELISTONLY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- RESTORE FILELISTONLY
- RESTORE_FILELISTONLY_TSQL
- FILELISTONLY
- FILELISTONLY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backups [SQL Server], file lists
- RESTORE FILELISTONLY statement
- listing backed up files
ms.assetid: 0b4b4d11-eb9d-4f3e-9629-6c79cec7a81a
caps.latest.revision: 83
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bdae49bd22b5398d120530db150bc9628e34d92a
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="restore-statements---filelistonly-transact-sql"></a>RESTAURAR instruções - FILELISTONLY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna um conjunto de resultados que contém uma lista dos arquivos de banco de dados e de log contidos no conjunto de backup no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Para obter as descrições dos argumentos, consulte [argumentos RESTORE &#40; Transact-SQL &#41; ](../../t-sql/statements/restore-statements-arguments-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
RESTORE FILELISTONLY   
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
 Para obter descrições dos argumentos RESTORE FILELISTONLY, consulte [argumentos RESTORE &#40; Transact-SQL &#41; ](../../t-sql/statements/restore-statements-arguments-transact-sql.md).  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Um cliente pode usar RESTORE FILELISTONLY para obter uma lista dos arquivos contidos em um conjunto de backups. Essas informações são retornadas como um conjunto de resultados que contém uma linha para cada arquivo.  
  
|Nome da coluna|Tipo de dados|Description|  
|-|-|-|  
|LogicalName|**nvarchar (128)**|Nome lógico do arquivo.|  
|PhysicalName|**nvarchar (260)**|Nome do arquivo físico ou do sistema operacional.|  
|Tipo|**char (1)**|O tipo de arquivo, um dentre:<br /><br /> **L** = Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] arquivo de log<br /><br /> **D**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] arquivo de dados<br /><br /> **F** = catálogo de texto completo<br /><br /> **S** = FileStream, FileTable ou [!INCLUDE[hek_2](../../includes/hek-2-md.md)] contêiner|  
|FileGroupName|**nvarchar (128)**|Nome do grupo de arquivos que contém o arquivo.|  
|Tamanho|**numeric(20,0)**|Tamanho atual em bytes.|  
|MaxSize|**numeric(20,0)**|Tamanho máximo permitido em bytes.|  
|FileID|**bigint**|Identificador de arquivo, exclusivo no banco de dados.|  
|CreateLSN|**numeric(25,0)**|Número da sequência de log na qual o arquivo foi criado.|  
|DropLSN|**numeric(25,0)** nulo|O número de sequência de log no qual o arquivo foi descartado. Se o arquivo não tiver sido descartado, esse valor será NULL.|  
|UniqueID|**uniqueidentifier**|Identificador exclusivo global do arquivo.|  
|ReadOnlyLSN|**numeric(25,0) NULL**|Número da sequência de log em que o grupo de arquivos que contém o arquivo alterado de leitura/gravação para somente leitura (a alteração mais recente).|  
|ReadWriteLSN|**numeric(25,0)** nulo|Número da sequência de log em que o grupo de arquivos que contém o arquivo alterado de somente leitura para leitura/gravação (a alteração mais recente).|  
|BackupSizeInBytes|**bigint**|Tamanho do backup do arquivo em bytes.|  
|SourceBlockSize|**int**|Tamanho do bloco do dispositivo físico que contém o arquivo em bytes (não o dispositivo de backup).|  
|FileGroupID|**int**|ID do grupo de arquivos.|  
|LogGroupGUID|**uniqueidentifier NULL**|NULL.|  
|DifferentialBaseLSN|**numeric(25,0)** nulo|Para backups diferenciais, as alterações com números de sequência de log maiores que ou iguais a **DifferentialBaseLSN** são incluídas no diferencial.<br /><br /> Para outros tipos de backup, o valor é NULL.|  
|DifferentialBaseGUID|**uniqueidentifier**|Para backups diferenciais, o identificador exclusivo da base diferencial.<br /><br /> Para outros tipos de backup, o valor é NULL.|  
|IsReadOnly|**bit**|**1** = o arquivo é somente leitura.|  
|IsPresent|**bit**|**1** = o arquivo está presente no backup.|  
|TDEThumbprint|**varbinary(32)**|Mostra a impressão digital da Chave de Criptografia do Banco de dados. A impressão digital do criptografador é um hash SHA-1 do certificado com o qual a chave é criptografada. Para obter informações sobre criptografia de banco de dados, consulte [Transparent Data Encryption &#40; TDE &#41; ](../../relational-databases/security/encryption/transparent-data-encryption.md).|  
|SnapshotURL|**nvarchar(360)**|A URL para o instantâneo do Azure do arquivo de banco de dados contido no backup FILE_SNAPSHOT. Retorna NULL se nenhum backup FILE_SNAPSHOT.|  
  
## <a name="security"></a>Segurança  
 Uma operação de backup pode, opcionalmente, especificar senhas para um conjunto de mídias, um conjunto de backup ou ambos. Quando uma senha tiver sido definida em um conjunto de backup ou de mídias, será preciso especificar a senha ou as senhas corretas na instrução RESTORE. Essas senhas impedem operações de restauração não autorizadas e Anexações não autorizadas de conjuntos de backup à mídia usando [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ferramentas. Porém, uma senha não impede a substituição da mídia usando a opção FORMAT da instrução BACKUP.  
  
> [!IMPORTANT]  
>  A proteção fornecida por esta senha é fraca. Destina-se a evitar uma restauração incorreta com o uso de ferramentas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por usuários autorizados ou não autorizados. Não impede a leitura dos dados de backup por outros meios ou a substituição da senha. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] A prática recomendada para proteger backups é armazenar as fitas de backup em um local seguro ou fazer backup em arquivos de disco protegidos por ACLs (listas de controle de acesso) adequadas. As ACLs devem ser definidas no diretório raiz em que os backups são criados.  
  
### <a name="permissions"></a>Permissões  
 A partir do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], para obter informações sobre um conjunto ou dispositivo de backup, é necessário ter a permissão CREATE DATABASE. Para obter mais informações, veja [GRANT Database Permissions &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna informações de um dispositivo de backup denominado `AdventureWorksBackups`. O exemplo usa a opção `FILE` para especificar o segundo conjunto de backup no dispositivo.  
  
```  
RESTORE FILELISTONLY FROM AdventureWorksBackups   
   WITH FILE=2;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Conjuntos de mídias, famílias de mídia e conjuntos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [RESTORE REWINDONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)   
 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Informações de histórico e cabeçalho de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)  
  
  
