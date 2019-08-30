---
title: Configurando SQL Server Backup gerenciado para o Azure | Microsoft Docs
ms.custom: ''
ms.date: 08/04/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 68ebb53e-d5ad-4622-af68-1e150b94516e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b69439226b55965e37f24f2131c77340ae833590
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70154722"
---
# <a name="setting-up-sql-server-managed-backup-to-azure"></a>Configurando SQL Server Backup gerenciado para o Azure
  Este tópico inclui dois tutoriais:  
  
 Configure o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] no nível do banco de dados, habilite a notificação por email e monitore a atividade de backup.  
  
 Ao configurar o  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] no nível da instância, habilite a notificação por email e monitore a atividade de backup.  
  
 Para obter um tutorial sobre como [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] configurar grupos de disponibilidade, confira Configurando [SQL Server Backup gerenciado para Microsoft Azure para grupos de disponibilidade](../../database-engine/setting-up-sql-server-managed-backup-to-windows-azure-for-availability-groups.md).  
  
## <a name="setting-up-includess_smartbackupincludesss-smartbackup-mdmd"></a>Configurando o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]  
  
### <a name="enable-and-configure-includess_smartbackupincludesss-smartbackup-mdmd-for-a-database"></a>Habilitar e configurar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para um banco de dados  
 Este tutorial descreve as etapas necessárias para habilitar e configurar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para um banco de dados (TestDB), seguidas pelas etapas para habilitar o monitoramento do status de integridade do [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] .  
  
 **Permissões:**  
  
-   Requer associação na função de banco de dados **db_backupoperator** , com permissões **ALTER ANY Credential** e `EXECUTE` permissões no procedimento armazenado **sp_delete_backuphistory**.  
  
-   Requer permissões **SELECT** na função **smart_admin.fn_get_current_xevent_settings**.  
  
-   Requer `EXECUTE` permissões no procedimento armazenado **smart_admin. sp_get_backup_diagnostics** . Além disso, requer permissões `VIEW SERVER STATE`, pois chama internamente outros objetos do sistema que exigem essa permissão.  
  
-   Requer `EXECUTE` `smart_admin.sp_backup_master_switch` permissões`smart_admin.sp_set_instance_backup` nos procedimentos armazenados e.  


1.  **Criar uma conta de armazenamento Microsoft Azure:** Os backups são armazenados no serviço de armazenamento Microsoft Azure. Você deve primeiro criar uma conta de armazenamento Microsoft Azure, se ainda não tiver uma conta.
    - SQL Server 2014 usa blobs de página, que são diferentes dos BLOBs de bloco e de acréscimo. Portanto, você deve criar uma conta de uso geral e não uma conta de BLOB. Para obter mais informações, consulte [sobre contas de armazenamento do Azure](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/).
    - Anote o nome da conta de armazenamento e as chaves de acesso. O nome da conta de armazenamento e as informações de chave de acesso são usados para criar uma Credencial SQL. A Credencial SQL é usada para realizar a autenticação na conta de armazenamento.  
 
2.  **Criar uma credencial do SQL:** Crie uma credencial do SQL usando o nome da conta de armazenamento como a identidade e a chave de acesso de armazenamento como a senha.  
  
3.  **Garantir que o serviço SQL Server Agent foi iniciado e está em execução:**  Inicie o SQL Server Agent se ele não estiver em execução.  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] requer que o SQL Server Agent esteja em execução na instância para executar operações de backup.  Talvez seja necessário definir o SQL Server Agent para ser executado automaticamente, a fim de assegurar que as operações de backup ocorrerão regularmente.  
  
4.  **Determinar o período de retenção:** determine o período de retenção dos arquivos de backup. O período de retenção é especificado em dias e pode variar de 1 a 30.  
  
5.  **Habilitar e configurar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]:**  Inicie o SQL Server Management Studio e conecte-se à instância em que o banco de dados do está instalado. Na janela de consulta, execute a seguinte instrução após modificar os valores do nome do banco de dados, a Credencial SQL, o período de retenção e as opções de criptografia de acordo com seus requisitos:  
  
     Para obter mais informações sobre como criar um certificado para criptografia, consulte a etapa **Criar um certificado de backup** em [Create an Encrypted Backup](create-an-encrypted-backup.md).  
  
    ```  
    Use msdb;  
    GO  
    EXEC smart_admin.sp_set_db_backup   
                    @database_name='TestDB'   
                    ,@retention_days=30   
                    ,@credential_name='MyCredential'  
                    ,@encryption_algorithm ='AES_128'  
                    ,@encryptor_type= 'Certificate'  
                    ,@encryptor_name='MyBackupCert'  
                    ,@enable_backup=1;  
    GO  
  
    ```  
  
     [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] está habilitado no banco de dados que você especificou. Podem ser necessários até 15 minutos para que as operações de backup no banco de dados comecem a ser executadas.  
  
6.  **Examinar a Configuração Padrão do Evento Estendido:** examine as configurações do Evento Estendido executando a instrução transact-SQL a seguir.  
  
    ```  
    SELECT * FROM smart_admin.fn_get_current_xevent_settings()  
    ```  
  
     Você verá que os eventos de canal Admin, Operacional e Analítico estão habilitados por padrão e não podem ser desabilitados. Isso deve ser suficiente para monitorar os eventos que requerem intervenção manual.  Você pode habilitar os eventos de depuração, mas os canais de depuração incluem eventos informativos e de depuração que o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] usa para detectar problemas e resolvê-los. Para obter mais informações, consulte [monitorar SQL Server Backup gerenciado para Microsoft Azure](sql-server-managed-backup-to-microsoft-azure.md).  
  
7.  **Habilitar e configurar a notificação do status de integridade:** [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] tem um procedimento armazenado que cria um trabalho de agente para enviar notificações por email sobre erros ou avisos que possam exigir atenção. As etapas a seguir descrevem o processo para habilitar e configurar notificações por email:  
  
    1.  Configure o Database Mail se ele ainda não estiver habilitado na instância. Para obter mais informações, consulte [Configure Database Mail](../database-mail/configure-database-mail.md).  
  
    2.  Configure o SQL Server Agent Notification para usar o Database Mail. Para obter mais informações, consulte [Configurar o SQL Server Agent Mail para usar o Database Mail](../database-mail/configure-sql-server-agent-mail-to-use-database-mail.md).  
  
    3.  **Habilitar notificações por email para receber avisos e erros de backup:** Na janela de consulta, execute as seguintes instruções Transact-SQL:  
  
        ```  
        EXEC msdb.smart_admin.sp_set_parameter  
        @parameter_name = 'SSMBackup2WANotificationEmailIds',  
        @parameter_value = '<email1;email2>'  
  
        ```  
  
         Para obter mais informações e um script de exemplo completo, consulte [monitorar SQL Server Backup gerenciado para Microsoft Azure](sql-server-managed-backup-to-microsoft-azure.md).  
  
8.  **Exibir arquivos de backup na Conta de Armazenamento do Microsoft Azure:** Conecte-se à conta de armazenamento do SQL Server Management Studio ou do Portal de Gerenciamento do Azure. Você verá um contêiner para a instância do SQL Server que hospeda o banco de dados que configurou para usar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. Você também poderá consultar um banco de dados e um backup de log 15 minutos depois de habilitar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para o banco de dados.  
  
9. **Monitorar o Status de Integridade:**  Realize o monitoramento por meio das notificações por email configuradas anteriormente ou monitore de forma ativa os eventos registrados em log. Estes são alguns exemplos de instruções Transact-SQL usados para exibir os eventos:  
  
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
  
    EXEC smart_admin.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek  
  
    SELECT * from @eventresult  
    WHERE event_type LIKE '%admin%'  
  
    ```  
  
    ```  
    -- to enable debug events  
    Use msdb;  
    Go  
             EXEC smart_admin.sp_set_parameter 'FileRetentionDebugXevent', 'True'  
  
    ```  
  
    ```  
    --  View all events in the current week  
    Use msdb;  
    Go  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)   
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
  
    EXEC smart_admin.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek;  
  
    ```  
  
 As etapas descritas nesta seção destinam-se especificamente à configuração do [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] pela primeira vez no banco de dados. Você pode modificar as configurações existentes usando o mesmo procedimento armazenado do sistema **smart_admin.sp_set_db_backup** e fornecer os novos valores. Para obter mais informações, consulte [SQL Server Backup gerenciado para Microsoft Azure-configurações de armazenamento e retenção](../../database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md).  
  
### <a name="enable-includess_smartbackupincludesss-smartbackup-mdmd-for-the-instance-with-default-settings"></a>Habilitar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para a instância com configurações padrão  
 Este tutorial descreve as etapas para habilitar e configurar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] o para a instância do, ' MyInstance\\',. Inclui etapas para habilitar o monitoramento do status de integridade do [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] .  
  
 **Permissões:**  
  
-   Requer associação na função de banco de dados **db_backupoperator** , com permissões **ALTER ANY Credential** e `EXECUTE` permissões no procedimento armazenado **sp_delete_backuphistory**.  
  
-   Requer permissões **SELECT** na função **smart_admin.fn_get_current_xevent_settings**.  
  
-   Requer `EXECUTE` permissões no procedimento armazenado **smart_admin. sp_get_backup_diagnostics** . Além disso, requer permissões `VIEW SERVER STATE`, pois chama internamente outros objetos do sistema que exigem essa permissão.  


1.  **Criar uma conta de armazenamento Microsoft Azure:** Os backups são armazenados no serviço de armazenamento Microsoft Azure. Você deve primeiro criar uma conta de armazenamento Microsoft Azure, se ainda não tiver uma conta.
    - SQL Server 2014 usa blobs de página, que são diferentes dos BLOBs de bloco e de acréscimo. Portanto, você deve criar uma conta de uso geral e não uma conta de BLOB. Para obter mais informações, consulte [sobre contas de armazenamento do Azure](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/).
    - Anote o nome da conta de armazenamento e as chaves de acesso. O nome da conta de armazenamento e as informações de chave de acesso são usados para criar uma Credencial SQL. A Credencial SQL é usada para realizar a autenticação na conta de armazenamento.  
  
2.  **Criar uma credencial do SQL:** Crie uma credencial do SQL usando o nome da conta de armazenamento como a identidade e a chave de acesso de armazenamento como a senha.  
  
3.  **Garantir que o serviço SQL Server Agent foi iniciado e está em execução:** Inicie o SQL Server Agent se ele não estiver em execução. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] requer que o SQL Server Agent esteja em execução na instância para executar operações de backup.  Talvez seja necessário definir o SQL Server Agent para ser executado automaticamente, a fim de assegurar que as operações de backup ocorrerão regularmente.  
  
4.  **Determinar o período de retenção:** determine o período de retenção dos arquivos de backup. O período de retenção é especificado em dias e pode variar de 1 a 30. Depois que o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] for habilitado no nível da instância com os valores padrão, os novos bancos de dados criados depois herdarão as configurações. Somente os bancos de dados definidos para modelos de recuperação completa ou bulk-logged têm suporte e serão configuradas automaticamente. Você poderá desabilitar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para um banco de dados específico a qualquer momento se não quiser o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] configurado. Você também pode alterar a configuração de um banco de dados configurando o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] no nível do banco de dados.  
  
5.  **Habilitar e configurar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]:**  Inicie SQL Server Management Studio e conecte-se à instância do SQL Server. Na janela de consulta, execute a seguinte instrução após modificar os valores do nome do banco de dados, a Credencial SQL, o período de retenção e as opções de criptografia de acordo com seus requisitos:  
  
     Para obter mais informações sobre como criar um certificado para criptografia, consulte a etapa **Criar um certificado de backup** em [Create an Encrypted Backup](create-an-encrypted-backup.md).  
  
    ```  
    Use msdb;  
    Go  
       EXEC smart_admin.sp_set_instance_backup  
                     @enable_backup=1  
                    ,@retention_days=30   
                    ,@credential_name='sqlbackuptoURL'  
                    ,@encryption_algorithm ='AES_128'  
                    ,@encryptor_type= 'Certificate'  
                    ,@encryptor_name='MyBackupCert';  
    GO  
  
    ```  
  
     O [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] agora está habilitado na instância.  
  
6.  Verifique os parâmetros de configuração executando a seguinte instrução Transact-SQL:  
  
    ```  
    Use msdb;  
    GO  
    SELECT * FROM smart_admin.fn_backup_instance_config ();  
  
    ```  
  
7.  Criar um novo banco de dados na instância Execute a seguinte instrução Transact-SQL para exibir os parâmetros de configuração do [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para o banco de dados:  
  
    ```  
    Use msdb  
    GO  
    SELECT * FROM smart_admin.fn_backup_db_config('NewDB')  
    ```  
  
     Podem ser necessários até 15 minutos para que configurações apareçam e as operações de backup no banco de dados comecem a ser executadas.  
  
8.  **Habilitar e configurar a notificação do status de integridade:** [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] tem um procedimento armazenado que cria um trabalho de agente para enviar notificações por email sobre erros ou avisos que possam exigir atenção.  Para receber essas notificações, você deve habilitar a execução do procedimento armazenado que cria um Trabalho do SQL Server Agent. As etapas a seguir descrevem o processo para habilitar e configurar notificações por email:  
  
    1.  Configure o Database Mail se ele ainda não estiver habilitado na instância. Para obter mais informações, consulte [Configure Database Mail](../database-mail/configure-database-mail.md).  
  
    2.  Configure o SQL Server Agent Notification para usar o Database Mail. Para obter mais informações, consulte [Configurar o SQL Server Agent Mail para usar o Database Mail](../database-mail/configure-sql-server-agent-mail-to-use-database-mail.md).  
  
    3.  **Habilitar notificações por email para receber avisos e erros de backup:** Na janela de consulta, execute as seguintes instruções Transact-SQL:  
  
        ```  
        EXEC msdb.smart_admin.sp_set_parameter  
        @parameter_name = 'SSMBackup2WANotificationEmailIds',  
        @parameter_value = '<email address>'  
  
        ```  
  
         Para obter mais informações sobre como monitorar o e um script de exemplo completo, consulte [monitorar SQL Server Backup gerenciado para Microsoft Azure](sql-server-managed-backup-to-microsoft-azure.md).  
  
9. **Exibir arquivos de backup na Conta de Armazenamento do Microsoft Azure:** Conecte-se à conta de armazenamento do SQL Server Management Studio ou do Portal de Gerenciamento do Azure. Você verá um contêiner para a instância do SQL Server que hospeda o banco de dados que configurou para usar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. Você também poderá consultar um banco de dados e um backup de log 15 minutos depois de criar um novo banco de dados.  
  
10. **Monitorar o Status de Integridade:**  Realize o monitoramento por meio das notificações por email configuradas anteriormente ou monitore de forma ativa os eventos registrados em log. Estes são alguns exemplos de instruções Transact-SQL usados para exibir os eventos:  
  
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
  
    EXEC smart_admin.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek  
  
    SELECT * from @eventresult  
    WHERE event_type LIKE '%admin%'  
  
    ```  
  
    ```  
    --  to enable debug events  
    Use msdb;  
    Go  
             EXEC smart_admin.sp_set_parameter 'FileRetentionDebugXevent', 'True'  
  
    ```  
  
    ```  
    --  View all events in the current week  
    Use msdb;  
    Go  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)   
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
  
    EXEC smart_admin.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek;  
  
    ```  
  
 As configurações padrão do [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] podem ser substituídas por um banco de dados específico através da definição das configurações no nível do banco de dados. Você também pode pausar e retomar o serviço do [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] temporariamente. Para obter mais informações, consulte [SQL Server Backup gerenciado para Microsoft Azure-configurações de armazenamento e retenção](../../database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md)  
  
  
