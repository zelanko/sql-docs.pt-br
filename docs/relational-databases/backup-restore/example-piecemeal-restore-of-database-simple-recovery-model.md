---
title: "Exemplo: Restaura&#231;&#227;o por etapas de banco de dados (modelo de recupera&#231;&#227;o simples) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "restaurações por etapas [SQL Server], modelo de recuperação simples"
  - "sequências de restauração [SQL Server], por etapas"
  - "modelo de recuperação simples [SQL Server], exemplos de RESTAURAÇÃO"
ms.assetid: 9834b14a-4e56-4654-b190-c2a38624b6b4
caps.latest.revision: 27
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 27
---
# Exemplo: Restaura&#231;&#227;o por etapas de banco de dados (modelo de recupera&#231;&#227;o simples)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Uma sequência de restauração por etapas restaura e recupera um banco de dados em etapas no nível do grupo de arquivos, começando pelo grupo de arquivos primários e todos os grupos de arquivos secundários de leitura e gravação.  
  
 Nesse exemplo, o banco de dados `adb` é restaurado em um computador novo depois de um desastre. O banco de dados está usando o modelo de recuperação simples. Antes do desastre, todos os grupos de arquivos estão online. Os grupos de arquivos `A` e `C` são de leitura/gravação e o grupo de arquivos `B` é somente leitura. O grupo de arquivos `B` se tornou somente leitura antes do mais recente backup parcial, que contém o grupo de arquivos primários e os grupos de arquivos secundários de leitura/gravação, `A` e `C`. Depois que o grupo de arquivos `B` tornou-se somente leitura, foi feito um backup de arquivo separado do grupo de arquivos `B`.  
  
## Sequências da restauração  
  
1.  Restauração parcial do grupo de arquivos primários e grupos de arquivos `A` e `C`.  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='A',FILEGROUP='C'   
       FROM partial_backup   
       WITH PARTIAL, RECOVERY;  
  
    ```  
  
     Neste momento, o grupo de arquivos primários e os grupos de arquivos `A` e `C` estão online. Todos os arquivos no grupo de arquivos `B` estão com recuperação pendente e o grupo de arquivos está offline.  
  
2.  Restauração online do grupo de arquivos `B`.  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='B' FROM backup WITH RECOVERY;  
  
    ```  
  
     Todos os grupos de arquivos agora estão online.  
  
## Exemplos adicionais  
  
-   [Exemplo: restauração por etapas de apenas alguns grupos de arquivos &#40;Modelo de recuperação simples&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [Exemplo: restauração online de um arquivo somente leitura &#40;Modelo de recuperação simples&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [Exemplo: restauração por etapas de banco de dados &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [Exemplo: restauração por etapas de apenas alguns grupos de arquivos &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [Exemplo: restauração online de um arquivo de leitura/gravação #40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [Exemplo: restauração online de um arquivo somente leitura &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
## Consulte também  
 [Restauração online &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../Topic/RESTORE%20\(Transact-SQL\).md)   
 [Restaurações por etapas &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  