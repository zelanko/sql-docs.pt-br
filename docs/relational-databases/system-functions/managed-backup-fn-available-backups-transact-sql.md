---
title: fn_available_backups (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- smart_admin.fn_available_backups
- smart_admin.fn_available_backups_TSQL
- fn_available_backups_TSQL
- fn_available_backups
dev_langs: TSQL
helpviewer_keywords:
- fn_available_backups
- smart_admin.fn_available_backups
ms.assetid: 7aa84474-16e5-49bd-a703-c8d1408ef107
caps.latest.revision: "15"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4e5b69caf7cde64cae7454c7132e1ee739898fff
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="managedbackupfnavailablebackups-transact-sql"></a>fn_available_backups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Retorna uma tabela de 0, uma ou mais linhas dos arquivos de backup disponíveis para o banco de dados especificado. Os arquivos de backup retornados são backups criados pelo [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```tsql  
managed_backup.fn_available_backups ([@database_name = ] 'database name')  
```  
  
##  <a name="Arguments"></a> Argumentos  
 @database_name  
 O nome do banco de dados. O @database_name é nvarchar (512).  
  
## <a name="table-returned"></a>Tabela retornada  
 A tabela tem uma restrição clusterizada exclusiva em (database_guid, backup_start_date e first_lsn, backup_type).   
Se um banco de dados for ignorado e, em seguida, recriado, os conjuntos de backup para todos os bancos de dados serão retornados. A saída é ordenada pelo database_guid, que identifica exclusivamente cada banco de dados.   
Se houver lacunas no LSN, significando que há uma quebra na cadeia de logs, a tabela conterá uma linha especial para cada segmento ausente do LSN.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|Backup_path|NVARCHAR(260) COLLATE Latin1_General_CI_AS_KS_WS|A URL do arquivo de backup.|  
|backup_type|NVARCHAR(6)|‘DB’ para o backup do banco de dados ‘LOG’ para o backup de log|  
|expiration_date|DATETIME|A data em que este arquivo deve ser excluído. Isso é definido com base na capacidade de recuperar o banco de dados para um ponto no tempo dentro do período de retenção especificado.|  
|database_guid|UNIQUEIDENTIFIER|O valor de GUID para o banco de dados especificado.  A GUID identifica um banco de dados com exclusividade.|  
|first_lsn|NUMERIC(25, 0)|Número de sequência de log do primeiro ou mais antigo registro de log no conjunto de backup. Pode ser NULL.|  
|last_lsn|NUMERIC(25, 0)|Número de sequência de log do próximo registro de log após o conjunto de backup. Pode ser NULL.|  
|backup_start_date|DATETIME|Data e hora em que a operação de backup foi iniciada.|  
|backup_finish_date|NVARCHAR(128)|Data e hora em que a operação de backup foi concluída.|  
|machine_name|NVARCHAR(128)|Nome do computador onde a instância do SQL Server está instalada e executando o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].|  
|last_recovery_fork_id|UNIQUEIDENTIFIER|Número de identificação para a bifurcação de recuperação final.|  
|first_recovery_fork_id|UNIQUEIDENTIFIER|ID da bifurcação de recuperação inicial. Para backups de dados, first_recovery_fork_guid é igual a last_recovery_fork_guid.|  
|fork_point_lsn|NUMERIC(25, 0)|Se first_recovery_fork_id não for igual a last_recovery_fork_id, esse será o número de sequência de log do ponto de bifurcação. Caso contrário, esse valor será NULL.|  
|availability_group_guid|UNIQUEIDENTIFIER|Se um banco de dados é um banco de dados AlwaysOn, esse é o GUID do grupo de disponibilidade. Caso contrário, esse valor é NULL.|  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito) ou 1 (falha).  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Requer **selecione** permissões sobre essa função.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir lista todos os backups disponíveis feitos pelo [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para o banco de dados ‘MyDB’  
  
```  
SELECT *   
FROM managed_backup.fn_available_backups ('MyDB')  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Backup gerenciado do SQL Server para o Microsoft Azure](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)   
 [Restaurando de backups armazenados no Microsoft Azure](../../relational-databases/backup-restore/restoring-from-backups-stored-in-microsoft-azure.md)  
  
  
