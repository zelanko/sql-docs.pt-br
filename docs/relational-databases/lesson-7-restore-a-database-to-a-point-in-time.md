---
title: "Lição 7: Restaurar um banco de dados em um ponto no tempo | Microsoft Docs"
ms.custom: SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: a9f99670-e1de-441e-972c-69faffcac17a
caps.latest.revision: "13"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 479f890cd6623b457b53cc0024691f9169937538
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="lesson-7-restore-a-database-to-a-point-in-time"></a>Lição 7: Restaurar um banco de dados em um ponto específico
Nesta lição, você aprenderá a restaurar o banco de dados AdventureWorks2014 em um ponto específico entre dois backups de log de transações.  
  
Com backups tradicionais, para realizar a restauração pontual, você precisará usar o backup do banco de dados completo, talvez um backup diferencial, e todos os arquivos de log de transações incluindo e logo após o ponto específico para o qual você quer restaurar. Com os backups de instantâneo de arquivo, você só precisa de dois arquivos de log de backup adjacentes que fornecem as postagens de meta enquadrando o tempo para o qual você quer restaurar. Você só precisa dois conjuntos de backup de instantâneo de arquivo de log, pois cada backup de log cria um instantâneo de arquivo de cada arquivo de banco de dados (cada arquivo de dados e o arquivo de log).  
  
Para restaurar um banco de dados para um ponto específico por meio de conjuntos de backup de instantâneo de arquivo, siga estas etapas:  
  
1.  Conecte-se ao SQL Server Management Studio.  
  
2.  Abra uma nova janela de consulta e conecte-se à instância do SQL Server 2016 do mecanismo de banco de dados na máquina virtual do Azure.  
  
3.  Copie, cole e execute o script Transact-SQL a seguir na janela de consulta. Verifique se a tabela Production.Location tem 29.939 linhas antes de restaurarmos para um ponto específico quando há menos linhas na etapa 5.  
  
    ```  
  
    -- Verify row count at start  
    SELECT COUNT (*) from AdventureWorks2014.Production.Location  
  
    ```  
  
    ![A contagem de linhas 29.939 é exibida](../relational-databases/media/5e2f4229-1970-49c9-89b3-e96b6f7fde83.JPG "A contagem de linhas 29.939 é exibida")  
  
4.  Copie e cole o script Transact-SQL a seguir na janela de consulta. Selecione dois arquivos de backup de log adjacentes e converta o nome de arquivo na data e hora de que você precisará para esse script. Modifique a URL de forma adequada para o nome de sua conta de armazenamento e o contêiner especificado na Lição 1, forneça os nomes do primeiro e segundo arquivos de backup, forneça a hora STOPAT no formato “26 de junho de 2015 01h48” e execute este script. Esse script levará alguns minutos para ser concluído  
  
    ```  
  
    -- restore and recover to a point in time between the times of two transaction log backups, and then verify the row count  
    ALTER DATABASE AdventureWorks2014 SET SINGLE_USER WITH ROLLBACK IMMEDIATE;  
    RESTORE DATABASE AdventureWorks2014   
       FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/<firstbackupfile>.bak'   
       WITH NORECOVERY,REPLACE;  
    RESTORE LOG AdventureWorks2014   
       FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/<secondbackupfile>.bak'    
       WITH RECOVERY, STOPAT = 'June 26, 2015 01:48 PM';  
    ALTER DATABASE AdventureWorks2014 set multi_user;  
    -- get new count  
    SELECT COUNT (*) FROM AdventureWorks2014.Production.Location ;  
  
    ```  
  
5.  Examine a saída. Observe que, após a restauração, a contagem de linhas é 18.389, que é um número de contagem de linhas entre o backup de log 5 e 6 (a contagem de linhas poderá variar).  
  
    ![Painel Resultados mostrando a contagem de linhas após a recuperação pontual](../relational-databases/media/4a0c6d8b-e2ed-4e93-bd7a-ade22a4aecc6.JPG "Painel Resultados mostrando a contagem de linhas após a recuperação pontual")  
  
**Próxima lição:**  
  
[Lição 8. Restaurar como um novo banco de dados por meio do backup de log](../relational-databases/lesson-8-restore-as-new-database-from-log-backup.md)  
  
  
  
