---
title: 'Restauração por etapas: apenas alguns grupos de arquivos (modelo de recuperação simples)'
description: Este exemplo mostra uma restauração por etapas no SQL Server de apenas alguns grupos de arquivos de um banco de dados usando o modelo de recuperação simples.
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- piecemeal restores [SQL Server], simple recovery model
- restore sequences [SQL Server], piecemeal
- simple recovery model [SQL Server], RESTORE examples
ms.assetid: d7ad026c-5355-4308-9560-0dc843940d4f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 1673e3999b6a37ea6383b940bb5e7b66ac922984
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "82179078"
---
# <a name="example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model"></a>Exemplo: Restauração por etapas de apenas alguns grupos de arquivos (modelo de recuperação simples)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este tópico é pertinente para bancos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sob o modelo de recuperação simples que contenham um grupo de arquivos somente leitura.  
  
 Uma sequência de restauração por etapas restaura e recupera um banco de dados em etapas no nível do grupo de arquivos, começando pelo grupo de arquivos primário e todos os grupos de arquivos secundários de leitura e gravação.  
  
 Nesse exemplo, um banco de dados nomeado `adb`, que usa o modelo de recuperação simples, contém três grupos de arquivos. O grupo de arquivos `A` é de leitura/gravação e os grupos de arquivos `B` e `C` são somente leitura. Inicialmente, todos os grupos de arquivos estão online.  
  
 O grupo de arquivos primário e `B` do banco de dados `adb` parecem estar danificados; então, o administrador de banco de dados decide restaurá-los usando uma sequência de restauração por etapas. Sob o modelo de recuperação simples, todos os grupos de arquivos de leitura/gravação devem ser restaurados do mesmo backup parcial. Embora o grupo de arquivos `A` esteja intacto, deve ser restaurado com o grupo de arquivos primário para ter certeza que eles são consistentes (o banco de dados será restaurado a tempo ao ponto definido ao final do último backup parcial). Grupo de arquivos `C` está intacto, mas deve ser recuperado para ser colocado online. Grupo de arquivos `B`, embora danificado, contém dados menos essenciais que o grupo de arquivos `C`; então, `B` será restaurado por último.  
  
## <a name="restore-sequences"></a>Sequências da restauração  
  
> [!NOTE]  
>  A sintaxe para uma sequência de restauração online é igual à de uma sequência de restauração offline.  
  
1.  Restauração parcial do grupo de arquivos primário e `A` de um backup parcial.  
  
    ```  
    RESTORE DATABASE adb READ_WRITE_FILEGROUPS FROM partial_backup   
    WITH PARTIAL, RECOVERY  
    ```  
  
     Neste momento, o grupo de arquivos primário e o grupo de arquivos `A` estão online. Os arquivos nos grupos de arquivos `B` e `C` estão com sua recuperação pendente e os grupos de arquivos estão offline.  
  
2.  Recuperação online do grupo de arquivos `C`.  
  
     Grupo de arquivos `C` é consistente porque o backup parcial que foi restaurado acima foi realizado depois que grupo de arquivos `C` tornou-se somente leitura, embora o banco de dados tenha sido recuperado a tempo pela restauração. O administrador de banco de dados recupera o grupo de arquivos `C`, sem restaurá-lo, colocá-lo online.  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='C' WITH RECOVERY  
    ```  
  
     Neste momento, o grupo de arquivos primário e os grupos de arquivos `A` e `C` estão online. Os arquivos no grupo de arquivosB permanecem em recuperação pendente, com o grupo de arquivos offline.  
  
3.  Restauração online do grupo de arquivos `B.`  
  
     Arquivos em grupo de arquivos `B` devem ser restaurados. O administrador de banco de dados restaura o backup do grupo de arquivos `B` realizado após o grupo de arquivos `B` tornar-se somente leitura e antes do backup parcial.  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='B' FROM backup   
    WITH RECOVERY  
    ```  
  
     Todos os grupos de arquivos agora estão online.  
  
## <a name="additional-examples"></a>Exemplos adicionais  
  
-   [Exemplo: Restauração por etapas de banco de dados &#40;Modelo de recuperação simples&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [Exemplo: restauração online de um arquivo somente leitura &#40;Modelo de recuperação simples&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [Exemplo: Restauração por etapas de banco de dados &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [Exemplo: Restauração por etapas de apenas alguns grupos de arquivos &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [Exemplo: restauração online de um arquivo de leitura/gravação #40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [Exemplo: restauração online de um arquivo somente leitura #40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Restauração online &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Restaurações por etapas &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  
