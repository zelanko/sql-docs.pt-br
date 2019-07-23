---
title: Restaurações de arquivos (modelo de recuperação completa) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- file restores [SQL Server]
- full recovery model [SQL Server], performing restores
- restoring files [SQL Server], Transact-SQL restore sequence
- restoring files [SQL Server]
- file restores [SQL Server], full recovery model
- restoring files [SQL Server], full recovery model
- Transact-SQL restore sequence
- file restores [SQL Server], Transact-SQL restore sequence
ms.assetid: d2236a2a-4cf1-4c3f-b542-f73f6096e15c
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 8c7c50136b05c94bacda9d400bf8afd5d8640f0c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138758"
---
# <a name="file-restores-full-recovery-model"></a>Restaurações de arquivo (modelo de recuperação completa)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este tópico é relevante apenas para bancos de dados que contêm vários arquivos ou grupos de arquivos sob o modelo de recuperação completa ou de carregamento em massa.  
  
 Em uma restauração de arquivo, a meta é restaurar um ou mais arquivos danificados sem restaurar todo o banco de dados. Um cenário de restauração de arquivo consiste em uma única sequência de restauração que copia, efetua roll forward e recupera os dados apropriados  
  
 Se o grupo de arquivos que é restaurado for de leitura/gravação, uma cadeia ininterrupta de backups de log deve ser aplicada após o último backup de dados ou diferencial ser restaurado. Isso faz com que o grupo de arquivos avance para os registros de log nos registros de log ativos atuais no arquivo de log. O ponto de recuperação está normalmente próximo o término do log, mas não necessariamente.  
  
 Se o grupo de arquivos que está sendo restaurado for somente leitura, normalmente aplicar backups de log será desnecessário e ignorado. Se o backup for realizado depois que o arquivo se torne somente leitura, ele será o último backup a restaurar. Roll-forward para no ponto de destino.  
  
 Os cenários de restauração de arquivo são os seguintes:  
  
-   Restauração de arquivo offline  
  
     Em uma *restauração de arquivo offline*, o banco de dados fica offline enquanto os arquivos ou grupos de arquivos danificados são restaurados. Ao término da sequência de restauração, o banco de dados fica online.  
  
     Todas as edições do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] oferecem suporte à restauração de arquivos offline.  
  
-   Restauração de arquivo online  
  
     Em uma *restauração de arquivo online*, se o banco de dados estiver online no momento da restauração, ele permanecerá online durante a restauração do arquivo. Porém, cada grupo de arquivos no qual um arquivo está sendo restaurado fica offline durante a operação de restauração. Depois que todos os arquivos de um grupo de arquivos offline são recuperados, o grupo de arquivos é automaticamente colocado online.  
  
     Para obter informações sobre o suporte para restauração de arquivo e de página online, consulte [Recursos com suporte e edições do SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md). Para obter informações sobre restaurações online, consulte [Restauração online (SQL Server)](../../relational-databases/backup-restore/online-restore-sql-server.md).
  
    > [!TIP]  
    >  Se você deseja que o banco de dados esteja offline para uma restauração arquivo, coloque o banco de dados offline antes de iniciar a sequência de restauração executando a seguinte instrução [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-set-options.md): ALTER DATABASE *database_name* SET OFFLINE.  
  
  
##  <a name="Overview"></a> Restaurando arquivos danificados de backups de arquivo  
  
1.  Antes de restaurar um ou mais arquivos danificados, tente criar um [backup da parte final do log](../../relational-databases/backup-restore/tail-log-backups-sql-server.md).  
  
     Se o log tiver sido danificado e não for possível criar um backup da parte final do log, você deverá restaurar todo o banco de dados.  
  
     Para obter informações sobre como fazer backup de um log de transações, veja [Backups de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md).  
  
    > [!IMPORTANT]  
    >  Para uma restauração de arquivo offline, você deve sempre fazer um backup do final do log antes da restauração do arquivo. Para uma restauração de arquivo online, você deve sempre fazer o backup do log após a restauração do arquivo. Este backup de log é necessário para permitir que o arquivo seja recuperado a um estado consistente com o restante do banco de dados.  
  
2.  Restaure cada arquivo danificado do backup de arquivos mais recente desse arquivo.  
  
3.  Restaure o backup de arquivo diferencial mais recente, se houver, para cada arquivo restaurado.  
  
4.  Restaure backups de log de transações em sequência, iniciando com o backup que inclui o mais antigo dos arquivos restaurados e terminando com o backup do final do log criado na etapa 1.  
  
     Você deve restaurar os backups de log de transações que foram criados após os backups de arquivo para trazer o banco de dados a um estado consistente. Os backups de log de transações podem ser rolados para frente rapidamente, porque somente são aplicadas as mudanças que se aplicam aos arquivos restaurados. Restaurar arquivos individuais pode ser melhor que restaurar todo o banco de dados, porque não são copiados arquivos não danificados e rolados para frente. Porém, a cadeia inteira de backups de log ainda tem que ser lida.  
  
5.  Recuperar o banco de dados.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

> [!NOTE]  
>  Podem ser usados backups de arquivo para restaurar o banco de dados a um ponto anterior no tempo. Para fazê-lo, você deve restaurar um conjunto completo de backups de arquivo e então restaurar backups de log de transações em sequência para alcançar um ponto de destino que busca o término do backup de arquivo restaurado mais recente. Para obter mais informações sobre a recuperação pontual, veja [Restaurar um banco de dados do SQL Server em um ponto específico &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md).  
  
## <a name="transact-sql-restore-sequence-for-an-offline-file-restore-full-recovery-model"></a>Sequência de restauração Transact-SQL para uma restauração de arquivo offline (modelo de recuperação completo)  
 Um cenário de restauração de arquivo consiste em uma única sequência de restauração que copia, rola para frente e recupera os dados apropriados.  
  
 Esta seção mostra as opções básicas de [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) para uma sequência de restauração de arquivo. Sintaxe e detalhes que não sejam relevantes para esse propósito são omitidos.  
  
 A sequência de restauração de exemplo a seguir mostra uma restauração offline de dois arquivos secundários, `A` e `B`, usando WITH NORECOVERY. Em seguida, dois backups de log são aplicados com NORECOVERY, seguido pelo backup do final do log que é restaurado com WITH RECOVERY.  
  
> [!NOTE]  
>  A sequência de restauração de exemplo a seguir começa colocando o arquivo offline e cria um backup do final do log.  
  
```  
--Take the file offline.  
ALTER DATABASE database_name MODIFY FILE SET OFFLINE;  
-- Back up the currently active transaction log.  
BACKUP LOG database_name  
   TO <tail_log_backup>  
   WITH NORECOVERY;  
GO   
-- Restore the files.  
RESTORE DATABASE database_name FILE=name   
   FROM <file_backup_of_file_A>   
   WITH NORECOVERY;  
RESTORE DATABASE database_name FILE=<name> ......  
   FROM <file_backup_of_file_B>   
   WITH NORECOVERY;  
-- Restore the log backups.  
RESTORE LOG database_name FROM <log_backup>   
   WITH NORECOVERY;  
RESTORE LOG database_name FROM <log_backup>   
   WITH NORECOVERY;  
RESTORE LOG database_name FROM <tail_log_backup>   
   WITH RECOVERY;  
```  
  
## <a name="examples"></a>Exemplos  
  
-   [Exemplo: restauração online de um arquivo de leitura/gravação #40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [Exemplo: restauração online de um arquivo somente leitura #40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
-   [Exemplo: restauração offline do grupo de arquivos primário e mais um &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/example-offline-restore-of-primary-and-one-other-filegroup-full-recovery-model.md)  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
 **Para restaurar arquivos e grupos de arquivos**  
  
-   [Restaurar arquivos em um novo local &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-to-a-new-location-sql-server.md)  
  
-   [Restaurar arquivos e grupos de arquivos &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.SqlRestore%2A> (SMO)  
  
  
## <a name="see-also"></a>Consulte Também  
 [Backup e Restauração: Interoperabilidade e Coexistência &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-and-restore-interoperability-and-coexistence-sql-server.md)   
 [Backups diferenciais &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)   
 [Backups completos de arquivos &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-file-backups-sql-server.md)   
 [Visão geral do backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [Visão geral de restauração e recuperação &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Restaurações completas de banco de dados &#40;Modelo de recuperação simples#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)   
 [Restaurações por etapas &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  
