---
title: 'Início Rápido: Backup e restauração do SQL Server para o Serviço de Armazenamento de Blobs do Azure | Microsoft Docs'
ms.custom: ''
ms.date: 04/09/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 9e1d94ce-2c93-45d1-ae2a-2a7d1fa094c4
author: rothja
ms.author: jroth
ms.openlocfilehash: ae4d9cd9333e8dd42582f972a0d19260b2c9a3ee
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155706"
---
# <a name="quickstart-sql-server-backup-and-restore-to-azure-blob-storage-service"></a>Início Rápido: Backup e restauração do SQL Server no serviço de Armazenamento de Blobs do Azure
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Este início rápido ajuda você a compreender como gravar backups e fazer restaurações no Serviço de Armazenamento de Blobs do Azure.  Este início rápido explica como criar um Contêiner de Blob do Azure, credenciais para acessar a conta de armazenamento, gravar um backup do serviço Blob e executar uma restauração simples.
  
### <a name="prerequisites"></a>Prerequisites  
Para concluir este início rápido, você deve estar familiarizado com os conceitos de backup e restauração do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e a sintaxe do T-SQL. Para usar este início rápido, você precisará de uma conta de armazenamento do Azure, do SSMS (SQL Server Management Studio), de acesso a um servidor que executa o SQL Server e de um banco de dados do AdventureWorks. Além disso, a conta de usuário usada para emitir os comandos BACKUP e RESTORE deve estar na função de banco de dados **db_backupoperator** com as permissões **Alterar qualquer credencial**. 

- Obtenha uma [conta do Azure](https://azure.microsoft.com/offers/ms-azr-0044p/) gratuita.
- Crie uma [conta de armazenamento do Azure](https://docs.microsoft.com/azure/storage/common/storage-quickstart-create-account?tabs=portal).
- Instalar o [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
- Instalar o [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads).
- Atribua a conta de usuário à função [db_backupoperator](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/database-level-roles) e conceda permissões para [Alterar qualquer credencial](https://docs.microsoft.com/sql/t-sql/statements/alter-credential-transact-sql). 


## <a name="create-azure-blob-container"></a>Criar o Contêiner de Blob do Azure
Um contêiner fornece um agrupamento de conjunto de blobs. Todos os blobs devem estar em um contêiner. Uma conta pode conter um número ilimitado de contêineres, mas deve ter pelo menos um contêiner. Um contêiner pode armazenar um número ilimitado de blobs. 

[!INCLUDE[freshInclude](../includes/paragraph-content/fresh-note-steps-feedback.md)]

Para criar um Contêiner, siga estas etapas:

1. Abra o portal do Azure. 
1. Navegue até sua Conta de Armazenamento. 
1. Selecione a conta de armazenamento e role para baixo até **Serviços de Blob**.
1. Selecione **Blobs** e, em seguida, selecione +**Contêiner** para adicionar um novo contêiner. 
1. Insira o nome do contêiner e anote o nome especificado. Essas informações são usadas na URL (caminho para o arquivo de backup) nas instruções T-SQL mais adiante neste início rápido. 
1. Escolha **OK**. 
    
    ![Novo contêiner](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/new-container.png)


  > [!NOTE]
  > A autenticação na conta de armazenamento é necessária para o backup e a restauração do SQL Server, mesmo se você optar por criar um contêiner público. Você também pode criar uma contêiner de modo programático usando APIs REST. Para obter mais informações, consulte [Criar contêiner](https://docs.microsoft.com/rest/api/storageservices/Create-Container)

## <a name="create-a-test-database"></a>Criar um banco de dados de teste 

1. Inicie o [SSMS (SQL Server Management Studio)](../ssms/download-sql-server-management-studio-ssms.md) e conecte-se à instância do SQL Server.
1. Abra uma janela **Nova Consulta**. 
1. Execute o seguinte código T-SQL (Transact-SQL) para criar o banco de dados de teste. Atualize o nó **Bancos de Dados** no **Pesquisador de Objetos** para ver o novo banco de dados. 

```sql
USE [master]
GO

CREATE DATABASE [SQLTestDB]
GO

USE [SQLTestDB]
GO
CREATE TABLE SQLTest (
    ID INT NOT NULL PRIMARY KEY,
    c1 VARCHAR(100) NOT NULL,
    dt1 DATETIME NOT NULL DEFAULT getdate()
)
GO


USE [SQLTestDB]
GO

INSERT INTO SQLTest (ID, c1) VALUES (1, 'test1')
INSERT INTO SQLTest (ID, c1) VALUES (2, 'test2')
INSERT INTO SQLTest (ID, c1) VALUES (3, 'test3')
INSERT INTO SQLTest (ID, c1) VALUES (4, 'test4')
INSERT INTO SQLTest (ID, c1) VALUES (5, 'test5')
GO

SELECT * FROM SQLTest
GO
```


## <a name="create-a-sql-server-credential"></a>Criar uma credencial do SQL Server
Uma credencial do SQL Server é um objeto usado para armazenar as informações de autenticação necessárias para se conectar a um recurso fora do SQL Server. Aqui, os processos de backup e restauração do SQL Server usam credenciais para autenticação no serviço de Armazenamento de Blobs do Azure. A Credencial armazena o nome da conta de armazenamento e os valores de **access key** da conta de armazenamento. Depois que a credencial for criada, ela deverá ser especificada na opção WITH CREDENTIAL ao emitir instruções BACKUP/RESTORE. Para obter mais informações sobre credenciais, consulte [Credenciais](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/credentials-database-engine). 

  > [!IMPORTANT]
  > Os requisitos para criar uma credencial do SQL Server descritos abaixo são específicos dos processos do backup do SQL Server ([Backup do SQL Server para URL](backup-restore/sql-server-backup-to-url.md)e [Backup gerenciado do SQL Server no Microsoft Azure](backup-restore/sql-server-managed-backup-to-microsoft-azure.md)). O SQL Server usa o nome da conta de armazenamento e as informações da chave de acesso ao acessar o armazenamento do Azure para gravar ou ler backups.

### <a name="access-keys"></a>Chaves de acesso
Você precisará das chaves de acesso para a conta de armazenamento para criar a credencial. 

1. Navegue até a **Conta de Armazenamento** no portal do Azure. 
1. Selecione **Chaves de Acesso** em **Configurações**. 
1. Salve a chave e a cadeia de conexão para usar mais adiante neste início rápido. 

   ![Chaves de acesso](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/access-keys.png)

### <a name="create-a-sql-server-credential"></a>Criar uma credencial do SQL Server
Usando a chave de acesso que você salvou, crie a credencial do SQL Server seguindo as etapas a seguir. 

1. Conecte-se ao seu SQL Server usando o SQL Server Management Studio. 
1. Selecione o banco de dados **SQLTestDB** e abra uma janela **Nova Consulta**. 
1. Copie, cole e execute o exemplo a seguir na janela de consulta, modificando conforme necessário: 

   ```sql
   CREATE CREDENTIAL mycredential   
   WITH IDENTITY= 'msftutorialstorage', -- this is the name of the storage account you specified when creating a storage account   
   SECRET = '<storage account access key>' -- this should be either the Primary or Secondary Access Key for the storage account 
   ```

1. Execute a instrução para criar a credencial. 

## <a name="back-up-database-to-the-azure-blob-storage-service"></a>Fazer backup do banco de dados no serviço de Armazenamento de Blobs do Azure
Nesta seção, você usará uma instrução T-SQL para executar um backup completo de banco de dados no serviço de Armazenamento de Blobs do Azure. 

1. Conecte-se ao seu SQL Server usando o SQL Server Management Studio. 
1. Selecione o banco de dados **SQLTestDB** e abra uma janela **Nova Consulta**. 
1. Copie e cole o exemplo a seguir na janela de consulta, modificando conforme necessário: 

     ```sql
     BACKUP DATABASE [SQLTestDB] 
     TO URL = 'https://msftutorialstorage.blob.core.windows.net/sql-backup/SQLTestDB.bak' 
     /* URL includes the endpoint for the BLOB service, followed by the container name, and the name of the backup file*/ 
     WITH CREDENTIAL = 'mycredential';
     /* name of the credential you created in the previous step */ 
     GO
     ```

1. Execute a instrução para fazer backup do banco de dados SQLTestDB na URL. 

 
## <a name="restore-database-from-azure-blob-storage-service"></a>Restaurar banco de dados do serviço de Armazenamento de Blobs do Azure
Nesta seção, você usará uma instrução T-SQL para restaurar o backup do banco de dados completo. 

1. Conecte-se ao seu SQL Server usando o SQL Server Management Studio. 
1. Abra uma janela **Nova Consulta**. 
1. Copie e cole o exemplo a seguir na janela de consulta, modificando conforme necessário: 

 ```sql
 RESTORE DATABASE [SQLTestDB] 
 FROM URL = 'https://msftutorialstorage.blob.core.windows.net/sql-backup/SQLTestDB.bak' 
 WITH CREDENTIAL = 'mycredential',
 STATS = 5 -- use this to see monitor the progress
 GO
 ``` 

## <a name="see-also"></a>Confira também 
Estas são algumas leituras que podem ajudar a compreender os conceitos e as práticas recomendadas ao usar o serviço de armazenamento de Blobs do Azure para backups do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   [Backup e restauração do SQL Server com o Serviço de Armazenamento de Blobs do Microsoft Azure](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)   
-   [Práticas recomendadas e solução de problemas de backup do SQL Server para URL](../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
  
