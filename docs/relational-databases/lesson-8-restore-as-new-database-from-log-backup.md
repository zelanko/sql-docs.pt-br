---
title: "Lição 8: Restaurar como um novo banco de dados por meio do backup de log | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: ebba12c7-3d13-4c9d-8540-ad410a08356d
caps.latest.revision: 12
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 281259fb737bbc41885a61e62a4fcc83b3001119
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="lesson-8-restore-as-new-database-from-log-backup"></a>Lição 8: Restaurar como um novo banco de dados por meio do backup de log
Nesta lição, você aprenderá a restaurar o banco de dados AdventureWorks2014 como um novo banco de dados por meio de um backup de log de transações de instantâneo de arquivo.  
  
Nesse cenário, você está realizando uma restauração de uma instância do SQL Server em outra máquina virtual para fins de análise de negócios e relatório. A restauração em uma instância diferente em outra máquina virtual descarrega a carga de trabalho em uma máquina virtual dedicada e dimensionada para essa finalidade, removendo os requisitos de recursos do sistema transacional.  
  
A restauração por meio de um backup de log de transações com backup de instantâneo de arquivo é muito rápida e significativamente mais rápida do que com backups tradicionais de streaming. Com backups tradicionais de streaming, você precisaria usar o backup completo do banco de dados, talvez um backup diferencial e alguns ou todos os backups de log de transações (ou um novo backup completo do banco de dados). No entanto, com backups de log de instantâneo de arquivo, você só precisa do backup de log mais recente (ou outro backup de log ou os dois backups de log adjacentes para restauração pontual em um ponto entre dois horários de backup de log). Para ser claro, é necessário apenas um conjunto de backup de instantâneo de arquivo de log, porque cada backup de log de instantâneo de arquivo cria um instantâneo de arquivo de cada arquivo de banco de dados (cada arquivo de dados e o arquivo de log).  
  
Para restaurar um banco de dados em um novo banco de dados por meio de um backup de log de transações usando o backup de instantâneo de arquivo, siga estas etapas:  
  
1.  Conecte-se ao SQL Server Management Studio.  
  
2.  Abra uma nova janela de consulta e conecte-se à instância do SQL Server 2016 do mecanismo de banco de dados em uma máquina virtual do Azure.  
  
    > [!NOTE]  
    > Se esta for uma máquina virtual do Azure diferente da que você usou nas lições anteriores, verifique se você seguiu as etapas na [Lição 2: Criar uma credencial do SQL Server usando uma assinatura de acesso compartilhado](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md). Se você deseja restaurar para um contêiner diferente, siga as etapas em [Lição 1: Criar uma política de acesso armazenado e uma assinatura de acesso compartilhado em um contêiner do Azure](../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md) e [Lição 2: Criar uma credencial do SQL Server usando uma assinatura de acesso compartilhado](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md) para o novo contêiner.  
  
3.  Copie e cole o script Transact-SQL a seguir na janela de consulta. Selecione o arquivo de backup de log que você deseja usar. Modifique a URL de forma adequada para o nome de sua conta de armazenamento e o contêiner especificado na Lição 1, forneça o nome do arquivo de backup de log e execute este script.  
  
    ```  
  
    -- restore as a new database from a transaction log backup file  
    RESTORE DATABASE AdventureWorks2014_EOM   
        FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/<logbackupfile.bak'    
        WITH MOVE 'AdventureWorks2014_data' to 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_EOM_Data.mdf'  
       , MOVE 'AdventureWorks2014_log' to 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_EOM_Log.ldf'  
       , RECOVERY  
    --, REPLACE  
  
    ```  
  
4.  Examine a saída para verificar se a restauração foi bem-sucedida.  
  
5.  No Pesquisador de Objetos, conecte-se ao armazenamento do Azure.  
  
6.  Expanda Contêineres, expanda o contêiner criado na Lição 1 (atualize, se necessário) e verifique se os novos arquivos de log e de dados são exibidos no contêiner, juntamente com os blobs das lições anteriores.  
  
    ![Contêiner do Azure mostrando os arquivos de dados e de log do novo banco de dados](../relational-databases/media/e9705083-86bc-4309-a0bf-92c15f174c0a.JPG "Contêiner do Azure mostrando os arquivos de dados e de log do novo banco de dados")  
  
[Lição 9: Gerenciar conjuntos de backup e backups de instantâneo de arquivo](../relational-databases/lesson-9-manage-backup-sets-and-file-snapshot-backups.md)  
  
  
  

