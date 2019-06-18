---
title: Restaurar o banco de dados para o ponto de falha – recuperação completa | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- point of failure [SQL Server]
- restoring databases [SQL Server], point of failure
- database restores [SQL Server], point of failure
ms.assetid: 04106e18-bbf7-4a5e-a2e1-3d65319814d5
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9ba2b49bf53a95836923e8016b68e2fbf7c7bbb1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62507097"
---
# <a name="restore-database-to-point-of-failure---full-recovery"></a>Restaurar o banco de dados para o ponto de falha – Recuperação completa
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este tópico explica como restaurar até o ponto de falha. O tópico é relevante apenas para bancos de dados que estejam usando modelos de recuperação completa ou com bulk-logged.  
  
### <a name="to-restore-to-the-point-of-failure"></a>Para restaurar até o ponto de falha  
  
1.  Faça backup do final do log executando a seguinte instrução básica [BACKUP](../../t-sql/statements/backup-transact-sql.md) :  
  
    ```  
    BACKUP LOG <database_name> TO <backup_device>   
       WITH NORECOVERY, NO_TRUNCATE;  
    ```  
  
2.  Restaure um backup de banco de dados completo executando a seguinte instrução básica [RESTORE DATABASE](../../t-sql/statements/restore-statements-transact-sql.md) :  
  
    ```  
    RESTORE DATABASE <database_name> FROM <backup_device>   
       WITH NORECOVERY;  
    ```  
  
3.  Opcionalmente, restaure um backup de banco de dados diferencial executando a seguinte instrução básica RESTORE DATABASE:  
  
    ```  
    RESTORE DATABASE <database_name> FROM <backup_device>   
       WITH NORECOVERY;  
    ```  
  
4.  Aplique cada log de transações, inclusive o backup do final do log criado na etapa 1, especificando WITH NORECOVERY na instrução RESTORE LOG:  
  
    ```  
    RESTORE LOG <database_name> FROM <backup_device>   
       WITH NORECOVERY;  
    ```  
  
5.  Recupere o banco de dados executando a seguinte instrução RESTORE DATABASE:  
  
    ```  
    RESTORE DATABASE <database_name>   
       WITH RECOVERY;  
    ```  
  
## <a name="example"></a>Exemplo  
 Antes de você poder executar o exemplo, é necessário completar as seguintes preparações:  
  
1.  O modelo padrão de recuperação da base de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] é o modelo de recuperação simples. Como esse modelo de recuperação não oferece suporte à restauração ao ponto de uma falha, defina [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] para usar o modelo de recuperação completa executando a seguinte instrução [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) :  
  
    ```  
    USE master;  
    GO  
    ALTER DATABASE AdventureWorks2012 SET RECOVERY FULL;  
    ```  
  
2.  Crie um backup completo do banco de dados usando a seguinte instrução BACKUP:  
  
    ```  
    BACKUP DATABASE AdventureWorks2012 TO DISK = 'C:\AdventureWorks2012_Data.bck';  
    ```  
  
3.  Crie uma rotina de backup de log:  
  
    ```  
    BACKUP LOG AdventureWorks2012 TO DISK = 'C:\AdventureWorks2012_Log.bck';  
    ```  
  
 O exemplo a seguir restaura os backups criados anteriormente, depois de criar um backup do final do log do banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . (Esta etapa supõe que o disco de log pode ser acessado).  
  
 Primeiro, o exemplo cria um backup do final do log que captura o log ativo e deixa o banco de dados no estado Restaurando. Em seguida, o exemplo restaura um backup de banco de dados, aplica o backup de log de rotina criado anteriormente, e aplica o backup do final do log. Por fim, o exemplo recupera o banco de dados em uma etapa separada.  
  
> [!NOTE]  
>  O comportamento padrão é recuperar um banco de dados como parte da instrução que restaura o backup final.  
  
```  
/* Example of restoring a to the point of failure */  
-- Step 1: Create a tail-log backup by using WITH NORECOVERY.  
BACKUP LOG AdventureWorks2012  
   TO DISK = 'C:\AdventureWorks2012_Log.bck'  
   WITH NORECOVERY;  
GO  
-- Step 2: Restore the full database backup.  
RESTORE DATABASE AdventureWorks2012  
   FROM DISK = 'C:\AdventureWorks2012_Data.bck'  
   WITH NORECOVERY;  
GO  
-- Step 3: Restore the first transaction log backup.  
RESTORE LOG AdventureWorks2012  
   FROM DISK = 'C:\AdventureWorks2012_Log.bck'  
   WITH NORECOVERY;  
GO  
-- Step 4: Restore the tail-log backup.  
RESTORE LOG AdventureWorks2012  
   FROM  DISK = 'C:\AdventureWorks2012_Log.bck'  
   WITH NORECOVERY;  
GO  
-- Step 5: Recover the database.  
RESTORE DATABASE AdventureWorks2012  
   WITH RECOVERY;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
