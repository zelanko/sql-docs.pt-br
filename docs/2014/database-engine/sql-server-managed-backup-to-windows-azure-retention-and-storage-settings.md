---
title: SQL Server Managed Backup to Windows Azure - Retention and Storage Settings | Microsoft Docs
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: c4aa26ea-5465-40cc-8b83-f50603cb9db1
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6f9f9db58c48e74a91ec85972befb206ed3fb07f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62773531"
---
# <a name="sql-server-managed-backup-to-windows-azure---retention-and-storage-settings"></a>Backup gerenciado do SQL Server no Windows Azure - Configurações de retenção e armazenamento
  Este tópico descreve as etapas básicas para configurar o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] de um banco de dados e para definir as configurações padrão da instância. O tópico também descreve as etapas necessárias para pausar e retomar os serviços de [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] para a instância.  
  
 Para obter uma explicação completa de configuração [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] ver [Configurando o SQL Server Managed Backup to Windows Azure](../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md) e [Configurando o SQL Server Managed Backup to Windows Azure para grupos de disponibilidade](../../2014/database-engine/setting-up-sql-server-managed-backup-to-windows-azure-for-availability-groups.md).  
  
 
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Não habilite o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] em bancos de dados que estejam usando planos de manutenção ou envio de logs. Para obter mais informações sobre a interoperabilidade e coexistência com outros recursos do SQL Server, consulte [SQL Server Managed Backup to Windows Azure: Interoperabilidade e coexistência](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-interoperability-and-coexistence.md)  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
  
-   O SQL Server Agent deve estar em execução.  
  
    > [!WARNING]  
    >  Se o SQL Server Agent estiver parado por um período de tempo e, em seguida, reinicializado, você poderá ver uma atividade de backup maior dependendo do período de tempo decorrido entre a parada e o início do SQL Agent, e poderá haver uma lista de pendências de backups de log aguardando para serem executados. Configure o SQL Server Agent para iniciar automaticamente na inicialização.  
  
-   Uma conta de armazenamento do Windows Azure e uma Credencial SQL que armazenam informações de autenticação para a conta de armazenamento devem ser criadas antes da configuração do [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]. Para obter mais informações, consulte [Introduction to Key Components and Concepts](../relational-databases/backup-restore/sql-server-backup-to-url.md#intorkeyconcepts) seção o **SQL Server Backup to URL** tópico, e [lição 2: Criar uma credencial do SQL Server](../../2014/tutorials/lesson-2-create-a-sql-server-credential.md).  
  
    > [!IMPORTANT]  
    >  O [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] cria os contêineres necessários para armazenar os backups. O nome do contêiner é criado usando o formato 'nome de instância do nome da máquina'. Para Grupos de Disponibilidade AlwaysOn, o contêiner é nomeado por meio do GUID do grupo de disponibilidade.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Para executar os procedimentos armazenados que habilitam [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)], é necessário ser um uma `System Administrator` ou membro na **db_backupoperator** função de banco de dados com **ALTER ANY CREDENTIAL** epermissões`EXECUTE` permissões de **sp_delete_backuphistory**, e `smart_admin.sp_backup_master_switch` procedimentos armazenados.  Os procedimentos armazenados e as funções usados para analisar as configurações existentes geralmente requerem permissões `Execute` no procedimento armazenado e `Select` na função, respectivamente.  
  

  
###  <a name="Considerations"></a> Considerações para habilitar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] para bancos de dados e instâncias  
 O [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] pode ser habilitado para bancos de dados individuais separadamente ou para a instância inteira. As opções dependem dos requisitos de recuperação dos bancos de dados na instância, exigências para gerenciar vários bancos de dados e instâncias, e usar estrategicamente o armazenamento do Windows Azure.  
  
#### <a name="enabling-includesssmartbackupincludesss-smartbackup-mdmd-at-the-database-level"></a>Habilitando o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] no nível do banco de dados  
 Se um banco de dados tiver requisitos específicos para backup e período de retenção (SLA de recuperação) que sejam diferentes dos requisitos de outros bancos de dados na instância, configure o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] no nível do banco de dados para esse banco de dados. As configurações no nível do banco de dados substituem os parâmetros de configuração no nível da instância. No entanto, ambas as opções podem ser usadas juntas na mesma instância. A seguir, é apresentada uma lista das vantagens e considerações ao habilitar o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] no nível do banco de dados.  
  
-   Mais granular: Definições de configuração separado para cada banco de dados. Pode oferecer suporte a diferentes períodos de retenção para bancos de dados individuais.  
  
-   Substitui as configurações no nível da instância para o banco de dados.  
  
-   Pode ser usado para reduzir os custos de armazenamento selecionando os bancos de dados individuais para fazer backup.  
  
-   Requer o gerenciamento de cada banco de dados  
  
#### <a name="enabling-includesssmartbackupincludesss-smartbackup-mdmd-at-the-instance-level-with-default-settings"></a>Habilitando o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] no nível da instância com configurações padrão  
 Use essa configuração se a maioria dos bancos de dados da instância tiver os mesmos requisitos para políticas de backup e de retenção ou se você quiser que novas instâncias do banco de dados sejam incluídas automaticamente no backup durante a criação. Alguns bancos de dados que são exceção à política ainda podem ser configurados individualmente. A seguir é apresentada uma lista de vantagens e de considerações ao habilitar o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] no nível da instância.  
  
-   Automação no nível da instância: Configurações comuns aplicadas automaticamente para novos bancos de dados adicionados depois.  
  
-   Os novos bancos de dados terão seu backup feito automaticamente logo depois de criados nas instâncias  
  
-   Pode ser se aplicado a bancos de dados que têm os mesmos requisitos de período de retenção.  
  
-   Você ainda pode configurar os bancos de dados individuais que requerem uma período de retenção, mesmo com o backup do [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] habilitado no nível da instância com as configurações padrão. Você também pode desabilitar o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] para bancos de dados se não quiser usar o armazenamento do Windows Azure para os backups.  
  
##  <a name="DatabaseConfigure"></a> Habilitar e configurar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] para um banco de dados  
 O procedimento armazenado `smart_admin.sp_set_db_backup` do sistema é usado para habilitar o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] para um banco de dados específico. Quando o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] for habilitado pela primeira vez no banco de dados, as informações a seguir deverão ser especificadas, além da habilitação de [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]:  
  
-   O nome do banco de dados.  
  
-   O período de retenção.  
  
-   Credencial SQL usada para autenticar a conta de armazenamento do Windows Azure.  
  
-   Especifique que não criptografar usando *@encryption_algorithm*  =  **NO_ENCRYPTION** ou especifique um algoritmo de criptografia com suporte. Para obter mais informações sobre criptografia, consulte [Backup Encryption](../relational-databases/backup-restore/backup-encryption.md).  
  
 O [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] para a configuração do nível de banco de dados só tem suporte com o Transact-SQL.  
  
 Após a habilitação do [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] para um banco de dados, essas informações serão mantidas. Se você estiver alterando a configuração, somente o nome do banco de dados e a configuração que você deseja alterar serão necessários; o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] retém os valores existentes para outros parâmetros quando não especificado.  
  
> [!IMPORTANT]  
>  Antes de configurar o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] em um banco de dados, talvez ele seja útil para a configuração existente, se houver. A etapa de revisão de parâmetros de configuração de um banco de dados será explicada posteriormente nesta seção.  
  
-   **Usando Transact-SQL:**  
  
     Se você estiver habilitando [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] pela primeira vez, os parâmetros necessários são: *@database_name* , *@credential_name* , *@encryption_algorithm* , *@enable_backup* O *@storage_url* parâmetro é opcional. Se você não fornecer um valor para o @storage_url parâmetro, o valor é derivado usando as informações de conta de armazenamento da credencial do SQL. Se você fornecer a URL de armazenamento, só deverá fornecer a URL da raiz da conta de armazenamento e fazer a correspondência das informações na Credencial SQL que você especificou.  
  
    1.  Conecte-se ao [!INCLUDE[ssDE](../includes/ssde-md.md)].  
  
    2.  Na barra Padrão, clique em **Nova Consulta**.  
  
    3.  Copie e cole o exemplo a seguir na janela de consulta e clique em `Execute`. Este exemplo habilita [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] para o banco de dados 'TestDB'. O período de retenção é definido como 30 dias. Este exemplo usa a opção de criptografia especificando o algoritmo de criptografia e as informações do criptografador.  
  
    ```  
    Use msdb;  
    GO  
    EXEC smart_admin.sp_set_db_backup   
                    @database_name='TestDB'   
                    ,@enable_backup=1  
                    ,@retention_days =30   
                    ,@credential_name ='MyCredential'  
                    ,@encryption_algorithm ='AES_256'  
                    ,@encryptor_type= 'Certificate'  
                    ,@encryptor_name='MyBackupCert'  
    GO  
  
    ```  
  
    > [!IMPORTANT]  
    >  O período de retenção pode ser definido para qualquer valor de 1 a 30 dias.  
    >   
    >  Para obter mais informações sobre como criar um certificado para criptografia, consulte a etapa Criar um certificado de backup em [Create an Encrypted Backup](../relational-databases/backup-restore/create-an-encrypted-backup.md).  
  
     Para obter mais informações sobre esse procedimento armazenado, consulte [smart_admin.set_db_backup &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/dn451013(v=sql.120).aspx)  
  
     Para examinar os parâmetros de configuração de um banco de dados, use a seguinte consulta:  
  
    ```  
    Use msdb  
    GO  
    SELECT * FROM smart_admin.fn_backup_db_config('TestDB')  
    ```  
  
##  <a name="InstanceConfigure"></a> Habilitar e configurar o padrão [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] as configurações da instância  
 Você pode habilitar e configurar o padrão [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] configurações no nível da instância de duas maneiras:  Usando o sistema de procedimento armazenado `smart_backup.set_instance_backup` ou **SQL Server Management Studio**. Os dois métodos são explicados abaixo:  
  
 **smart_backup.set_instance_backup:** . Especificando o valor **1** para *@enable_backup* parâmetro, você pode habilitar o backup e definir as configurações padrão. Após a aplicação no nível de instância, essas configurações padrão serão aplicadas a qualquer novo banco de dados adicionado a essa instância.  Quando o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] for habilitado pela primeira vez, as informações a seguir deverão ser fornecidas, além da habilitação de [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] na instância:  
  
-   O período de retenção.  
  
-   Credencial SQL usada para autenticar a conta de armazenamento do Windows Azure.  
  
-   A opção de criptografia. Especifique que não criptografar usando *@encryption_algorithm*  =  **NO_ENCRYPTION** ou especifique um algoritmo de criptografia com suporte. Para obter mais informações sobre criptografia, consulte [Backup Encryption](../relational-databases/backup-restore/backup-encryption.md).  
  
 Depois de habilitadas, essas configurações serão mantidas. Se você estiver alterando a configuração, somente o nome do banco de dados e a configuração que você deseja alterar serão necessários. O [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] retém os valores existentes quando não especificado.  
  
> [!IMPORTANT]  
>  Antes de configurar o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] em uma instância, talvez seja útil verificar a configuração existente, se houver. A etapa de revisão de parâmetros de configuração de um banco de dados será explicada posteriormente nesta seção.  
  
 **SQL Server Management Studio:** Para fazer essa tarefa no SQL Server Management Studio, vá até o Pesquisador de objetos, expanda o **Management** nó e o botão direito do mouse em **Backup gerenciado**. Selecione **Configurar**. Essa ação abre a caixa de diálogo **Backup Gerenciado** . Use essa caixa de diálogo para especificar o período de retenção, a Credencial do SQL, a URL de Armazenamento e as configurações de criptografia. Para obter ajuda específica com esta caixa de diálogo, consulte [configurar o Backup gerenciado &#40;SQL Server Management Studio&#41;](configure-managed-backup-sql-server-management-studio.md).  
  
#### <a name="using-transact-sql"></a>Usando Transact-SQL  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em `Execute`.  
  
```  
Use msdb;  
Go  
   EXEC smart_admin.sp_set_instance_backup  
                @retention_days=30   
                ,@credential_name='sqlbackuptoURL'  
                ,@encryption_algorithm ='AES_128'  
                ,@encryptor_type= 'Certificate'  
                ,@encryptor_name='MyBackupCert'  
                ,@enable_backup=1;  
GO  
  
```  
  
> [!IMPORTANT]  
>  O período de retenção pode ser definido para qualquer valor de 1 a 30 dias.  
>   
>  Para obter mais informações sobre como criar um certificado para criptografia, consulte a etapa Criar um certificado de backup em [Create an Encrypted Backup](../relational-databases/backup-restore/create-an-encrypted-backup.md).  
  
 Para exibir os parâmetros de configuração padrão para a instância, use a seguinte consulta:  
  
```  
Use msdb;  
GO  
SELECT * FROM smart_admin.fn_backup_instance_config ();  
  
```  
  
#### <a name="using-powershell"></a>Usando o PowerShell  
  
1.  Iniciar uma instância do PowerShell  
  
2.  Executar o script a seguir depois de modificá-lo de acordo com suas configurações  
  
    ```  
    C:\ PS> cd SQLSERVER:\SQL\Computer\MyInstance   
    $encryptionOption = New-SqlBackupEncryptionOption -EncryptionAlgorithm Aes128 -EncryptorType ServerCertificate -EncryptorName "MyBackupCert"  
    Get-SqlSmartAdmin | Set-SqlSmartAdmin -BackupEnabled $True -BackupRetentionPeriodInDays 10 -EncryptionOption $encryptionOption  
    ```  
  
> [!IMPORTANT]  
>  Quando você cria um novo banco de dados depois de definir as configurações padrão, podem demorar até 15 minutos para que o banco de dados seja definido com as configurações padrão. Isso também se aplica a bancos de dados que são alterados de **Simple** para **Full** ou o modelo de recuperação **Bulk-Logged** .  
  
##  <a name="DatabaseDisable"></a> Desabilitar o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] para um banco de dados  
 Você pode desabilitar as configurações do [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] usando o procedimento armazenado `sp_set_db_backup` do sistema. O *@enableparameter* é usado para habilitar e desabilitar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] configurações para um banco de dados específico, onde 1 habilita e 0 desabilita os parâmetros de configuração.  
  
#### <a name="to-disable-includesssmartbackupincludesss-smartbackup-mdmd-for-a-specific-database"></a>Para desabilitar o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] para um banco de dados específico:  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em `Execute`.  
  
```  
Use msdb;  
Go  
EXEC smart_admin.sp_set_db_backup   
                @database_name='TestDB'   
                ,@enable_backup=0;  
GO  
  
```  
  
##  <a name="DatabaseAllDisable"></a> Desabilitar o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] para todos os bancos de dados na instância  
 O procedimento a seguir deverá ser usado quando você quiser desabilitar parâmetros de configuração do [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] de todos os bancos de dados que atualmente têm o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] habilitado na instância.  Os parâmetros de configuração, como a URL de armazenamento, retenção e a Credencial do SQL permanecerão nos metadados e poderão ser usados se o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] for habilitado para o banco de dados posteriormente. Se você quiser apenas pausar os serviços do [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] temporariamente, poderá usar a opção mestra explicada nas seções a seguir mais adiante neste tópico.  
  
#### <a name="to-disable-includesssmartbackupincludesss-smartbackup-mdmdfor-all-the-databases"></a>Para desabilitar o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]para todos os bancos de dados:  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em `Execute`. O exemplo a seguir identifica se o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] está configurado no nível da instância e em todos os bancos de dados habilitados do [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] na instância, e executa o procedimento armazenado `sp_set_db_backup` do sistema para desabilitar o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)].  
  
```  
-- Create a working table to store the database names  
Declare @DBNames TABLE  
  
       (  
             RowID int IDENTITY PRIMARY KEY  
             ,DBName varchar(500)  
  
       )  
-- Define the variables  
DECLARE @rowid int  
DECLARE @dbname varchar(500)  
DECLARE @SQL varchar(2000)  
-- Get the database names from the system function  
  
INSERT INTO @DBNames (DBName)  
  
SELECT db_name  
       FROM   
  
       smart_admin.fn_backup_db_config (NULL)  
       WHERE is_smart_backup_enabled = 1  
  
       --Select DBName from @DBNames  
  
       select @rowid = min(RowID)  
       FROM @DBNames  
  
       WHILE @rowID IS NOT NULL  
       Begin  
  
             Set @dbname = (Select DBName From @DBNames Where RowID = @rowid)  
             Begin  
             Set @SQL = 'EXEC smart_admin.sp_set_db_backup    
                @database_name= '''+'' + @dbname+ ''+''',   
                @enable_backup=0'  
  
            EXECUTE (@SQL)  
  
             END  
             Select @rowid = min(RowID)  
             From @DBNames Where RowID > @rowid  
  
       END  
  
```  
  
 Para examinar os parâmetros de configuração de todos os bancos de dados da instância, use a seguinte consulta:  
  
```  
Use msdb;  
GO  
SELECT * FROM smart_admin.fn_backup_db_config (NULL);  
GO  
  
```  
  
##  <a name="InstanceDisable"></a> Habilitar as configurações padrão do [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] para a instância  
 As configurações padrão no nível da instância se aplicam a todos os novos bancos de dados criados nessa instância.  Se não precisar mais das configurações padrão ou estas não forem mais exigidas, você poderá desabilitar essa configuração usando o procedimento armazenado **smart_admin.sp_set_instance_backup** do sistema. A desabilitação não remove os outros parâmetros de configuração como a URL de armazenamento, a configuração de retenção ou o nome da Credencial do SQL. Essas configurações serão usadas se o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] estiver habilitado para a instância mais tarde.  
  
#### <a name="to-disable-includesssmartbackupincludesss-smartbackup-mdmd-default-configuration-settings"></a>Para desabilitar os parâmetros de configuração padrão do [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] :  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em `Execute`.  
  
    ```  
    Use msdb;  
    Go  
    EXEC smart_admin.sp_set_instance_backup  
                    @enable_backup=0;  
    GO  
  
    ```  
  
#### <a name="using-powershell"></a>Usando o PowerShell  
  
1.  Iniciar uma instância do PowerShell  
  
2.  Execute o seguinte script:  
  
    ```  
    C:\ PS> cd SQLSERVER:\SQL\Computer\MyInstance   
    Set-SqlSmartAdmin -BackupEnabled $False  
    ```  
  
##  <a name="InstancePause"></a> Pause o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] no nível da instância  
 Pode haver momentos em que você precise pausar temporariamente os serviços do [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] por um curto período de tempo.  O procedimento armazenado `smart_admin.sp_backup_master_switch` do sistema permite que você desabilite o serviço do [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] no nível da instância.  O mesmo procedimento armazenado é usado para retomar o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]. O parâmetro @state é usado para definir se o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] deve ser desativado ou ativado.  
  
#### <a name="to-pause-includesssmartbackupincludesss-smartbackup-mdmd-services-using-transact-sql"></a>Para pausar os serviços do [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] usando o Transact-SQL:  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e, em seguida, clique em `Execute`  
  
```  
Use msdb;  
GO  
EXEC smart_admin.sp_backup_master_switch @new_state=0;  
Go  
  
```  
  
#### <a name="to-pause-includesssmartbackupincludesss-smartbackup-mdmd-using-powershell"></a>Para pausar o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] usando PowerShell  
  
1.  Iniciar uma instância do PowerShell  
  
2.  Executar o script a seguir depois de modificá-lo de acordo com suas configurações  
  
    ```  
    C:\ PS> cd SQLSERVER:\SQL\Computer\MyInstance   
    Get-SqlSmartAdmin | Set-SqlSmartAdmin -MasterSwitch $False  
    ```  
  
#### <a name="to-resume-includesssmartbackupincludesss-smartbackup-mdmd-using-transact-sql"></a>Para retomar o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] usando Transact-SQL  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e, em seguida, clique em `Execute`.  
  
```  
Use msdb;  
Go  
EXEC smart_admin. sp_backup_master_switch @new_state=1;  
GO  
  
```  
  
#### <a name="to-resume-includesssmartbackupincludesss-smartbackup-mdmd-using-powershell"></a>Para retomar o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] usando PowerShell  
  
1.  Iniciar uma instância do PowerShell  
  
2.  Executar o script a seguir depois de modificá-lo de acordo com suas configurações  
  
    ```  
    C:\ PS> cd SQLSERVER:\SQL\Computer\MyInstance   
    Get-SqlSmartAdmin | Set-SqlSmartAdmin -MasterSwitch $True  
    ```  
  
  
