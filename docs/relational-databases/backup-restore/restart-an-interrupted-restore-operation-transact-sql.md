---
title: "Reiniciar uma opera&#231;&#227;o de restaura&#231;&#227;o interrompida (Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "operação de restauração interrompida"
  - "restaurando bancos de dados [SQL Server], reiniciando operação interrompida"
  - "reconfigurando opções alteradas depois de backup"
  - "restaurações de banco de dados [SQL Server], reiniciando operação interrompida"
  - "reiniciando uma operação de restauração interrompida"
  - "reiniciando uma operação interrompida [SQL Server]"
ms.assetid: 6413a07d-fd90-448d-8f29-12c5a1972618
caps.latest.revision: 24
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 24
---
# Reiniciar uma opera&#231;&#227;o de restaura&#231;&#227;o interrompida (Transact-SQL)
  Este tópico explica como reiniciar uma operação de restauração interrompida.  
  
### Para reinicializar uma operação de restauração interrompida  
  
1.  Execute a instrução interrompida RESTORE novamente, especificando:  
  
    -   As mesmas cláusulas usadas na instrução RESTORE original.  
  
    -   A cláusula RESTART.  
  
## Exemplo  
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
  
## Consulte também  
 [Restaurações completas de banco de dados &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)   
 [Restaurações completas de banco de dados &#40;Modelo de recuperação simples#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)   
 [RESTORE &#40;Transact-SQL&#41;](../Topic/RESTORE%20\(Transact-SQL\).md)  
  
  