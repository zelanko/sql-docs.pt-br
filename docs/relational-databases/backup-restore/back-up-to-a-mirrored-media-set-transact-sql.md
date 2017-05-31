---
title: "Fazer backup de um conjunto de mídias espelhado (Transact-SQL)   Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5fc43a5d-dfd6-4c53-a4ef-3c8da23ccc81
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5c73a69d7816dee3f9be301995a2522fafb8091c
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="back-up-to-a-mirrored-media-set-transact-sql"></a>Fazer backup em um conjunto de mídias espelhado (Transact-SQL)
  Este tópico descreve como usar a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)][BACKUP](../../t-sql/statements/backup-transact-sql.md) para especificar um conjunto de mídias espelhado ao fazer backup de um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Na instrução BACKUP, especifique o primeiro espelho na cláusula TO. Em seguida, especifique cada espelho em sua própria cláusula MIRROR TO. As cláusulas TO e MIRROR TO devem especificar o mesmo número e tipo de dispositivos de backup.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir cria o conjunto de mídias espelhado mostrado na ilustração anterior e faz backup do banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] para ambos os espelhos.  
  
```  
BACKUP DATABASE AdventureWorks2012  
TO TAPE = '\\.\tape0', TAPE = '\\.\tape1'  
MIRROR TO TAPE = '\\.\tape2', TAPE = '\\.\tape3'  
WITH  
    FORMAT,  
    MEDIANAME = 'AdventureWorks2012Set1';  
GO  
```  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
 **Para restaurar um backup espelhado**  
  
-   [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
## <a name="see-also"></a>Consulte também  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Conjuntos de mídias de backup espelhadas &#40;SQL Server&#41;](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md)  
  
  
