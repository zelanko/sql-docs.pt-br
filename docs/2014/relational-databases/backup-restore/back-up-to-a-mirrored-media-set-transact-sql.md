---
title: Fazer backup de um conjunto de mídias espelhado (Transact-SQL)   Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 5fc43a5d-dfd6-4c53-a4ef-3c8da23ccc81
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 255a3c190139c029f5211dcab9780b6d07d975a4
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84959483"
---
# <a name="back-up-to-a-mirrored-media-set-transact-sql"></a>Fazer backup em um conjunto de mídias espelhado (Transact-SQL)
  Este tópico descreve como usar a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] [backup](/sql/t-sql/statements/backup-transact-sql) para especificar um conjunto de mídias espelhadas ao fazer backup de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados do. Na instrução BACKUP, especifique o primeiro espelho na cláusula TO. Em seguida, especifique cada espelho em sua própria cláusula MIRROR TO. As cláusulas TO e MIRROR TO devem especificar o mesmo número e tipo de dispositivos de backup.  
  
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
  
## <a name="related-tasks"></a>Related Tasks  
 **Para restaurar um backup espelhado**  
  
-   [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
## <a name="see-also"></a>Consulte Também  
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [Conjuntos de mídias de backup espelhadas &#40;SQL Server&#41;](mirrored-backup-media-sets-sql-server.md)  
  
  
