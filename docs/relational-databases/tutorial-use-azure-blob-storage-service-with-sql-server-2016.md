---
title: 'Tutorial: Usar o serviço de Armazenamento de Blobs do Azure com o SQL Server 2016 | Microsoft Docs'
ms.custom: ''
ms.date: 01/09/2019
ms.prod: sql
ms.technology: ''
ms.prod_service: database-engine
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- SQL Server 2016
ms.assetid: e69be67d-da1c-41ae-8c9a-6b12c8c2fb61
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e6833381664fa71f61e6e021d81154afdb0945cb
ms.sourcegitcommit: c6e71ed14198da67afd7ba722823b1af9b4f4e6f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54327767"
---
# <a name="tutorial-use-azure-blob-storage-service-with-sql-server-2016"></a>Tutorial: Usar o serviço de Armazenamento de Blobs do Azure com o SQL Server 2016

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Bem-vindo ao tutorial “Trabalhando com o SQL Server 2016 no serviço de Armazenamento de Blobs do Microsoft Azure”. Este tutorial o ajudará a entender como usar o serviço de armazenamento de Blobs do Microsoft Azure para arquivos de dados e backups do SQL Server.  
  
O suporte da integração do SQL Server no serviço de armazenamento de Blobs do Microsoft Azure começou como uma melhoria do SQL Server 2012 Service Pack 1 CU2 e foi aprimorado ainda mais com o SQL Server 2014 e SQL Server 2016. Para obter uma visão geral da funcionalidade e dos benefícios do uso desse recurso, confira [Arquivos de dados do SQL Server no Microsoft Azure](../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md). Para uma demonstração ao vivo, confira [Demonstração da recuperação pontual](https://channel9.msdn.com/Blogs/Windows-Azure/File-Snapshot-Backups-Demo).  

Este tutorial mostra como trabalhar com arquivos de dados do SQL Server no serviço de Armazenamento de Blobs do Microsoft Azure em várias seções. Cada seção é centrada em uma tarefa específica e as seções devem ser concluídas na sequência. Primeiro, você aprenderá a criar um novo contêiner no armazenamento de Blobs com uma política de acesso armazenado e uma assinatura de acesso compartilhado. Em seguida, você aprenderá a criar uma credencial do SQL Server para integrar o SQL Server com o Armazenamento de Blobs do Azure. Em seguida, você vai fazer backup de um banco de dados no armazenamento de Blobs e restaurá-lo em uma máquina virtual do Azure. Depois, você vai usar o backup de log de transações de instantâneo de arquivo do SQL Server 2016 para restaurá-lo em um ponto específico e em um novo banco de dados. Por fim, o tutorial demonstrará o uso dos procedimentos armazenados e funções do sistema de metadados para ajudá-lo a entender e trabalhar com backups de instantâneo de arquivo.
  
## <a name="prerequisites"></a>Prerequisites

Para concluir este tutorial, você deve estar familiarizado com os conceitos de backup e restauração do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e a sintaxe do T-SQL. Para usar este tutorial, você precisa de uma conta de Armazenamento do Azure, o SSMS (SQL Server Management Studio), acesso a uma instância local do SQL Server, acesso a uma VM (máquina virtual) do Azure que execute o SQL Server 2016 e um banco de dados AdventureWorks2016. Além disso, a conta de usuário usada para emitir os comandos BACKUP e RESTORE deve estar na função de banco de dados **db_backupoperator** com as permissões **Alterar qualquer credencial**. 

- Obtenha uma [conta do Azure](https://azure.microsoft.com/offers/ms-azr-0044p/) gratuita.
- Crie uma [conta de armazenamento do Azure](https://docs.microsoft.com/azure/storage/common/storage-quickstart-create-account?tabs=portal).
- Instalar o [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads).
- Provisionar uma [VM do Azure que executa o SQL Server](https://azure.microsoft.com/documentation/articles/virtual-machines-provision-sql-server/)
- Instalar o [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
- Baixar [Bancos de dados de exemplo do AdventureWorks2016](https://docs.microsoft.com/sql/samples/adventureworks-install-configure).
- Atribua a conta de usuário à função [db_backupoperator](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/database-level-roles) e conceda permissões para [Alterar qualquer credencial](https://docs.microsoft.com/sql/t-sql/statements/alter-credential-transact-sql). 
 
## <a name="1---create-stored-access-policy-and-shared-access-storage"></a>1 – Criar uma política de acesso armazenado e um armazenamento de acesso compartilhado

Nesta seção, você usará um script do [Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) para criar uma assinatura de acesso compartilhado em um contêiner de Blobs do Azure usando uma política de acesso armazenado.  
  
> [!NOTE]  
> Esse script é escrito com o Azure PowerShell 5.0.10586.  
  
Uma assinatura de acesso compartilhado é um URI que concede direitos de acesso restrito a contêineres, blobs, filas ou tabelas. Uma política de acesso armazenado fornece um nível adicional de controle sobre as assinaturas de acesso compartilhado do servidor, incluindo revogação, expiração ou extensão do acesso. Ao usar essa nova melhoria, você precisa criar uma política em um contêiner com direitos de leitura, gravação e lista.  
  
Você pode criar uma política de acesso armazenado e uma assinatura de acesso compartilhado usando o Azure PowerShell, o SDK do Armazenamento do Azure, a API REST do Azure ou um utilitário de terceiros. Este tutorial demonstra como usar um script do Azure PowerShell para concluir esta tarefa. O script usa o modelo de implantação do Resource Manager e cria os seguintes novos recursos  
  
-   Grupo de recursos   
-   Conta de armazenamento  
-   Contêiner de blobs do Azure   
-   Política do SAS    

Esse script começa declarando diversas variáveis para especificar os nomes dos recursos acima e os nomes dos seguintes valores de entrada necessários:  
  
-   Um nome de prefixo usado na nomeação de outros objetos de recurso    
-   Nome da assinatura    
-   Local do datacenter  

  
O script é concluído com a geração da instrução CREATE CREDENTIAL apropriada que você usará em [2 – Criar uma credencial do SQL Server usando uma assinatura de acesso compartilhado](#2---create-a-sql-server-credential-using-a-shared-access-signature). Essa instrução é copiada na área de transferência para você e é gerada no console para exibição.  
  
Para criar uma política no contêiner e gerar uma chave SAS (Assinatura de Acesso Compartilhado), siga estas etapas:  
  
1.  Abra a janela do Windows PowerShell ou o ISE do Windows PowerShell (consulte os requisitos de versão acima).  
  
2.  Edite e execute o script b:  
  
    ```powershell
    # Define global variables for the script  
    $prefixName = '<a prefix name>'  # used as the prefix for the name for various objects  
    $subscriptionID=='<your subscription ID>'   # the ID  of subscription name you will use  
    $locationName = '<a data center location>'  # the data center region you will use  
    $storageAccountName= $prefixName + 'storage' # the storage account name you will create or use  
    $containerName= $prefixName + 'container'  # the storage container name to which you will attach the SAS policy with its SAS token  
    $policyName = $prefixName + 'policy' # the name of the SAS policy 

    # Set a variable for the name of the resource group you will create or use  
    $resourceGroupName=$prefixName + 'rg'   
  
    # Add an authenticated Azure account for use in the session   
    Connect-AzAccount    
  
    # Set the tenant, subscription and environment for use in the rest of   
    Set-AzContext -SubscriptionId $subscriptionID   
  
    # Create a new resource group - comment out this line to use an existing resource group  
    New-AzResourceGroup -Name $resourceGroupName -Location $locationName   
  
    # Create a new Azure Resource Manager storage account - comment out this line to use an existing Azure Resource Manager storage account  
    New-AzStorageAccount -Name $storageAccountName -ResourceGroupName $resourceGroupName -Type Standard_RAGRS -Location $locationName   
  
    # Get the access keys for the Azure Resource Manager storage account  
    $accountKeys = Get-AzStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName  
  
    # Create a new storage account context using an Azure Resource Manager storage account  
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $accountKeys[0].Value

    # Creates a new container in blob storage  
    $container = New-AzureStorageContainer -Context $storageContext -Name $containerName  
  
    # Sets up a Stored Access Policy and a Shared Access Signature for the new container  
    $policy = New-AzureStorageContainerStoredAccessPolicy -Container $containerName -Policy $policyName -Context $storageContext -StartTime $(Get-Date).ToUniversalTime().AddMinutes(-5) -ExpiryTime $(Get-Date).ToUniversalTime().AddYears(10) -Permission rwld

    # Gets the Shared Access Signature for the policy  
    $sas = New-AzureStorageContainerSASToken -name $containerName -Policy $policyName -Context $storageContext
    Write-Host 'Shared Access Signature= '$($sas.Substring(1))''  

    # Sets the variables for the new container you just created
    $container = Get-AzureStorageContainer -Context $storageContext -Name $containerName
    $cbc = $container.CloudBlobContainer 
  
    # Outputs the Transact SQL to the clipboard and to the screen to create the credential using the Shared Access Signature  
    Write-Host 'Credential T-SQL'  
    $tSql = "CREATE CREDENTIAL [{0}] WITH IDENTITY='Shared Access Signature', SECRET='{1}'" -f $cbc.Uri,$sas.Substring(1)   
    $tSql | clip  
    Write-Host $tSql 

    # Once you're done with the tutorial, remove the resource group to clean up the resources. 
    # Remove-AzResourceGroup -Name $resourceGroupName  
    ```  

3.  Após a conclusão do script, a instrução CREATE CREDENTIAL estará localizada na área de transferência para uso na próxima seção.  


## <a name="2---create-a-sql-server-credential-using-a-shared-access-signature"></a>2 – Criar uma credencial do SQL Server usando uma assinatura de acesso compartilhado

Nesta seção, você aprenderá a criar uma credencial para armazenar as informações de segurança que serão usadas pelo SQL Server para gravar e ler o contêiner do Azure criado na etapa anterior.  
  
Uma credencial do SQL Server é um objeto usado para armazenar as informações de autenticação necessárias para se conectar a um recurso fora do SQL Server. A credencial armazena o caminho de URI do contêiner de armazenamento e a assinatura de acesso compartilhado desse contêiner.  

Para criar uma credencial do SQL Server, siga estas etapas:  
  
1.  Conecte-se ao SQL Server Management Studio.  
2.  Abra uma nova janela de consulta e conecte-se à instância do SQL Server do mecanismo de banco de dados no ambiente local.  
  
3.  Na nova janela de consulta, cole a instrução CREATE CREDENTIAL com a assinatura de acesso compartilhado da seção 1 e execute esse script.  
  
    O script será parecido com o código a seguir.  
  
    ```sql   
    USE master  
    CREATE CREDENTIAL [https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>] -- this name must match the container path, start with https and must not contain a forward slash at the end, the general format 
       WITH IDENTITY='SHARED ACCESS SIGNATURE' -- this is a mandatory string and do not change it.   
       , SECRET = 'sharedaccesssignature' -- this is the shared access signature key that you obtained in section 1.   
    GO   

    USE master  
    CREATE CREDENTIAL [https://msfttutorial.blob.core.windows.net/containername] -- this name must match the container path, start with https and must not contain a forward slash at the end, the general format 
       WITH IDENTITY='SHARED ACCESS SIGNATURE' -- this is a mandatory string and do not change it.   
       , SECRET = 'sharedaccesssignature' -- this is the shared access signature key that you obtained in section 1.   
    GO   
    ```  
  
4.  Para ver todas as credenciais disponíveis, você pode executar a seguinte instrução em uma janela de consulta conectada à sua instância:  
  
    ```sql  
    SELECT * from sys.credentials  
    ```  
  
5.  Abra uma nova janela de consulta e conecte-se à instância do SQL Server do mecanismo de banco de dados na máquina virtual do Azure.  
  
6.  Na nova janela de consulta, cole a instrução CREATE CREDENTIAL com a assinatura de acesso compartilhado da seção 1 e execute esse script.  
  
7.  Repita as etapas 5 e 6 para todas as outras instâncias do SQL Server às quais você quer conceder acesso ao contêiner do Azure.  

## <a name="3---database-backup-to-url"></a>3 – Backup de banco de dados em URL

Nesta seção, você fará backup do banco de dados AdventureWorks2016 na sua instância local do SQL Server 2016 no contêiner do Azure criado na [Seção 1](#1---create-stored-access-policy-and-shared-access-storage).
  
> [!NOTE]  
> Se quiser fazer backup de um banco de dados SQL Server 2012 SP1 CU2 ou posterior ou SQL Server 2014 nesse contêiner do Azure, você poderá usar a sintaxe preterida documentada [aqui](https://docs.microsoft.com/sql/relational-databases/backup-restore/sql-server-backup-to-url?view=sql-server-2014) para fazer backup na URL usando a sintaxe WITH CREDENTIAL.  
  
Para fazer backup de um banco de dados no armazenamento de Blobs, siga estas etapas:  
  
1.  Conecte-se ao SQL Server Management Studio.  
2.  Abra uma nova janela de consulta e conecte-se à instância do SQL Server 2016 do mecanismo de banco de dados na máquina virtual do Azure.  
3.  Copie e cole o script Transact-SQL a seguir na janela de consulta. Modifique a URL de forma adequada para o nome de sua conta de armazenamento e o contêiner especificado na Seção 1 e execute este script.  
  
    ```sql  
  
    -- To permit log backups, before the full database backup, modify the database to use the full recovery model.  
    USE master;  
    ALTER DATABASE AdventureWorks2016  
       SET RECOVERY FULL;  
  
    -- Back up the full AdventureWorks2016 database to the container that you created in section 1  
    BACKUP DATABASE AdventureWorks2016   
       TO URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2016_onprem.bak'  
  
    ```  
  
4.  Abra o Pesquisador de Objetos e conecte-se ao armazenamento do Azure usando sua conta de armazenamento e a chave de conta. 
    1.  Expanda Contêineres, expanda o contêiner criado na seção 1 e verifique se o backup da etapa 3 acima é exibido nesse contêiner.  
  
   ![Conectar a uma conta de Armazenamento do Azure](media/tutorial-use-azure-blob-storage-service-with-sql-server-2016/connect-to-azure-storage.png)


## <a name="4----restore-database-to-virtual-machine-from-url"></a>4 – Restaurar o banco de dados na máquina virtual por meio da URL

Nesta seção, você restaurará o banco de dados AdventureWorks2016 na instância do SQL Server 2016 na máquina virtual do Azure.
  
> [!NOTE]  
> Para fins de simplicidade neste tutorial, estamos usando o mesmo contêiner para os arquivos de log e de dados que foram usados para o backup do banco de dados. Em um ambiente de produção, provavelmente, você usará vários contêineres e, com frequência, vários arquivos de dados também. Com o SQL Server 2016, você poderá também considerar a distribuição do backup em vários blobs, a fim de aumentar o desempenho do backup ao fazer backup de um banco de dados grande.  
  
Para restaurar o banco de dados AdventureWorks2016 do Armazenamento de Blobs do Azure para a instância do SQL Server 2016 na máquina virtual do Azure, siga estas etapas:  
  
1.  Conecte-se ao SQL Server Management Studio.   
2.  Abra uma nova janela de consulta e conecte-se à instância do SQL Server 2016 do mecanismo de banco de dados na máquina virtual do Azure.   
3.  Copie e cole o script Transact-SQL a seguir na janela de consulta. Modifique a URL de forma adequada para o nome de sua conta de armazenamento e o contêiner especificado na Seção 1 e execute este script.  
  
    ```sql  
    -- Restore AdventureWorks2016 from URL to SQL Server instance using Azure blob storage for database files  
    RESTORE DATABASE AdventureWorks2016   
       FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2016_onprem.bak'   
       WITH  
          MOVE 'AdventureWorks2016_data' to 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2016_Data.mdf'  
         ,MOVE 'AdventureWorks2016_log' to 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2016_Log.ldf'  
    --, REPLACE  
  
    ```  
  
4.  Abra o Pesquisador de Objetos e conecte-se à instância do Azure SQL Server 2016.   
5.  No Pesquisador de Objetos, expanda o nó Bancos de Dados e verifique se o banco de dados AdventureWorks2016 foi restaurado (atualize o nó, conforme necessário)    
    1. Clique com o botão direito do mouse no AdventureWorks2016 e selecione Propriedades.
    1. Selecione Arquivos e verifique se os caminhos para os dois arquivos de banco de dados são URLs que apontam para blobs no seu contêiner de blogs do Azure (selecione Cancelar ao concluir).
    
     ![Banco de dados AdventureWorks em VM do Azure](media/tutorial-use-azure-blob-storage-service-with-sql-server-2016/adventureworks-on-azure-vm.png)

    
8.  No Pesquisador de Objetos, conecte-se ao armazenamento do Azure.
    1. Expanda Contêineres, expanda o contêiner criado na seção 1 e verifique se o AdventureWorks2016_Data.mdf e o AdventureWorks2016_Log.ldf da etapa 3 acima são exibidos nesse contêiner, juntamente com o arquivo de backup da seção 3 (atualize o nó, conforme necessário).  
  
   ![Arquivos de dados dentro do contêiner no Azure](media/tutorial-use-azure-blob-storage-service-with-sql-server-2016/data-files-in-container.png)

## <a name="5---backup-database-using-file-snapshot-backup"></a>5 – Fazer backup do banco de dados usando o backup de instantâneo de arquivo

Nesta seção, você fará backup do banco de dados AdventureWorks2016 na máquina virtual do Azure usando o backup de instantâneo de arquivo para executar um backup quase instantâneo usando instantâneos do Azure. Para obter mais informações sobre backups de instantâneo, veja [Backups de instantâneo de arquivo para arquivos de banco de dados no Azure](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)  
  
Para fazer backup do banco de dados AdventureWorks2016 usando o backup de instantâneo de arquivo, siga estas etapas:  
  
1.  Conecte-se ao SQL Server Management Studio.   
2.  Abra uma nova janela de consulta e conecte-se à instância do SQL Server 2016 do mecanismo de banco de dados na máquina virtual do Azure.  
3.  Copie, cole e execute o script Transact-SQL a seguir na janela de consulta (não feche esta janela de consulta – você executará esse script novamente na etapa 5). Esse procedimento armazenado do sistema permite exibir os backups de instantâneo de arquivo existentes de cada arquivo que consiste em um banco de dados especificado. Você observará que não há nenhum backup de instantâneo de arquivo desse banco de dados.  
  
    ```sql  
    -- Verify that no file snapshot backups exist  
    SELECT * FROM sys.fn_db_backup_file_snapshots ('AdventureWorks2016');  
    ```  
  
4.  Copie e cole o script Transact-SQL a seguir na janela de consulta. Modifique a URL de forma adequada para o nome de sua conta de armazenamento e o contêiner especificado na Seção 1 e execute este script. Observe como o backup ocorre rapidamente.  
  
    ```sql  
    -- Backup the AdventureWorks2016 database with FILE_SNAPSHOT  
    BACKUP DATABASE AdventureWorks2016   
       TO URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2016_Azure.bak'   
       WITH FILE_SNAPSHOT;    
    ```  
  
5.  Depois de verificar se o script da etapa 4 foi executado com êxito, execute novamente o script a seguir. Observe que a operação de backup de instantâneo de arquivo da etapa 4 gerou instantâneos de arquivo dos dados e do arquivo de log.  
  
    ```sql  
    -- Verify that two file-snapshot backups exist  
    SELECT * FROM sys.fn_db_backup_file_snapshots ('AdventureWorks2016');  
  
    ```  
  
    ![Resultados de fn_db_backup_file_snapshots mostrando instantâneos](media/tutorial-use-azure-blob-storage-service-with-sql-server-2016/results-showing-snapshot.png) 
  
6.  No Pesquisador de Objetos, na instância do SQL Server 2016 na máquina virtual do Azure, expanda o nó Bancos de Dados e verifique se o banco de dados AdventureWorks2016 foi restaurado para essa instância (atualize o nó, conforme necessário).  
7.  No Pesquisador de Objetos, conecte-se ao armazenamento do Azure.   
8.  Expanda Contêineres, expanda o contêiner criado na seção 1 e verifique se o AdventureWorks2016_Azure.bak da etapa 4 acima é exibido nesse contêiner, juntamente com o arquivo de backup da seção 3 e os arquivos de banco de dados da seção 4 (atualize o nó, conforme necessário).  
  
    ![Backup de instantâneo no Azure](media/tutorial-use-azure-blob-storage-service-with-sql-server-2016/snapshot-backup-on-azure.PNG)

## <a name="6----generate-activity-and-backup-log-using-file-snapshot-backup"></a>6 – Gerar log de atividade e de backup usando o backup de instantâneo de arquivo

Nesta seção, você gerará atividade no banco de dados AdventureWorks2016 e criará periodicamente backups de log de transações usando backups de instantâneo de arquivo. Para obter mais informações sobre como usar backups de instantâneo de arquivo, veja [Backups de instantâneo de arquivo para arquivos de banco de dados no Azure](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md).  
  
Para gerar atividade no banco de dados AdventureWorks2016 e criar periodicamente backups de log de transações usando backups de instantâneo de arquivo, siga estas etapas:  
  
1.  Conecte-se ao SQL Server Management Studio.   
2.  Abra duas novas janelas de consulta e conecte cada uma delas à instância do SQL Server 2016 do mecanismo de banco de dados na máquina virtual do Azure.   
3.  Copie, cole e execute o script Transact-SQL a seguir em uma das janelas de consulta. Observe que a tabela Production.Location tem 14 linhas antes de adicionarmos novas linhas na etapa 4.  
  
    ```sql 
    -- Verify row count at start  
    SELECT COUNT (*) from AdventureWorks2016.Production.Location;    
    ```  
  
4.  Copie e cole os dois scripts Transact-SQL a seguir em duas janelas de consulta separadas. Modifique a URL de forma adequada para o nome da sua conta de armazenamento e o contêiner especificado na seção 1 e execute estes scripts simultaneamente em janelas de consulta separadas. Esses scripts levarão cerca de sete minutos para serem concluídos.  
  
    ```sql  
    -- Insert 30,000 new rows into the Production.Location table in the AdventureWorks2014 database in batches of 75  
    DECLARE @count INT=1, @inner INT;  
    WHILE @count < 400  
       BEGIN  
          BEGIN TRAN;  
             SET @inner =1;  
                WHILE @inner <= 75  
                   BEGIN;  
                      INSERT INTO AdventureWorks2016.Production.Location    
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
  
    ```sql  
    --take 7 transaction log backups with FILE_SNAPSHOT, one per minute, and include the row count and the execution time in the backup file name   
    DECLARE @count INT=1, @device NVARCHAR(120), @numrows INT;  
    WHILE @count <= 7  
       BEGIN  
             SET @numrows = (SELECT COUNT (*) FROM AdventureWorks2016.Production.Location);  
             SET @device = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/tutorial-' + CONVERT (varchar(10),@numrows) + '-' + FORMAT(GETDATE(), 'yyyyMMddHHmmss') + '.bak';  
             BACKUP LOG AdventureWorks2016 TO URL = @device WITH FILE_SNAPSHOT;  
             SELECT * from sys.fn_db_backup_file_snapshots ('AdventureWorks2016');  
          WAITFOR DELAY '00:1:00';   
             SET @count = @count + 1;  
       END;  
    ```  
  
5.  Examine a saída do primeiro script e observe que a contagem de linhas final agora é de 29.939.  
  
    ![A contagem de linhas 29.939 é exibida](media/tutorial-use-azure-blob-storage-service-with-sql-server-2016/29-thousand-rows.png)
  
6.  Examine a saída do segundo script e observe que sempre que a instrução BACKUP LOG é executada, são criados dois novos instantâneos de arquivo: um instantâneo de arquivo do arquivo de log e um instantâneo de arquivo do arquivo de dados – em um total de dois instantâneos de arquivo para cada arquivo de banco de dados. Após a conclusão do segundo script, observe que agora há um total de 16 instantâneos de arquivo, 8 para cada arquivo de banco de dados – um da instrução BACKUP DATABASE e um para cada execução da instrução BACKUP LOG.  
  
   ![Resultados de instantâneo de backup](media/tutorial-use-azure-blob-storage-service-with-sql-server-2016/snapshot-back-results.png)
  
7.  No Pesquisador de Objetos, conecte-se ao armazenamento do Azure.  
  
8.  Expanda Contêineres, expanda o contêiner criado na seção 1 e verifique se sete novos arquivos de backup são exibidos, juntamente com os arquivos de dados das seções anteriores (atualize o nó, conforme necessário).  
  
    ![Vários instantâneos no Contêiner do Azure](media/tutorial-use-azure-blob-storage-service-with-sql-server-2016/tutorial-snapshots-in-container.png)

## <a name="7---restore-a-database-to-a-point-in-time"></a>7 – Restaurar um banco de dados para um momento determinado

Nesta seção, você aprenderá a restaurar o banco de dados AdventureWorks2016 para um ponto específico entre dois backups de log de transações.  
  
Com backups tradicionais, para realizar a restauração pontual, você precisaria usar o backup do banco de dados completo, talvez um backup diferencial, e todos os arquivos de log de transações incluindo e logo após o ponto específico para o qual você quer restaurar. Com os backups de instantâneo de arquivo, você só precisa de dois arquivos de backup de log de transações adjacentes que fornecem as metas que enquadram o tempo para o qual você quer restaurar. Você só precisa dois conjuntos de backup de instantâneo de arquivo de log, pois cada backup de log cria um instantâneo de arquivo de cada arquivo de banco de dados (cada arquivo de dados e o arquivo de log).  
  
Para restaurar um banco de dados para um ponto específico por meio de conjuntos de backup de instantâneo de arquivo, siga estas etapas:  
  
1.  Conecte-se ao SQL Server Management Studio.  
2.  Abra uma nova janela de consulta e conecte-se à instância do SQL Server 2016 do mecanismo de banco de dados na máquina virtual do Azure.   
3.  Copie, cole e execute o script Transact-SQL a seguir na janela de consulta. Verifique se a tabela Production.Location tem 29.939 linhas antes de restaurarmos para um ponto específico quando há menos linhas na etapa 5.  
  
    ```sql
    -- Verify row count at start  
    SELECT COUNT (*) from AdventureWorks2016.Production.Location   
    ```  
  
    ![A contagem de linhas 29.939 é exibida](media/tutorial-use-azure-blob-storage-service-with-sql-server-2016/29-thousand-rows.png) 
  
4.  Copie e cole o script Transact-SQL a seguir na janela de consulta. Selecione dois arquivos de backup de log adjacentes e converta o nome de arquivo na data e hora de que você precisará para esse script. Modifique a URL de forma adequada para o nome de sua conta de armazenamento e o contêiner especificado na seção 1, forneça os nomes do primeiro e segundo arquivos de backup, forneça a hora STOPAT no formato “26 de junho, 2018 01:48 PM” e execute este script. Esse script levará alguns minutos para ser concluído  
  
    ```sql  
    -- restore and recover to a point in time between the times of two transaction log backups, and then verify the row count  
    ALTER DATABASE AdventureWorks2016 SET SINGLE_USER WITH ROLLBACK IMMEDIATE;  
    RESTORE DATABASE AdventureWorks2016   
       FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/<firstbackupfile>.bak'   
       WITH NORECOVERY,REPLACE;  
    RESTORE LOG AdventureWorks2016   
       FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/<secondbackupfile>.bak'    
       WITH RECOVERY, STOPAT = 'June 26, 2018 01:48 PM';  
    ALTER DATABASE AdventureWorks2016 set multi_user;  
    -- get new count  
    SELECT COUNT (*) FROM AdventureWorks2016.Production.Location ;
    ```  
  
5.  Examine a saída. Observe que, após a restauração, a contagem de linhas é 18.389, que é um número de contagem de linhas entre o backup de log 5 e 6 (a contagem de linhas poderá variar).  
  
    ![18-thousand-rows.JPG](media/tutorial-use-azure-blob-storage-service-with-sql-server-2016/18-thousand-rows.png)

## <a name="8----restore-as-new-database-from-log-backup"></a>8 – Restaurar como um novo banco de dados por meio do backup de log de transações

Nesta seção, você aprenderá a restaurar o banco de dados AdventureWorks2016 como um novo banco de dados por meio de um backup de log de transações de instantâneo de arquivo.  
  
Nesse cenário, você realiza uma restauração de uma instância do SQL Server em outra máquina virtual para fins de análise de negócios e relatório. A restauração em uma instância diferente em outra máquina virtual descarrega a carga de trabalho em uma máquina virtual dedicada e dimensionada para essa finalidade, removendo os requisitos de recursos do sistema transacional.  
  
A restauração por meio de um backup de log de transações com backup de instantâneo de arquivo é muito rápida e significativamente mais rápida do que com backups tradicionais de streaming. Com backups de streaming tradicionais, você precisaria usar o backup completo do banco de dados, talvez um backup diferencial e alguns ou todos os backups de log de transações (ou um novo backup completo do banco de dados). No entanto, com backups de log de instantâneo de arquivo, você só precisa do backup de log mais recente (ou outro backup de log ou os dois backups de log adjacentes para restauração pontual em um ponto entre dois horários de backup de log). Para ser claro, é necessário apenas um conjunto de backup de instantâneo de arquivo de log, porque cada backup de log de instantâneo de arquivo cria um instantâneo de arquivo de cada arquivo de banco de dados (cada arquivo de dados e o arquivo de log).  
  
Para restaurar um banco de dados em um novo banco de dados por meio de um backup de log de transações usando o backup de instantâneo de arquivo, siga estas etapas:  
  
1.  Conecte-se ao SQL Server Management Studio.   
2.  Abra uma nova janela de consulta e conecte-se à instância do SQL Server 2016 do mecanismo de banco de dados em uma máquina virtual do Azure.  
  
    > [!NOTE]  
    > Se esta for uma máquina virtual do Azure diferente da que você usou nas seções anteriores, verifique se você seguiu as etapas em [2–Criar uma credencial do SQL Server usando uma assinatura de acesso compartilhado](#2---create-a-sql-server-credential-using-a-shared-access-signature). Se você desejar restaurar para um contêiner diferente, siga as etapas em [1 – Criar política de acesso armazenado e armazenamento de acesso compartilhado](#1---create-stored-access-policy-and-shared-access-storage) para o novo contêiner.  
  
3.  Copie e cole o script Transact-SQL a seguir na janela de consulta. Selecione o arquivo de backup de log que você deseja usar. Modifique a URL de forma adequada para o nome de sua conta de armazenamento e o contêiner especificado na seção 1, forneça o nome do arquivo de backup de log e execute este script.  
  
    ```sql  
    -- restore as a new database from a transaction log backup file  
    RESTORE DATABASE AdventureWorks2016_EOM   
        FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/<logbackupfile.bak'    
        WITH MOVE 'AdventureWorks2016_data' to 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_EOM_Data.mdf'  
       , MOVE 'AdventureWorks2016_log' to 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_EOM_Log.ldf'  
       , RECOVERY  
    --, REPLACE   
    ```  
  
4.  Examine a saída para verificar se a restauração foi bem-sucedida.   
5.  No Pesquisador de Objetos, conecte-se ao armazenamento do Azure.    
6.  Expanda Contêineres, expanda o contêiner criado na seção 1 (atualize se necessário) e verifique se os novos arquivos de log e de dados são exibidos no contêiner, juntamente com os blobs das seções anteriores.  
  
    ![Contêiner do Azure mostrando os arquivos de log e de dados para o novo banco de dados](media/tutorial-use-azure-blob-storage-service-with-sql-server-2016/new-db-in-azure-container.png)

## <a name="9---manage-backup-sets-and-file-snapshot-backups"></a>9–Gerenciar conjuntos de backup e backups de instantâneo de arquivo

Nesta seção, você excluirá um conjunto de backup usando o procedimento armazenado do sistema [sp_delete_backup &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup.md). Esse procedimento armazenado do sistema exclui o arquivo de backup e o arquivo de instantâneo em cada arquivo de banco de dados associado a esse conjunto de backup.  
  
> [!NOTE]  
> Se tentar excluir um conjunto de backup excluindo apenas o arquivo de backup do contêiner de Blobs do Azure, você só excluirá o arquivo de backup em si – os instantâneos de arquivo associados permanecerão. Se você se deparar com este cenário, use a função do sistema [sys.fn_db_backup_file_snapshots &#40;Transact-SQL&#41;](../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md) para identificar a URL dos instantâneos de arquivo órfão e use o procedimento armazenado do sistema [sp_delete_backup_file_snapshot &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md) para excluir cada instantâneo de arquivo órfão. Para obter mais informações, consulte  [Backups de instantâneo de arquivo para arquivos de banco de dados no Azure](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md).  
  
Para excluir um conjunto de backup de instantâneo de arquivo, siga estas etapas:  
  
1.  Conecte-se ao SQL Server Management Studio.  
2.  Abra uma janela de nova consulta e conecte-se à instância do Azure SQL Server 2016 do mecanismo de banco de dados na máquina virtual do Azure (ou a qualquer instância do SQL Server 2016 com permissões de leitura e gravação nesse contêiner).   
3.  Copie e cole o script Transact-SQL a seguir na janela de consulta. Selecione o backup de log que você deseja excluir, juntamente com seus instantâneos de arquivo associados. Modifique a URL de forma adequada para o nome de sua conta de armazenamento e o contêiner especificado na seção 1, forneça o nome do arquivo de backup de log e execute este script.  
  
  ```sql
  sys.sp_delete_backup 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/tutorial-21764-20181003205236.bak';  
  ```  
  
4.  No Pesquisador de Objetos, conecte-se ao armazenamento do Azure.  
5.  Expanda Contêineres, expanda o contêiner criado na seção 1 e verifique se o arquivo de backup utilizado na etapa 3 não é mais exibido neste contêiner (atualize o nó, conforme necessário).  
  
    ![Contêiner do Azure mostrando a exclusão do blob de backup de log de transações](media/tutorial-use-azure-blob-storage-service-with-sql-server-2016/deleted-backup-snapshot.png)
  
6.  Copie, cole e execute o script Transact-SQL a seguir na janela de consulta para verificar se os dois instantâneos de arquivo foram excluídos.  
  
    ```sql  
    -- verify that two file snapshots have been removed  
    SELECT * from sys.fn_db_backup_file_snapshots ('AdventureWorks2016');   
    ```  
    ![Painel de resultados mostrando dois instantâneos de arquivo excluídos](media/tutorial-use-azure-blob-storage-service-with-sql-server-2016/results-of-two-deleted-snapshot-files.png)

## <a name="10---remove-resources"></a>10–Remover recursos

Depois de concluir este tutorial, e para conservar recursos, exclua o grupo de recursos criado neste tutorial. 

Para excluir o grupo de recursos, execute o seguinte código do powershell:

  ```powershell
  # Define global variables for the script  
  $prefixName = '<prefix name>'  # should be the same as the beginning of the tutorial
  
  # Set a variable for the name of the resource group you will create or use  
  $resourceGroupName=$prefixName + 'rg'   
  
  # Adds an authenticated Azure account for use in the session   
  Connect-AzAccount    
  
  # Set the tenant, subscription and environment for use in the rest of   
  Set-AzContext -SubscriptionId $subscriptionID    
    
  # Remove the resource group
  Remove-AzResourceGroup -Name $resourceGroupName   
  ```


  
## <a name="see-also"></a>Consulte Também

[Arquivos de dados do SQL Server no Microsoft Azure](../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md)  
[Backups de instantâneo de arquivo para arquivos de banco de dados no Azure](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)  
[Backup do SQL Server para URL](../relational-databases/backup-restore/sql-server-backup-to-url.md) 
[Assinaturas de Acesso Compartilhado, Parte 1: Noções básicas sobre o modelo SAS](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/)  
[Criar contêiner](https://msdn.microsoft.com/library/azure/dd179468.aspx)  
[Definir ACL do contêiner](https://msdn.microsoft.com/library/azure/dd179391.aspx)  
[Obter ACL do contêiner](https://msdn.microsoft.com/library/azure/dd179469.aspx)
[Credenciais &#40;Mecanismo de Banco de Dados&#41;](../relational-databases/security/authentication-access/credentials-database-engine.md)  
[CREATE CREDENTIAL &#40;Transact-SQL&#41;](../t-sql/statements/create-credential-transact-sql.md)  
[sys.credentials &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
[sp_delete_backup &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup.md)  
[sys.fn_db_backup_file_snapshots &#40;Transact-SQL&#41;](../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md)  
[sp_delete_backup_file_snapshot &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md) [Backups de instantâneo de arquivo para arquivos de banco de dados no Azure](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)  
