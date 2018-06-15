---
title: Habilitar o backup gerenciado do SQL Server no Microsoft Azure | Microsoft Docs
ms.custom: ''
ms.date: 10/03/2016
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.suite: sql
ms.technology: backup-restore
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 68ebb53e-d5ad-4622-af68-1e150b94516e
caps.latest.revision: 25
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c8aebe504f63e5b99818a928f114841e3c90b075
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32921051"
---
# <a name="enable-sql-server-managed-backup-to-microsoft-azure"></a>Habilitar o backup gerenciado do SQL Server no Microsoft Azure
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como habilitar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] com as configurações padrão nos níveis de instância e de banco de dados. Também descreve como habilitar as notificações por email e como monitorar a atividade de backup.  
  
 Este tutorial usa o Azure PowerShell. Antes de iniciar o tutorial, [baixe e instale o Azure PowerShell](http://azure.microsoft.com/en-us/documentation/articles/powershell-install-configure/).  
  
> [!IMPORTANT]  
>  Se você também quiser habilitar opções avançadas ou usar uma agenda personalizada, defina essas configurações antes de habilitar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. Para saber mais, confira [Configure Advanced Options for SQL Server Managed Backup to Microsoft Azure](../../relational-databases/backup-restore/configure-advanced-options-for-sql-server-managed-backup-to-microsoft-azure.md).  
  
## <a name="enable-and-configure-includesssmartbackupincludesss-smartbackup-mdmd-with-default-settings"></a>Habilitar e configurar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] com as configurações padrão  
  
#### <a name="create-the-azure-blob-container"></a>Criar o contêiner de blob do Azure  
  
1.  **Inscrever-se no Azure:** se você já tiver uma assinatura do Azure, vá para a próxima etapa. Caso contrário, você pode começar com uma [avaliação gratuita](http://azure.microsoft.com/pricing/free-trial/) ou explorar as [opções de compra](http://azure.microsoft.com/pricing/purchase-options/).  
  
2.  **Criar uma conta de armazenamento do Azure:** se você já tiver uma conta de armazenamento, vá para a próxima etapa. Caso contrário, você pode usar o [Portal de Gerenciamento do Azure](https://manage.windowsazure.com/) ou o Azure PowerShell para criar a conta de armazenamento. O comando `New-AzureStorageAccount` a seguir cria uma conta de armazenamento chamada `managedbackupstorage` na região Leste dos EUA.  
  
    ```powershell  
    New-AzureStorageAccount -StorageAccountName "managedbackupstorage" -Location "EAST US"  
    ```  
  
     Para saber mais sobre contas de armazenamento, confira [Sobre as contas de armazenamento do Azure](http://azure.microsoft.com/en-us/documentation/articles/storage-create-storage-account/).  
  
3.  **Criar um contêiner de blob para os arquivos de backup:** você pode criar um contêiner de blob no Portal de Gerenciamento do Azure ou com o Azure PowerShell. O comando `New-AzureStorageContainer` a seguir cria um contêiner de blob chamado `backupcontainer` na conta de armazenamento `managedbackupstorage` .  
  
    ```powershell  
    $context = New-AzureStorageContext -StorageAccountName managedbackupstorage -StorageAccountKey (Get-AzureStorageKey -StorageAccountName managedbackupstorage).Primary  
    New-AzureStorageContainer -Name backupcontainer -Context $context  
    ```  
  
4.  **Gerar uma SAS (Assinatura de Acesso Compartilhado):** para acessar o contêiner, é necessário criar uma SAS. Isso pode ser feito em algumas ferramentas, código e no Azure PowerShell. O comando `New-AzureStorageContainerSASToken` a seguir cria um token SAS para o contêiner de blob `backupcontainer` que expira em um ano.  
  
    ```powershell  
    $context = New-AzureStorageContext -StorageAccountName managedbackupstorage -StorageAccountKey (Get-AzureStorageKey -StorageAccountName managedbackupstorage).Primary   
    New-AzureStorageContainerSASToken -Name backupcontainer -Permission rwdl -ExpiryTime (Get-Date).AddYears(1) -FullUri -Context $context  
    ```  
  
     A saída desse comando conterá a URL para o contêiner e o token SAS. A seguir, é mostrado um exemplo:  
  
    ```  
    https://managedbackupstorage.blob.core.windows.net/backupcontainer?sv=2014-02-14&sr=c&sig=xM2LXVo1Erqp7LxQ%9BxqK9QC6%5Qabcd%9LKjHGnnmQWEsDf%5Q%se=2015-05-14T14%3B93%4V20X&sp=rwdl  
    ```  
  
     No exemplo anterior, separe a URL do contêiner do token SAS no ponto de interrogação (não inclua o ponto de interrogação). Por exemplo, a saída anterior resultaria nos dois valores a seguir.  
  
    |||  
    |-|-|  
    |**URL do Contêiner:**|https://managedbackupstorage.blob.core.windows.net/backupcontainer|  
    |**Token SAS:**|sv=2014-02-14&sr=c&sig=xM2LXVo1Erqp7LxQ%9BxqK9QC6%5Qabcd%9LKjHGnnmQWEsDf%5Q%se=2015-05-14T14%3B93%4V20X&sp=rwdl|  
  
     Registre a URL do contêiner e a SAS para uso na criação de uma CREDENCIAL DO SQL. Para saber mais sobre SAS, confira [Assinaturas de Acesso Compartilhado, parte 1: noções básicas sobre o modelo SAS](http://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/).  
  
#### <a name="enable-includesssmartbackupincludesss-smartbackup-mdmd"></a>Habilitar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]  
  
1.  **Criar uma Credencial do SQL para a URL SAS:** use o token SAS para criar uma Credencial do SQL para a URL do contêiner de blob. No SQL Server Management Studio, use a seguinte consulta Transact-SQL a fim de criar a credencial para a URL de seu contêiner de blob, com base no exemplo a seguir:  
  
    ```sql  
    CREATE CREDENTIAL [https://managedbackupstorage.blob.core.windows.net/backupcontainer]   
    WITH IDENTITY = 'Shared Access Signature',  
    SECRET = 'sv=2014-02-14&sr=c&sig=xM2LXVo1Erqp7LxQ%9BxqK9QC6%5Qabcd%9LKjHGnnmQWEsDf%5Q%se=2015-05-14T14%3B93%4V20X&sp=rwdl'  
    ```  
  
2.  **Verificar se o serviço SQL Server Agent foi iniciado e está em execução:** inicie o SQL Server Agent se ele não estiver em execução.  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] requer que o SQL Server Agent esteja em execução na instância para executar operações de backup.  Talvez seja necessário definir o SQL Server Agent para ser executado automaticamente, a fim de assegurar que as operações de backup ocorrerão regularmente.  
  
3.  **Determinar o período de retenção:** determina o período de retenção dos arquivos de backup. O período de retenção é especificado em dias e pode variar de 1 a 30.  
  
4.  **Enable and configure [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] :** inicie o SQL Server Management Studio e conecte-se à instância de destino do SQL Server. Na janela de consulta, execute a seguinte instrução após modificar os valores do nome do banco de dados, da URL do contêiner e do período de retenção, de acordo com seus requisitos:  
  
    > [!IMPORTANT]  
    >  Para habilitar o backup gerenciado no nível da instância, especifique `NULL` ou para o parâmetro `database_name` .  
  
    ```sql  
    Use msdb;  
    GO  
    EXEC msdb.managed_backup.sp_backup_config_basic   
     @enable_backup = 1,   
     @database_name = 'yourdatabasename',  
     @container_url = 'https://managedbackupstorage.blob.core.windows.net/backupcontainer',   
     @retention_days = 30  
    GO  
    ```  
  
     [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] está habilitado no banco de dados que você especificou. Podem ser necessários até 15 minutos para que as operações de backup no banco de dados comecem a ser executadas.  
  
5.  **Examinar a configuração padrão do Evento Estendido:** examine as configurações do Evento Estendido executando a instrução Transact-SQL a seguir.  
  
    ```  
    SELECT * FROM msdb.managed_backup.fn_get_current_xevent_settings()  
    ```  
  
     Você verá que os eventos de canal Admin, Operacional e Analítico estão habilitados por padrão e não podem ser desabilitados. Isso deve ser suficiente para monitorar os eventos que requerem intervenção manual.  Você pode habilitar os eventos de depuração, mas os canais de depuração incluem eventos informativos e de depuração que o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] usa para detectar problemas e resolvê-los.  
  
6.  **Habilitar e configurar a notificação do status de integridade:** [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] tem um procedimento armazenado que cria um trabalho de agente para enviar notificações por email sobre erros ou avisos que possam exigir atenção. As etapas a seguir descrevem o processo para habilitar e configurar notificações por email:  
  
    1.  Configure o Database Mail se ele ainda não estiver habilitado na instância. Para obter mais informações, consulte [Configure Database Mail](../../relational-databases/database-mail/configure-database-mail.md).  
  
    2.  Configure o SQL Server Agent Notification para usar o Database Mail. Para saber mais, confira [Configure SQL Server Agent Mail to Use Database Mail](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md).  
  
    3.  **Habilitar notificações por email para receber erros e avisos de backup:** na janela da consulta, execute as seguintes instruções Transact-SQL:  
  
        ```  
        EXEC msdb.managed_backup.sp_set_parameter  
        @parameter_name = 'SSMBackup2WANotificationEmailIds',  
        @parameter_value = '<email1;email2>'  
  
        ```  
  
7.  **Exibir arquivos de backup na Conta de Armazenamento do Microsoft Azure:** conecte-se à conta de armazenamento no SQL Server Management Studio ou no Portal de Gerenciamento do Azure. Você verá os arquivos de backup no contêiner especificado. Observe que você poderá ver um banco de dados e um backup de log após 5 minutos da habilitação do [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para o banco de dados.  
  
8.  **Monitorar o status de integridade:**  é possível monitorar por meio das notificações por email que você configurou antes ou monitorar ativamente os eventos registrados. Estes são alguns exemplos de instruções Transact-SQL usados para exibir os eventos:  
  
    ```  
    --  view all admin events  
    Use msdb;  
    Go  
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
  
    ```  
    -- to enable debug events  
    Use msdb;  
    Go  
             EXEC managed_backup.sp_set_parameter 'FileRetentionDebugXevent', 'True'  
  
    ```  
  
    ```  
    --  View all events in the current week  
    Use msdb;  
    Go  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)   
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
  
    EXEC managed_backup.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek;  
  
    ```  
  
 As etapas descritas nesta seção destinam-se especificamente à configuração do [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] pela primeira vez no banco de dados. Você pode modificar as configurações existentes usando o mesmo procedimento armazenado do sistema e fornecer os novos valores.  
  
## <a name="see-also"></a>Consulte Também  
 [Backup gerenciado do SQL Server no Microsoft Azure](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)  
  
  
