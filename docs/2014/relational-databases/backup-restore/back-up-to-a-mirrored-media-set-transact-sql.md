---
title: Fazer backup de um conjunto de mídias espelhado (Transact-SQL)   Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: backup-restore
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5fc43a5d-dfd6-4c53-a4ef-3c8da23ccc81
caps.latest.revision: 4
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b423352337f224c0f3a920e08040f686fd4d49fb
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37201516"
---
# <a name="back-up-to-a-mirrored-media-set-transact-sql"></a>Fazer backup em um conjunto de mídias espelhado (Transact-SQL)
  Este tópico descreve como usar a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)][BACKUP](/sql/t-sql/statements/backup-transact-sql) para especificar um conjunto de mídias espelhado ao fazer backup de um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Na instrução BACKUP, especifique o primeiro espelho na cláusula TO. Em seguida, especifique cada espelho em sua própria cláusula MIRROR TO. As cláusulas TO e MIRROR TO devem especificar o mesmo número e tipo de dispositivos de backup.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [Conjuntos de mídias de backup espelhadas &#40;SQL Server&#41;](mirrored-backup-media-sets-sql-server.md)  
  
  
