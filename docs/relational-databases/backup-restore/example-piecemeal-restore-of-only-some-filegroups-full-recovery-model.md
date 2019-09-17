---
title: 'Exemplo: restauração por etapas de apenas alguns grupos de arquivos (modelo de recuperação completa) | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- full recovery model [SQL Server], RESTORE example
- piecemeal restores [SQL Server], full recovery model
- restore sequences [SQL Server], piecemeal
ms.assetid: bced4b54-e819-472b-b784-c72e14e72a0b
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: ec01941d4e8b333f3c29a38fd701b051acf04721
ms.sourcegitcommit: 26715b4dbef95d99abf2ab7198a00e6e2c550243
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70279484"
---
# <a name="example-piecemeal-restore-of-only-some-filegroups-full-recovery-model"></a>Exemplo: Restauração por etapas de apenas alguns grupos de arquivos (modelo de recuperação completa)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este tópico é relevante para bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sob o modelo de recuperação completa que contém vários arquivos ou grupos de arquivos.  
  
 Uma sequência de restauração por etapas restaura e recupera um banco de dados em etapas no nível do grupo de arquivos, começando pelo grupo de arquivos primários e todos os grupos de arquivos secundários de leitura e gravação.  
  
 Neste exemplo, um banco de dados nomeado `adb`, que usa o modelo de recuperação completa, contém três grupos de arquivos. O grupo de arquivos `A` é de leitura/gravação e os grupos de arquivos `B` e `C` são somente leitura. Inicialmente, todos os grupos de arquivos estão online.  
  
 O primário e grupo de arquivos `B` do banco de dados `adb` parecem estar danificados. O grupo de arquivos primário é bastante pequeno e pode ser restaurado rapidamente. O administrador do banco de dados decide restaurá-los usando a seguinte sequência de restauração por etapas: Primeiro, o grupo de arquivos primário e os logs de transações subsequentes são restaurados e o banco de dados é recuperado.  
  
 Os grupos de arquivos intactos `A` e `C` contêm dados críticos. Portanto, eles serão recuperados a seguir para colocá-los online o mais rápido possível. Finalmente, o grupo de arquivos secundário danificado, `B`, é restaurado e recuperado.  
  
## <a name="restore-sequences"></a>Sequências de restauração:  
  
> [!NOTE]  
>  A sintaxe para uma sequência de restauração online é igual à de uma sequência de restauração offline.  
  
1.  Crie um backup do final do log do banco de dados `adb`. Essa etapa é essencial para deixar os grupos de arquivos intactos `A` e `C` em dia com o ponto de recuperação do banco de dados.  
  
    ```  
    BACKUP LOG adb TO tailLogBackup WITH NORECOVERY  
    ```  
  
2.  Restauração parcial do grupo de arquivos primários.  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='Primary' FROM backup   
    WITH PARTIAL, NORECOVERY  
    RESTORE LOG adb FROM log_backup1 WITH NORECOVERY  
    RESTORE LOG adb FROM log_backup2 WITH NORECOVERY  
    RESTORE LOG adb FROM log_backup3 WITH NORECOVERY  
    RESTORE LOG adb FROM tailLogBackup WITH RECOVERY  
    ```  
  
     Neste momento o primário está online. Os arquivos nos grupos de arquivos `A`, `B`e `C` estão com sua recuperação pendente e os grupos de arquivos estão offline.  
  
3.  Restauração online dos grupos de arquivos `A` e `C`.  
  
     Como seus dados não estão danificados, esses grupos de arquivos não têm de ser restaurados de um backup, mas eles têm de ser recuperados para serem colocados online.  
  
     O administrador do banco de dados recupera `A` e `C` imediatamente.  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='A', FILEGROUP='C' WITH RECOVERY  
    ```  
  
     Neste momento, o grupo de arquivos primário e os grupos de arquivos `A` e `C` estão online. Os arquivos no grupo de arquivos `B` permanecem em recuperação pendente, com o grupo de arquivos offline.  
  
4.  Restauração online do grupo de arquivos `B`.  

   Os arquivos no grupo de arquivos `B` são restaurados a partir desse momento.  
  
   > [!NOTE]  
   >  O backup do grupo de arquivos `B` foi realizado depois de o grupo de arquivos tornar-se somente leitura; portanto, não há necessidade de efetuar roll-forward nesses arquivos.  
  
   ```sql  
   RESTORE DATABASE adb FILEGROUP='B' FROM backup WITH RECOVERY  
   ```  
  
   Todos os grupos de arquivos agora estão online.  
  
## <a name="additional-examples"></a>Exemplos adicionais  
  
-   [Exemplo: Restauração por etapas de banco de dados &#40;Modelo de recuperação simples&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [Exemplo: Restauração por etapas de apenas alguns grupos de arquivos &#40;Modelo de recuperação simples&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [Exemplo: restauração online de um arquivo somente leitura &#40;Modelo de recuperação simples&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [Exemplo: Restauração por etapas de banco de dados &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [Exemplo: restauração online de um arquivo de leitura/gravação #40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [Exemplo: restauração online de um arquivo somente leitura #40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
## <a name="see-also"></a>Consulte Também  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Restauração online &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [Aplicar backups de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Restaurações por etapas &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  
