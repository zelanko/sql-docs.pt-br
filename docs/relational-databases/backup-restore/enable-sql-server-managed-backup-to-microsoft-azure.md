---
title: Usar o backup de gerenciado no Azure"
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.description: Enable SQL Server managed backup to Azure
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 68ebb53e-d5ad-4622-af68-1e150b94516e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 07bb9cf8f0fc697e1d31a80e22a72cd5a0ea484a
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75257949"
---
# <a name="enable-sql-server-managed-backup-to-azure"></a>Habilitar o backup gerenciado do SQL Server no Azure

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como habilitar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] com as configurações padrão nos níveis de instância e de banco de dados. Também descreve como habilitar as notificações por email e como monitorar a atividade de backup.  
  
 Este tutorial usa o Azure PowerShell. Antes de iniciar o tutorial, [baixe e instale o Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).  
  
> [!IMPORTANT]  
>  Se você também quiser habilitar opções avançadas ou usar uma agenda personalizada, defina essas configurações antes de habilitar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. Para saber mais, confira [Configurar opções avançadas de backup gerenciado do SQL Server para o Microsoft Azure](../../relational-databases/backup-restore/configure-advanced-options-for-sql-server-managed-backup-to-microsoft-azure.md).  
  
## <a name="create-the-azure-blob-container"></a>Criar o contêiner de blob do Azure

O processo exige uma conta do Azure. Caso já tenha uma conta, vá para a próxima etapa. Caso contrário, você pode começar com uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/) ou explorar as [opções de compra](https://azure.microsoft.com/pricing/purchase-options/).

Para saber mais sobre contas de armazenamento, confira [Sobre as contas de armazenamento do Azure](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/). 

#### <a name="azure-clitabazure-cli"></a>[CLI do Azure](#tab/azure-cli)

1. Entre em sua conta do Azure.

    ```azurecli-interactive
    az login
    ```
  
1. Crie uma conta de armazenamento do Azure. Se você já tiver uma conta de armazenamento, vá para a próxima etapa. O comando a seguir cria uma conta de armazenamento chamada `<backupStorage>` na região Leste dos EUA.  
  
    ```azurecli-interactive
    az storage account create -n <backupStorage> -l "eastus" --resource-group <resourceGroup>
    ```  
    
1. Crie um contêiner de blob chamado `<backupContainer>` para os arquivos de backup.
  
    ```azurecli-interactive
    $keys = az storage account keys list --account-name <backupStorage> --resource-group <resourceGroup> | ConvertFrom-Json
    az storage container create --name <backupContainer> --account-name <backupStorage> --account-key $keys[0].value 
    ```  
  
1. Gere uma SAS (Assinatura de Acesso Compartilhado) para acessar o contêiner. O comando a seguir cria um token SAS para o contêiner de blob `<backupContainer>` que expira em um ano.  
  
    ```azurecli-interactive 
    az storage container generate-sas --name <backupContainer> --account-name <backupStorage> --account-key $keys[0].value
    ```

#### <a name="powershelltabazure-powershell"></a>[PowerShell](#tab/azure-powershell)

1. O comando a seguir conecta você à sua conta do Azure.

    ```azurepowershell-interactive
    Connect-AzAccount
    Set-AzContext -SubscriptionId "<subscriptionId>"
    ```
  
1. Crie uma conta de armazenamento do Azure. Se você já tiver uma conta de armazenamento, vá para a próxima etapa. O comando a seguir cria uma conta de armazenamento chamada `<backupStorage>` na região Leste dos EUA.  
  
    ```azurepowershell-interactive
    New-AzStorageAccount -StorageAccountName <backupStorage> -Location "EAST US" -ResourceGroupName <resourceGroup> -SkuName Standard_GRS
    ```   
  
1. Crie um contêiner de blob chamado `<backupContainer>` para os arquivos de backup.  
  
    ```azurepowershell-interactive
    $context = New-AzStorageContext -StorageAccountName <backupStorage> -StorageAccountKey (Get-AzStorageAccountKey -Name <backupStorage> -ResourceGroupName <resourceGroup>).Value[0]  
    New-AzStorageContainer -Name <backupContainer> -Context $context  
    ```  
  
1. Gere uma SAS (Assinatura de Acesso Compartilhado) para acessar o contêiner. O comando a seguir cria um token SAS para o contêiner de blob `<backupContainer>` que expira em um ano.
  
    ```azurepowershell-interactive 
    New-AzStorageContainerSASToken -Name <backupContainer> -Permission rwdl -ExpiryTime (Get-Date).AddYears(1) -FullUri -Context $context 
    ```

* * *

> [!NOTE]
> Essas etapas também podem ser realizadas usando o [portal do Azure](https://portal.azure.com/).

A saída conterá a URL para o contêiner e/ou o token SAS. A seguir, é mostrado um exemplo:  
  
  `https://managedbackupstorage.blob.core.windows.net/backupcontainer?sv=2014-02-14&sr=c&sig=xM2LXVo1Erqp7LxQ%9BxqK9QC6%5Qabcd%9LKjHGnnmQWEsDf%5Q%se=2015-05-14T14%3B93%4V20X&sp=rwdl`
  
Se a URL for incluída, separe-a do token SAS no ponto de interrogação (não inclua o ponto de interrogação). Por exemplo, a saída anterior resultaria nos dois valores a seguir.  
  
|||  
|-|-|  
|**URL do Contêiner**|https://managedbackupstorage.blob.core.windows.net/backupcontainer|  
|**Token SAS**|sv=2014-02-14&sr=c&sig=xM2LXVo1Erqp7LxQ%9BxqK9QC6%5Qabcd%9LKjHGnnmQWEsDf%5Q%se=2015-05-14T14%3B93%4V20X&sp=rwdl|  
|||
  
Registre a URL do contêiner e a SAS para uso na criação de uma CREDENCIAL DO SQL. Para saber mais sobre SAS, confira [Shared Access Signatures, Part 1: Understanding the SAS Model](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/) (Assinaturas de Acesso Compartilhado, Parte 1: noções básicas sobre o modelo de SAS)  
  
## <a name="enable-managed-backup-to-azure"></a>Habilitar o backup gerenciado no Azure
  
1.  **Criar uma Credencial do SQL para a URL SAS:** Use o token SAS para criar uma Credencial do SQL para a URL do contêiner de blobs. No SQL Server Management Studio, use a seguinte consulta Transact-SQL a fim de criar a credencial para a URL de seu contêiner de blob, com base no exemplo a seguir:  
  
    ```sql  
    CREATE CREDENTIAL [https://managedbackupstorage.blob.core.windows.net/backupcontainer]   
    WITH IDENTITY = 'Shared Access Signature',  
    SECRET = 'sv=2014-02-14&sr=c&sig=xM2LXVo1Erqp7LxQ%9BxqK9QC6%5Qabcd%9LKjHGnnmQWEsDf%5Q%se=2015-05-14T14%3B93%4V20X&sp=rwdl'  
    ```  
  
2.  **Garantir que o serviço SQL Server Agent foi iniciado e está em execução:** Inicie o SQL Server Agent se ele não estiver em execução.  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] requer que o SQL Server Agent esteja em execução na instância para executar operações de backup.  Talvez seja necessário definir o SQL Server Agent para ser executado automaticamente, a fim de assegurar que as operações de backup ocorrerão regularmente.  
  
3.  **Determinar o período de retenção:** determine o período de retenção dos arquivos de backup. O período de retenção é especificado em dias e pode variar de 1 a 30.  
  
4.  **Habilitar e configurar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]:**  Inicie o SQL Server Management Studio e conecte-se à instância e destino do SQL Server. Na janela de consulta, execute a seguinte instrução após modificar os valores do nome do banco de dados, da URL do contêiner e do período de retenção, de acordo com seus requisitos:  
  
    > [!IMPORTANT]  
    >  Para habilitar o backup gerenciado no nível da instância, especifique `NULL` ou para o parâmetro `database_name` .  
  
    ```sql  
    USE msdb;  
    GO  
    EXEC msdb.managed_backup.sp_backup_config_basic   
     @enable_backup = 1,   
     @database_name = 'yourdatabasename',  
     @container_url = 'https://managedbackupstorage.blob.core.windows.net/backupcontainer',   
     @retention_days = 30  
    GO  
    ```  
  
     [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] está habilitado no banco de dados que você especificou. Podem ser necessários até 15 minutos para que as operações de backup no banco de dados comecem a ser executadas.  
  
5.  **Examinar a Configuração Padrão do Evento Estendido:** examine as configurações do Evento Estendido executando a instrução transact-SQL a seguir.  
  
    ```sql
    SELECT * FROM msdb.managed_backup.fn_get_current_xevent_settings()  
    ```  
  
     Você verá que os eventos de canal Admin, Operacional e Analítico estão habilitados por padrão e não podem ser desabilitados. Isso deve ser suficiente para monitorar os eventos que requerem intervenção manual.  Você pode habilitar os eventos de depuração, mas os canais de depuração incluem eventos informativos e de depuração que o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] usa para detectar problemas e resolvê-los.  
  
6.  **Habilitar e configurar a notificação do status de integridade:** [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] tem um procedimento armazenado que cria um trabalho de agente para enviar notificações por email sobre erros ou avisos que possam exigir atenção. As etapas a seguir descrevem o processo para habilitar e configurar notificações por email:  
  
    1.  Configure o Database Mail se ele ainda não estiver habilitado na instância. Para obter mais informações, consulte [Configure Database Mail](../../relational-databases/database-mail/configure-database-mail.md).  
  
    2.  Configure o SQL Server Agent Notification para usar o Database Mail. Para obter mais informações, consulte [Configurar o SQL Server Agent Mail para usar o Database Mail](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md).  
  
    3.  **Habilitar notificações por email para receber avisos e erros de backup:** Na janela de consulta, execute as seguintes instruções Transact-SQL:  
  
        ```sql
        EXEC msdb.managed_backup.sp_set_parameter  
        @parameter_name = 'SSMBackup2WANotificationEmailIds',  
        @parameter_value = '<email1;email2>'  
        ```  
  
7.  **Exibir arquivos de backup na conta de armazenamento do Azure:** Conecte-se à conta de armazenamento no SQL Server Management Studio ou no portal do Azure. Você verá os arquivos de backup no contêiner especificado. Observe que você poderá ver um banco de dados e um backup de log após 5 minutos da habilitação do [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para o banco de dados.  
  
8.  **Monitorar o Status de Integridade:**  Realize o monitoramento por meio das notificações por email configuradas anteriormente ou monitore de forma ativa os eventos registrados em log. Estes são alguns exemplos de instruções Transact-SQL usados para exibir os eventos:  
  
    ```sql  
    --  view all admin events  
    USE msdb;  
    GO  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)   
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
  
    DECLARE @eventresult TABLE  
    (event_type nvarchar(512),  
    event nvarchar (512),  
    timestamp datetime  
    )  
  
    INSERT INTO @eventresult  
  
    EXEC managed_backup.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek  
  
    SELECT * from @eventresult  
    WHERE event_type LIKE '%admin%'  
    ```  
  
    ```sql  
    -- to enable debug events  
    USE msdb;  
    GO  
    EXEC managed_backup.sp_set_parameter 'FileRetentionDebugXevent', 'True'  
    ```  
  
    ```sql  
    --  View all events in the current week  
    USE msdb;  
    GO  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)   
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
  
    EXEC managed_backup.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek;  
    ```
  
As etapas descritas nesta seção destinam-se especificamente à configuração do [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] pela primeira vez no banco de dados. Você pode modificar as configurações existentes usando o mesmo procedimento armazenado do sistema e fornecer os novos valores.  
  
## <a name="see-also"></a>Confira também  
 [Backup gerenciado do SQL Server no Azure](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)  
