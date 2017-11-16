---
title: "Exemplo: restauração por etapas de banco de dados (modelo de recuperação completa) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- full recovery model [SQL Server], RESTORE example
- piecemeal restores [SQL Server], full recovery model
- restore sequences [SQL Server], piecemeal
ms.assetid: 0a84892d-2f7a-4e77-b2d0-d68b95595210
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: de3fcaf6e6b0eb39a5f9ef189bd109aaa3850a26
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="example-piecemeal-restore-of-database-full-recovery-model"></a>Exemplo: Restauração de banco de dados por etapas (modelo de recuperação completa)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Uma sequência de restauração por etapas restaura e recupera um banco de dados em etapas no nível do grupo de arquivos, começando pelo grupo de arquivos primário e todos os grupos de arquivo secundários de leitura e gravação.  
  
 Nesse exemplo, o banco de dados `adb` é restaurado em um computador novo depois de um desastre. O banco de dados está usando o modelo de recuperação completa; portanto, antes do início da restauração, um backup do final do log deve ser extraído do banco de dados. Antes do desastre, todos os grupos de arquivos estão online. O grupo de arquivos `B` é somente leitura. Todos os grupos de arquivos secundários precisam ser restaurados, mas são restaurados em ordem de importância: `A` (mais alto), `C`, e por fim `B`. Nesse exemplo, há quatro backups de log, inclusive o backup do final do log.  
  
## <a name="tail-log-backup"></a>Backup do final do log  
 Antes de restaurar o banco de dados, o administrador do banco de dados deve fazer backup do final do log. Como o banco de dados está danificado, é preciso usar a opção NO_TRUNCATE para criar o backup do final do log:  
  
```  
BACKUP LOG adb TO tailLogBackup WITH NORECOVERY, NO_TRUNCATE  
```  
  
 O backup do final do log é o último backup aplicado nas sequências de restauração a seguir.  
  
## <a name="restore-sequences"></a>Sequências da restauração  
  
> [!NOTE]  
>  A sintaxe para uma sequência de restauração online é igual à de uma sequência de restauração offline.  
  
1.  Restauração parcial do grupo de arquivos primário e secundário `A`.  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='Primary' FROM backup1   
       WITH PARTIAL, NORECOVERY  
    RESTORE DATABASE adb FILEGROUP='A' FROM backup2   
       WITH NORECOVERY  
    RESTORE LOG adb FROM backup3 WITH NORECOVERY  
    RESTORE LOG adb FROM backup4 WITH NORECOVERY  
    RESTORE LOG adb FROM backup5 WITH NORECOVERY  
    RESTORE LOG adb FROM tailLogBackup WITH RECOVERY  
    ```  
  
2.  Restauração online do grupo de arquivos `C`.  
  
     Neste momento, o grupo de arquivos primário e o grupo de arquivos secundário `A` estão online. Todos os arquivos nos grupos de arquivos `B` e `C` estão em recuperação pendente e os grupos de arquivos estão offline.  
  
     Mensagens da última instrução `RESTORE LOG` na etapa 1 indicam que a reversão das transações que envolvem o grupo de arquivos `C` foi adiada, porque o grupo de arquivos não está disponível. As operações regulares podem continuar, mas bloqueios são mantidos por essas transações e o truncamento de log não acontecerá até que a reversão esteja concluída.  
  
     Na segunda sequência de restauração, o administrador de banco de dados restaura o grupo de arquivos `C`:  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='C' FROM backup2a WITH NORECOVERY  
    RESTORE LOG adb FROM backup3 WITH NORECOVERY  
    RESTORE LOG adb FROM backup4 WITH NORECOVERY  
    RESTORE LOG adb FROM backup5 WITH NORECOVERY  
    RESTORE LOG adb FROM tailLogBackup WITH RECOVERY  
    ```  
  
     Neste momento, o grupo de arquivos primário e os grupos de arquivos `A` e `C` estão online. Os arquivos no grupo de arquivos `B` permanecem em recuperação pendente, com o grupo de arquivos offline. As transações adiadas foram resolvidas e o truncamento de log acontece.  
  
3.  Restauração online do grupo de arquivos `B`.  
  
     Na terceira sequência de restauração, o administrador de banco de dados restaura o grupo de arquivos `B`. O backup do grupo de arquivos `B` foi realizado depois de o grupo de arquivos tornar-se somente leitura; portanto, não tem de efetuar roll forward durante a recuperação.  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='B' FROM backup2b WITH RECOVERY  
    ```  
  
     Todos os grupos de arquivos agora estão online.  
  
## <a name="additional-examples"></a>Exemplos adicionais  
  
-   [Exemplo: restauração por etapas de banco de dados &#40;Modelo de recuperação simples&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [Exemplo: restauração por etapas de apenas alguns grupos de arquivos &#40;Modelo de recuperação simples&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [Exemplo: restauração online de um arquivo somente leitura &#40;Modelo de recuperação simples&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [Exemplo: restauração por etapas de apenas alguns grupos de arquivos &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [Exemplo: restauração online de um arquivo de leitura/gravação #40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [Exemplo: restauração online de um arquivo somente leitura &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
## <a name="see-also"></a>Consulte também  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Restauração online &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [Aplicar backups de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Restaurações por etapas &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  
