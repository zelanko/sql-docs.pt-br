---
title: sp_delete_backup (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/03/2015
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 808e50ae-ff6e-4520-9ce2-530591d3d59b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fbf04bbd9b60a99a2e972db139daaf8bb4361389
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43037449"
---
# <a name="spdeletebackup-transact-sql"></a>sp_delete_backup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Exclui todos os instantâneos e o arquivo de backup que compõem um backup de instantâneo definido do banco de dados especificado. Esse procedimento armazenado do sistema é o único método recomendado para gerenciar conjuntos de backup de instantâneo. Para obter mais informações, consulte [Backups de instantâneo de arquivo para arquivos de banco de dados no Azure](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.sp_delete_backup   
    [ @backup_url = ] backup_metadata_file_url  
    ,[ [ @db_name = ] database_name | NULL ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *[ @backup_url = ] backup_meta_file_url*  
 A URL do backup a ser excluído, o que exclui todos os instantâneos que compõem o conjunto incluindo o arquivo de backup de backup especificado.  
  
 *[ @db_name =] database_name*  
 O nome do banco de dados que contém o instantâneo a ser excluído. Quando um nome de banco de dados for fornecido, o sistema verifica se a URL de backup fornecida é uma URL de backup para o banco de dados especificado e usa [sp_delete_backup_file_snapshot &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md) para excluir cada instantâneo. Se nenhum nome de banco de dados for fornecido, essa verificação de banco de dados não será executada.  
  
## <a name="permissions"></a>Permissões  
 Requer permissão ALTER ANY DATABASE ou permissão ALTER no banco de dados especificado.  
  
## <a name="see-also"></a>Consulte também  
 [sys.fn_db_backup_file_snapshots &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md)   
 [sp_delete_backup_file_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md)  
  
  
