---
title: 'Lição 9: Restaurar um banco de dados do armazenamento do Azure | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: ebba12c7-3d13-4c9d-8540-ad410a08356d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 464961600f69f14a2b66515a75906c0fd4af3f82
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/30/2019
ms.locfileid: "70175361"
---
# <a name="lesson-9-restore-a-database-from-azure-storage"></a>Lição 9: Restaurar um banco de dados do armazenamento do Azure
  Nesta lição, você aprenderá a restaurar um arquivo de backup de banco de dados do armazenamento do Azure para um banco de dados, que reside no local ou em uma máquina virtual no Azure. Para acompanhar esta lição, você não precisará concluir as lições 4, 5, 6, 7 e 8.  
  
 Esta lição supõe que você já concluiu as seguintes etapas:  
  
-   Você criou um banco de dados no computador de origem.  
  
-   Você criou um backup do seu banco de dados (. bak) no armazenamento do Azure usando o recurso de [SQL Server Backup e restauração com o serviço de armazenamento de BLOBs do Azure](backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md) . Observe que você precisará criar outra Credencial do SQL Server nesta etapa. Essa credencial usará as chaves da conta de armazenamento.  
  
-   Você tem uma conta de armazenamento do Azure.  
  
-   Você criou um contêiner em sua conta de armazenamento do Azure.  
  
-   Você criou uma política em um contêiner com direitos de leitura, gravação e lista. Você também gerou uma chave de SAS.  
  
-   Você criou uma credencial de SQL Server no seu computador para o recurso de integração de armazenamento do Azure. Observe que essa credencial exige uma chave SAS (assinatura de acesso compartilhado).  
  
 Para restaurar um banco de dados do armazenamento do Azure, você pode seguir estas etapas:  
  
1.  Inicie o SQL Server Management Studio. Conecte-se à instância padrão.  
  
2.  Clique em **nova consulta** na barra de ferramentas padrão.  
  
3.  Copie e cole o script completo a seguir na janela de consulta. Modifique o script conforme necessário.  
  
     **Observação:** Você executa a `RESTORE` instrução para restaurar o backup do banco de dados (. bak) no armazenamento do Azure para uma instância de banco de dados em outro computador.  
  
    ```sql  
  
    USE master   
    GO   
    -- Create a new database to be backed up.   
    CREATE DATABASE TestDbRestoreFrom;   
    GO   
    USE TestDbRestoreFrom;   
    GO   
    CREATE TABLE Table1 (Col1 int primary key, Col2 varchar(20));   
    GO   
    INSERT INTO Table1 (Col1, Col2) VALUES (1, 'string1'), (2, 'string2');   
    GO   
    USE TestDbRestoreFrom;   
    GO   
    SELECT * from dbo.Table1;   
    GO   
    -- Create a credential to be used by SQL Server Backup and Restore with Azure -----Blob Storage Service.   
    USE master;   
    GO   
    CREATE CREDENTIAL BackupCredential    
    WITH IDENTITY= 'teststorageaccnt',   
    SECRET = 'BO1nH/lWRdnc8TGPlQIXmGLWVCoEa48suYSGiAlC73+S0TX5VXo5/LCm8qiyGCYafDg4ZsueDIV3GQ5RXHaRGw=='    
    GO   
    -- Display the newly created credential   
    SELECT * from sys.credentials   
    -- Create a backup in Azure Storage.   
    BACKUP DATABASE TestDBRestoreFrom    
    TO URL = 'https://teststorageaccnt.blob.core.windows.net/testrestorefrom/TestDBRestoreFrom.bak'    
          WITH CREDENTIAL = 'BackupCredential'    
         ,COMPRESSION   
         ,STATS = 5;   
    GO    
    -- Create a Shared Access Signature credential   
    CREATE CREDENTIAL [https://teststorageaccnt.blob.core.windows.net/testrestorefrom]   
    WITH IDENTITY='SHARED ACCESS SIGNATURE',   
    SECRET = 'sv=2012-02-12&sr=c&si=policy_resfrom&sig=EhVpzLUXjG4ThAMLmVhrnoiCt8IfmD3BsuYiMawGzxc%3D'   
    GO   
    USE master;   
    GO   
    RESTORE DATABASE TestDBRestoreFrom    
    FROM URL = 'https://teststorageaccnt.blob.core.windows.net/testrestorefrom/TestDBRestoreFrom.bak'    
    WITH    
    CREDENTIAL = 'BackupCredential',    
    REPLACE,   
    MOVE 'TestDBRestoreFrom' TO 'C:\Backup\TestDBRestoreFrom.mdf',     
    MOVE 'TestDBRestoreFrom_log' TO 'C:\Backup\TestDBRestoreFrom_log.ldf';   
    GO  
  
    ```  
  
 **Fim do tutorial: SQL Server arquivos de dados no serviço de armazenamento do Azure**  
  
  
