---
title: 'Lição 6: Gerar log de atividade e de backup usando o backup de instantâneo de arquivo | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: tutorial
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 26aa534a-afe7-4a14-b99f-a9184fc699bd
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9a0c763bb826140ef12e51d32900623d7f82764e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="lesson-6-generate-activity-and-backup-log-using-file-snapshot-backup"></a>Lição 6: Gerar log de atividade e de backup usando o backup de instantâneo de arquivo
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Nesta lição, você aprenderá a gerar atividade no banco de dados AdventureWorks2014 e criar periodicamente backups de log de transações usando backups de instantâneo de arquivo. Para obter mais informações sobre como usar backups de instantâneo de arquivo, veja [Backups de instantâneo de arquivo para arquivos de banco de dados no Azure](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md).  
  
Para gerar atividade no banco de dados AdventureWorks2014 e criar periodicamente backups de log de transações usando backups de instantâneo de arquivo, siga estas etapas:  
  
1.  Conecte-se ao SQL Server Management Studio.  
  
2.  Abra duas novas janelas de consulta e conecte cada uma delas à instância do SQL Server 2016 do mecanismo de banco de dados na máquina virtual do Azure.  
  
3.  Copie, cole e execute o script Transact-SQL a seguir em uma das janelas de consulta. Observe que a tabela Production.Location tem 14 linhas antes de adicionarmos novas linhas na etapa 4.  
  
    ```  
  
    -- Verify row count at start  
    SELECT COUNT (*) from AdventureWorks2014.Production.Location;  
  
    ```  
  
4.  Copie e cole os dois scripts Transact-SQL a seguir em duas janelas de consulta separadas. Modifique a URL de forma adequada para o nome de sua conta de armazenamento e o contêiner especificado na Lição 1 e execute estes scripts simultaneamente em janelas de consulta separadas. Esses scripts levarão cerca de sete minutos para serem concluídos.  
  
    ```  
    -- Insert 30,000 new rows into the Production.Location table in the AdventureWorks2014 database in batches of 75  
    DECLARE @count INT=1, @inner INT;  
    WHILE @count < 400  
       BEGIN  
          BEGIN TRAN;  
             SET @inner =1;  
                WHILE @inner <= 75  
                   BEGIN;  
                      INSERT INTO AdventureWorks2014.Production.Location    
                         (Name, CostRate, Availability, ModifiedDate)   
                            VALUES (NEWID(), .5, 5.2, GETDATE());  
                      SET @inner = @inner + 1;  
                   END;  
          COMMIT;  
       WAITFOR DELAY '00:00:01';   
       SET @count = @count + 1;  
       END;  
    SELECT COUNT (*) from AdventureWorks2014.Production.Location;  
  
    ```  
  
    ```  
    --take 7 transaction log backups with FILE_SNAPSHOT, one per minute, and include the row count and the execution time in the backup file name   
    DECLARE @count INT=1, @device NVARCHAR(120), @numrows INT;  
    WHILE @count <= 7  
       BEGIN  
             SET @numrows = (SELECT COUNT (*) FROM AdventureWorks2014.Production.Location);  
             SET @device = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/tutorial-' + CONVERT (varchar(10),@numrows) + '-' + FORMAT(GETDATE(), 'yyyyMMddHHmmss') + '.bak';  
             BACKUP LOG AdventureWorks2014 TO URL = @device WITH FILE_SNAPSHOT;  
             SELECT * from sys.fn_db_backup_file_snapshots ('AdventureWorks2014');  
          WAITFOR DELAY '00:1:00';   
             SET @count = @count + 1;  
       END;  
    ```  
  
5.  Examine a saída do primeiro script e observe que a contagem de linhas final agora é de 29.939.  
  
    ![A contagem de linhas 29.939 é exibida](../relational-databases/media/5e2f4229-1970-49c9-89b3-e96b6f7fde83.JPG "A contagem de linhas 29.939 é exibida")  
  
6.  Examine a saída do segundo script e observe que sempre que a instrução BACKUP LOG é executada, são criados dois novos instantâneos de arquivo: um instantâneo de arquivo do arquivo de log e um instantâneo de arquivo do arquivo de dados – em um total de dois instantâneos de arquivo para cada arquivo de banco de dados. Após a conclusão do segundo script, observe que agora há um total de 16 instantâneos de arquivo, 8 para cada arquivo de banco de dados – um da instrução BACKUP DATABASE e um para cada execução da instrução BACKUP LOG.  
  
    ![painel Resultados mostrando instantâneos de arquivo do arquivo de log e de dados quando é feito um backup de log](../relational-databases/media/acd213b8-895e-425c-bd72-2bf10e65a5ba.JPG "painel Resultados mostrando instantâneos de arquivo do arquivo de log e de dados quando é feito um backup de log")  
  
    ![quatro instantâneos de arquivo são exibidos](../relational-databases/media/e7eff77d-85b9-4e52-abd8-e49952c8118a.JPG "quatro instantâneos de arquivo são exibidos")  
  
    ![painel Resultados mostrando um total de 16 instantâneos de arquivo](../relational-databases/media/c3ddff17-a83c-4bf0-a670-a38834f9c922.JPG "painel Resultados mostrando um total de 16 instantâneos de arquivo")  
  
7.  No Pesquisador de Objetos, conecte-se ao armazenamento do Azure.  
  
8.  Expanda Contêineres, expanda o contêiner criado na Lição 1 e verifique se sete novos arquivos de backup são exibidos, juntamente com os blobs das lições anteriores (atualize o nó, conforme necessário).  
  
    ![Contêiner do Azure mostrando 7 blobs de backup de log](../relational-databases/media/cfa5a326-87a2-4202-9a04-38bf577d2d0b.JPG "Contêiner do Azure mostrando 7 blobs de backup de log")  
  
**Próxima lição:**  
  
[Lição 7: Restaurar um banco de dados em um ponto específico](../relational-databases/lesson-7-restore-a-database-to-a-point-in-time.md)  
  
  
  
