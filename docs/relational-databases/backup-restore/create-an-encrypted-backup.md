---
title: Criar um backup criptografado | Microsoft Docs
ms.custom: 
ms.date: 08/04/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e29061d3-c2ab-4d98-b9be-8e90a11d17fe
caps.latest.revision: "17"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: c9dc51c3288ceae6e91cd014b1220ea890d3114f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="create-an-encrypted-backup"></a>Criar um backup criptografado
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Este tópico descreve as etapas necessárias para criar um backup criptografado usando Transact-SQL.  Para obter um exemplo de como usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], consulte [Criar um backup completo de banco de dados (SQL Server)](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md). 
  
## <a name="backup-to-disk-with-encryption"></a>Backup em disco com criptografia  
 **Pré-requisitos:**  
  
-   Acesso a um disco local ou ao armazenamento com espaço suficiente para criar um backup do banco de dados.  
  
-   Uma Chave Mestra do Banco de Dados para o banco de dados mestre, e um certificado ou uma chave assimétrica disponível na instância do SQL Server. Para requisitos e permissões de criptografia, consulte [Backup Encryption](../../relational-databases/backup-restore/backup-encryption.md).  
  
 Use as etapas a seguir para criar um backup criptografado de um banco de dados em um disco local. Este exemplo usa um banco de dados de usuário chamado MyTestDB.  
  
1.  **Criar uma Chave Mestra do Banco de Dados para o banco de dados mestre:** escolha uma senha para criptografar a cópia da chave mestra que será armazenada no banco de dados. Conecte-se ao mecanismo de banco de dados, inicie uma nova janela de consulta, copie e cole o exemplo a seguir e clique em **Executar**.  
  
    ```  
    -- Creates a database master key.   
    -- The key is encrypted using the password "<master key password>"  
    USE master;  
    GO  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<master key password>';  
    GO  
  
    ```  
  
2.  **Criar um Certificado de backup:** Crie um certificado de backup no banco de dados mestre. Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    Use Master  
    GO  
    CREATE CERTIFICATE MyTestDBBackupEncryptCert  
       WITH SUBJECT = 'MyTestDB Backup Encryption Certificate';  
    GO  
  
    ```  
  
3.  **Backup de banco de dados:** Especifique o algoritmo de criptografia e o certificado a ser usado. Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    BACKUP DATABASE [MyTestDB]  
    TO DISK = N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\MyTestDB.bak'  
    WITH  
      COMPRESSION,  
      ENCRYPTION   
       (  
       ALGORITHM = AES_256,  
       SERVER CERTIFICATE = MyTestDBBackupEncryptCert  
       ),  
      STATS = 10  
    GO  
  
    ```  
  
 Para obter um exemplo de como criptografar um backup protegido por uma EKM, veja [Gerenciamento extensível de chaves usando o Cofre de Chaves do Azure &#40;SQL Server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md).  
  
### <a name="backup-to-windows-azure-storage-with-encryption"></a>Backup no armazenamento do Windows Azure com criptografia  
 Se você estiver criando um backup no armazenamento do Windows Azure usando a opção de **Backup do SQL Server para URL** , as etapas de criptografia serão as mesmas, mas você deve usar a URL como destino e uma Credencial SQL a ser autenticada no armazenamento do Windows Azure. Se você quiser configurar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] com opções de criptografia, veja [Habilitar o backup gerenciado do SQL Server no Microsoft Azure](../../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md).  
  
 **Pré-requisitos:**  
  
-   Uma conta de armazenamento do Windows e um contêiner. Para obter mais informações, consulte: [Lesson 1: Create Windows Azure Storage Objects](http://msdn.microsoft.com/library/74edd1fd-ab00-46f7-9e29-7ba3f1a446c5).  
  
-   Uma Chave Mestra do Banco de Dados para o banco de dados mestre, e um certificado ou uma chave assimétrica na instância do SQL Server. Para requisitos e permissões de criptografia, consulte [Backup Encryption](../../relational-databases/backup-restore/backup-encryption.md).  
  
1.  **Criar uma credencial do SQL Server:** Para criar uma credencial do SQL Server, conecte-se ao Mecanismo de Banco de Dados, abra uma nova janela de consulta, copie e cole o exemplo a seguir e clique em **Executar**.  
  
    ```  
    CREATE CREDENTIAL mycredential   
    WITH IDENTITY= 'mystorageaccount' – this is the name of the storage account you specified when creating a storage account    
    , SECRET = '<storage account access key>' – this should be either the Primary or Secondary Access Key for the storage account  
    ```  
  
2.  **Criar uma chave mestra de banco de dados:** Escolha uma senha por criptografar a cópia da chave mestra que será armazenada no banco de dados. Conecte-se ao mecanismo de banco de dados, inicie uma nova janela de consulta, copie e cole o exemplo a seguir e clique em **Executar**.  
  
    ```  
    -- Creates a database master key.  
    -- The key is encrypted using the password "<master key password>"  
    USE Master;  
    GO  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<master key password>';  
    GO  
  
    ```  
  
3.  **Criar um Certificado de backup:** Crie um Certificado de backup no banco de dados mestre. Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE Master;  
    GO  
    CREATE CERTIFICATE MyTestDBBackupEncryptCert  
       WITH SUBJECT = 'MyTestDBBackupEncryptCert ';  
    GO  
  
    ```  
  
4.  **Backup de banco de dados:** Especifique o algoritmo de criptografia e o certificado a ser utilizado. Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    BACKUP DATABASE [MyTestDB]  
    TO URL = N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\MyTestDB.bak'  
    WITH  
      CREDENTIAL 'mycredential' – this is the name of the credential created in the first step.  
      ,COMPRESSION  
      ,ENCRYPTION   
       (  
       ALGORITHM = AES_256,  
       SERVER CERTIFICATE = MyTestDBBackupEncryptCert  
       ),  
      STATS = 10  
    GO  
  
    ```  
  
  
