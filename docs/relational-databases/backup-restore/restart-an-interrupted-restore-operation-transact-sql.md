---
title: "Reiniciar uma operação de restauração interrompida (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interrupted restore operation
- restoring databases [SQL Server], restarting interrupted operation
- resetting options changed after backup
- database restores [SQL Server], restarting interrupted operation
- restarting interrupted restore operation
- restoring interrupted operation [SQL Server]
ms.assetid: 6413a07d-fd90-448d-8f29-12c5a1972618
caps.latest.revision: 24
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1a41e345b6122be18ca05186e7bc82d48c566fb9
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="restart-an-interrupted-restore-operation-transact-sql"></a>Reiniciar uma operação de restauração interrompida (Transact-SQL)
  Este tópico explica como reiniciar uma operação de restauração interrompida.  
  
### <a name="to-restart-an-interrupted-restore-operation"></a>Para reinicializar uma operação de restauração interrompida  
  
1.  Execute a instrução interrompida RESTORE novamente, especificando:  
  
    -   As mesmas cláusulas usadas na instrução RESTORE original.  
  
    -   A cláusula RESTART.  
  
## <a name="example"></a>Exemplo  
 Esse exemplo reinicia uma operação de restauração interrompida.  
  
```tsql  
-- Restore a full database backup of the AdventureWorks database.  
RESTORE DATABASE AdventureWorks  
   FROM DISK = 'C:\AdventureWorks.bck'  
GO  
-- The restore operation halted prematurely.  
-- Repeat the original RESTORE statement specifying WITH RESTART.  
RESTORE DATABASE AdventureWorks   
   FROM DISK = 'C:\AdventureWorks.bck'  
   WITH RESTART  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Restaurações completas de banco de dados &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)   
 [Restaurações completas de banco de dados &#40;Modelo de recuperação simples#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
