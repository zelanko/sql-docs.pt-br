---
title: sys. fn_db_backup_file_snapshots (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/03/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 45010ff2-219f-4086-9ea4-016a6c17cddd
author: rothja
ms.author: jroth
ms.openlocfilehash: 5159b72cb91cfdcf21129c6216cab4cf0e8d4dea
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68120267"
---
# <a name="sysfndbbackupfilesnapshots-transact-sql"></a>sys.fn_db_backup_file_snapshots (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Retorna os instantâneos do Azure associados com os arquivos de banco de dados. Se o banco de dados especificado não for encontrado ou se os arquivos de banco de dados não são armazenados no serviço de armazenamento de BLOBs do Microsoft Azure, nenhuma linha será retornada. Use essa função do sistema junto com o **sp_delete_backup_file_snapshot** sistema de procedimento armazenado para identificar e excluir instantâneos de backup órfãos. Para obter mais informações, consulte [Backups de instantâneo de arquivo para arquivos de banco de dados no Azure](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.fn_db_backup_file_snapshots   
   [ ( database_name ) ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *Database_name*  
 O nome do banco de dados que está sendo consultado. Se for NULL, essa função é executada no escopo do banco de dados atual.  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|file_id|**int**|A ID do arquivo para o banco de dados. Não permite valor nulo.|  
|snapshot_time|**nvarchar(260)**|O carimbo de hora do instantâneo como ele é retornado pela API REST. Retorna NULL se nenhum instantâneo existe.|  
|snapshot_url|**nvarchar(360)**|A URL completa para o instantâneo de arquivo. Retorna nulo se nenhum instantâneo existe.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW DATABASE STATE no banco de dados.  
  
## <a name="see-also"></a>Consulte também  
 [sp_delete_backup_file_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md)   
 [sp_delete_backup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup.md)  
  
  
