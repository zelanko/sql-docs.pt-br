---
title: RESTORE VERIFYONLY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
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
- VERIFYONLY
- RESTORE VERIFYONLY
- VERIFYONLY_TSQL
- RESTORE_VERIFYONLY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- RESTORE VERIFYONLY statement
- backups [SQL Server], verifying
- verifying backups
- checking backups
ms.assetid: cba3b6a0-b48e-4c94-812b-5b3cbb408bd6
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b5cd93baf9fc13bd5333f5589dbb56413091671a
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="restore-statements---verifyonly-transact-sql"></a>Instruções - de RESTORE VERIFYONLY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Verifica o backup, mas não o restaura, e verifica se o conjunto de backup está completo e se todo o backup pode ser lido. Porém, RESTORE VERIFYONLY não tenta verificar a estrutura dos dados contida nos volumes de backup. Em [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], RESTORE VERIFYONLY foi aprimorado para executar uma verificação adicional nos dados para aumentar a probabilidade de detecção de erros. A meta é estar o mais próximo de uma operação de restauração real. Para obter mais informações, consulte Comentários.  
  
 Se o backup for válido, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] retorna uma mensagem de êxito.  
  
> [!NOTE]  
>  Para obter as descrições dos argumentos, consulte [argumentos RESTORE &#40; Transact-SQL &#41; ](../../t-sql/statements/restore-statements-arguments-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
RESTORE VERIFYONLY  
FROM <backup_device> [ ,...n ]  
[ WITH    
 {  
   LOADHISTORY   
  
--Restore Operation Option  
 | MOVE 'logical_file_name_in_backup' TO 'operating_system_file_name'   
          [ ,...n ]   
  
--Backup Set Options  
 | FILE = { backup_set_file_number | @backup_set_file_number }   
 | PASSWORD = { password | @password_variable }   
  
--Media Set Options  
 | MEDIANAME = { media_name | @media_name_variable }   
 | MEDIAPASSWORD = { mediapassword | @mediapassword_variable }  
  
--Error Management Options  
 | { CHECKSUM | NO_CHECKSUM }   
 | { STOP_ON_ERROR | CONTINUE_AFTER_ERROR }  
  
--Monitoring Options  
 | STATS [ = percentage ]   
  
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
 Para obter descrições dos argumentos RESTORE VERIFYONLY, consulte [argumentos RESTORE &#40; Transact-SQL &#41; ](../../t-sql/statements/restore-statements-arguments-transact-sql.md).  
  
## <a name="general-remarks"></a>Comentários gerais  
 O conjunto de mídias ou o conjunto de backup deve conter informações corretas mínimas para que possam ser interpretadas como formato de fita Microsoft. Caso contrário, RESTORE VERIFYONLY parará e indicará que o formato do backup é inválido.  
  
 As verificações executadas por RESTORE VERIFYONLY incluem:  
  
-   Se o conjunto de backup está completo e todos os volumes são legíveis.  
  
-   Alguns campos de cabeçalho de páginas de banco de dados, como ID da página (como se estivesse relacionado à gravação de dados).  
  
-   Soma da verificação (se presente na mídia).  
  
-   Verificação de espaço suficiente nos dispositivos de destino.  
  
> [!NOTE]  
>  RESTORE VERIFYONLY não funciona em um instantâneo do banco de dados. Para verificar um instantâneo do banco de dados antes uma operação de reversão, você pode executar DBCC CHECKDB.  
  
> [!NOTE]  
>  Com backups de instantâneo, RESTORE VERIFYONLY confirma a existência de instantâneos nos locais especificados no arquivo de backup. Backups de instantâneo são um novo recurso no [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]. Para obter mais informações sobre Backups de instantâneo, consulte [Backups de instantâneo de arquivo para arquivos de banco de dados no Azure](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md).  
  
## <a name="security"></a>Segurança  
 Uma operação de backup pode, opcionalmente, especificar senhas para um conjunto de mídias, um conjunto de backup ou ambos. Quando uma senha tiver sido definida em um conjunto de backup ou de mídias, será preciso especificar a senha ou as senhas corretas na instrução RESTORE. Essas senhas impedem operações de restauração não autorizadas e anexações não autorizadas de conjuntos de backup para mídia usando ferramentas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Porém, uma senha não impede a substituição da mídia usando a opção FORMAT da instrução BACKUP.  
  
> [!IMPORTANT]  
>  A proteção fornecida por esta senha é fraca. Destina-se a evitar uma restauração incorreta com o uso de ferramentas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por usuários autorizados ou não autorizados. Não impede a leitura dos dados de backup por outros meios ou a substituição da senha. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]A prática recomendada para proteger backups é armazenar as fitas de backup em um local seguro ou fazer backup de arquivos de disco que são protegidos por listas de controle de acesso adequadas (ACLs). As ACLs devem ser definidas no diretório raiz em que os backups são criados.  
  
### <a name="permissions"></a>Permissões  
 A partir do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], para obter informações sobre um conjunto ou dispositivo de backup, é necessário ter a permissão CREATE DATABASE. Para obter mais informações, veja [GRANT Database Permissions &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md).  
  
## <a name="see-also"></a>Consulte também  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Conjuntos de mídias, famílias de mídia e conjuntos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [RESTORE REWINDONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Informações de histórico e cabeçalho de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)  
  
  
