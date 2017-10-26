---
title: "Práticas recomendadas e solução de problemas de backup do SQL Server para URL | Microsoft Docs"
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: de676bea-cec7-479d-891a-39ac8b85664f
caps.latest.revision: 26
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: c0e55c0e35039490f0ce4cd8a7fb6d7e232c05aa
ms.openlocfilehash: b76a0f262fd12e53797c0ad86c991a6e4423927a
ms.contentlocale: pt-br
ms.lasthandoff: 07/31/2017

---
# <a name="sql-server-backup-to-url-best-practices-and-troubleshooting"></a>Práticas recomendadas e solução de problemas de backup do SQL Server para URL
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Este tópico inclui práticas recomendadas e dicas de solução de problemas para backup e restaurações do SQL Server no serviço de Blob do Windows Azure.  
  
 Para obter mais informações sobre como usar o serviço de armazenamento de Blob do Windows Azure para operações de backup ou restauração do SQL Server, consulte:  
  
-   [Backup e restauração do SQL Server com o Serviço de Armazenamento de Blobs do Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)  
  
-   [Tutorial: Backup e restauração do SQL Server para o serviço de armazenamento de Blob do Windows Azure](~/relational-databases/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)  
  
## <a name="managing-backups"></a>Gerenciando backups  
 A lista a seguir inclui recomendações gerais para gerenciar backups:  
  
-   O nome de arquivo exclusivo para cada backup é recomendável para evitar a substituição acidental dos blobs.  
  
-   Ao criar um contêiner, é recomendável definir o nível de acesso para **privado**, de forma que apenas os usuários ou as contas que podem fornecer as informações sobre autenticação necessárias possam ler ou gravar os blobs no contêiner.  
  
-   Para bancos de dados do SQL Server em uma instância do SQL Server em execução em uma máquina virtual do Windows Azure, use uma conta de armazenamento na mesma região que a máquina virtual para evitar custos com transferência de dados entre regiões. O uso da mesma região também assegura o desempenho ideal para operações de backup e restauração.  
  
-   A atividade de backup com falha pode resultar em um arquivo de backup inválido. Recomendamos a identificação periódica de backup com falha e exclusão dos arquivos de blob. Para obter mais informações, consulte [Deleting Backup Blob Files with Active Leases](../../relational-databases/backup-restore/deleting-backup-blob-files-with-active-leases.md).  
  
-   O uso da opção **WITH COMPRESSION** durante o backup pode minimizar os custos com armazenamento e transações de armazenamento. Ele também pode diminuir o tempo necessário para concluir o processo de backup.  
  
## <a name="handling-large-files"></a>Tratando arquivos grandes  
  
-   A operação de backup do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa vários threads para otimizar a transferência de dados para os serviços de armazenamento de Blob do Windows Azure.  No entanto, o desempenho depende de vários fatores, como largura de banda do ISV e tamanho do banco de dados. Se você pretende fazer backup de bancos de dados ou grupos de arquivos grandes em um banco de dados do SQL Server no local, é recomendável que você teste a taxa de transferência primeiro. O [SLA para armazenamento](http://azure.microsoft.com/support/legal/sla/storage/v1_0/) do Azure tem tempos de processamento máximos para blobs que você pode levar em consideração.  
  
-   Usar a opção **WITH COMPRESSION** como recomendado na seção **Gerenciando o backup** é muito importante ao fazer backup de arquivos grandes.  
  
## <a name="troubleshooting-backup-to-or-restore-from-url"></a>Solução de problemas de backup para ou restauração de URL  
 Estas são algumas maneiras rápidas de solucionar problemas de erros ao fazer backup ou restauração do serviço de armazenamento de Blob do Windows Azure.  
  
 Para evitar erros devido às opções sem suporte ou às limitações, examine a lista de limitações e as informações de suporte aos comandos BACKUP e RESTORE no artigo [Backup e restauração do SQL Server com o Serviço de Armazenamento de Blobs do Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md) .  
  
 **Erros de autenticação:**  
  
-   WITH CREDENTIAL é uma nova opção, necessário para fazer backup ou restauração no serviço de armazenamento de Blob do Windows Azure. As falhas relacionadas à credencial podem ser as seguintes:  
  
     A credencial especificada no comando **BACKUP** ou **RESTORE** não existe. Para evitar esse problema, inclua instruções T-SQL para criar a credencial caso não exista nenhuma na instrução de backup. Este é um exemplo que você pode usar:  
  
    ```  
    IF NOT EXISTS  
    (SELECT * FROM sys.credentials   
    WHERE credential_identity = 'mycredential')  
    CREATE CREDENTIAL <credential name> WITH IDENTITY = 'mystorageaccount'  
    ,SECRET = '<storage access key> ;  
  
    ```  
  
-   A credencial existem, mas a conta de logon usada para executar o comando de backup não tem permissões para acessar as credenciais. Use uma conta de logon na função **db_backupoperator** com permissões **Alterar qualquer credencial** .  
  
-   Verifique o nome da conta de armazenamento e os valores de chave. As informações armazenadas na credencial devem corresponder aos valores de propriedade da conta de armazenamento do Windows Azure que você está usando nas operações de backup e restauração.  
  
 **Erros/falhas de backup:**  
  
-   Os backups paralelos no mesmo Blob ocasionam a falha de um dos backups com o erro **Falha na inicialização** .  
  
-   Use os seguintes logs de erro para facilitar a solução de problemas de backup:  
  
    -   Defina o sinalizador de rastreamento 3051 para ativar o registro em um log de erros específico com o seguinte formato:  
  
         BackupToUrl-\<instname>-\<dbname>-action-\<PID>.log em que \<action> é um dentre:  
  
        -   **DB**  
  
        -   **FILELISTONLY**  
  
        -   **LABELONLY**  
  
        -   **HEADERONLY**  
  
        -   **VERIFYONLY**  
  
    -   Você também pode localizar informações analisando o Log de Eventos do Windows nos logs de aplicativo com o nome ‘SQLBackupToUrl’.  
  
-   Ao fazer a restauração em um backup compactado, você verá o seguinte erro:  
  
    -   `SqlException 3284 occurred. Severity: 16 State: 5`  
        **A marca de arquivo da mensagem no dispositivo `'https://mystorage.blob.core.windows.net/mycontainer/TestDbBackupSetNumber2_0.bak'` não está alinhada. Emita novamente a instrução Restore com o mesmo tamanho de bloco usado para criar o conjunto de backup: '65536' parece um valor possível.**  
  
         Para corrigir esse erro, emita novamente a instrução **BACKUP** com **BLOCKSIZE = 65536** especificada.  
  
-   Erro durante o backup devido a blobs que têm a concessão ativa neles: a atividade de backup com falha pode resultar em blobs com concessões ativas.  
  
     Se houver uma nova tentativa de uso de uma instrução de backup, a operação de backup pode falhar com um erro semelhante ao seguinte:  
  
     **A opção backup a URL recebeu uma exceção do ponto de extremidade remoto. Mensagem de exceção: o servidor remoto retornou um erro: (412) há uma concessão no blob e nenhuma ID de concessão foi especificada na solicitação**.  
  
     Se for feita uma nova tentativa de uso de uma instrução de restauração em um arquivo de blob de backup que tenha uma concessão ativa, a operação de restauração falhará com um erro semelhante a:  
  
     **Mensagem de exceção: O servidor remoto retornou um erro: (409) Conflito.**  
  
     Quando esse erro ocorre, os arquivos de blob precisam ser excluídos. Para obter mais informações sobre esse cenário e como corrigir o problema, consulte [Deleting Backup Blob Files with Active Leases](../../relational-databases/backup-restore/deleting-backup-blob-files-with-active-leases.md)  
  
## <a name="proxy-errors"></a>Erros de proxy  
 Se você estiver usando servidores proxy para acessar a Internet, poderá ver os seguintes problemas:  
  
 **Conexão limitada por servidores proxy:**  
  
 Os servidores proxy podem ter configurações que limitam o número de conexões por minuto. O processo de Backup para URL é multi-threaded e, portanto, pode ir além desse limite. Se isso acontecer, o servidor proxy elimina a conexão. Para resolver esse problema, altere as configurações de proxy para que o SQL Server não use o proxy.   A seguir estão alguns exemplos dos tipos ou mensagens de erro que você pode ver no log de erros:  
  
-   A gravação em "http://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak" falhou: o backup para URL recebeu uma exceção do ponto de extremidade remoto. Mensagem de exceção: não é possível ler dados da conexão de transporte: a conexão foi fechada.  
  
-   Ocorreu um erro de E/S não recuperável no arquivo “`http://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak:`” Não foi possível coletar o erro do ponto de extremidade remoto.  
  
     Msg 3013, Nível 16, Estado 1, Linha 2  
  
     BACKUP DATABASE está sendo encerrado de forma anormal.  
  
-   BackupIoRequest::ReportIoError: falha de gravação no dispositivo de backup http://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak'. Erro de sistema operacional: a opção Backup para URL recebeu uma exceção do ponto de extremidade remoto. Mensagem de exceção: não é possível ler dados da conexão de transporte: a conexão foi fechada.  
  
 Se você ativar o log detalhado usando o sinalizador de rastreamento 3051, também poderá ver a seguinte mensagem nos logs:  
  
 Código de status HTTP 502, Erro de proxy da mensagem de status HTTP (o número de solicitações HTTP por minuto excedeu o limite configurado. Contate o administrador do ISA Server.  )  
  
 **Configurações de proxy padrão não escolhidas:**  
  
 Às vezes as configurações padrão não são selecionadas, causando erros de autenticação de proxy como:*Ocorreu um erro de E/S irrecuperável no arquivo “`http://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak:`” O Backup para URL recebeu uma exceção do ponto de extremidade remoto. Mensagem de exceção: o servidor remoto retornou um erro: (407)* **Autenticação de proxy necessária**.  
  
 Para resolver esse problema, crie um arquivo de configuração que permite que o processo de Backup para URL use as configurações de proxy padrão usando as seguintes etapas:  
  
1.  Crie um arquivo de configuração chamado BackuptoURL.exe.config com o seguinte xml:  
  
    ```  
    \<?xml version ="1.0"?>  
    <configuration>   
                    \<system.net>   
                                    <defaultProxy enabled="true" useDefaultCredentials="true">   
                                                    <proxy usesystemdefault="true" />   
                                    </defaultProxy>   
                    \</system.net>  
    </configuration>  
  
    ```  
  
2.  Coloque o arquivo de configuração na pasta Binn da instância do SQL Server. Por exemplo, se o SQL Server estiver instalado na unidade C do computador, coloque o arquivo de configuração aqui: *C:\Arquivos de Programas\Microsoft SQL Server\MSSQL13.\<InstanceName>\MSSQL\Binn*.  
  
## <a name="see-also"></a>Consulte também  
 [Restaurando de backups armazenados no Microsoft Azure](../../relational-databases/backup-restore/restoring-from-backups-stored-in-microsoft-azure.md)  
[BACKUP (Transact-SQL)](../../t-sql/statements/backup-transact-sql.md)  
[RESTORE (Transact-SQL)](../../t-sql/statements/restore-statements-transact-sql.md)
  

