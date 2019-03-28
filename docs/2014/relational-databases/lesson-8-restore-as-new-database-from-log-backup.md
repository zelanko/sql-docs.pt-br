---
title: 'Lição 9: Restaurar um banco de dados do armazenamento do Windows Azure | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: ebba12c7-3d13-4c9d-8540-ad410a08356d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 38d807fae60099022e847e4799196305ccfbadf8
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58534438"
---
# <a name="lesson-9-restore-a-database-from-windows-azure-storage"></a>Lição 9: Restaurar um banco de dados a partir do Armazenamento do Windows Azure
  Nesta lição, você aprenderá a restaurar um arquivo de backup de banco de dados do Armazenamento do Windows Azure para um banco de dados, que reside no local ou em uma máquina virtual do Windows Azure. Para acompanhar esta lição, você não precisará concluir as lições 4, 5, 6, 7 e 8.  
  
 Esta lição supõe que você já concluiu as seguintes etapas:  
  
-   Você criou um banco de dados no computador de origem.  
  
-   Você criou um backup do banco de dados (. bak) no armazenamento do Windows Azure usando o [SQL Server Backup and Restore with Windows Azure Blob Storage Service](backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md) recurso. Observe que você precisará criar outra Credencial do SQL Server nesta etapa. Essa credencial usará as chaves da conta de armazenamento.  
  
-   Você tem uma conta de Armazenamento do Windows Azure.  
  
-   Você criou um contêiner na sua conta de Armazenamento do Windows Azure.  
  
-   Você criou uma política em um contêiner com direitos de leitura, gravação e lista. Você também gerou uma chave de SAS.  
  
-   Você criou uma credencial do SQL Server no computador para o recurso de Integração do Armazenamento do Windows Azure. Observe que essa credencial exige uma chave SAS (assinatura de acesso compartilhado).  
  
 Para restaurar um banco de dados a partir do Armazenamento do Windows Azure, siga estas etapas:  
  
1.  Inicie o SQL Server Management Studio. Conecte-se à instância padrão.  
  
2.  Clique em **nova consulta** na barra de ferramentas padrão.  
  
3.  Copie e cole o script completo a seguir na janela de consulta. Modifique o script conforme necessário.  
  
     **Observação:** execute a instrução `RESTORE` para restaurar o backup de banco de dados (.bak) no Armazenamento do Microsoft Azure para uma instância do banco de dados em outro computador.  
  
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
    -- Create a credential to be used by SQL Server Backup and Restore with Windows Azure -----Blob Storage Service.   
    USE master;   
    GO   
    CREATE CREDENTIAL BackupCredential    
    WITH IDENTITY= 'teststorageaccnt',   
    SECRET = 'BO1nH/lWRdnc8TGPlQIXmGLWVCoEa48suYSGiAlC73+S0TX5VXo5/LCm8qiyGCYafDg4ZsueDIV3GQ5RXHaRGw=='    
    GO   
    -- Display the newly created credential   
    SELECT * from sys.credentials   
    -- Create a backup in Windows Azure Storage.   
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
  
 **Fim do Tutorial: Arquivos de dados do SQL Server no serviço de armazenamento do Windows Azure**  
  
  
