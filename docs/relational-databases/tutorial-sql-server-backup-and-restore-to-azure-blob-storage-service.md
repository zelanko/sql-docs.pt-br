---
title: 'Início Rápido: Backup e restauração do serviço de armazenamento de Blobs do Azure'
description: 'Início Rápido: saiba como gravar backups e fazer restaurações no Serviço de Armazenamento de Blobs do Azure. Crie um contêiner de Blob do Azure, grave um backup e, então, restaure.'
ms.custom: seo-dt-2019
ms.date: 04/09/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: quickstart
ms.assetid: 9e1d94ce-2c93-45d1-ae2a-2a7d1fa094c4
author: rothja
ms.author: jroth
ms.openlocfilehash: 59968cad65f3a80c2d511dad3dc804d151d33095
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2020
ms.locfileid: "86458038"
---
# <a name="quickstart-sql-backup-and-restore-to-azure-blob-storage-service"></a>Início Rápido: Backup e restauração do SQL no serviço de armazenamento de Blob do Azure
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md](../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]
Este início rápido ajuda você a compreender como gravar backups e fazer restaurações no Serviço de Armazenamento de Blobs do Azure.  O artigo explica como criar um Contêiner de Blob do Azure, gravar um backup no serviço blob e, em seguida, executar uma restauração.
  
## <a name="prerequisites"></a>Pré-requisitos  
Para concluir este início rápido, você deve estar familiarizado com os conceitos de backup e restauração do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e a sintaxe do T-SQL.  Você precisa de uma conta de armazenamento do Azure, SSMS (SQL Server Management Studio) e acesso a um servidor que esteja executando o SQL Server ou uma instância gerenciada do Banco de Dados SQL do Azure. Além disso, a conta de usuário usada para emitir os comandos BACKUP e RESTORE deve estar na função de banco de dados **db_backupoperator** com as permissões **Alterar qualquer credencial**. 

- Obtenha uma [conta do Azure](https://azure.microsoft.com/offers/ms-azr-0044p/) gratuita.
- Crie uma [conta de armazenamento do Azure](https://docs.microsoft.com/azure/storage/common/storage-quickstart-create-account?tabs=portal).
- Instale o [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
- Instale o [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads) ou implante uma [instância gerenciada](/azure/sql-database/sql-database-managed-instance-get-started) com conectividade estabelecida por meio de uma [máquina virtual SQL do Azure](/azure/sql-database/sql-database-managed-instance-configure-vm) ou [ponto a site](/azure/sql-database/sql-database-managed-instance-configure-p2s).
- Atribua a conta de usuário à função [db_backupoperator](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/database-level-roles) e conceda permissões para [Alterar qualquer credencial](https://docs.microsoft.com/sql/t-sql/statements/alter-credential-transact-sql). 

## <a name="create-azure-blob-container"></a>Criar o contêiner de Blob do Azure
Um contêiner fornece um agrupamento de conjunto de blobs. Todos os blobs devem estar em um contêiner. Uma conta de armazenamento pode conter um número ilimitado de contêineres, mas deve ter pelo menos um contêiner. Um contêiner pode armazenar um número ilimitado de blobs. 

Para criar um Contêiner, siga estas etapas:

1. Abra o portal do Azure. 
1. Navegue até sua Conta de Armazenamento. 
1. Selecione a conta de armazenamento e role para baixo até **Serviços de Blob**.
1. Selecione **Blobs** e, em seguida, selecione **+ Contêiner** para adicionar um novo contêiner. 
1. Insira o nome do contêiner e anote o nome especificado. Essas informações são usadas na URL (caminho para o arquivo de backup) nas instruções T-SQL mais adiante neste início rápido. 
1. Selecione **OK**. 
    
    ![Novo contêiner](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/new-container.png)

  > [!NOTE]
  > A autenticação na conta de armazenamento é necessária para o backup e a restauração do SQL Server, mesmo se você optar por criar um contêiner público. Você também pode criar uma contêiner de modo programático usando APIs REST. Para obter mais informações, consulte [Criar contêiner](https://docs.microsoft.com/rest/api/storageservices/Create-Container)

## <a name="create-a-test-database"></a>Criar um banco de dados de teste 
Nesta etapa, crie um banco de dados de teste usando o SSMS (SQL Server Management Studio). 

1. Inicie o [SSMS (SQL Server Management Studio)](../ssms/download-sql-server-management-studio-ssms.md) e conecte-se à instância do SQL Server.
1. Abra uma janela **Nova Consulta**. 
1. Execute o seguinte código T-SQL (Transact-SQL) para criar o banco de dados de teste. Atualize o nó **Bancos de Dados** no **Pesquisador de Objetos** para ver o novo banco de dados. Os bancos de dados criados recentemente em uma instância gerenciada do Banco de Dados SQL do Azure têm o TDE habilitado automaticamente, portanto, você precisará desabilitá-lo para continuar. 

```sql
USE [master]
GO

-- Create database
CREATE DATABASE [SQLTestDB]
GO

-- Create table in database
USE [SQLTestDB]
GO
CREATE TABLE SQLTest (
    ID INT NOT NULL PRIMARY KEY,
    c1 VARCHAR(100) NOT NULL,
    dt1 DATETIME NOT NULL DEFAULT getdate()
)
GO

-- Populate table 
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

-- Disable TDE for newly-created databases on a managed instance 
USE [SQLTestDB];
GO
ALTER DATABASE [SQLTestDB] SET ENCRYPTION OFF;
GO
```

## <a name="create-credential"></a>Criar credencial

Use a GUI no SQL Server Management Studio para criar a credencial seguindo as etapas abaixo. Como alternativa, você também pode criar a credencial [programaticamente](tutorial-use-azure-blob-storage-service-with-sql-server-2016.md#2---create-a-sql-server-credential-using-a-shared-access-signature). 

1. Expanda o nó **Banco de dados** no **Pesquisador de Objetos** do [SSMS (SQL Server Management Studio)](../ssms/download-sql-server-management-studio-ssms.md).
1. Clique com o botão direito do mouse no novo banco de dados `SQLTestDB`, focalize **Tarefas** e, em seguida, selecione **Fazer backup...** para iniciar o assistente de **Backup do Banco de Dados**. 
1. Selecione **URL** na lista suspensa de destino **Backup até** e, em seguida, selecione **Adicionar** para iniciar a caixa de diálogo **Selecionar destino de backup**. 

   ![Fazer backup na URL](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/back-up-to-url.png)

1. Selecione o **Novo contêiner** na caixa de diálogo **Selecionar destino do backup** para iniciar a janela **Conectar-se a uma Assinatura da Microsoft**. 

   ![Destino do backup](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/select-backup-destination.png)

1. Entre no portal do Azure selecionando **Entrar...** e, em seguida, prossiga com o processo de entrada. 
1. Selecione sua **assinatura** na lista suspensa. 
1. Selecione sua **conta de armazenamento** na lista suspensa. 
1. Selecione o contêiner que você criou anteriormente na lista suspensa. 
1. Selecione **Criar credencial** para gerar sua *SAS (assinatura de acesso compartilhado)* .  **Salve esse valor, pois você precisará dele para a restauração.**

   ![Criar credencial](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/create-credential.png)

1. Selecione **OK** para fechar a janela **Conectar-se a uma Assinatura da Microsoft**. Isso preenche o valor do *contêiner de armazenamento do Azure* na caixa de diálogo **Selecionar destino do backup**. Selecione **OK** para escolher o contêiner de armazenamento selecionado e feche a caixa de diálogo. 
1. Neste ponto, você pode pular para a etapa 4 na próxima seção para fazer o backup do banco de dados ou pode fechar o assistente de **Backup do banco de dados**, caso deseje continuar usando o Transact-SQL para fazer backup do banco de dados. 


## <a name="back-up-database"></a>Backup do banco de dados
Nesta etapa, faça o backup do banco de dados `SQLTestDB` em sua conta de armazenamento de Blob do Azure usando a GUI do SQL Server Management Studio ou o T-SQL (Transact-SQL). 

# <a name="ssms"></a>[SSMS](#tab/SSMS)

1. Se o assistente de **Backup do banco de dados** ainda não estiver aberto, expanda o nó **Banco de dados** no **Pesquisador de Objetos** do [SSMS (SQL Server Management Studio)](../ssms/download-sql-server-management-studio-ssms.md).
1. Clique com o botão direito do mouse no novo banco de dados `SQLTestDB`, focalize **Tarefas** e, em seguida, selecione **Fazer backup...** para iniciar o assistente de **Backup do Banco de Dados**. 
1. Selecione **URL** na lista suspensa de **Backup até** e, em seguida, selecione **Adicionar** para iniciar a caixa de diálogo **Selecionar destino de backup**. 

   ![Fazer backup na URL](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/back-up-to-url.png)

1. Selecione o contêiner que você criou na etapa anterior na lista suspensa do **Contêiner de armazenamento do Azure**. 

   ![Contêiner de armazenamento do Azure](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/azure-storage-container.png)

1. Selecione **OK** no assistente de **Backup do banco de dados** para fazer backup do seu banco de dados. 
1. Selecione **OK** depois que o backup do banco de dados for concluído com êxito para fechar todas as janelas relacionadas ao backup. 

   > [!TIP]
   > Você pode gerar o script do Transact-SQL por trás desse comando selecionando **Script** na parte superior do assistente de **Backup do banco de dados**: ![Comando de script](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/script-backup-command.png)


# <a name="transact-sql"></a>[Transact-SQL](#tab/tsql)

Faça backup do banco de dados usando o Transact-SQL executando o seguinte comando: 


```sql
USE [master]

BACKUP DATABASE [SQLTestDB] 
TO  URL = N'https://msftutorialstorage.blob.core.windows.net/sql-backup/sqltestdb_backup_2020_01_01_000001.bak' 
WITH  COPY_ONLY, CHECKSUM
GO
```

---

## <a name="delete-database"></a>Excluir banco de dados
Nesta etapa, exclua o banco de dados antes de executar a restauração. Esta etapa é necessária apenas para fins deste tutorial, mas é improvável que seja usada em procedimentos normais de gerenciamento de banco de dados. Você pode ignorar esta etapa, mas precisará alterar o nome do banco de dados durante a restauração em uma instância gerenciada ou executar o comando restore `WITH REPLACE` para restaurar com sucesso o banco de dados no local. 

# <a name="ssms"></a>[SSMS](#tab/SSMS)

1. Expanda o nó **Banco de dados** no **Pesquisador de Objetos**, clique com o botão direito do mouse no banco de dados `SQLTestDB` e selecione excluir para iniciar o assistente **Excluir objeto**. 
1. Em uma instância gerenciada, selecione **OK** para excluir o banco de dados. No local, marque a caixa de seleção ao lado de **Fechar conexões existentes** e, em seguida, selecione **OK** para excluir o banco de dados. 

# <a name="transact-sql"></a>[Transact-SQL](#tab/tsql)

Exclua o banco de dados executando o seguinte comando Transact-SQL:

```sql
USE [master]
GO
DROP DATABASE [SQLTestDB]
GO

-- If connections currently exist on-premises, you'll need to set the database into single user mode first
USE [master]
GO
ALTER DATABASE [SQLTestDB] SET  SINGLE_USER WITH ROLLBACK IMMEDIATE
GO
USE [master]
GO
DROP DATABASE [SQLTestDB]
GO
```

---


## <a name="restore-database"></a>Restaurar Banco de Dados 
Nesta etapa, restaure o banco de dados usando a GUI no SQL Server Management Studio ou o Transact-SQL. 

# <a name="ssms"></a>[SSMS](#tab/SSMS)

1. Clique com o botão direito do mouse no nó **Banco de dados** no **Pesquisador de Objetos** do SQL Server Management Studio e selecione **Restaurar o banco de dados**. 
1. Selecione **Dispositivo** e, em seguida, selecione as reticências (...) para escolher o dispositivo. 

   ![Selecionar o dispositivo de restauração](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/select-restore-device.png)

1. Selecione a **URL** na lista suspensa **Tipo de mídia de backup** e selecione **Adicionar** para adicionar seu dispositivo. 

   ![Adicionar o dispositivo de backup](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/add-backup-device.png)

1. Selecione o contêiner na lista suspensa e cole a SAS (Assinatura de Acesso Compartilhado) que você salvou ao criar a credencial. 

   ![Destino do backup](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/restore-from-container.png)

1. Selecione **OK** para selecionar o local do arquivo de backup. 
1. Expanda **Containers** e selecione o contêiner no qual o arquivo de backup existe. 
1. Selecione o arquivo de backup que deseja restaurar e, em seguida, selecione **OK**. Se não houver nenhum arquivo visível, pode ser que você esteja usando a chave SAS incorreta. Você pode gerar novamente a chave SAS seguindo as mesmas etapas de antes para adicionar o contêiner. 

   ![Selecionar o arquivo de restauração](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/select-restore-file.png)

1. Clique em **OK** para fechar a caixa de diálogo **Selecionar dispositivos de backup**. 
1. Selecione **OK** para restaurar o banco de dados. 

# <a name="transact-sql"></a>[Transact-SQL](#tab/tsql)

Para restaurar seu banco de dados local do armazenamento de Blob do Azure, modifique o comando Transact-SQL a seguir para usar sua própria conta de armazenamento e, em seguida, execute-o em uma nova janela de consulta. 

```sql
USE [master]
RESTORE DATABASE [SQLTestDB] FROM 
URL = N'https://msftutorialstorage.blob.core.windows.net/sql-backup/sqltestdb_backup_2020_01_01_000001.bak'
```

---


## <a name="see-also"></a>Confira também 
Estas são algumas leituras que podem ajudar a compreender os conceitos e as práticas recomendadas ao usar o serviço de armazenamento de Blobs do Azure para backups do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   [Backup e restauração do SQL Server com o Serviço de Armazenamento de Blobs do Microsoft Azure](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)   
-   [Solução de problemas e melhores práticas de backup do SQL Server para URL](../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
  
