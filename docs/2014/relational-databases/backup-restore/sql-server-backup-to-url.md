---
title: Backup para URL do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 01/25/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 11be89e9-ff2a-4a94-ab5d-27d8edf9167d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d3911ab34a01b2da971aa602df37c8c559ed6390
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62920740"
---
# <a name="sql-server-backup-to-url"></a>Backup do SQL Server para URL
  Este tópico apresenta os conceitos, os requisitos e os componentes necessários para usar o serviço de armazenamento de Blob do Windows Azure como um destino de backup. A funcionalidade de backup e restauração tem o mesmo efeito de DISK ou TAPE, com algumas diferenças. As diferenças, todas as exceções notáveis e alguns exemplos de código são incluídos neste tópico.  
  
## <a name="requirements-components-and-concepts"></a>Requisitos, componentes e conceitos  
 **Nesta seção:**  
  
-   [Segurança](#security)  
  
-   [Introdução aos principais componentes e conceitos](#intorkeyconcepts)  
  
-   [Serviço de armazenamento de BLOBs do Azure do Windows](#Blob)  
  
-   [Componentes do SQL Server](#sqlserver)  
  
-   [Limitações](#limitations)  
  
-   [Suporte a instruções de backup/restauração](#Support)  
  
-   [Usando a tarefa de backup no SQL Server Management Studio](sql-server-backup-to-url.md#BackupTaskSSMS)  
  
-   [Backup do SQL Server para a URL usando o Assistente de Plano de Manutenção](sql-server-backup-to-url.md#MaintenanceWiz)  
  
-   [Restaurando a partir do armazenamento do Windows Azure por meio do SQL Server Management Studio](sql-server-backup-to-url.md#RestoreSSMS)  
  
###  <a name="security"></a> Segurança  
 Estes são os requisitos e as considerações de segurança para backup e restauração dos serviços de armazenamento de Blob do Windows Azure.  
  
-   Ao criar um contêiner para o serviço de armazenamento de Blob do Windows Azure, recomendamos que você defina o acesso como **privado**. A definição do acesso como privado restringe o acesso a usuários ou contas capazes de fornecer as informações necessárias para realizar a autenticação na conta do Windows Azure.  
  
    > [!IMPORTANT]  
    >  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requer que a autenticação da chave de acesso e do nome da conta do Windows Azure seja armazenada em uma credencial do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essas informações são usadas para realizar a autenticação na conta do Windows Azure quando ele executa as operações de backup ou restauração.  
  
-   A conta de usuário usada para emitir os comandos BACKUP ou RESTORE deve estar na função de banco de dados **operador db_backup** com as permissões **Alterar qualquer credencial** .  
  
###  <a name="intorkeyconcepts"></a> Introdução aos principais componentes e conceitos  
 As duas seções a seguir apresentam o serviço de armazenamento de Blob do Windows Azure, e os componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usados durante o backup ou a restauração do serviço de armazenamento de Blob do Windows Azure. É importante entender os componentes e a interação entre eles para fazer um backup ou uma restauração no serviço de armazenamento de Blob do Windows Azure.  
  
 A criação de uma conta do Windows Azure é a primeira etapa desse processo. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa o **nome de conta de armazenamento do Windows Azure** e seu **chave de acesso** valores para se autenticar, gravar e ler blobs no serviço de armazenamento. A credencial do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] armazena essas informações de autenticação e é usada durante as operações de backup ou restauração. Para obter um passo a passo completo de como criar uma conta de armazenamento e executar uma restauração simples, consulte o [Tutorial sobre uso do serviço de armazenamento do Microsoft Azure para backup e restauração do SQL Server](https://go.microsoft.com/fwlink/?LinkId=271615).  
  
 ![mapeamento de conta de armazenamento para as credenciais do sql](../../tutorials/media/backuptocloud-storage-credential-mapping.gif "mapeando a conta de armazenamento para as credenciais do sql")  
  
###  <a name="Blob"></a> Serviço de armazenamento de BLOBs do Azure do Windows  
 **Conta de armazenamento:** A conta de armazenamento é o ponto de partida de todos os serviços de armazenamento. Para acessar o serviço de armazenamento de Blob do Windows Azure, primeiro crie uma conta de armazenamento do Windows Azure. O **storage account name** e as respectivas propriedades de **access key** são necessários para realizar a autenticação no serviço de armazenamento de Blob do Windows Azure e seus componentes.  
  
 **Contêiner:** Um contêiner fornece um agrupamento de um conjunto de Blobs e pode armazenar um número ilimitado de Blobs. Para gravar um backup do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no serviço de Blob do Windows Azure, você deve ter pelo menos o contêiner raiz criado.  
  
 **Blob:** Um arquivo de qualquer tipo e tamanho. Há dois tipos de blobs que podem ser armazenados no serviço de armazenamento de Blob do Windows Azure: blobs de bloco e de página. O backup do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa Blobs de página. BLOBs são endereçáveis usando o seguinte formato de URL: https://\<conta de armazenamento >.blob.core.windows.net/\<contêiner > /\<blob >  
  
 ![Armazenamento de Blobs do Azure](../../database-engine/media/backuptocloud-blobarchitecture.gif "Armazenamento de Blobs do Azure")  
  
 Para obter mais informações sobre o serviço de armazenamento de Blob do Windows Azure, consulte [Como usar o serviço de armazenamento de Blob do Windows Azure](http://www.windowsazure.com/develop/net/how-to-guides/blob-storage/)  
  
 Para obter mais informações sobre Blobs de página, consulte [Noções básicas sobre Blobs de bloco e de página](https://msdn.microsoft.com/library/windowsazure/ee691964.aspx)  
  
###  <a name="sqlserver"></a> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Componentes  
 **URL:** Uma URL especifica um URI (Uniform Resource Identifier) para um arquivo de backup exclusivo. A URL é usada para fornecer o local e o nome do arquivo de backup do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Nessa implementação, a única URL válida é a que aponta para um Blob de página em uma conta de armazenamento do Windows Azure. A URL deve apontar para um Blob real, e não apenas para um contêiner. Se o Blob não existir, ele será criado. Se um Blob existente for especificado, o BACKUP falhará, a menos que a opção "WITH FORMAT" é especificada.  
  
> [!WARNING]  
>  Se você optar por copiar e carregar um arquivo de backup para o serviço de armazenamento de Blob do Windows Azure, use o blob de página como opção de armazenamento. Não há suporte para restaurações de Blobs de bloco. A RESTAURAÇÃO de um blob de bloco falhará.  
  
 Este é um valor de URL de exemplo: http[s]://ACCOUNTNAME.Blob.Core.Windows.NET/\<CONTÊINER > /\<nomedoarquivo. bak >. O HTTPS não é obrigatório, mas é recomendado.  
  
 **Credencial:** Uma credencial do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é um objeto usado para armazenar as informações de autenticação necessárias para se conectar a um recurso fora do SQL Server.  Aqui, os processos de backup e restauração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usam a credencial para autenticação no serviço de armazenamento de Blob do Windows Azure. A Credencial armazena o nome da conta de armazenamento e os valores de **access key** da conta de armazenamento. Depois que a credencial for criada, ela deverá ser especificada na opção WITH CREDENTIAL ao emitir instruções BACKUP/RESTORE. Para obter mais informações sobre como exibir, copiar ou gerar novamente as **access keys**da conta de armazenamento, consulte [Chaves de acesso da conta de armazenamento](https://msdn.microsoft.com/library/windowsazure/hh531566.aspx).  
  
 Para obter instruções passo a passo sobre como criar uma credencial do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , consulte o exemplo [Create a Credential](#credential) mais adiante neste tópico.  
  
 Para obter informações gerais sobre credenciais, consulte [Credenciais](../security/authentication-access/credentials-database-engine.md)  
  
 Para obter informações sobre outros exemplos em que as credenciais são usadas, consulte [Criar um proxy do SQL Server Agent](../../ssms/agent/create-a-sql-server-agent-proxy.md).  
  
###  <a name="limitations"></a> Limitações  
  
-   Não há suporte para backup em armazenamento premium.  
  
-   O tamanho máximo de backup com suporte é 1 TB.  
  
-   Você pode emitir instruções de backup ou restauração usando cmdlets do TSQL, SMO ou PowerShell. Um backup ou uma restauração no serviço de armazenamento de Blob do Windows Azure usando o assistente de backup ou restauração do SQL Server Management Studio não estão habilitados no momento.  
  
-   Não há suporte para a criação de um nome de dispositivo lógico. Portanto, não há suporte para a adição de uma URL como dispositivo de backup por meio de sp_dumpdevice ou do SQL Server Management Studio.  
  
-   Não há suporte para a anexação de blobs de backup. Os backups em um Blob existente só podem ser substituídos através da opção WITH FORMAT.  
  
-   Não há suporte para backup em vários blobs em uma única operação de backup. O exemplo a seguir retornará um erro:  
  
    ```  
    BACKUP DATABASE AdventureWorks2012   
    TO URL = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012_1.bak'   
       URL = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012_2.bak'   
          WITH CREDENTIAL = 'mycredential'   
         ,STATS = 5;  
    GO  
  
    ```  
  
-   Não há suporte para a especificação de um tamanho de bloco com `BACKUP`.  
  
-   Não há suporte para a especificação de `MAXTRANSFERSIZE`.  
  
-   Não há suporte para a especificação das opções de conjunto de backup - `RETAINDAYS` e `EXPIREDATE`.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tem um limite máximo de 259 caracteres em um nome de dispositivo de backup. O BACKUP TO URL consome 36 caracteres para os elementos necessários usados para especificar a URL – 'https://.blob.core.windows.net//.bak ', deixando 223 caracteres para os nomes da conta, do contêiner e do blob juntos.  
  
###  <a name="Support"></a> Suporte a instruções de backup/restauração  
  
|||||  
|-|-|-|-|  
|Instrução de backup/restauração|Tem suporte|Exceções|Comentários|  
|BACKUP|???|Não há suporte para BLOCKSIZE e MAXTRANSFERSIZE.|Requer a especificação de WITH CREDENTIAL|  
|RESTORE|???||Requer a especificação de WITH CREDENTIAL|  
|RESTORE FILELISTONLY|???||Requer a especificação de WITH CREDENTIAL|  
|RESTORE HEADERONLY|???||Requer a especificação de WITH CREDENTIAL|  
|RESTORE LABELONLY|???||Requer a especificação de WITH CREDENTIAL|  
|RESTORE VERIFYONLY|???||Requer a especificação de WITH CREDENTIAL|  
|RESTORE REWINDONLY|???|||  
  
 Para obter a sintaxe e informações gerais sobre as instruções de backup, consulte [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql).  
  
 Para obter a sintaxe e informações gerais sobre as instruções de restauração, consulte [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql).  
  
### <a name="support-for-backup-arguments"></a>Suporte para argumentos de backup  
  
|||||  
|-|-|-|-|  
|Argumento|Tem suporte|Exceção|Comentários|  
|DATABASE|???|||  
|LOG|???|||  
||  
|TO (URL)|???|Diferente de DISK e TAPE, a URL não oferece suporte para a especificação ou criação de um nome lógico.|Esse argumento é usado para especificar o caminho da URL para o arquivo de backup.|  
|MIRROR TO|???|||  
|**Opções WITH:**||||  
|CREDENTIAL|???||Há suporte para WITH CREDENTIAL somente quando a opção BACKUP TO URL é usada para fazer backup no serviço de armazenamento de Blob do Windows Azure.|  
|DIFFERENTIAL|???|||  
|COPY_ONLY|???|||  
|COMPRESSION&#124;NO_COMPRESSION|???|||  
|DESCRIPTION|???|||  
|NAME|???|||  
|EXPIREDATE &#124; RETAINDAYS|???|||  
|NOINIT &#124; INIT|???||Esta opção será ignorada se for usada.<br /><br /> Não é possível anexar aos blobs. Para substituir um backup, use o argumento FORMAT.|  
|NOSKIP &#124; SKIP|???|||  
|NOFORMAT &#124; FORMAT|???||Esta opção será ignorada se for usada.<br /><br /> Um backup feito em um blob existente falhará, a menos que WITH FORMAT seja especificado. O blob existente será substituído quando WITH FORMAT for especificado.|  
|MEDIADESCRIPTION|???|||  
|MEDIANAME|???|||  
|BLOCKSIZE|???|||  
|BUFFERCOUNT|???|||  
|MAXTRANSFERSIZE|???|||  
|NO_CHECKSUM &#124; CHECKSUM|???|||  
|STOP_ON_ERROR &#124; CONTINUE_AFTER_ERROR|???|||  
|STATS|???|||  
|REWIND &#124; NOREWIND|???|||  
|UNLOAD &#124; NOUNLOAD|???|||  
|NORECOVERY &#124; STANDBY|???|||  
|NO_TRUNCATE|???|||  
  
 Para obter mais informações sobre os argumentos de backup, consulte [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql).  
  
### <a name="support-for-restore-arguments"></a>Suporte para argumentos de restauração  
  
|||||  
|-|-|-|-|  
|Argumento|Tem suporte|Exceções|Comentários|  
|DATABASE|???|||  
|LOG|???|||  
|FROM (URL)|???||O argumento FROM URL é usado para especificar o caminho da URL do arquivo de backup.|  
|**WITH Options:**||||  
|CREDENTIAL|???||Há suporte para WITH CREDENTIAL somente quando a opção RESTORE FROM URL é usada para realizar a restauração no serviço de armazenamento de Blob do Windows Azure.|  
|PARTIAL|???|||  
|RECOVERY &#124; NORECOVERY &#124; STANDBY|???|||  
|LOADHISTORY|???|||  
|MOVE|???|||  
|REPLACE|???|||  
|RESTART|???|||  
|RESTRICTED_USER|???|||  
|FILE|???|||  
|PASSWORD|???|||  
|MEDIANAME|???|||  
|MEDIAPASSWORD|???|||  
|BLOCKSIZE|???|||  
|BUFFERCOUNT|???|||  
|MAXTRANSFERSIZE|???|||  
|CHECKSUM &#124; NO_CHECKSUM|???|||  
|STOP_ON_ERROR &#124; CONTINUE_AFTER_ERROR|???|||  
|FILESTREAM|???|||  
|STATS|???|||  
|REWIND &#124; NOREWIND|???|||  
|UNLOAD &#124; NOUNLOAD|???|||  
|KEEP_REPLICATION|???|||  
|KEEP_CDC|???|||  
|ENABLE_BROKER &#124; ERROR_BROKER_CONVERSATIONS &#124; NEW_BROKER|???|||  
|STOPAT &#124; STOPATMARK &#124; STOPBEFOREMARK|???|||  
  
 Para obter mais informações sobre os argumentos de restauração, consulte [Argumentos de RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-arguments-transact-sql).  
  
##  <a name="BackupTaskSSMS"></a> Usando a tarefa de Backup no SQL Server Management Studio  
 A tarefa Backup no SQL Server Management Studio foi aprimorada para incluir a URL como uma das opções de destino, e outros objetos de suporte necessários para fazer backup no armazenamento do Windows Azure, como a Credencial SQL.  
  
 As etapas a seguir descrevem as alterações feitas na tarefa Backup de Banco de Dados para favorecer o backup no armazenamento do Windows Azure:  
  
1.  Inicie o SQL Server Management Studio e conecte-se à instância do SQL Server.  Selecione um banco de dados que você deseja fazer backup e clique com botão direito **tarefas**e selecione **fazer backup...** . Isso abre a caixa de diálogo de backup do banco de dados.  
  
2.  Na página Geral, a opção **URL** é usada para criar um backup no armazenamento do Windows Azure. Quando você selecionar essa opção, verá outras opções habilitadas na página:  
  
    1.  **Nome de Arquivo:** Nome do arquivo de backup.  
  
    2.  **Credencial do SQL:** Você pode especificar uma credencial do SQL Server existente ou pode criar um novo clicando na **criar** ao lado da caixa credencial SQL.  
  
        > [!IMPORTANT]  
        >  A caixa de diálogo que é aberta quando você clica em **Criar** exige um certificado de gerenciamento ou o perfil da publicação para a assinatura. No momento, o SQL Server oferece suporte à versão do perfil de publicação 2.0. Para baixar a versão com suporte do perfil de publicação, consulte [Download do perfil de publicação 2.0](https://go.microsoft.com/fwlink/?LinkId=396421).  
        >   
        >  Se você não tiver acesso ao certificado de gerenciamento ou perfil de publicação, poderá criar uma credencial de SQL especificando o nome da conta de armazenamento e as informações da chave de acesso usando Transact-SQL ou SQL Server Management Studio. Consulte o código de exemplo na seção [Criar uma credencial](#credential) para criar uma credencial usando Transact-SQL. Como alternativa, usando o SQL Server Management Studio, na instância do mecanismo de banco de dados, clique com o botão direito do mouse em **Segurança**, selecione **Novo**e **Credencial**. Especifique o nome da conta de armazenamento para **Identidade** e a chave de acesso no campo **Senha** .  
  
    3.  **Contêiner de armazenamento do Azure:** O nome do contêiner de armazenamento do Windows Azure para armazenar os arquivos de backup.  
  
    4.  **Prefixo da URL:** Isso é criado automaticamente usando as informações especificadas nos campos descritos nas etapas anteriores. Se você editar esse valor manualmente, verifique se ele corresponde às outras informações fornecidas anteriormente. Por exemplo, se você modificar a URL de armazenamento, verifique se a Credencial SQL será definida para ser autenticada na mesma conta de armazenamento.  
  
 Quando você selecionar a URL como destino, determinadas opções na página **Opções de Mídia** serão desabilitadas.  Os tópicos a seguir têm mais informações na caixa de diálogo Backup de Banco de Dados:  
  
 [Fazer backup do banco de dados &#40;página Geral&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)  
  
 [Fazer backup do banco de dados &#40;página Opções de Mídia&#41;](back-up-database-media-options-page.md)  
  
 [Fazer backup do banco de dados &#40;página Opções de Backup&#41;](back-up-database-backup-options-page.md)  
  
 [Criar credencial - autenticar no Armazenamento do Azure](create-credential-authenticate-to-azure-storage.md)  
  
##  <a name="MaintenanceWiz"></a> Backup do SQL Server para a URL usando o Assistente de Plano de Manutenção  
 Assim como a tarefa de backup descrita anteriormente, o Assistente de Plano de Manutenção no SQL Server Management Studio foi aprimorado para incluir a **URL** como uma das opções de destino, e outros objetos de suporte necessários ao backup no armazenamento do Windows Azure, como a Credencial SQL. Para obter mais informações, consulte a seção **Definir tarefas de Backup** em [Using Maintenance Plan Wizard](../maintenance-plans/use-the-maintenance-plan-wizard.md#SSMSProcedure).  
  
##  <a name="RestoreSSMS"></a> Restauração do armazenamento do Windows Azure usando o SQL Server Management Studio  
 Se você estiver restaurando um banco de dados, a **URL** será incluída como o dispositivo a partir do qual a restauração será realizada. As etapas a seguir descrevem as alterações na tarefa Restaurar para permitir a restauração a partir do armazenamento do Windows Azure:  
  
1.  Quando você seleciona **Dispositivos** na página **Geral** da tarefa Restaurar no SQL Server Management Studio, a caixa de diálogo **Selecione dispositivos de backup** , que inclui **URL** como um tipo de mídia de backup, é exibida.  
  
2.  Quando você seleciona **URL** e clica em **Adicionar**, a caixa de diálogo **Conectar-se ao armazenamento do Windows Azure** é aberta. Especifique as informações da Credencial SQL para fazer a autenticação no armazenamento do Windows Azure.  
  
3.  Em seguida, o SQL Server se conecta ao armazenamento do Windows Azure usando as informações da Credencial SQL e abre a caixa de diálogo **Localizar Arquivo de Backup no Windows Azure** . Os arquivos de backup que residem no armazenamento são exibidos nessa página. Selecione o arquivo que deseja usar para restaurar e clique em **OK**. Isso o levará de volta à caixa de diálogo **Selecione dispositivos de backup** . Se você clicar em **OK** nessa caixa de diálogo, será levado de volta à caixa de diálogo **Restaurar** , na qual poderá concluir a restauração.  Para obter mais informações, consulte os seguintes tópicos:  
  
     [Restaurar banco de dados &#40;página Geral&#41;](restore-database-general-page.md)  
  
     [Restaurar banco de dados &#40;página Arquivos&#41;](restore-database-files-page.md)  
  
     [Restaurar banco de dados &#40;página Opções&#41;](restore-database-options-page.md)  
  
##  <a name="Examples"></a> Exemplos de código  
 Esta seção contém os seguintes exemplos:  
  
-   [Criar uma credencial](#credential)  
  
-   [Fazendo backup de um banco de dados completo](#complete)  
  
-   [Fazendo backup do banco de dados e do log](#databaselog)  
  
-   [Criando um backup completo do arquivo do grupo de arquivos primário](#filebackup)  
  
-   [Criando um backup de arquivo diferencial dos grupos de arquivos primários](#differential)  
  
-   [Restaurando um banco de dados e movendo arquivos](#restoredbwithmove)  
  
-   [Restauração pontual usando STOPAT](#PITR)  
  
###  <a name="credential"></a> Criar uma credencial  
 O exemplo a seguir cria uma credencial que armazena as informações sobre autenticação do armazenamento do Windows Azure.  
  
1.  **Tsql**  
  
    ```  
    IF NOT EXISTS  
    (SELECT * FROM sys.credentials   
    WHERE credential_identity = 'mycredential')  
    CREATE CREDENTIAL mycredential WITH IDENTITY = 'mystorageaccount'  
    ,SECRET = '<storage access key>' ;  
  
    ```  
  
2.  **C#**  
  
    ```  
    // Connect to default sql server instance on local machine  
    Server server = new Server(".");  
    string identity = "mystorageaccount";  
    string secret = "<storage access key>";  
  
    // Create a Credential  
    string credentialName = "mycredential";  
    Credential credential = new Credential(server, credentialName);  
    credential.Create(identity, secret);  
    ```  
  
3.  **PowerShell**  
  
    ```  
    # create variables  
    $storageAccount = "mystorageaccount"  
    $storageKey = "<storage access key>"  
    $secureString = convertto-securestring $storageKey  -asplaintext -force  
    $credentialName = "mycredential"  
  
    $srvPath = "SQLSERVER:\SQL\COMPUTERNAME\INSTANCENAME"  
    # for default instance, the $srvpath variable would be "SQLSERVER:\SQL\COMPUTERNAME\DEFAULT"  
  
    # Create a credential  
     New-SqlCredential -Name $credentialName -Path $srvpath -Identity $storageAccount -Secret $secureString  
  
    ```  
  
###  <a name="complete"></a> Fazendo backup de um banco de dados completo  
 O exemplo a seguir faz backup do banco de dados AdventureWorks2012 no serviço do armazenamento de Blob do Windows Azure.  
  
1.  **Tsql**  
  
    ```  
    BACKUP DATABASE AdventureWorks2012   
    TO URL = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012.bak'   
          WITH CREDENTIAL = 'mycredential'   
         ,COMPRESSION  
         ,STATS = 5;  
    GO  
  
    ```  
  
1.  **C#**  
  
    ```  
    // Connect to default sql server instance on local machine  
    Server server = new Server(".");  
    string identity = "mystorageaccount";  
  
    string credentialName = "mycredential";  
    string dbName = "AdventureWorks2012";  
    string blobContainerName = "mycontainer";  
  
    // Generate Unique Url  
    string url = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}-{3}.bak",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
    // Backup to Url  
    Backup backup = new Backup();  
    backup.CredentialName = credentialName;  
    backup.Database = dbName;  
    backup.CompressionOption = BackupCompressionOptions.On;  
    backup.Devices.AddDevice(url, DeviceType.Url);  
    backup.SqlBackup(server);  
    ```  
  
2.  **PowerShell**  
  
    ```  
    # create variables  
    $backupUrlContainer = "https://mystorageaccount.blob.core.windows.net/mycontainer/"  
    $credentialName = "mycredential"  
    $srvPath = "SQLSERVER:\SQL\COMPUTERNAME\INSTANCENAME"   
    # for default instance, the $srvpath varilable would be "SQLSERVER:\SQL\COMPUTERNAME\DEFAULT"  
  
    # navigate to SQL Server Instance  
    CD $srvPath   
    $backupFile = $backupUrlContainer + "AdventureWorks2012" +  ".bak"  
    Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupFile  -SqlCredential $credentialName -CompressionOption On  
  
    ```  
  
###  <a name="databaselog"></a> Fazendo backup do banco de dados e log  
 O exemplo a seguir faz backup do banco de dados de exemplo AdventureWorks2012, que, por padrão, usa o modelo de recuperação simples. Para oferecer suporte a backups de log, o banco de dados AdventureWorks2012 é modificado para usar o modelo de recuperação completa. Em seguida, o exemplo cria um backup de banco de dados completo no Blob do Windows Azure e, após um período de atividades de atualização, faz o backup do log. Esse exemplo cria um nome de arquivo de backup com um carimbo de data/hora.  
  
1.  **Tsql**  
  
    ```  
    -- To permit log backups, before the full database backup, modify the database   
    -- to use the full recovery model.  
    USE master;  
    GO  
    ALTER DATABASE AdventureWorks2012  
       SET RECOVERY FULL;  
    GO  
  
    -- Back up the full AdventureWorks2012 database.  
           -- First create a file name for the backup file with DateTime stamp  
  
    DECLARE @Full_Filename AS VARCHAR (300);  
    SET @Full_Filename = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012_Full_'+   
    REPLACE (REPLACE (REPLACE (CONVERT (VARCHAR (40), GETDATE (), 120), '-','_'),':', '_'),' ', '_') + '.bak';   
    --Back up Adventureworks2012 database  
  
    BACKUP DATABASE AdventureWorks2012  
    TO URL =  @Full_Filename  
    WITH CREDENTIAL = 'mycredential';  
    ,COMPRESSION  
    GO  
    -- Back up the AdventureWorks2012 log.  
    DECLARE @Log_Filename AS VARCHAR (300);  
    SET @Log_Filename = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012_Log_'+   
    REPLACE (REPLACE (REPLACE (CONVERT (VARCHAR (40), GETDATE (), 120), '-','_'),':', '_'),' ', '_') + '.trn';  
    BACKUP LOG AdventureWorks2012  
     TO URL = @Log_Filename  
    WITH CREDENTIAL = 'mycredential'  
    ,COMPRESSION;  
    GO  
    ```  
  
2.  **C#**  
  
    ```  
    // Connect to default sql server instance on local machine  
    Server server = new Server(".");  
    string identity = "mystorageaccount";  
  
    string credentialName = "mycredential";  
    string dbName = "AdventureWorks2012";  
    string blobContainerName = "mycontainer";  
  
    // Generate Unique Url for data backup  
    string urlDataBackup = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}_Data-{3}.bak",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
    // Backup Database to Url  
    Backup backupData = new Backup();  
    backupData.CredentialName = credentialName;  
    backupData.Database = dbName;  
    backup.CompressionOption = BackupCompressionOptions.On;  
    backupData.Devices.AddDevice(urlDataBackup, DeviceType.Url);  
    backupData.SqlBackup(server);  
  
    // Generate Unique Url for data backup  
    string urlLogBackup = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}_Log-{3}.bak",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
    // Backup Database Log to Url  
    Backup backupLog = new Backup();  
    backupLog.CredentialName = credentialName;  
    backupLog.Database = dbName;  
    backup.CompressionOption = BackupCompressionOptions.On;  
    backupLog.Devices.AddDevice(urlLogBackup, DeviceType.Url);  
    backupLog.Action = BackupActionType.Log;  
    backupLog.SqlBackup(server);  
    ```  
  
3.  **PowerShell**  
  
    ```  
  
    #create variables  
    $backupUrlContainer = "https://mystorageaccount.blob.core.windows.net/mycontainer/"  
    $credentialName = "mycredential"  
    $srvPath = "SQLSERVER:\SQL\COMPUTERNAME\INSTANCENAME"  
    # for default instance, the $srvpath variable would be "SQLSERVER:\SQL\COMPUTERNAME\DEFAULT"  
  
    # navigate to theSQL Server Instance  
  
    CD $srvPath   
    #Create a unique file name for the full database backup  
    $backupFile = $backupUrlContainer + "AdventureWorks2012_" + (Get-Date).ToString("s").Replace("-","_").Replace(":", "_").Replace(" ","_").Replace("/", "_") +  ".bak"  
  
    #Backup Database to URL  
  
    Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupFile  -SqlCredential $credentialName -CompressionOption On -BackupAction Database    
  
    #Create a unique file name for log backup  
  
    $backupFile = $backupUrlContainer + "AdventureWorks2012_" + (Get-Date).ToString("s").Replace("-","_").Replace(":", "_").Replace(" ","_").Replace("/", "_") +  ".trn"  
  
    #Backup Log to URL  
  
    Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupFile  -SqlCredential $credentialName -CompressionOption On -BackupAction Log  
  
    ```  
  
###  <a name="filebackup"></a> Criando um backup completo do arquivo do grupo de arquivos primário  
 O exemplo a seguir cria um backup de arquivo completo do grupo de arquivos primário.  
  
1.  **Tsql**  
  
    ```  
    --Back up the files in Primary:  
    BACKUP DATABASE AdventureWorks2012  
       FILEGROUP = 'Primary'  
       TO URL = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012files.bck'  
       WITH CREDENTIAL = 'mycredential'  
       ,COMPRESSION;  
    GO  
    ```  
  
2.  **C#**  
  
    ```  
    // Connect to default sql server instance on local machine  
    Server server = new Server(".");  
    string identity = "mystorageaccount";  
  
    string credentialName = "mycredential";  
    string dbName = "AdventureWorks2012";  
    string blobContainerName = "mycontainer";  
  
    // Generate Unique Url  
    string url = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}-{3}.bck",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
    // Backup to Url  
    Backup backup = new Backup();  
    backup.CredentialName = credentialName;  
    backup.Database = dbName;  
    backup.Action = BackupActionType.Files;  
    backup.DatabaseFileGroups.Add("PRIMARY");  
    backup.CompressionOption = BackupCompressionOptions.On;  
    backup.Devices.AddDevice(url, DeviceType.Url);  
    backup.SqlBackup(server);  
  
    ```  
  
3.  **PowerShell**  
  
    ```  
  
    #create variables  
    $backupUrlContainer = "https://mystorageaccount.blob.core.windows.net/mycontainer/"  
    $credentialName = "mycredential"  
    $srvPath = "SQLSERVER:\SQL\COMPUTERNAME\INSTANCENAME"  
    # for default instance, the $srvpath variable would be "SQLSERVER:\SQL\COMPUTERNAME\DEFAULT"  
  
    # navigate to the SQL Server Instance  
  
    CD $srvPath   
    #Create a unique file name for the file backup  
    $backupFile = $backupUrlContainer + "AdventureWorks2012_" + (Get-Date).ToString("s").Replace("-","_").Replace(":", "_").Replace(" ","_").Replace("/", "_") +  ".bck"  
  
    #Backup Primary File Group to URL  
  
    Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupFile  -SqlCredential $credentialName -CompressionOption On -BackupAction Files -DatabaseFileGroup Primary  
  
    ```  
  
###  <a name="differential"></a> Criando um backup de arquivo diferencial do grupo de arquivos primário  
 O exemplo a seguir cria um backup de arquivo diferencial do grupo de arquivos primário.  
  
1.  **Tsql**  
  
    ```  
    --Back up the files in Primary:  
    BACKUP DATABASE AdventureWorks2012  
       FILEGROUP = 'Primary'  
       TO URL = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012filesdiff.bck'  
       WITH   
          CREDENTIAL = 'mycredential'  
          ,COMPRESSION  
      ,DIFFERENTIAL;  
    GO  
  
    ```  
  
2.  **C#**  
  
    ```  
    // Connect to default sql server instance on local machine  
    Server server = new Server(".");  
    string identity = "mystorageaccount";  
  
    string credentialName = "mycredential";  
    string dbName = "AdventureWorks2012";  
    string blobContainerName = "mycontainer";  
  
    // Generate Unique Url  
    string url = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}-{3}.bak",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
    // Backup to Url  
    Backup backup = new Backup();  
    backup.CredentialName = credentialName;  
    backup.Database = dbName;  
    backup.Action = BackupActionType.Files;  
    backup.DatabaseFileGroups.Add("PRIMARY");  
    backup.Incremental = true;  
    backup.CompressionOption = BackupCompressionOptions.On;  
    backup.Devices.AddDevice(url, DeviceType.Url);  
    backup.SqlBackup(server);  
  
    ```  
  
3.  **PowerShell**  
  
    ```  
  
    #create variables  
    $backupUrlContainer = "https://mystorageaccount.blob.core.windows.net/mycontainer/"  
    $credentialName = "mycredential"  
    $srvPath = "SQLSERVER:\SQL\COMUTERNAME\INSTANCENAME"  
    # for default instance, the $srvpath variable would be "SQLSERVER:\SQL\COMPUTERNAME\DEFAULT"  
  
    # navigate to SQL Server Instance  
  
    CD $srvPath   
  
    #create a unique file name for the full backup  
    $backupdbFile = $backupUrlContainer + "AdventureWorks2012_" + (Get-Date).ToString("s").Replace("-","_").Replace(":", "_").Replace(" ","_").Replace("/", "_") +  ".bak"  
  
    #Create a differential backup of the primary filegroup  
  
    Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupFile  -SqlCredential $credentialName -CompressionOption On -BackupAction Files -DatabaseFileGroup Primary -Incremental  
  
    ```  
  
###  <a name="restoredbwithmove"></a> Restaurar um banco de dados e mover arquivos  
 Para restaurar um backup de banco de dados completo e mover o banco de dados restaurado para o diretório C:\Arquivos de Programas\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Data, execute as etapas a seguir.  
  
1.  **Tsql**  
  
    ```  
    -- Backup the tail of the log first  
  
    DECLARE @Log_Filename AS VARCHAR (300);  
    SET @Log_Filename = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012_Log_'+   
    REPLACE (REPLACE (REPLACE (CONVERT (VARCHAR (40), GETDATE (), 120), '-','_'),':', '_'),' ', '_') + '.trn';  
    BACKUP LOG AdventureWorks2012  
     TO URL = @Log_Filename  
    WITH CREDENTIAL = 'mycredential'  
    ,NORECOVERY;  
    GO  
  
    RESTORE DATABASE AdventureWorks2012 FROM URL = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012.bak'  
    WITH CREDENTIAL = 'mycredential'  
    ,MOVE 'AdventureWorks2012_data' to 'C:\Program Files\Microsoft SQL Server\myinstance\MSSQL\DATA\AdventureWorks2012.mdf'  
    ,MOVE 'AdventureWorks2012_log' to 'C:\Program Files\Microsoft SQL Server\myinstance\MSSQL\DATA\AdventureWorks2012.ldf'  
    ,STATS = 5  
  
    ```  
  
2.  **C#**  
  
    ```  
    // Connect to default sql server instance on local machine  
    Server server = new Server(".");  
    string identity = "mystorageaccount";  
  
    string credentialName = "mycredential";  
    string dbName = "AdventureWorks2012";  
    string blobContainerName = "mycontainer";  
  
    // Generate Unique Url  
    string urlBackupData = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}-Data{3}.bak",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
    // Backup to Url  
    Backup backup = new Backup();  
    backup.CredentialName = credentialName;  
    backup.Database = dbName;  
    backup.Devices.AddDevice(urlBackupData, DeviceType.Url);  
    backup.SqlBackup(server);  
  
    // Generate Unique Url for tail log backup  
    string urlTailLogBackup = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}-TailLog{3}.bak",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
    // Backup Tail Log to Url  
    Backup backupTailLog = new Backup();  
    backupTailLog.CredentialName = credentialName;  
    backupTailLog.Database = dbName;  
    backupTailLog.Action = BackupActionType.Log;  
    backupTailLog.NoRecovery = true;  
    backupTailLog.Devices.AddDevice(urlTailLogBackup, DeviceType.Url);  
    backupTailLog.SqlBackup(server);  
  
    // Restore a database and move files  
    string newDataFilePath = server.MasterDBLogPath  + @"\" + dbName + DateTime.Now.ToString("s").Replace(":", "-") + ".mdf";  
    string newLogFilePath = server.MasterDBLogPath  + @"\" + dbName + DateTime.Now.ToString("s").Replace(":", "-") + ".ldf";  
  
    Restore restore = new Restore();  
    restore.CredentialName = credentialName;  
    restore.Database = dbName;  
    restore.ReplaceDatabase = true;  
    restore.Devices.AddDevice(urlBackupData, DeviceType.Url);  
    restore.RelocateFiles.Add(new RelocateFile(dbName, newDataFilePath));  
    restore.RelocateFiles.Add(new RelocateFile(dbName+ "_Log", newLogFilePath));  
    restore.SqlRestore(server);  
  
    ```  
  
3.  **PowerShell**  
  
    ```  
  
    #create variables  
    $backupUrlContainer = "https://mystorageaccount.blob.core.windows.net/mycontainer/"  
    $credentialName = "mycredential"  
    $srvPath = "SQLSERVER:\SQL\COMPUTERNAME\INSTNACENAME"  
    # for default instance, the $srvpath variable would be "SQLSERVER:\SQL\COMPUTERNAME\DEFAULT"  
  
    # navigate to SQL Server Instance   
  
    CD $srvPath   
  
    #create a unique file name for the full backup  
    $backupdbFile = $backupUrlContainer + "AdventureWorks2012_" + (Get-Date).ToString("s").Replace("-","_").Replace(":", "_").Replace(" ","_").Replace("/", "_") +  ".bak"  
  
    # Full database backup to URL  
    Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupdbFile  -SqlCredential $credentialName -CompressionOption On      
  
    #Create a unique file name for the tail log backup  
    $backuplogFile = $backupUrlContainer + "AdventureWorks2012_" + (Get-Date).ToString("s").Replace("-","_").Replace(":", "_").Replace(" ","_").Replace("/", "_") +  ".trn"  
  
    #Backup tail log to URL  
  
    Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupFile  -SqlCredential $credentialName  -BackupAction Log -NoRecovery    
  
    # Restore Database and move files  
  
    $newDataFilePath = New-Object Microsoft.SqlServer.Management.Smo.RelocateFile ("AdventureWorks_Data","C:\Program Files\Microsoft SQL Server\myinstance\MSSQL\DATA\AdventureWorks2012.mdf")  
    $newLogFilePath = New-Object Microsoft.SqlServer.Management.Smo.RelocateFile("AdventureWorks_Log","C:\Program Files\Microsoft SQL Server\myinstance\MSSQL\DATA\AdventureWorks2012.ldf")  
  
    Restore-SqlDatabase -Database AdventureWorks2012 -SqlCredential $credentialName -BackupFile $backupdbFile -RelocateFile @($newDataFilePath,$newLogFilePath)  
  
    ```  
  
###  <a name="PITR"></a> Restauração pontual usando STOPAT  
 O exemplo a seguir restaura um banco de dados para seu estado em um determinado ponto e mostra uma operação de restauração.  
  
1.  **Tsql**  
  
    ```  
    RESTORE DATABASE AdventureWorks FROM URL = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012.bak'   
    WITH   
     CREDENTIAL = 'mycredential'  
    ,MOVE 'AdventureWorks2012_data' to 'C:\Program Files\Microsoft SQL Server\myinstance\MSSQL\DATA\AdventureWorks2012.mdf'  
    ,Move 'AdventureWorks2012_log' to 'C:\Program Files\Microsoft SQL Server\myinstance\MSSQL\DATA\AdventureWorks2012.ldf'  
    ,NORECOVERY  
    --,REPLACE  
    ,STATS = 5;  
    GO   
  
    RESTORE LOG AdventureWorks FROM URL = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012.trn'   
    WITH CREDENTIAL = 'mycredential'  
    ,RECOVERY   
    ,STOPAT = 'Oct 23, 2012 5:00 PM'   
    GO  
    ```  
  
2.  **C#**  
  
    ```  
    // Connect to default sql server instance on local machine  
    Server server = new Server(".");  
    string identity = "mystorageaccount";  
  
    string credentialName = "mycredential";  
    string dbName = "AdventureWorks2012";  
    string blobContainerName = "mycontainer";  
  
    // Generate Unique Url  
    string urlBackupData = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}-Data{3}.bak",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
    // Backup to Url  
    Backup backup = new Backup();  
    backup.CredentialName = credentialName;  
    backup.Database = dbName;  
    backup.Devices.AddDevice(urlBackupData, DeviceType.Url);  
    backup.SqlBackup(server);  
  
    // Generate Unique Url for Tail Log backup  
    string urlTailLogBackup = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}-TailLog{3}.bak",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
    // Backup Tail Log to Url  
    Backup backupTailLog = new Backup();  
    backupTailLog.CredentialName = credentialName;  
    backupTailLog.Database = dbName;  
    backupTailLog.Action = BackupActionType.Log;  
    backupTailLog.NoRecovery = true;  
    backupTailLog.Devices.AddDevice(urlTailLogBackup, DeviceType.Url);  
    backupTailLog.SqlBackup(server);  
  
    // Restore a database and move files  
    string newDataFilePath = server.MasterDBLogPath + @"\" + dbName + DateTime.Now.ToString("s").Replace(":", "-") + ".mdf";  
    string newLogFilePath = server.MasterDBLogPath + @"\" + dbName + DateTime.Now.ToString("s").Replace(":", "-") + ".ldf";  
  
    Restore restore = new Restore();  
    restore.CredentialName = credentialName;  
    restore.Database = dbName;  
    restore.ReplaceDatabase = true;  
    restore.NoRecovery = true;  
    restore.Devices.AddDevice(urlBackupData, DeviceType.Url);  
    restore.RelocateFiles.Add(new RelocateFile(dbName, newDataFilePath));  
    restore.RelocateFiles.Add(new RelocateFile(dbName + "_Log", newLogFilePath));  
    restore.SqlRestore(server);  
  
    // Restore transaction Log with stop at   
    Restore restoreLog = new Restore();  
    restoreLog.CredentialName = credentialName;  
    restoreLog.Database = dbName;  
    restoreLog.Action = RestoreActionType.Log;  
    restoreLog.Devices.AddDevice(urlBackupData, DeviceType.Url);  
    restoreLog.ToPointInTime = DateTime.Now.ToString();   
    restoreLog.SqlRestore(server);  
  
    ```  
  
3.  **PowerShell**  
  
    ```  
  
    #create variables  
    $backupUrlContainer = "https://mystorageaccount.blob.core.windows.net/mycontainer/"  
    $credentialName = "mycredential"  
    $srvPath = "SQLSERVER:\SQL\COMPUTERNAME\INSTANCENAME"  
    # for default instance, the $srvpath variable would be "SQLSERVER:\SQL\COMPUTERNAME\DEFAULT"  
  
    # Navigate to SQL Server Instance Directory  
  
    CD $srvPath   
  
    #create a unique file name for the full backup  
    $backupdbFile = $backupUrlContainer + "AdventureWorks2012_" + (Get-Date).ToString("s").Replace("-","_").Replace(":", "_").Replace(" ","_").Replace("/", "_") +  ".bak"  
  
    # Full database backup to URL  
    Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupdbFile  -SqlCredential $credentialName -CompressionOption On     
  
    #Create a unique file name for the tail log backup  
    $backuplogFile = $backupUrlContainer + "AdventureWorks2012_" + (Get-Date).ToString("s").Replace("-","_").Replace(":", "_").Replace(" ","_").Replace("/", "_") +  ".trn"  
  
    #Backup tail log to URL  
  
    Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupFile  -SqlCredential $credentialName  -BackupAction Log -NoRecovery     
  
    # Restore Database and move files  
  
    $newDataFilePath = New-Object Microsoft.SqlServer.Management.Smo.RelocateFile ("AdventureWorks_Data","C:\Program Files\Microsoft SQL Server\myinstance\MSSQL\DATA\AdventureWorks2012.mdf")  
    $newLogFilePath = New-Object Microsoft.SqlServer.Management.Smo.RelocateFile("AdventureWorks_Log","C:\Program Files\Microsoft SQL Server\myinstance\MSSQL\DATA\AdventureWorks2012.ldf")  
  
    Restore-SqlDatabase -Database AdventureWorks2012 -SqlCredential $credentialName -BackupFile $backupdbFile -RelocateFile @($newDataFilePath,$newLogFilePath) -NoRecovery    
  
    # Restore Transaction log with Stop At:  
    Restore-SqlDatabase -Database AdventureWorks2012 -SqlCredential $credentialName -BackupFile $backuplogFile  -ToPointInTime (Get-Date).ToString()  
  
    ```  
  
## <a name="see-also"></a>Consulte também  
 [Práticas recomendadas e solução de problemas de backup do SQL Server para URL](sql-server-backup-to-url-best-practices-and-troubleshooting.md)   
 [Fazer backup e restaurar bancos de dados do sistema &#40;SQL Server&#41;](back-up-and-restore-of-system-databases-sql-server.md)   
 [Tutorial: Backup e restauração do SQL Server para o serviço de Armazenamento de Blobs do Azure](../tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)  
  
  
