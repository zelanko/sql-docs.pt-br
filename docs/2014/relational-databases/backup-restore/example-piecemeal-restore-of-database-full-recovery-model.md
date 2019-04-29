---
title: 'Exemplo: restauração por etapas de banco de dados (modelo de recuperação completa) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- full recovery model [SQL Server], RESTORE example
- piecemeal restores [SQL Server], full recovery model
- restore sequences [SQL Server], piecemeal
ms.assetid: 0a84892d-2f7a-4e77-b2d0-d68b95595210
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 157541fe3792ba082d9b1ec84c3ab45ca0617060
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62875818"
---
# <a name="example-piecemeal-restore-of-database-full-recovery-model"></a>Exemplo: Restauração de banco de dados por etapas (modelo de recuperação completa)
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
  
-   [Exemplo: Restauração por etapas de banco de dados &#40;Modelo de recuperação simples&#41;](example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [Exemplo: Restauração por etapas de apenas alguns grupos de arquivos &#40;Modelo de recuperação simples&#41;](example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [Exemplo: restauração online de um arquivo somente leitura &#40;Modelo de recuperação simples&#41;](example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [Exemplo: Restauração por etapas de apenas alguns grupos de arquivos &#40;Modelo de recuperação completa&#41;](example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [Exemplo: restauração online de um arquivo de leitura/gravação #40;Modelo de recuperação completa&#41;](example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [Exemplo: restauração online de um arquivo somente leitura #40;Modelo de recuperação completa&#41;](example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
## <a name="see-also"></a>Consulte também  
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [Restauração online &#40;SQL Server&#41;](online-restore-sql-server.md)   
 [Aplicar backups de log de transações &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [Restaurações por etapas &#40;SQL Server&#41;](piecemeal-restores-sql-server.md)  
  
  
