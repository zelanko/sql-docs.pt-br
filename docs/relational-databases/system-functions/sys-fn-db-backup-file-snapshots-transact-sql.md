---
description: sys.fn_db_backup_file_snapshots (Transact-SQL)
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
ms.openlocfilehash: 067a1d65b65c1e2cc9bde252e6f56951e87950a8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88427788"
---
# <a name="sysfn_db_backup_file_snapshots-transact-sql"></a>sys.fn_db_backup_file_snapshots (Transact-SQL)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  Retorna instantâneos do Azure associados aos arquivos de banco de dados. Se o banco de dados especificado não for encontrado ou se os arquivos de banco de dados não estiverem armazenados no serviço de armazenamento de blob Microsoft Azure, nenhuma linha será retornada. Use essa função de sistema em conjunto com o procedimento armazenado do sistema **Sys. sp_delete_backup_file_snapshot** para identificar e excluir instantâneos de backup órfãos. Para obter mais informações, consulte [Backups de instantâneo de arquivo para arquivos de banco de dados no Azure](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.fn_db_backup_file_snapshots   
   [ ( database_name ) ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *Database_name*  
 O nome do banco de dados que está sendo consultado. Se for NULL, essa função será executada no escopo do banco de dados atual.  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|file_id|**int**|A ID do arquivo para o banco de dados. Não permite valor nulo.|  
|snapshot_time|**nvarchar(260)**|O carimbo de data/hora do instantâneo como ele é retornado pela API REST. Retornará NULL se não existir nenhum instantâneo.|  
|snapshot_url|**nvarchar(360)**|A URL completa para o instantâneo do arquivo. Retornará NULL se não existir nenhum instantâneo.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW DATABASE STATE no banco de dados.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_delete_backup_file_snapshot ](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md)   
 [sp_delete_backup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup.md)  
  
  
