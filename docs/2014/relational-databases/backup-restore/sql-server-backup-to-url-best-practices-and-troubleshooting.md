---
title: Práticas recomendadas e solução de problemas de backup do SQL Server para URL | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: de676bea-cec7-479d-891a-39ac8b85664f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ac34c95e7ee4dc6f57ef7d8806a7db1bb981a944
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/30/2019
ms.locfileid: "70175968"
---
# <a name="sql-server-backup-to-url-best-practices-and-troubleshooting"></a>Práticas recomendadas e solução de problemas de backup do SQL Server para URL
  Este tópico inclui as práticas recomendadas e dicas de solução de problemas para SQL Server Backup e restaurações para o serviço blob do Azure.  
  
 Para obter mais informações sobre como usar o serviço de armazenamento de BLOBs do Azure para SQL Server operações de backup ou restauração, consulte:  
  
-   [SQL Server Backup e restauração com o serviço de armazenamento de BLOBs do Azure](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)  
  
-   [Tutorial: SQL Server Backup e restauração para o serviço de armazenamento de BLOBs do Azure](../tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)  
  
## <a name="managing-backups"></a>Gerenciando backups  
 A lista a seguir inclui recomendações gerais para gerenciar backups:  
  
-   O nome de arquivo exclusivo para cada backup é recomendável para evitar a substituição acidental dos blobs.  
  
-   Ao criar um contêiner, é recomendável definir o nível de acesso para **privado**, de forma que apenas os usuários ou as contas que podem fornecer as informações sobre autenticação necessárias possam ler ou gravar os blobs no contêiner.  
  
-   Para SQL Server bancos de dados em uma instância do SQL Server em execução em uma máquina virtual do Azure, use uma conta de armazenamento na mesma região que a máquina virtual para evitar custos de transferência de dados entre regiões. O uso da mesma região também assegura o desempenho ideal para operações de backup e restauração.  
  
-   A atividade de backup com falha pode resultar em um arquivo de backup inválido. Recomendamos a identificação periódica de backup com falha e exclusão dos arquivos de blob. Para obter mais informações, consulte [Deleting Backup Blob Files with Active Leases](deleting-backup-blob-files-with-active-leases.md).  
  
-   O uso da opção `WITH COMPRESSION` durante o backup pode minimizar os custos com armazenamento e transações de armazenamento. Ele também pode diminuir o tempo necessário para concluir o processo de backup.  
  
## <a name="handling-large-files"></a>Tratando arquivos grandes  
  
-   A [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] operação de backup usa vários threads para otimizar a transferência de dados para os serviços de armazenamento de BLOBs do Azure.  No entanto, o desempenho depende de vários fatores, como largura de banda do ISV e tamanho do banco de dados. Se você pretende fazer backup de bancos de dados ou grupos de arquivos grandes em um banco de dados do SQL Server no local, é recomendável que você teste a taxa de transferência primeiro. Os [SLA do armazenamento do Azure](https://go.microsoft.com/fwlink/?LinkId=271619) têm tempos de processamento máximos para BLOBs que você pode levar em consideração.  
  
-   O uso da opção `WITH COMPRESSION`, como recomendado na seção **Gerenciando o backup**, é muito importante ao fazer backup de arquivos grandes.  
  
## <a name="troubleshooting-backup-to-or-restore-from-url"></a>Solução de problemas de backup para ou restauração de URL  
 Veja a seguir algumas maneiras rápidas de solucionar erros durante o backup ou a restauração do serviço de armazenamento de BLOBs do Azure.  
  
 Para evitar erros devido a opções ou limitações sem suporte, examine a lista de limitações e suporte para comandos de BACKUP e restauração no artigo [SQL Server Backup e restauração com o serviço de armazenamento de BLOBs do Azure](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md) .  
  
 **Erros de autenticação:**  
  
-   COM CREDENTIAL é uma nova opção e é necessária para fazer backup ou restauração a partir do serviço de armazenamento de BLOBs do Azure. As falhas relacionadas à credencial podem ser as seguintes:  
  
     A credencial especificada no comando `BACKUP` ou `RESTORE` não existe. Para evitar esse problema, inclua instruções T-SQL para criar a credencial caso não exista nenhuma na instrução de backup. Este é um exemplo que você pode usar:  
  
    ```  
    IF NOT EXISTS  
    (SELECT * FROM sys.credentials   
    WHERE credential_identity = 'mycredential')  
    CREATE CREDENTIAL <credential name> WITH IDENTITY = 'mystorageaccount'  
    ,SECRET = '<storage access key> ;  
  
    ```  
  
-   A credencial existem, mas a conta de logon usada para executar o comando de backup não tem permissões para acessar as credenciais. Use uma conta de logon na função **db_backupoperator** com permissões **Alterar qualquer credencial** .  
  
-   Verifique o nome da conta de armazenamento e os valores de chave. As informações armazenadas na credencial devem corresponder aos valores de propriedade da conta de armazenamento do Azure que você está usando nas operações de backup e restauração.  
  
 **Erros/falhas de backup:**  
  
-   Os backups paralelos no mesmo Blob ocasionam a falha de um dos backups com o erro **Falha na inicialização** .  
  
-   Use os seguintes logs de erro para facilitar a solução de problemas de backup:  
  
    -   Defina o sinalizador de rastreamento 3051 para ativar o registro em um log de erros específico com o seguinte formato:  
  
         BackupToUrl-\<instname>-\<dbname>-action-\<PID>.log em que \<action> é um dentre:  
  
        -   `DB`  
  
        -   `FILELISTONLY`  
  
        -   `LABELONLY`  
  
        -   `HEADERONLY`  
  
        -   `VERIFYONLY`  
  
    -   Você também pode encontrar informações examinando o log de eventos do Windows-em logs de aplicativo com o nome ' SQLBackupToUrl '.  
  
-   Ao fazer a restauração em um backup compactado, você verá o seguinte erro:  
  
    -   Ocorreu a **SqlException 3284. Severity 16 Estados: 5**  
        **A marca de mensagem do dispositivo https://mystorage.blob.core.windows.net/mycontainer/TestDbBackupSetNumber2_0.bak ' ' não está alinhada. Emita novamente a instrução RESTORE com o mesmo tamanho de bloco usado para criar o conjunto de backup: ' 65536 ' é semelhante a um valor possível.**  
  
         Para corrigir esse erro, emita novamente a instrução `BACKUP` com `BLOCKSIZE = 65536` especificada.  
  
-   Erro durante o backup devido a blobs que têm concessão ativa: A atividade de backup com falha pode resultar em blobs com concessões ativas.  
  
     Se houver uma nova tentativa de uso de uma instrução de backup, a operação de backup pode falhar com um erro semelhante ao seguinte:  
  
     **A opção backup a URL recebeu uma exceção do ponto de extremidade remoto. Mensagem de exceção: O servidor remoto retornou um erro: (412) atualmente, há uma concessão no BLOB e nenhuma ID de concessão foi especificada na solicitação**.  
  
     Se for feita uma nova tentativa de uso de uma instrução de restauração em um arquivo de blob de backup que tenha uma concessão ativa, a operação de restauração falhará com um erro semelhante a:  
  
     **Mensagem de exceção: O servidor remoto retornou um erro: (409) conflito..**  
  
     Quando esse erro ocorre, os arquivos de blob precisam ser excluídos. Para obter mais informações sobre esse cenário e como corrigir o problema, consulte [Deleting Backup Blob Files with Active Leases](deleting-backup-blob-files-with-active-leases.md)  
  
## <a name="proxy-errors"></a>Erros de proxy  
 Se você estiver usando servidores proxy para acessar a Internet, poderá ver os seguintes problemas:  
  
 **Conexão limitada por servidores proxy:**  
  
 Os servidores proxy podem ter configurações que limitam o número de conexões por minuto. O processo de Backup para URL é multi-threaded e, portanto, pode ir além desse limite. Se isso acontecer, o servidor proxy elimina a conexão. Para resolver esse problema, altere as configurações de proxy para que o SQL Server não use o proxy.   A seguir estão alguns exemplos dos tipos ou mensagens de erro que você pode ver no log de erros:  
  
-   Falha ao gravar http://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak em "": O backup para a URL recebeu uma exceção do ponto de extremidade remoto. Mensagem de exceção: Não é possível ler os dados da conexão de transporte: A conexão foi fechada.  
  
-   Ocorreu um erro de E/S não recuperável no arquivo “http://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak: ” Não foi possível coletar o erro do ponto de extremidade remoto.  
  
     Msg 3013, Nível 16, Estado 1, Linha 2  
  
     BACKUP DATABASE está sendo encerrado de forma anormal.  
  
-   BackupIoRequest:: ReportIoError: falha de gravação no dispositivo de http://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak backup ' '. Erro de sistema operacional: a opção Backup para URL recebeu uma exceção do ponto de extremidade remoto. Mensagem de exceção: Não é possível ler os dados da conexão de transporte: A conexão foi fechada.  
  
 Se você ativar o log detalhado usando o sinalizador de rastreamento 3051, também poderá ver a seguinte mensagem nos logs:  
  
 Código de status HTTP 502, Erro de proxy da mensagem de status HTTP (o número de solicitações HTTP por minuto excedeu o limite configurado. Contate o administrador do ISA Server.  )  
  
 **Configurações de proxy padrão não escolhidas:**  
  
 Às vezes as configurações padrão não são selecionadas, causando erros de autenticação de proxy como:*Ocorreu um erro de E/S irrecuperável no arquivo “http://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak: ” O Backup para URL recebeu uma exceção do ponto de extremidade remoto. Mensagem de exceção: O servidor remoto retornou um erro: (407) **Autenticação de proxy necessária.***  
  
 Para resolver esse problema, crie um arquivo de configuração que permite que o processo de Backup para URL use as configurações de proxy padrão usando as seguintes etapas:  
  
1.  Crie um arquivo de configuração chamado BackuptoURL.exe.config com o seguinte xml:  
  
    ```  
    <?xml version ="1.0"?>  
    <configuration>   
                    <system.net>   
                                    <defaultProxy enabled="true" useDefaultCredentials="true">   
                                                    <proxy usesystemdefault="true" />   
                                    </defaultProxy>   
                    </system.net>  
    </configuration>  
  
    ```  
  
2.  Coloque o arquivo de configuração na pasta Binn da instância do SQL Server. Por exemplo, se o meu SQL Server estiver instalado na unidade C do computador, coloque o arquivo de configuração aqui: *C:\Arquivos de PROGRAMAS\MICROSOFT SQL Server\MSSQL12. InstanceName\<> \MSSQL\Binn*.  
  
## <a name="troubleshooting-sql-server-managed-backup-to-azure"></a>Solução de problemas SQL Server Backup gerenciado para o Azure  
 Como o backup gerenciado do SQL Server é criado com base no Backup para URL, as dicas de solução de problemas descritas nas seções anteriores aplicam-se a bancos de dados ou instâncias que usam o Backup Gerenciado do SQL Server.  Informações sobre solução de problemas SQL Server Backup gerenciado para o Azure são descritas em detalhes em [solução de problemas SQL Server Backup gerenciado para o Azure](sql-server-managed-backup-to-microsoft-azure.md).  
  
## <a name="see-also"></a>Consulte também  
 [Restaurando de backups armazenados no Azure](restoring-from-backups-stored-in-microsoft-azure.md)  
  
  
