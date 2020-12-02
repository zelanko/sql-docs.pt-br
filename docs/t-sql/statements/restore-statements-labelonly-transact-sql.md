---
description: Instruções RESTORE – LABELONLY (Transact-SQL)
title: RESTORE LABELONLY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- LABELONLY
- RESTORE_LABELONLY_TSQL
- LABELONLY_TSQL
- RESTORE LABELONLY
dev_langs:
- TSQL
helpviewer_keywords:
- RESTORE LABELONLY statement
- backup media [SQL Server], content information
ms.assetid: 7cf0641e-0d55-4ffb-9500-ecd6ede85ae5
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 4bb66a3711bcb2a5a309c4b712470c4fb3b16bb9
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88478701"
---
# <a name="restore-statements---labelonly-transact-sql"></a>Instruções RESTORE – LABELONLY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md )]
  Retorna um conjunto de resultados que contém informações sobre as mídias de backup identificadas pelo dispositivo de backup designado.  
  
> [!NOTE]  
>  Para obter as descrições dos argumentos, consulte [Argumentos de RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
  
RESTORE LABELONLY   
FROM <backup_device>   
[ WITH   
 {  
--Media Set Options  
   MEDIANAME = { media_name | @media_name_variable }   
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
   | { DISK | TAPE | URL } = { 'physical_backup_device_name' |  
       @physical_backup_device_name_var }   
}  
  
```  
> [!NOTE] 
> URL é o formato usado para especificar o local e o nome do arquivo para o Armazenamento de Blobs do Microsoft Azure e o suporte a ele começa no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2. Embora o Armazenamento do Microsoft Azure seja um serviço, a implementação é semelhante ao disco e à fita para permitir uma experiência de restauração consistente e direta para todos os três dispositivos.
  
## <a name="arguments"></a>Argumentos  
 Para obter descrições dos argumentos de RESTORE LABELONLY, confira [Argumentos de RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md).  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 O conjunto de resultados de RESTORE LABELONLY consiste em uma única linha com essas informações.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**MediaName**|**nvarchar(128)**|Nome da mídia.|  
|**MediaSetId**|**uniqueidentifier**|Número de identificação exclusivo do conjunto de mídias.|  
|**FamilyCount**|**int**|Número de famílias de mídias no conjunto de mídias.|  
|**FamilySequenceNumber**|**int**|Número de sequência desta família.|  
|**MediaFamilyId**|**uniqueidentifier**|Número de identificação exclusivo da família de mídia.|  
|**MediaSequenceNumber**|**int**|Número de sequência dessa mídia na família de mídias.|  
|**MediaLabelPresent**|**tinyint**|Se a descrição de mídia contiver:<br /><br /> **1** = [!INCLUDE[msCoName](../../includes/msconame-md.md)] Rótulo da mídia de formato de fita<br /><br /> **0** = descrição da mídia|  
|**MediaDescription**|**nvarchar(255)**|Descrição da mídia, em texto de formato livre, ou rótulo de mídia de formato de fita.|  
|**SoftwareName**|**nvarchar(128)**|Nome do software de backup que gravou o rótulo.|  
|**SoftwareVendorId**|**int**|Número exclusivo de identificação do fornecedor do software que gravou o backup.|  
|**MediaDate**|**datetime**|Data e hora em que o rótulo foi gravado.|  
|**Mirror_Count**|**int**|Número de espelhos no conjunto (1-4).<br /><br /> Observação: os rótulos gravados para espelhos diferentes em um conjunto são idênticos.|  
|**IsCompressed**|**bit**|Se o backup é compactado:<br /><br /> 0 = não compactado<br /><br /> 1 = compactado|  
  
> [!NOTE]  
>  Se as senhas forem definidas para o conjunto de mídias, RESTORE LABELONLY retornará informações apenas se a senha de mídia correta for especificada na opção MEDIAPASSWORD do comando.  
  
## <a name="general-remarks"></a>Comentários gerais  
 A execução de RESTORE LABELONLY é um modo rápido de descobrir o que a mídia de backup contém. Como RESTORE LABELONLY lê só o cabeçalho da mídia, essa instrução terminará rapidamente mesmo quando estiverem sendo usados dispositivos de fita de alta capacidade.  
  
## <a name="security"></a>Segurança  
 Uma operação de backup pode opcionalmente especificar senhas para um conjunto de mídias. Quando uma senha tiver sido definida em um conjunto de mídias, será preciso especificar a senha correta na instrução RESTORE. A senha impede operações de restauração não autorizadas e acréscimos não autorizados de conjuntos de backup à mídia usando ferramentas do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Porém, uma senha não impede a substituição da mídia usando a opção FORMAT da instrução BACKUP.  
  
> [!IMPORTANT]  
>  A proteção fornecida por esta senha é fraca. Destina-se a evitar uma restauração incorreta com o uso de ferramentas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por usuários autorizados ou não autorizados. Não impede a leitura dos dados de backup por outros meios ou a substituição da senha. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]A melhor prática para proteger backups é armazenar as fitas de backup em um local seguro ou fazer backup em arquivos de disco protegidos por ACLs (listas de controle de acesso) adequadas. As ACLs devem ser definidas no diretório raiz em que os backups são criados.  
  
### <a name="permissions"></a>Permissões  
 No [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e em versões posteriores, a obtenção de informações sobre um conjunto ou dispositivo de backup exige a permissão CREATE DATABASE. Para obter mais informações, veja [GRANT Database Permissions &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md).  
  
## <a name="see-also"></a>Consulte Também  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Conjuntos de mídias, famílias de mídia e conjuntos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [RESTORE REWINDONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)   
 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Informações de histórico e cabeçalho de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)  
  
  
