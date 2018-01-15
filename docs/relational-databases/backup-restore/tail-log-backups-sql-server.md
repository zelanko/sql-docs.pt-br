---
title: Backups da parte final do log (SQL Server) | Microsoft Docs
ms.custom: 
ms.date: 08/01/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- backing up [SQL Server], tail of log
- transaction log backups [SQL Server], tail-log backups
- NO_TRUNCATE clause
- backups [SQL Server], log backups
- tail-log backups
- backups [SQL Server], tail-log backups
ms.assetid: 313ddaf6-ec54-4a81-a104-7ffa9533ca58
caps.latest.revision: "55"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 2a1254e44ac2fcc110a81d9ac7f566a348812f80
ms.sourcegitcommit: 1eac335235847c3578e376e0854413710d345dee
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2018
---
# <a name="tail-log-backups-sql-server"></a>Backups da parte final do log (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Este tópico é relevante apenas para o backup e a restauração dos bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que estão usando modelos de recuperação completa ou bulk-logged.  
  
 Um *backup da parte final do log* captura qualquer registro de log que ainda não foi submetido a backup (a *parte final do log*) para impedir a perda de trabalho e manter a cadeia de logs intacta. Para que você possa recuperar um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] até seu momento determinado mais recente, você deve fazer backup da parte final do log de transações. O backup da parte final do log será o último backup de interesse no plano de recuperação do banco de dados.  
  
> **OBSERVAÇÃO:** nem todos os cenários de restauração exigem um backup da parte final do log. Você não precisará de um backup da parte final do log se o ponto de recuperação estiver em um backup de log anterior. Além disso, um backup da parte final do log será desnecessário se você estiver movendo ou substituindo um banco de dados e não precisar restaurá-lo para um momento determinado após o seu backup mais recente.  
  
   ##  <a name="TailLogScenarios"></a> Cenários que exigem um backup da parte final do log  
 É recomendável fazer um backup da parte final do log nos seguintes cenários:  
  
-   Se o banco de dados estiver online e você planeja realizar uma operação de restauração nele, comece fazendo backup da parte final do log. Para evitar um erro para um banco de dados online, você deve usar a opção … Opção WITH NORECOVERY da instrução [BACKUP](../../t-sql/statements/backup-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
-   Se um banco de dados estiver offline e não puder ser iniciado, e você precisar restaurar o banco de dados, primeiro faça backup da parte final do log. Como nenhuma transação pode ocorrer nesse momento, o uso de WITH NORECOVERY é opcional.  
  
-   Se um banco de dados for danificado, tente fazer um backup da parte final do log usando a opção WITH CONTINUE_AFTER_ERROR da instrução BACKUP.  
  
     Em um banco de dados danificado, o backup da parte final do log só terá êxito se os arquivos de log não estiverem danificados, o banco de dados estiver em um estado que ofereça suporte a backups da parte final do log e o banco de dados não tiver nenhuma alteração bulk-logged. Se um backup da parte final do log não puder ser criado, qualquer transação confirmada após o backup mais recente será perdida.  
  
 A tabela a seguir resume as opções BACKUP NORECOVERY e CONTINUE_AFTER_ERROR.  
  
|Opção BACKUP LOG|Comentários|  
|-----------------------|--------------|  
|NORECOVERY|Use NORECOVERY sempre que pretender continuar com uma operação de restauração no banco de dados. NORECOVERY coloca o banco de dados no estado de restauração. Isso garante que o banco de dados não seja alterado depois do backup da parte final do log. O log será truncado, a menos que a opção NO_TRUNCATE ou COPY_ONLY também seja especificada.<br /><br /> **Importante:** evite usar NO_TRUNCATE, exceto quando o banco de dados estiver danificado.|  
|CONTINUE_AFTER_ERROR|Use CONTINUE_AFTER_ERROR somente se estiver fazendo backup da parte final de um banco de dados danificado.<br /><br /> Quando você usa o backup da parte final do log em um banco de dados danificado, alguns dos metadados que são normalmente capturados em backups de log poderão estar indisponíveis. Para obter mais informações, consulte [Backups da parte final do log com backup incompleto de metadados](#IncompleteMetadata)neste tópico.|  
  
##  <a name="IncompleteMetadata"></a> Backups da parte final do log que têm metadados de backup incompletos  
 Backups da parte final do log capturam a parte final do log até mesmo se o banco de dados estiver offline, danificado, ou com arquivos de dados faltando. Isso pode causar metadados incompletos dos comandos de informação de restauração e de **msdb**. Entretanto, apenas os metadados estão incompletos; o log capturado está completo e utilizável.  
  
 Se um backup da parte final do log tiver metadados incompletos, na tabela [backupset](../../relational-databases/system-tables/backupset-transact-sql.md) , **has_incomplete_metadata** é definido como **1**. Além disso, na saída de [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md), **HasIncompleteMetadata** é definido para **1**.  
  
 Se os metadados em um backup da parte final do log estiverem incompletos, a tabela [backupfilegroup](../../relational-databases/system-tables/backupfilegroup-transact-sql.md) estará sem a maioria das informações sobre os grupos de arquivos na hora do backup da parte final do log. A maioria das colunas da tabela **backupfilegroup** é NULL; as únicas colunas significativas são como as seguintes:  
  
-   **backup_set_id**  
-   **filegroup_id**  
-   **tipo**  
-   **type_desc**  
-   **is_readonly**  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
 Para criar um backup da parte final do log, consulte [Fazer backup do log de transações quando o banco de dados está danificado &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md).  
  
 Para restaurar um backup de log de transações, consulte [Restaurar um backup de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md).  
    
## <a name="see-also"></a>Consulte Também  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Fazer backup e restaurar bancos de dados do SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Backups somente cópia &#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md)   
 [Backups de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)   
 [Aplicar backups de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)    
 [Guia de arquitetura e gerenciamento de log de transações do SQL Server](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md)
  
