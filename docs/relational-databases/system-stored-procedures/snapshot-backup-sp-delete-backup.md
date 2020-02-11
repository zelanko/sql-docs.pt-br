---
title: sp_delete_backup (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/03/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 808e50ae-ff6e-4520-9ce2-530591d3d59b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 49eb0906a9a5af1fec2abfeec3ef58845b605e69
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67941828"
---
# <a name="sp_delete_backup-transact-sql"></a>sp_delete_backup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Exclui todos os instantâneos e o arquivo de backup que compõem um conjunto de backup de instantâneo do banco de dados especificado. Esse procedimento armazenado do sistema é o único método recomendado para gerenciar conjuntos de backup de instantâneo. Para obter mais informações, consulte [Backups de instantâneo de arquivo para arquivos de banco de dados no Azure](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.sp_delete_backup   
    [ @backup_url = ] backup_metadata_file_url  
    ,[ [ @db_name = ] database_name | NULL ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *[ @backup_url =] backup_meta_file_url*  
 A URL do backup a ser excluído, que exclui todos os instantâneos que compõem o conjunto de backup especificado, incluindo o próprio arquivo de backup.  
  
 *[ @db_name =] database_name*  
 O nome do banco de dados que contém o instantâneo a ser excluído. Quando um nome de banco de dados é fornecido, o sistema verifica se a URL de backup fornecida é uma URL de backup para o banco de dados especificado e usa [sp_delete_backup_file_snapshot &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md) para excluir cada instantâneo. Se nenhum nome de banco de dados for fornecido, essa verificação de banco de dados não será executada.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER ANY DATABASE ou a permissão ALTER no banco de dados especificado.  
  
## <a name="see-also"></a>Consulte Também  
 [sys. fn_db_backup_file_snapshots &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_delete_backup_file_snapshot](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md)  
  
  
