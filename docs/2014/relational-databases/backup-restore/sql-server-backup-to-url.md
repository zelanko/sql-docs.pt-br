---
title: SQL Server Backup para URL | Microsoft Docs
ms.custom: ''
ms.date: 10/18/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 11be89e9-ff2a-4a94-ab5d-27d8edf9167d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0ebc7fb8d170ddac10f1a326b3c05a54a0896666
ms.sourcegitcommit: 82a1ad732fb31d5fa4368c6270185c3f99827c97
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/21/2019
ms.locfileid: "72688740"
---
# <a name="sql-server-backup-to-url"></a>SQL Server Backup para URL
  Este tópico apresenta os conceitos, os requisitos e os componentes necessários para usar o serviço de armazenamento de BLOBs do Azure como um destino de backup. A funcionalidade de backup e restauração é igual ou semelhante ao uso de disco ou fita, com algumas diferenças. As diferenças são e quaisquer exceções notáveis, e alguns exemplos de código são incluídos neste tópico.  
  
## <a name="requirements-components-and-concepts"></a>Requisitos, componentes e conceitos  
 **Nesta seção:**  
  
-   [Segurança](#security)  
  
-   [Introdução aos principais componentes e conceitos](#intorkeyconcepts)  
  
-   [Serviço de armazenamento de BLOBs do Azure](#Blob)  
  
-   [Componentes do SQL Server](#sqlserver)  
  
-   [Limitações](#limitations)  
  
-   [Suporte para instruções de backup/restauração](#Support)  
  
-   [Usando a tarefa de backup no SQL Server Management Studio](sql-server-backup-to-url.md#BackupTaskSSMS)  
  
-   [SQL Server Backup para URL usando o assistente de plano de manutenção](sql-server-backup-to-url.md#MaintenanceWiz)  
  
-   [Restaurando do armazenamento do Azure usando o SQL Server Management Studio](sql-server-backup-to-url.md#RestoreSSMS)  
  
###  <a name="security"></a>Segurança  
 Veja a seguir as considerações e os requisitos de segurança ao fazer backup ou restauração dos serviços de armazenamento de BLOBs do Azure.  
  
-   Ao criar um contêiner para o serviço de armazenamento de BLOBs do Azure, recomendamos que você defina o acesso como **particular**. Definir o acesso como privado restringe o acesso a usuários ou contas capazes de fornecer as informações necessárias para se autenticar na conta do Azure.  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requer que o nome da conta do Azure e a autenticação de chave de acesso sejam armazenados em uma credencial [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essas informações são usadas para autenticar a conta do Azure quando ele executa operações de backup ou restauração.  
  
-   A conta de usuário usada para emitir comandos de BACKUP ou restauração deve estar na função de banco de dados do **operador db_backup** com permissões **ALTER ANY Credential** .  
  
###  <a name="intorkeyconcepts"></a>Introdução aos principais componentes e conceitos  
 As duas seções a seguir introduzem o serviço de armazenamento de BLOBs do Azure e os componentes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usados ao fazer backup ou restaurar do serviço de armazenamento de BLOBs do Azure. É importante entender os componentes e a interação entre eles para fazer um backup ou restauração a partir do serviço de armazenamento de BLOBs do Azure.  
  
 A criação de uma conta do Azure é a primeira etapa desse processo. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa o **nome da conta de armazenamento do Azure** e seus valores de **chave de acesso** para autenticar e gravar e ler BLOBs no serviço de armazenamento. A credencial de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] armazena essas informações de autenticação e é usada durante as operações de backup ou restauração. Para obter uma explicação completa de como criar uma conta de armazenamento e executar uma restauração simples, consulte [tutorial usando o serviço de armazenamento do Azure para SQL Server Backup e restauração](https://go.microsoft.com/fwlink/?LinkId=271615).  
  
 ![mapeando a conta de armazenamento para credenciais do SQL](../../tutorials/media/backuptocloud-storage-credential-mapping.gif "mapeando a conta de armazenamento para credenciais do SQL")  
  
###  <a name="Blob"></a>Serviço de armazenamento de BLOBs do Azure  
 **Conta de armazenamento:** A conta de armazenamento é o ponto de partida para todos os serviços de armazenamento. Para acessar o serviço de armazenamento de BLOBs do Azure, primeiro crie uma conta de armazenamento do Azure. O **nome da conta de armazenamento** e suas propriedades de **chave de acesso** são necessários para autenticar o serviço de armazenamento de BLOBs do Azure e seus componentes.  
  
 **Contêiner:** Um contêiner fornece um agrupamento de um conjunto de BLOBs e pode armazenar um número ilimitado de BLOBs. Para gravar um backup de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no serviço blob do Azure, você deve ter pelo menos o contêiner raiz criado.  
  
 **Blob:** Um arquivo de qualquer tipo e tamanho. Há dois tipos de BLOBs que podem ser armazenados no serviço de armazenamento de BLOBs do Azure: blobs de bloco e de página. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] backup usa blobs de página como o tipo de BLOB. Os BLOBs são endereçáveis usando o seguinte formato de URL: https://\<storage conta >. blob. Core. Windows. net/\<container >/\<blob >  
  
 ![Armazenamento de BLOBs do Azure](../../database-engine/media/backuptocloud-blobarchitecture.gif "Armazenamento de BLOBs do Azure")  
  
 Para obter mais informações sobre o serviço de armazenamento de BLOBs do Azure, consulte [como usar o serviço de armazenamento de BLOBs do Azure](http://www.windowsazure.com/develop/net/how-to-guides/blob-storage/)  
  
 Para obter mais informações sobre blobs de página, consulte [noções básicas sobre blobs de bloco e de página](https://msdn.microsoft.com/library/windowsazure/ee691964.aspx)  
  
###  <a name="sqlserver"></a>Componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 **URL:** Uma URL especifica um URI (Uniform Resource Identifier) para um arquivo de backup exclusivo. A URL é usada para fornecer o local e o nome do arquivo de backup do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Nessa implementação, a única URL válida é aquela que aponta para um blob de páginas em uma conta de armazenamento do Azure. A URL deve apontar para um blob real, não apenas para um contêiner. Se o BLOB não existir, ele será criado. Se um blob existente for especificado, o BACKUP falhará, a menos que a opção "com formato" seja especificada.  
  
> [!WARNING]  
>  Se você optar por copiar e carregar um arquivo de backup para o serviço de armazenamento de BLOBs do Azure, use o blob de páginas como sua opção de armazenamento. Não há suporte para restaurações de blobs de blocos. A restauração de um tipo de blob de blocos falha com um erro.  
  
 Aqui está um valor de URL de exemplo: http [s]://ACCOUNTNAME.Blob.core.windows.net/\<CONTAINER >/\<FILENAME. bak >. O HTTPS não é necessário, mas é recomendado.  
  
 **Credencial:** Uma credencial [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é um objeto usado para armazenar as informações de autenticação necessárias para se conectar a um recurso fora do SQL Server.  Aqui, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] processos de backup e restauração usam a credencial para autenticar o serviço de armazenamento de BLOBs do Azure. A Credencial armazena o nome da conta de armazenamento e os valores de **access key** da conta de armazenamento. Depois que a credencial é criada, ela deve ser especificada na opção WITH CREDENTIAL ao emitir as instruções BACKUP/RESTOre. Para obter mais informações sobre como exibir, copiar ou regenerar chaves de **acesso**da conta de armazenamento, consulte [chaves de acesso da conta de armazenamento](https://msdn.microsoft.com/library/windowsazure/hh531566.aspx).  
  
 Para obter instruções passo a passo sobre como criar uma credencial do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , consulte o exemplo [Criar uma credencial](#credential) mais adiante neste tópico.  
  
 Para obter informações gerais sobre credenciais, consulte [credenciais](../security/authentication-access/credentials-database-engine.md)  
  
 Para obter informações, em outros exemplos em que as credenciais são usadas, consulte [criar um proxy de SQL Server Agent](../../ssms/agent/create-a-sql-server-agent-proxy.md).  
  
###  <a name="limitations"></a>Limitações  
  
-   Não há suporte para backup no armazenamento Premium.  
  
-   O tamanho máximo de backup com suporte é 1 TB.  
  
-   Você pode emitir instruções de backup ou restauração usando cmdlets TSQL, SMO ou PowerShell. Um backup ou restauração do serviço de armazenamento de BLOBs do Azure usando SQL Server Management Studio assistente de backup ou restauração não está habilitado no momento.  
  
-   Não há suporte para a criação de um nome de dispositivo lógico. Portanto, não há suporte para a adição de URL como um dispositivo de backup usando sp_dumpdevice ou por meio de SQL Server Management Studio.  
  
-   Não há suporte para a anexação de blobs de backup. Os backups para um blob existente só podem ser substituídos usando a opção WITH FORMAT.  
  
-   Não há suporte para backup em vários BLOBs em uma única operação de backup. Por exemplo, o seguinte retorna um erro:  
  
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
  
-   Não há suporte para a especificação de opções de backupset-`RETAINDAYS` e `EXPIREDATE`.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tem um limite máximo de 259 caracteres para um nome de dispositivo de backup. O BACKUP para URL consome 36 caracteres para os elementos necessários usados para especificar a URL-' https://.blob.core.windows.net//.bak ', deixando 223 caracteres para os nomes de conta, contêiner e BLOB agrupados.  
  
###  <a name="Support"></a>Suporte para instruções de backup/restauração  
  
|||||  
|-|-|-|-|  
|Instrução backup/restore|Porta|Exceção|Feitos|  
|BACKUP|&#x2713;|Não há suporte para BLOCKSIZE e MAXTRANSFERSIZE.|Requer com CREDENCIAl especificada|  
|RECUPERAR|&#x2713;||Requer com CREDENCIAl especificada|  
|RESTAURAR FILELISTONLY|&#x2713;||Requer com CREDENCIAl especificada|  
|RESTAURAR HEADERONLY|&#x2713;||Requer com CREDENCIAl especificada|  
|RESTAURAR LABELONLY|&#x2713;||Requer com CREDENCIAl especificada|  
|RESTAURAR VERIFYONLY|&#x2713;||Requer com CREDENCIAl especificada|  
|RESTAURAR REWINDONLY|&#x2713;|||  
  
 Para obter a sintaxe e informações gerais sobre instruções de backup, consulte [ &#40;backup&#41;Transact-SQL](/sql/t-sql/statements/backup-transact-sql).  
  
 Para obter a sintaxe e informações gerais sobre instruções RESTORE, consulte [Restore &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql).  
  
### <a name="support-for-backup-arguments"></a>Suporte para argumentos de backup  
  
|||||  
|-|-|-|-|  
|Argumento|Porta|Exception|Feitos|  
|BANCO|&#x2713;|||  
|Façam|&#x2713;|||  
||  
|PARA (URL)|&#x2713;|Ao contrário do disco e da fita, a URL não dá suporte à especificação ou à criação de um nome lógico.|Esse argumento é usado para especificar o caminho da URL para o arquivo de backup.|  
|ESPELHAR PARA|&#x2713;|||  
|**COM OPÇÕES:**||||  
|PROVEDORES|&#x2713;||COM a CREDENCIAl só tem suporte ao usar a opção BACKUP TO URL para fazer backup no serviço de armazenamento de BLOBs do Azure.|  
|DIFFERENTIAL|&#x2713;|||  
|COPY_ONLY|&#x2713;|||  
|NO_COMPRESSION&#124;de compactação|&#x2713;|||  
|NDESCRIÇÃO|&#x2713;|||  
|NOMES|&#x2713;|||  
|&#124; RetainDays expirado|&#x2713;|||  
|inicialização NOINIT &#124;|&#x2713;||Essa opção será ignorada se for usada.<br /><br /> Anexar a BLOBs não é possível. Para substituir um backup, use o argumento FORMAT.|  
|não ignorar &#124; ignorar|&#x2713;|||  
|formato noformativo &#124;|&#x2713;||Essa opção será ignorada se for usada.<br /><br /> Um backup feito em um blob existente falhará, a menos que WITH FORMAT seja especificado. O blob existente é substituído quando WITH FORMAT é especificado.|  
|MEDIADESCRIPTION|&#x2713;|||  
|MEDIANAME|&#x2713;|||  
|BLOCKSIZE|&#x2713;|||  
|BUFFERCOUNT|&#x2713;|||  
|MAXTRANSFERSIZE|&#x2713;|||  
|soma &#124; de verificação NO_CHECKSUM|&#x2713;|||  
|STOP_ON_ERROR &#124; CONTINUE_AFTER_ERROR|&#x2713;|||  
|Estatísticas|&#x2713;|||  
|RETROCEDEr &#124; noretrocesso|&#x2713;|||  
|Descarregar &#124; NOUNLOAD|&#x2713;|||  
|modo &#124; de espera do NORECOVERY|&#x2713;|||  
|NO_TRUNCATE|&#x2713;|||  
  
 Para obter mais informações sobre argumentos de backup, consulte [backup &#40;Transact&#41;-SQL](/sql/t-sql/statements/backup-transact-sql).  
  
### <a name="support-for-restore-arguments"></a>Suporte para argumentos de restauração  
  
|||||  
|-|-|-|-|  
|Argumento|Porta|Exceção|Feitos|  
|BANCO|&#x2713;|||  
|Façam|&#x2713;|||  
|DE (URL)|&#x2713;||O argumento FROM URL é usado para especificar o caminho da URL para o arquivo de backup.|  
|**COM opções:**||||  
|PROVEDORES|&#x2713;||COM a CREDENCIAl só tem suporte ao usar a opção restaurar de URL para restaurar do serviço de armazenamento de BLOBs do Azure.|  
|PARCIAL|&#x2713;|||  
|em &#124; espera &#124; de recuperação NORECOVERY|&#x2713;|||  
|LOADHISTORY|&#x2713;|||  
|PROSSEGUIR|&#x2713;|||  
|Substitua|&#x2713;|||  
|REINICIAR|&#x2713;|||  
|RESTRICTED_USER|&#x2713;|||  
|Grupo|&#x2713;|||  
|LA|&#x2713;|||  
|MEDIANAME|&#x2713;|||  
|MEDIAPASSWORD|&#x2713;|||  
|BLOCKSIZE|&#x2713;|||  
|BUFFERCOUNT|&#x2713;|||  
|MAXTRANSFERSIZE|&#x2713;|||  
|NO_CHECKSUM &#124; de soma de verificação|&#x2713;|||  
|STOP_ON_ERROR &#124; CONTINUE_AFTER_ERROR|&#x2713;|||  
|FILESTREAM|&#x2713;|||  
|Estatísticas|&#x2713;|||  
|RETROCEDEr &#124; noretrocesso|&#x2713;|||  
|Descarregar &#124; NOUNLOAD|&#x2713;|||  
|KEEP_REPLICATION|&#x2713;|||  
|KEEP_CDC|&#x2713;|||  
|ENABLE_BROKER &#124; ERROR_BROKER_CONVERSATIONS &#124; NEW_BROKER|&#x2713;|||  
|STOPATMARK &#124; &#124; de STOPAT STOPBEFOREMARK|&#x2713;|||  
  
 Para obter mais informações sobre argumentos de restauração, consulte [argumentos &#40;de Restore Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-arguments-transact-sql).  
  
##  <a name="BackupTaskSSMS"></a>Usando a tarefa de backup no SQL Server Management Studio  
 A tarefa de backup no SQL Server Management Studio foi aprimorada para incluir a URL como uma das opções de destino e outros objetos de suporte necessários para fazer backup no armazenamento do Azure, como a credencial SQL.  
  
 As etapas a seguir descrevem as alterações feitas na tarefa backup de banco de dados para permitir o backup no armazenamento do Azure.:  
  
1.  Inicie SQL Server Management Studio e conecte-se à instância de SQL Server.  Selecione um banco de dados cujo backup você deseja fazer e clique com o botão direito do mouse em **tarefas**e selecione **fazer backup.** .. Isso abre a caixa de diálogo backup de banco de dados.  
  
2.  Na página geral, a opção **URL** é usada para criar um backup para o armazenamento do Azure. Ao selecionar essa opção, você verá outras opções habilitadas nesta página:  
  
    1.  **Nome do Arquivo:** nome do arquivo de backup.  
  
    2.  **Credencial SQL:** Você pode especificar uma credencial de SQL Server existente ou pode criar uma nova clicando na caixa **criar** ao lado da credencial do SQL.  
  
        > [!IMPORTANT]  
        >  A caixa de diálogo que é aberta quando você clica em **criar** requer um certificado de gerenciamento ou o perfil de publicação para a assinatura. O SQL Server atualmente dá suporte ao perfil de publicação versão 2,0. Para baixar a versão com suporte do perfil de publicação, consulte [baixar o perfil de publicação 2,0](https://go.microsoft.com/fwlink/?LinkId=396421).  
        >   
        >  Se você não tiver acesso ao certificado de gerenciamento ou ao perfil de publicação, poderá criar uma credencial do SQL especificando o nome da conta de armazenamento e as informações de chave de acesso usando Transact-SQL ou SQL Server Management Studio. Consulte o código de exemplo na seção [criar uma credencial](#credential) para criar uma credencial usando o TRANSACT-SQL. Como alternativa, usando o SQL Server Management Studio, na instância do mecanismo de banco de dados, clique com o botão direito do mouse em **Segurança**, selecione **Novo**e **Credencial**. Especifique o nome da conta de armazenamento para **identidade** e a chave de acesso no campo **senha** .  
  
    3.  **Contêiner de armazenamento do Azure:** O nome do contêiner de armazenamento do Azure para armazenar os arquivos de backup.  
  
    4.  **Prefixo da URL:** Isso é criado automaticamente usando as informações especificadas nos campos descritos nas etapas anteriores. Se você editar esse valor manualmente, verifique se ele corresponde às outras informações fornecidas anteriormente. Por exemplo, se você modificar a URL de armazenamento, verifique se a credencial do SQL está definida para autenticar para a mesma conta de armazenamento.  
  
 Quando você seleciona URL como o destino, determinadas opções na página **Opções de mídia** são desabilitadas.  Os tópicos a seguir têm mais informações sobre a caixa de diálogo backup de banco de dados:  
  
 [Página de backup &#40;geral do banco de dados&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)  
  
 [Página backup de &#40;opções de mídia de banco de dados&#41;](back-up-database-media-options-page.md)  
  
 [Página fazer backup &#40;de banco de dados de opções&#41;](back-up-database-backup-options-page.md)  
  
 [Criar credencial-autenticar no armazenamento do Azure](create-credential-authenticate-to-azure-storage.md)  
  
##  <a name="MaintenanceWiz"></a>SQL Server Backup para URL usando o assistente de plano de manutenção  
 Semelhante à tarefa de backup descrita anteriormente, o assistente de plano de manutenção no SQL Server Management Studio foi aprimorado para incluir a **URL** como uma das opções de destino e outros objetos de suporte necessários para fazer backup no armazenamento do Azure, como o SQL Provedores. Para obter mais informações, consulte a seção **definir tarefas de backup** em [usando o assistente de plano de manutenção](../maintenance-plans/use-the-maintenance-plan-wizard.md#SSMSProcedure).  
  
##  <a name="RestoreSSMS"></a>Restaurando do armazenamento do Azure usando o SQL Server Management Studio  
 Se você estiver restaurando um banco de dados, a **URL** será incluída como o dispositivo a ser restaurado. As etapas a seguir descrevem as alterações na tarefa de restauração para permitir a restauração do armazenamento do Azure:  
  
1.  Quando você seleciona **dispositivos** na página **geral** da tarefa restaurar no SQL Server Management Studio, isso leva você para a caixa de diálogo **selecionar dispositivos de backup** que inclui a **URL** como um tipo de mídia de backup.  
  
2.  Quando você seleciona **URL** e clica em **Adicionar**, a caixa de diálogo **Conectar-se ao armazenamento do Windows Azure** é aberta. Especifique as informações de credencial do SQL para autenticar no armazenamento do Azure.  
  
3.  Em seguida, o SQL Server se conecta ao armazenamento do Azure usando as informações de credencial do SQL fornecidas e abre a caixa de diálogo **localizar arquivo de backup no Azure** . Os arquivos de backup que residem no armazenamento são exibidos nesta página. Selecione o arquivo que você deseja usar para restaurar e clique em **OK**. Isso o levará de volta para a caixa de diálogo **selecionar dispositivos de backup** e clicar em **OK** nessa caixa de diálogo o levará de volta para a caixa de diálogo de **restauração** principal, na qual você poderá concluir a restauração.  Para obter mais informações, consulte os seguintes tópicos:  
  
     [Página geral &#40;de restaurar banco de dados&#41;](restore-database-general-page.md)  
  
     [Página restaurar &#40;arquivos de banco de dados&#41;](restore-database-files-page.md)  
  
     [Página restaurar &#40;opções do banco de dados&#41;](restore-database-options-page.md)  
  
##  <a name="Examples"></a>Exemplos de código  
 Esta seção contém os exemplos a seguir.  
  
-   [Criar uma credencial](#credential)  
  
-   [Fazendo backup de um banco de dados completo](#complete)  
  
-   [Fazendo backup do banco de dados e do log](#databaselog)  
  
-   [Criando um backup de arquivo completo do grupo de arquivos primário](#filebackup)  
  
-   [Criando um backup de arquivo diferencial dos grupos de arquivos primários](#differential)  
  
-   [Restaurando um banco de dados e movendo arquivos](#restoredbwithmove)  
  
-   [Restaurando para um ponto no tempo usando STOPAT](#PITR)  
  
###  <a name="credential"></a>Criar uma credencial  
 O exemplo a seguir cria uma credencial que armazena as informações de autenticação do armazenamento do Azure.  
  
1.  **TSQL**  
  
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
  
###  <a name="complete"></a>Fazendo backup de um banco de dados completo  
 O exemplo a seguir faz backup do banco de dados AdventureWorks2012 para o serviço de armazenamento de BLOBs do Azure.  
  
1.  **TSQL**  
  
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
  
###  <a name="databaselog"></a>Fazendo backup do banco de dados e do log  
 O exemplo a seguir faz backup do banco de dados de exemplo AdventureWorks2012, que usa o modelo de recuperação simples por padrão. Para dar suporte a backups de log, o banco de dados AdventureWorks2012 é modificado para usar o modelo de recuperação completa. Em seguida, o exemplo cria um backup de banco de dados completo para o blob do Azure e, após um período de atividade de atualização, faz o backup do log. Este exemplo cria um nome de arquivo de backup com um carimbo de data e hora.  
  
1.  **TSQL**  
  
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
  
###  <a name="filebackup"></a>Criando um backup de arquivo completo do grupo de arquivos primário  
 O exemplo a seguir cria um backup de arquivo completo do grupo de arquivos primário.  
  
1.  **TSQL**  
  
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
  
###  <a name="differential"></a>Criando um backup de arquivo diferencial do grupo de arquivos primário  
 O exemplo a seguir cria um backup de arquivo diferencial do grupo de arquivos primário.  
  
1.  **TSQL**  
  
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
  
###  <a name="restoredbwithmove"></a>Restaurar um banco de dados e mover arquivos  
 Para restaurar um backup de banco de dados completo e mover o banco de dados restaurado para C:\Arquivos de Programas\microsoft SQL Server\MSSQL12. MSSQLSERVER\MSSQL\Data diretório, use as etapas a seguir.  
  
1.  **TSQL**  
  
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
  
###  <a name="PITR"></a>Restaurando para um ponto no tempo usando STOPAT  
 O exemplo a seguir restaura um banco de dados para seu estado em um determinado ponto e mostra uma operação de restauração.  
  
1.  **TSQL**  
  
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
 [Práticas recomendadas e solução de problemas do SQL Server Backup para URL](sql-server-backup-to-url-best-practices-and-troubleshooting.md)    
 [Backup e restauração de bancos de dados do sistema &#40;SQL Server&#41; ](back-up-and-restore-of-system-databases-sql-server.md)    
 [Tutorial: SQL Server Backup e restauração para o serviço de armazenamento de BLOBs do Azure](../tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)  
  
  
