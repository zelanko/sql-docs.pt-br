---
title: "Restaura&#231;&#245;es de arquivos (modelo de recupera&#231;&#227;o simples) | Microsoft Docs"
ms.custom: ""
ms.date: "03/24/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "restaurações de arquivos [SQL Server]"
  - "modelo de recuperação simples [SQL Server]"
  - "restaurando arquivos [SQL Server], sequência de restauração Transact-SQL"
  - "restaurando arquivos [SQL Server]"
  - "sequência de restauração Transact-SQL"
  - "restaurando arquivos [SQL Server], modelo de recuperação simples"
  - "restaurações de arquivo [SQL Server], modelo de recuperação simples"
  - "restaurações de arquivos [SQL Server], sequência de restauração Transact-SQL"
ms.assetid: b6d07386-7c6f-4cc6-be32-93289adbd3d6
caps.latest.revision: 57
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 56
---
# Restaura&#231;&#245;es de arquivos (modelo de recupera&#231;&#227;o simples)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Este tópico é relevante apenas para bancos de dados modelo simples que contêm pelo menos um grupo de arquivos secundário somente leitura.  
  
 Em uma restauração de arquivo, a meta é restaurar um ou mais arquivos danificados sem restaurar todo o banco de dados. No modelo de recuperação simples, os backups de arquivo possuem suporte apenas para grupos de arquivos somente leitura. O grupo de arquivos primário e os grupos de arquivos secundários leitura/gravação sempre são restaurados juntos, restaurando um banco de dados ou backup parcial.  
  
 Os cenários de restauração de arquivo são os seguintes:  
  
-   Restauração de arquivo offline  
  
     Em uma *restauração de arquivo offline*, o banco de dados fica offline enquanto os arquivos ou grupos de arquivos danificados são restaurados. Ao término da sequência de restauração, o banco de dados fica online.  
  
     Todas as edições do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] oferecem suporte à restauração de arquivos offline.  
  
-   Restauração de arquivo online  
  
     Em uma *restauração de arquivo online*, se o banco de dados estiver online no momento da restauração, ele permanecerá online durante a restauração do arquivo. Porém, cada grupo de arquivos no qual um arquivo está sendo restaurado fica offline durante a operação de restauração. Depois que todos os arquivos de um grupo de arquivos offline são recuperados, o grupo de arquivos é automaticamente colocado online.  
  
     Para obter informações sobre o suporte para restauração de arquivo e de página online, veja [Recursos com suporte nas edições do SQL Server 2016](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md). Para obter mais informações sobre restaurações online, veja [Restauração online &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md).  
  
    > [!TIP]  
    >  Se quiser que o banco de dados fique offline para uma restauração de arquivo, coloque o banco de dados offline antes de iniciar a sequência de restauração, executando a seguinte instrução [ALTER DATABASE](../Topic/ALTER%20DATABASE%20SET%20Options%20\(Transact-SQL\).md): ALTER DATABASE *database_name* SET OFFLINE.  
  
 **Neste tópico:**  
  
-   [Visão geral da restauração de arquivos e grupos de arquivos no modelo de recuperação simples](#Overview)  
  
-   [Tarefas relacionadas](#RelatedTasks)  
  
##  <a name="Overview"></a> Visão geral da restauração de arquivos e grupos de arquivos no modelo de recuperação simples  
 Um cenário de restauração de arquivos consiste em uma única sequência de restauração que copia, efetua roll forward e recupera os dados apropriados da seguinte maneira:  
  
1.  Restaure cada arquivo danificado de seu mais recente backup de arquivos.  
  
2.  Restaure o backup de arquivo diferencial mais recente para cada arquivo restaurado e recupere o banco de dados.  
  
### Etapas do Transact-SQL para a sequência de restauração de arquivos (modelo de recuperação simples)  
 Esta seção mostra as opções básicas de [RESTORE](../Topic/RESTORE%20\(Transact-SQL\).md) do [!INCLUDE[tsql](../../includes/tsql-md.md)] para uma sequência de restauração de arquivo simples. Sintaxe e detalhes que não sejam relevantes para esse propósito são omitidos.  
  
 A sequência de restauração contém apenas duas instruções [!INCLUDE[tsql](../../includes/tsql-md.md)]. A primeira instrução restaura um arquivo secundário, o arquivo `A`, que é restaurado usando WITH NORECOVERY. A segunda operação restaura dois outros arquivos, `B` e `C`, que são restaurados usando WITH RECOVERY de um dispositivo de backup diferente:  
  
1.  RESTORE DATABASE *database* FILE **=***name_of_file_A*  
  
     FROM *file_backup_of_file_A*  
  
     WITH NORECOVERY**;**  
  
2.  RESTORE DATABASE *database* FILE **=***name_of_file_B***,***name_of_file_C*  
  
     FROM *file_backup_of_files_B_and_C*  
  
     WITH RECOVERY**;**  
  
### Exemplos  
  
-   [Exemplo: restauração online de um arquivo somente leitura &#40;Modelo de recuperação simples&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [Exemplo: restauração offline do grupo de arquivos primário e mais um &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/example-offline-restore-of-primary-and-one-other-filegroup-full-recovery-model.md)  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
 **Para restaurar arquivos e grupos de arquivos**  
  
-   [Restaurar arquivos e grupos de arquivos sobre arquivos existentes &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-over-existing-files-sql-server.md)  
  
-   [Restaurar arquivos e grupos de arquivos &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-sql-server.md)  
  
-   [Restaurar arquivos e grupos de arquivos &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-sql-server.md)  
  
-   [Método Restore.SqlRestore (Servidor)](../Topic/SqlRestore%20Method.md) (SMO)  
  
## Consulte também  
 [Backup e restauração: interoperabilidade e coexistência &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-and-restore-interoperability-and-coexistence-sql-server.md)   
 [Backups diferenciais &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)   
 [Backups completos de arquivos &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-file-backups-sql-server.md)   
 [Visão geral do backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [Visão geral de restauração e recuperação &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../Topic/RESTORE%20\(Transact-SQL\).md)   
 [Restaurações completas de banco de dados &#40;Modelo de recuperação simples#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)   
 [Restaurações por etapas &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  