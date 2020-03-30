---
title: Melhores práticas e solução de problemas de backup para URL
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: de676bea-cec7-479d-891a-39ac8b85664f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 5f744f0bb5d1ced6424fc8882a0a215042fbfc69
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "76920339"
---
# <a name="sql-server-backup-to-url-best-practices-and-troubleshooting"></a>Melhores práticas e solução de problemas de backup para URL do SQL Server

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Este tópico inclui melhores práticas e dicas de solução de problemas para backup e restaurações do SQL Server no serviço de Blobs do Azure.  
  
 Para obter mais informações sobre como usar o serviço de Armazenamento de Blobs do Azure para operações de backup ou restauração do SQL Server, confira:  
  
-   [Backup e restauração do SQL Server com o Serviço de Armazenamento de Blobs do Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)  
  
-   [Tutorial: Backup e restauração do SQL Server no serviço de Armazenamento de Blobs do Azure](../../relational-databases/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)  
  
## <a name="managing-backups"></a><a name="managing-backups-mb1"></a> Como gerenciar backups  
 A lista a seguir inclui recomendações gerais para gerenciar backups:  
  
-   O nome de arquivo exclusivo para cada backup é recomendável para evitar a substituição acidental dos blobs.  
  
-   Ao criar um contêiner, é recomendável definir o nível de acesso para **privado**, de forma que apenas os usuários ou as contas que podem fornecer as informações sobre autenticação necessárias possam ler ou gravar os blobs no contêiner.  
  
-   Para os bancos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em execução em uma máquina virtual do Azure, use uma conta de armazenamento na mesma região que a máquina virtual para evitar custos com transferência de dados entre regiões. O uso da mesma região também assegura o desempenho ideal para operações de backup e restauração.  
  
-   A atividade de backup com falha pode resultar em um arquivo de backup inválido. Recomendamos a identificação periódica de backup com falha e exclusão dos arquivos de blob. Para obter mais informações, consulte [Deleting Backup Blob Files with Active Leases](../../relational-databases/backup-restore/deleting-backup-blob-files-with-active-leases.md).  
  
-   O uso da opção `WITH COMPRESSION` durante o backup pode minimizar os custos com armazenamento e transações de armazenamento. Ele também pode diminuir o tempo necessário para concluir o processo de backup.  

- Defina os argumentos `MAXTRANSFERSIZE` e `BLOCKSIZE` como recomendado em [Backup do SQL Server em URL](./sql-server-backup-to-url.md).
  
## <a name="handling-large-files"></a>Tratando arquivos grandes  
  
-   A operação de backup do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa vários threads a fim de otimizar a transferência de dados para os serviços de Armazenamento de Blobs do Azure.  No entanto, o desempenho depende de vários fatores, como largura de banda do ISV e tamanho do banco de dados. Se você pretende fazer backup de bancos de dados ou grupos de arquivos grandes em um banco de dados do SQL Server no local, é recomendável que você teste a taxa de transferência primeiro. O [SLA para armazenamento](https://azure.microsoft.com/support/legal/sla/storage/v1_0/) do Azure tem tempos de processamento máximos para blobs que você pode levar em consideração.  
  
-   O uso da opção `WITH COMPRESSION`, como recomendado na seção [Como gerenciar backups](#managing-backups-mb1), é muito importante ao fazer backup de arquivos grandes.  
  
## <a name="troubleshooting-backup-to-or-restore-from-url"></a>Solução de problemas de backup para ou restauração de URL  
 Veja a seguir algumas maneiras rápidas de solucionar problemas de erros ao fazer backup ou restauração do serviço de Armazenamento de Blobs do Azure.  
  
 Para evitar erros devido às opções sem suporte ou às limitações, examine a lista de limitações e as informações de suporte aos comandos BACKUP e RESTORE no artigo [Backup e restauração do SQL Server com o Serviço de Armazenamento de Blobs do Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md) .  
  
 **Erros de autenticação:**  
  
-   `WITH CREDENTIAL` é uma opção nova e obrigatória para fazer backup ou restauração no serviço de Armazenamento de Blobs do Azure. As falhas relacionadas à credencial podem ser as seguintes:  
  
     A credencial especificada no comando **BACKUP** ou **RESTORE** não existe. Para evitar esse problema, inclua instruções T-SQL para criar a credencial caso não exista nenhuma na instrução de backup. Este é um exemplo que você pode usar:  
  
    ```sql  
    IF NOT EXISTS  
    (SELECT * FROM sys.credentials   
    WHERE credential_identity = 'mycredential')  
    CREATE CREDENTIAL <credential name> WITH IDENTITY = 'mystorageaccount'  
    ,SECRET = '<storage access key> ;  
    ```  
  
-   A credencial existem, mas a conta de logon usada para executar o comando de backup não tem permissões para acessar as credenciais. Use uma conta de logon na função **db_backupoperator** com permissões ***Alterar qualquer credencial*** .  
  
-   Verifique o nome da conta de armazenamento e os valores de chave. As informações armazenadas na credencial devem corresponder aos valores de propriedade da conta de armazenamento do Azure que você está usando nas operações de backup e restauração.  
  
 **Erros/falhas de backup:**  
  
-   Os backups paralelos no mesmo Blob ocasionam a falha de um dos backups com o erro **Falha na inicialização** .  
  
-   Se você estiver usando blobs de páginas, por exemplo, `BACKUP... TO URL... WITH CREDENTIAL`, use os seguintes logs de erro para facilitar a solução de problemas de backup:  
  
    -   Defina o sinalizador de rastreamento 3051 para ativar o registro em um log de erros específico com o seguinte formato:  
  
        `BackupToUrl-\<instname>-\<dbname>-action-\<PID>.log`, em que `\<action>` é um dos seguintes:  
  
        -   **DB**  
        -   **FILELISTONLY**  
        -   **LABELONLY**  
        -   **HEADERONLY**  
        -   **VERIFYONLY**  
  
    -   Você também pode encontrar informações analisando o Log de Eventos do Windows nos logs de aplicativo com o nome `SQLBackupToUrl`.  

    -   Considere COMPRESSION, MAXTRANSFERSIZE, BLOCKSIZE e vários argumentos de URL ao fazer backup de bancos de dados grandes.  Consulte [Fazendo backup de um VLDB para o Armazenamento de Blobs do Azure](https://blogs.msdn.microsoft.com/sqlcat/2017/03/10/backing-up-a-vldb-to-azure-blob-storage/)
  
        ```console
        Msg 3202, Level 16, State 1, Line 1
        Write on "https://mystorage.blob.core.windows.net/mycontainer/TestDbBackupSetNumber2_0.bak" failed: 1117(The request could not be performed because of an I/O device error.)
        Msg 3013, Level 16, State 1, Line 1
        BACKUP DATABASE is terminating abnormally.
        ```

        ```sql  
        BACKUP DATABASE TestDb
        TO URL = 'https://mystorage.blob.core.windows.net/mycontainer/TestDbBackupSetNumber2_0.bak',
        URL = 'https://mystorage.blob.core.windows.net/mycontainer/TestDbBackupSetNumber2_1.bak',
        URL = 'https://mystorage.blob.core.windows.net/mycontainer/TestDbBackupSetNumber2_2.bak'
        WITH COMPRESSION, MAXTRANSFERSIZE = 4194304, BLOCKSIZE = 65536;  
        ```  

-   Ao fazer a restauração em um backup compactado, você verá o seguinte erro:  
  
    -   `SqlException 3284 occurred. Severity: 16 State: 5  
        Message Filemark on device 'https://mystorage.blob.core.windows.net/mycontainer/TestDbBackupSetNumber2_0.bak' is not aligned.           Reissue the Restore statement with the same block size used to create the backupset: '65536' looks like a possible value.`  
  
        Para corrigir esse erro, emita novamente a instrução **RESTORE** com **BLOCKSIZE = 65536** especificado.  
  
-   Erro durante o backup devido a blobs que têm concessão ativa: A atividade de backup com falha pode resultar em blobs com concessões ativas.  
  
     Se houver uma nova tentativa de uso de uma instrução de backup, a operação de backup pode falhar com um erro semelhante ao seguinte:  
  
     `Backup to URL received an exception from the remote endpoint. Exception Message: The remote server returned an error: (412) There is currently a lease on the blob and no lease ID was specified in the request.`  
  
     Se for feita uma nova tentativa de uso de uma instrução de restauração em um arquivo de blob de backup que tenha uma concessão ativa, a operação de restauração falhará com um erro semelhante a:  
  
     `Exception Message: The remote server returned an error: (409) Conflict..`  
  
     Quando esse erro ocorre, os arquivos de blob precisam ser excluídos. Para obter mais informações sobre esse cenário e como corrigir o problema, consulte [Deleting Backup Blob Files with Active Leases](../../relational-databases/backup-restore/deleting-backup-blob-files-with-active-leases.md)  
  
## <a name="proxy-errors"></a>Erros de proxy  
 Se você estiver usando servidores proxy para acessar a Internet, poderá ver os seguintes problemas:  
  
 **Conexão limitada por servidores proxy:**  
  
 Os servidores proxy podem ter configurações que limitam o número de conexões por minuto. O processo de Backup para URL é multi-threaded e, portanto, pode ir além desse limite. Se isso acontecer, o servidor proxy elimina a conexão. Para resolver esse problema, altere as configurações de proxy para que o SQL Server não use o proxy. A seguir estão alguns exemplos dos tipos ou mensagens de erro que você pode ver no log de erros:  
  
```console
Write on "https://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak" failed: Backup to URL received an exception from the remote endpoint. Exception Message: Unable to read data from the transport connection: The connection was closed.
```  
  
```console
A nonrecoverable I/O error occurred on file "https://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak:" Error could not be gathered from Remote Endpoint.  
  
Msg 3013, Level 16, State 1, Line 2  
  
BACKUP DATABASE is terminating abnormally.  
```

```console
BackupIoRequest::ReportIoError: write failure on backup device https://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak'. Operating system error Backup to URL received an exception from the remote endpoint. Exception Message: Unable to read data from the transport connection: The connection was closed.
```  
  
Se você ativar o log detalhado usando o sinalizador de rastreamento 3051, também poderá ver a seguinte mensagem nos logs:  
  
`HTTP status code 502, HTTP Status Message Proxy Error (The number of HTTP requests per minute exceeded the configured limit. Contact your ISA Server administrator.)` 
  
 **Configurações de proxy padrão não escolhidas:**  
  
Às vezes, as configurações padrão não são escolhidas, causando erros de autenticação de proxy, como mostrado abaixo:
 
 `A nonrecoverable I/O error occurred on file "https://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak:" Backup to URL received an exception from the remote endpoint. Exception Message: The remote server returned an error: (407)* **Proxy Authentication Required.`  
  
Para resolver esse problema, crie um arquivo de configuração que permite que o processo de Backup para URL use as configurações de proxy padrão usando as seguintes etapas:  
  
1.  Crie um arquivo de configuração chamado `BackuptoURL.exe.config` com o seguinte conteúdo XML:  
  
    ```xml  
    <?xml version ="1.0"?>  
    <configuration>   
                    <system.net>   
                                    <defaultProxy enabled="true" useDefaultCredentials="true">   
                                                    <proxy usesystemdefault="true" />   
                                    </defaultProxy>   
                    </system.net>  
    </configuration>  
    ```  
  
2.  Coloque o arquivo de configuração na pasta Binn da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por exemplo, se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver instalado na unidade C do computador, coloque o arquivo de configuração em `C:\Program Files\Microsoft SQL Server\MSSQL13.\<InstanceName>\MSSQL\Binn`.  
  
## <a name="see-also"></a>Consulte Também  
 [Restaurando de backups armazenados no Microsoft Azure](../../relational-databases/backup-restore/restoring-from-backups-stored-in-microsoft-azure.md)  
[BACKUP (Transact-SQL)](../../t-sql/statements/backup-transact-sql.md)  
[RESTORE (Transact-SQL)](../../t-sql/statements/restore-statements-transact-sql.md)
  
