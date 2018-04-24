---
title: Restaurações de arquivos (modelo de recuperação simples) | Microsoft Docs
ms.custom: ''
ms.date: 03/24/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: backup-restore
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- file restores [SQL Server]
- simple recovery model [SQL Server]
- restoring files [SQL Server], Transact-SQL restore sequence
- restoring files [SQL Server]
- Transact-SQL restore sequence
- restoring files [SQL Server], simple recovery model
- file restores [SQL Server], simple recovery model
- file restores [SQL Server], Transact-SQL restore sequence
ms.assetid: b6d07386-7c6f-4cc6-be32-93289adbd3d6
caps.latest.revision: 57
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ae3fc7b2bec061b467906086d2e35746b915f398
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="file-restores-simple-recovery-model"></a>Restaurações de arquivos (modelo de recuperação simples)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este tópico é relevante apenas para bancos de dados modelo simples que contêm pelo menos um grupo de arquivos secundário somente leitura.  
  
 Em uma restauração de arquivo, a meta é restaurar um ou mais arquivos danificados sem restaurar todo o banco de dados. No modelo de recuperação simples, os backups de arquivo possuem suporte apenas para grupos de arquivos somente leitura. O grupo de arquivos primário e os grupos de arquivos secundários leitura/gravação sempre são restaurados juntos, restaurando um banco de dados ou backup parcial.  
  
 Os cenários de restauração de arquivo são os seguintes:  
  
-   Restauração de arquivo offline  
  
     Em uma *restauração de arquivo offline*, o banco de dados fica offline enquanto os arquivos ou grupos de arquivos danificados são restaurados. Ao término da sequência de restauração, o banco de dados fica online.  
  
     Todas as edições do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] oferecem suporte à restauração de arquivos offline.  
  
-   Restauração de arquivo online  
  
     Em uma *restauração de arquivo online*, se o banco de dados estiver online no momento da restauração, ele permanecerá online durante a restauração do arquivo. Porém, cada grupo de arquivos no qual um arquivo está sendo restaurado fica offline durante a operação de restauração. Depois que todos os arquivos de um grupo de arquivos offline são recuperados, o grupo de arquivos é automaticamente colocado online.  
  
     Para obter informações sobre o suporte à restauração de páginas e arquivos online, consulte [Tarefas e recursos do mecanismo de banco de dados](http://msdn.microsoft.com/library/d9efe145-3306-4d61-bd77-e2af43e19c34). Para obter mais informações sobre restaurações online, veja [Restauração online &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md).  
  
    > [!TIP]  
    >  Se quiser que o banco de dados fique offline para uma restauração de arquivo, coloque o banco de dados offline antes de iniciar a sequência de restauração, executando a seguinte instrução [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-set-options.md) : ALTER DATABASE *database_name* SET OFFLINE.  
  
 **Neste tópico:**  
  
-   [Visão geral da restauração de arquivos e grupos de arquivos no modelo de recuperação simples](#Overview)  
  
-   [Tarefas relacionadas](#RelatedTasks)  
  
##  <a name="Overview"></a> Visão geral da restauração de arquivos e grupos de arquivos no modelo de recuperação simples  
 Um cenário de restauração de arquivos consiste em uma única sequência de restauração que copia, efetua roll forward e recupera os dados apropriados da seguinte maneira:  
  
1.  Restaure cada arquivo danificado de seu mais recente backup de arquivos.  
  
2.  Restaure o backup de arquivo diferencial mais recente para cada arquivo restaurado e recupere o banco de dados.  
  
### <a name="transact-sql-steps-for-file-restore-sequence-simple-recovery-model"></a>Etapas do Transact-SQL para a sequência de restauração de arquivos (modelo de recuperação simples)  
 Esta seção mostra as opções básicas de [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) do [!INCLUDE[tsql](../../includes/tsql-md.md)] para uma sequência de restauração de arquivo simples. Sintaxe e detalhes que não sejam relevantes para esse propósito são omitidos.  
  
 A sequência de restauração contém apenas duas instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] . A primeira instrução restaura um arquivo secundário, o arquivo `A`, que é restaurado usando WITH NORECOVERY. A segunda operação restaura dois outros arquivos, `B` e `C` , que são restaurados usando WITH RECOVERY de um dispositivo de backup diferente:  
  
1.  RESTORE DATABASE *database* FILE **=***name_of_file_A*  
  
     FROM *file_backup_of_file_A*  
  
     WITH NORECOVERY**;**  
  
2.  RESTORE DATABASE *database* FILE **=***name_of_file_B***,***name_of_file_C*  
  
     FROM *file_backup_of_files_B_and_C*  
  
     WITH RECOVERY**;**  
  
### <a name="examples"></a>Exemplos  
  
-   [Exemplo: restauração online de um arquivo somente leitura &#40;Modelo de recuperação simples&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [Exemplo: restauração offline do grupo de arquivos primário e mais um &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/example-offline-restore-of-primary-and-one-other-filegroup-full-recovery-model.md)  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
 **Para restaurar arquivos e grupos de arquivos**  
  
-   [Restaurar arquivos e grupos de arquivos sobre arquivos existentes &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-over-existing-files-sql-server.md)  
  
-   [Restaurar arquivos e grupos de arquivos &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-sql-server.md)  
  
-   [Restaurar arquivos e grupos de arquivos &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-sql-server.md)  
  
-   [Método Restore.SqlRestore (Servidor) (SMO)](http://msdn.microsoft.com/library/microsoft.sqlserver.management.smo.restore.sqlrestore.aspx)   
  
## <a name="see-also"></a>Consulte Também  
 [Backup e restauração: interoperabilidade e coexistência &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-and-restore-interoperability-and-coexistence-sql-server.md)   
 [Backups diferenciais &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)   
 [Backups completos de arquivos &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-file-backups-sql-server.md)   
 [Visão geral do backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [Visão geral de restauração e recuperação &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Restaurações completas de banco de dados &#40;Modelo de recuperação simples#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)   
 [Restaurações por etapas &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  
