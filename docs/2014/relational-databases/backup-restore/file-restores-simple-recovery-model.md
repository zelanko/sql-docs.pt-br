---
title: Restaurações de arquivos (modelo de recuperação simples) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
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
caps.latest.revision: 45
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: e49707105972ce957c96f226079e8700ccedb4fb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007950"
---
# <a name="file-restores-simple-recovery-model"></a>Restaurações de arquivos (modelo de recuperação simples)
  Este tópico é relevante apenas para bancos de dados modelo simples que contêm pelo menos um grupo de arquivos secundário somente leitura.  
  
 Em uma restauração de arquivo, a meta é restaurar um ou mais arquivos danificados sem restaurar todo o banco de dados. No modelo de recuperação simples, os backups de arquivo possuem suporte apenas para grupos de arquivos somente leitura. O grupo de arquivos primário e os grupos de arquivos secundários leitura/gravação sempre são restaurados juntos, restaurando um banco de dados ou backup parcial.  
  
 Os cenários de restauração de arquivo são os seguintes:  
  
-   Restauração de arquivo offline  
  
     Em uma *restauração de arquivo offline*, o banco de dados fica offline enquanto os arquivos ou grupos de arquivos danificados são restaurados. Ao término da sequência de restauração, o banco de dados fica online.  
  
     Todas as edições do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] oferecem suporte à restauração de arquivos offline.  
  
-   Restauração de arquivo online  
  
     Em uma *restauração de arquivo online*, se o banco de dados estiver online no momento da restauração, ele permanecerá online durante a restauração do arquivo. Porém, cada grupo de arquivos no qual um arquivo está sendo restaurado fica offline durante a operação de restauração. Depois que todos os arquivos de um grupo de arquivos offline são recuperados, o grupo de arquivos é automaticamente colocado online.  
  
     Para obter informações sobre o suporte para restauração de arquivo e de página online, consulte [Recursos com suporte nas edições do SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md). Para obter mais informações sobre restaurações online, veja [Restauração online &#40;SQL Server&#41;](online-restore-sql-server.md).  
  
    > [!TIP]  
    >  Se quiser que o banco de dados fique offline para uma restauração de arquivo, coloque o banco de dados offline antes de iniciar a sequência de restauração, executando a seguinte instrução [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-set-options) : ALTER DATABASE *database_name* SET OFFLINE.  
  

  
##  <a name="Overview"></a> Visão geral da restauração de arquivos e grupos de arquivos no modelo de recuperação simples  
 Um cenário de restauração de arquivos consiste em uma única sequência de restauração que copia, efetua roll forward e recupera os dados apropriados da seguinte maneira:  
  
1.  Restaure cada arquivo danificado de seu mais recente backup de arquivos.  
  
2.  Restaure o backup de arquivo diferencial mais recente para cada arquivo restaurado e recupere o banco de dados.  
  
### <a name="transact-sql-steps-for-file-restore-sequence-simple-recovery-model"></a>Etapas do Transact-SQL para a sequência de restauração de arquivos (modelo de recuperação simples)  
 Esta seção mostra as opções básicas de [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) do [!INCLUDE[tsql](../../../includes/tsql-md.md)] para uma sequência de restauração de arquivo simples. Sintaxe e detalhes que não sejam relevantes para esse propósito são omitidos.  
  
 A sequência de restauração contém apenas duas instruções [!INCLUDE[tsql](../../../includes/tsql-md.md)] . A primeira instrução restaura um arquivo secundário, o arquivo `A`, que é restaurado usando WITH NORECOVERY. A segunda operação restaura dois outros arquivos, `B` e `C` , que são restaurados usando WITH RECOVERY de um dispositivo de backup diferente:  
  
1.  RESTORE DATABASE *database* FILE **=***name_of_file_A*  
  
     FROM *file_backup_of_file_A*  
  
     WITH NORECOVERY **;**  
  
2.  RESTORE DATABASE *database* FILE **=***name_of_file_B***,***name_of_file_C*  
  
     FROM *file_backup_of_files_B_and_C*  
  
     WITH RECOVERY **;**  
  
### <a name="examples"></a>Exemplos  
  
-   [Exemplo: restauração online de um arquivo somente leitura &#40;Modelo de recuperação simples&#41;](example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [Exemplo: restauração offline do grupo de arquivos primário e mais um &#40;Modelo de recuperação completa&#41;](example-offline-restore-of-primary-and-one-other-filegroup-full-recovery-model.md)  
  
 
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
 **Para restaurar arquivos e grupos de arquivos**  
  
-   [Restaurar arquivos e grupos de arquivos sobre arquivos existentes &#40;SQL Server&#41;](restore-files-and-filegroups-over-existing-files-sql-server.md)  
  
-   [Restaurar arquivos e grupos de arquivos &#40;SQL Server&#41;](restore-files-and-filegroups-sql-server.md)  
  
-   [Restaurar arquivos e grupos de arquivos &#40;SQL Server&#41;](restore-files-and-filegroups-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.SqlRestore%2A> (SMO)  
  
  
  
## <a name="see-also"></a>Consulte também  
 [Backup e restauração: interoperabilidade e coexistência &#40;SQL Server&#41;](backup-and-restore-interoperability-and-coexistence-sql-server.md)   
 [Backups diferenciais &#40;SQL Server&#41;](differential-backups-sql-server.md)   
 [Backups completos de arquivos &#40;SQL Server&#41;](full-file-backups-sql-server.md)   
 [Visão geral do backup &#40;SQL Server&#41;](backup-overview-sql-server.md)   
 [Visão geral de restauração e recuperação &#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [Restaurações completas de banco de dados &#40;Modelo de recuperação simples#41;](complete-database-restores-simple-recovery-model.md)   
 [Restaurações por etapas &#40;SQL Server&#41;](piecemeal-restores-sql-server.md)  
  
  
