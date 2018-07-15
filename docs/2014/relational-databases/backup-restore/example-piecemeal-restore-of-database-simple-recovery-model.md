---
title: 'Exemplo: restauração por etapas de banco de dados (modelo de recuperação simples) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: backup-restore
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- piecemeal restores [SQL Server], simple recovery model
- restore sequences [SQL Server], piecemeal
- simple recovery model [SQL Server], RESTORE examples
ms.assetid: 9834b14a-4e56-4654-b190-c2a38624b6b4
caps.latest.revision: 26
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 12cbb85f6fc335fcb944bee8eb270315dca4957e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37170917"
---
# <a name="example-piecemeal-restore-of-database-simple-recovery-model"></a>Exemplo: Restauração por etapas de banco de dados (modelo de recuperação simples)
  Uma sequência de restauração por etapas restaura e recupera um banco de dados em etapas no nível do grupo de arquivos, começando pelo grupo de arquivos primários e todos os grupos de arquivos secundários de leitura e gravação.  
  
 Nesse exemplo, o banco de dados `adb` é restaurado em um computador novo depois de um desastre. O banco de dados está usando o modelo de recuperação simples. Antes do desastre, todos os grupos de arquivos estão online. Os grupos de arquivos `A` e `C` são de leitura/gravação e o grupo de arquivos `B` é somente leitura. O grupo de arquivos `B` se tornou somente leitura antes do mais recente backup parcial, que contém o grupo de arquivos primários e os grupos de arquivos secundários de leitura/gravação, `A` e `C`. Depois que o grupo de arquivos `B` tornou-se somente leitura, foi feito um backup de arquivo separado do grupo de arquivos `B` .  
  
## <a name="restore-sequences"></a>Sequências da restauração  
  
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
  
## <a name="additional-examples"></a>Exemplos adicionais  
  
-   [Exemplo: restauração por etapas de apenas alguns grupos de arquivos &#40;Modelo de recuperação simples&#41;](example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [Exemplo: restauração online de um arquivo somente leitura &#40;Modelo de recuperação simples&#41;](example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [Exemplo: restauração por etapas de banco de dados &#40;Modelo de recuperação completa&#41;](example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [Exemplo: restauração por etapas de apenas alguns grupos de arquivos &#40;Modelo de recuperação completa&#41;](example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [Exemplo: restauração online de um arquivo de leitura/gravação #40;Modelo de recuperação completa&#41;](example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [Exemplo: restauração online de um arquivo somente leitura &#40;Modelo de recuperação completa&#41;](example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
## <a name="see-also"></a>Consulte também  
 [Restauração online &#40;SQL Server&#41;](online-restore-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [Restaurações por etapas &#40;SQL Server&#41;](piecemeal-restores-sql-server.md)  
  
  
