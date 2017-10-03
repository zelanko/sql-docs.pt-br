---
title: "RESTAURAÇÃO (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- RESTORE DATABASE
- RESTORE_TSQL
- RESTORE_DATABASE_TSQL
- RESTORE
- RESTORE_LOG_TSQL
- RESTORE LOG
dev_langs:
- TSQL
helpviewer_keywords:
- RESTORE DATABASE, see RESTORE statement
- full backups [SQL Server]
- RECOVERY option
- database snapshots [SQL Server], reverting to
- STOPAT syntax
- differential backups, RESTORE statement
- point in time recovery [SQL Server]
- restoring [SQL Server]
- NORECOVERY option
- online restores [SQL Server], RESTORE statement
- moving databases
- RESTORE statement, syntax
- cross-platform restores
- restoring databases [SQL Server], options
- RESTORE statement
- snapshots [SQL Server database snapshots], reverting to
- reverting database snapshots
- transaction log backups [SQL Server], RESTORE statement
- RESTORE LOG, see RESTORE statement
ms.assetid: 877ecd57-3f2e-4237-890a-08f16e944ef1
caps.latest.revision: 248
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: e233de35336d5246c439c5dfb7b934cd2469b92c
ms.contentlocale: pt-br
ms.lasthandoff: 09/27/2017

---
# <a name="restore-statements-transact-sql"></a>RESTAURAR instruções (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restaura backups feitos por meio do comando BACKUP. Esse comando permite executar os seguintes cenários de restauração:  
  
-   Restaurar um banco de dados inteiro de um backup de banco de dados completo (uma restauração completa).  
  
-   Restaurar parte de um banco de dados (uma restauração parcial).  
  
-   Restaurar arquivos ou grupos de arquivos específicos para um banco de dados (uma restauração de arquivo).  
  
-   Restaurar páginas específicas para um banco de dados (uma restauração de página).  
  
-   Restaurar um log de transações em um banco de dados (uma restauração de log de transações).  
  
-   Reverter um banco de dados ao momento determinado capturado por um instantâneo do banco de dados.  
  
 Para obter mais informações sobre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cenários de restauração, consulte [visão geral de recuperação e restauração &#40; SQL Server &#41; ](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md).  Para obter mais informações sobre as descrições dos argumentos, consulte [argumentos RESTORE &#40; Transact-SQL &#41; ](../../t-sql/statements/restore-statements-arguments-transact-sql.md).   Ao restaurar um banco de dados de outra instância, considere as informações descritas em [Gerenciar metadados ao disponibilizar um banco de dados em outra instância do servidor (SQL Server)](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md).
  
> **Observação:** para obter mais informações sobre a restauração do serviço de armazenamento de Blob do Windows Azure, consulte [SQL Server Backup e restauração com o serviço de armazenamento de BLOBs do Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
--To Restore an Entire Database from a Full database backup (a Complete Restore):  
RESTORE DATABASE { database_name | @database_name_var }   
 [ FROM <backup_device> [ ,...n ] ]  
 [ WITH   
   {  
    [ RECOVERY | NORECOVERY | STANDBY =   
        {standby_file_name | @standby_file_name_var }   
       ]  
   | ,  <general_WITH_options> [ ,...n ]  
   | , <replication_WITH_option>  
   | , <change_data_capture_WITH_option>  
   | , <FILESTREAM_WITH_option>  
   | , <service_broker_WITH options>   
   | , \<point_in_time_WITH_options—RESTORE_DATABASE>   
   } [ ,...n ]  
 ]  
[;]  
  
--To perform the first step of the initial restore sequence  
-- of a piecemeal restore:  
RESTORE DATABASE { database_name | @database_name_var }   
   <files_or_filegroups> [ ,...n ]  
 [ FROM <backup_device> [ ,...n ] ]   
   WITH   
      PARTIAL, NORECOVERY   
      [  , <general_WITH_options> [ ,...n ]   
       | , \<point_in_time_WITH_options—RESTORE_DATABASE>   
      ] [ ,...n ]   
[;]  
  
--To Restore Specific Files or Filegroups:   
RESTORE DATABASE { database_name | @database_name_var }   
   <file_or_filegroup> [ ,...n ]  
 [ FROM <backup_device> [ ,...n ] ]   
   WITH   
   {  
      [ RECOVERY | NORECOVERY ]  
      [ , <general_WITH_options> [ ,...n ] ]  
   } [ ,...n ]   
[;]  
  
--To Restore Specific Pages:   
RESTORE DATABASE { database_name | @database_name_var }   
   PAGE = 'file:page [ ,...n ]'   
 [ , <file_or_filegroups> ] [ ,...n ]  
 [ FROM <backup_device> [ ,...n ] ]   
   WITH   
       NORECOVERY     
      [ , <general_WITH_options> [ ,...n ] ]  
[;]  
  
--To Restore a Transaction Log:  
RESTORE LOG { database_name | @database_name_var }   
 [ <file_or_filegroup_or_pages> [ ,...n ] ]  
 [ FROM <backup_device> [ ,...n ] ]   
 [ WITH   
   {  
     [ RECOVERY | NORECOVERY | STANDBY =   
        {standby_file_name | @standby_file_name_var }   
       ]  
    | ,  <general_WITH_options> [ ,...n ]  
    | , <replication_WITH_option>  
    | , \<point_in_time_WITH_options—RESTORE_LOG>   
   } [ ,...n ]  
 ]   
[;]  
  
--To Revert a Database to a Database Snapshot:     
RESTORE DATABASE { database_name | @database_name_var }   
FROM DATABASE_SNAPSHOT = database_snapshot_name   
  
<backup_device>::=  
{   
   { logical_backup_device_name |  
      @logical_backup_device_name_var }  
 | { DISK | TAPE | URL } = { 'physical_backup_device_name' |  
      @physical_backup_device_name_var }   
}   
Note: URL is the format used to specify the location and the file name for the Windows Azure Blob. Although Windows Azure storage is a service, the implementation is similar to disk and tape to allow for a consistent and seemless restore experince for all the three devices.  
<files_or_filegroups>::=   
{   
   FILE = { logical_file_name_in_backup | @logical_file_name_in_backup_var }   
 | FILEGROUP = { logical_filegroup_name | @logical_filegroup_name_var }   
 | READ_WRITE_FILEGROUPS  
}   
  
<general_WITH_options> [ ,...n ]::=   
--Restore Operation Options  
   MOVE 'logical_file_name_in_backup' TO 'operating_system_file_name'   
          [ ,...n ]   
 | REPLACE   
 | RESTART   
 | RESTRICTED_USER  | CREDENTIAL  
  
--Backup Set Options  
 | FILE = { backup_set_file_number | @backup_set_file_number }   
 | PASSWORD = { password | @password_variable }   
  
--Media Set Options  
 | MEDIANAME = { media_name | @media_name_variable }   
 | MEDIAPASSWORD = { mediapassword | @mediapassword_variable }   
 | BLOCKSIZE = { blocksize | @blocksize_variable }   
  
--Data Transfer Options  
 | BUFFERCOUNT = { buffercount | @buffercount_variable }   
 | MAXTRANSFERSIZE = { maxtransfersize | @maxtransfersize_variable }  
  
--Error Management Options  
 | { CHECKSUM | NO_CHECKSUM }   
 | { STOP_ON_ERROR | CONTINUE_AFTER_ERROR }   
  
--Monitoring Options  
 | STATS [ = percentage ]   
  
--Tape Options  
 | { REWIND | NOREWIND }   
 | { UNLOAD | NOUNLOAD }   
  
<replication_WITH_option>::=  
 | KEEP_REPLICATION   
  
<change_data_capture_WITH_option>::=  
 | KEEP_CDC  
  
<FILESTREAM_WITH_option>::=  
 | FILESTREAM ( DIRECTORY_NAME = directory_name )  
  
<service_broker_WITH_options>::=   
 | ENABLE_BROKER   
 | ERROR_BROKER_CONVERSATIONS   
 | NEW_BROKER  
  
\<point_in_time_WITH_options—RESTORE_DATABASE>::=   
 | {  
   STOPAT = { 'datetime'| @datetime_var }   
 | STOPATMARK = 'lsn:lsn_number'  
                 [ AFTER 'datetime']   
 | STOPBEFOREMARK = 'lsn:lsn_number'  
                 [ AFTER 'datetime']   
   }   
  
\<point_in_time_WITH_options—RESTORE_LOG>::=   
 | {  
   STOPAT = { 'datetime'| @datetime_var }   
 | STOPATMARK = { 'mark_name' | 'lsn:lsn_number' }  
                 [ AFTER 'datetime']   
 | STOPBEFOREMARK = { 'mark_name' | 'lsn:lsn_number' }  
                 [ AFTER 'datetime']   
   }  
  
```  
  
## <a name="arguments"></a>Argumentos  
 Para obter descrições dos argumentos, consulte [argumentos RESTORE &#40; Transact-SQL &#41; ](../../t-sql/statements/restore-statements-arguments-transact-sql.md).  
  
## <a name="about-restore-scenarios"></a>Sobre cenários de restauração  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte a vários cenários de restauração:  
  
-   restauração completa do banco de dados  
  
     Restaura todo o banco de dados, começando com um backup completo do banco de dados, que pode ser seguido pela restauração de um backup diferencial do banco de dados (e backups de log). Para obter mais informações, veja [Restaurações completas de banco de dados &#40;Modelo de recuperação simples#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md) ou [Restaurações completas de banco de dados &#40;Modelo de recuperação completa#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md).  
  
-   Restauração de arquivo  
  
     Restaura um arquivo ou grupo de arquivos em um banco de dados com vários grupos de arquivos. Observe que no modelo de recuperação simples, o arquivo deve pertencer a um grupo de arquivos somente leitura. Depois de uma restauração completa do arquivo, um backup de arquivo diferencial pode ser restaurado. Para obter mais informações, consulte [restaurações de arquivos &#40; Modelo de recuperação completa &#41; ](../../relational-databases/backup-restore/file-restores-full-recovery-model.md) e [arquivo restaurações &#40; Modelo de recuperação simples &#41; ](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md).  
  
-   Restauração de página  
  
     Restaura páginas individuais. A restauração de página só está disponível nos modelos de recuperação completa e bulk-logged. Para obter mais informações, veja [Restaurar páginas &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md).  
  
-   Restauração por etapas  
  
     Restaura o banco de dados por etapas, começando com o grupo de arquivos primário e um ou mais grupos de arquivos secundários. Uma restauração por etapas começa com um RESTORE DATABASE, usando a opção PARTIAL e especificando um ou mais grupos de arquivos secundários a serem restaurados. Para obter mais informações, veja [Restaurações por etapas &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md).  
  
-   Somente recuperação  
  
     Recupera dados que já estão consistentes com o banco de dados e só precisam ser disponibilizados. Para obter mais informações, veja [Recuperar um banco de dados sem restaurar dados &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/recover-a-database-without-restoring-data-transact-sql.md).  
  
-   Restauração de log de transações.  
  
     No modelo de recuperação completa ou bulk-logged, a restauração de backups de log é exigida para alcançar o ponto de recuperação desejado. Para obter mais informações sobre como restaurar backups de log, consulte [aplicar Backups de Log de transações &#40; SQL Server &#41; ](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md).  
  
-   Preparar um banco de dados de disponibilidade para um grupo de disponibilidade AlwaysOn  
  
     Para obter mais informações, veja [Preparar um banco de dados secundário manualmente para um grupo de disponibilidade &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md).  
  
-   Preparar um banco de dados espelho para espelhamento de banco de dados  
  
     Para obter mais informações, veja [Preparar um banco de dados espelho para espelhamento &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md).  
  
-   Restauração online  
  
    > **Observação:** restauração Online é permitida somente na edição Enterprise do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Quando houver suporte para a restauração online, se o banco de dados estiver online, restaurações de páginas e de arquivos serão automaticamente restaurações online e, também, restaurações de grupos de arquivos secundários após o estágio inicial de uma restauração por etapas.  
  
    > **Observação:** restaurações Online podem envolver [transações adiadas](../../relational-databases/backup-restore/deferred-transactions-sql-server.md).  
  
     Para obter mais informações, consulte [restauração Online &#40; SQL Server &#41; ](../../relational-databases/backup-restore/online-restore-sql-server.md).  
  
## <a name="additional-considerations-about-restore-options"></a>Considerações adicionais sobre opções de RESTORE  
  
### <a name="discontinued-restore-keywords"></a>Palavras-chave de RESTORE descontinuadas  
 As palavras-chave a seguir foram descontinuadas no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]:  
  
|Palavra-chave descontinuada|Substituída por...|Exemplo de palavra-chave de substituição|  
|--------------------------|------------------|------------------------------------|  
|LOAD|RESTORE|`RESTORE DATABASE`|  
|TRANSACTION|LOG|`RESTORE LOG`|  
|DBO_ONLY|RESTRICTED_USER|`RESTORE DATABASE ... WITH RESTRICTED_USER`|  
  
### <a name="restore-log"></a>RESTORE LOG  
 RESTORE LOG pode incluir uma lista de arquivos para permitir a criação de arquivos durante o roll forward. Isso é usado quando o backup de log contiver registros de log gravados quando um arquivo foi adicionado ao banco de dados.  
  
> **Observação:** para um banco de dados usando o modelo de recuperação completa ou bulk-logged, na maioria dos casos você deve fazer backup da parte final do log antes de restaurar o banco de dados. Restaurar um banco de dados sem antes fazer backup do final do log resultará em um erro, a não ser que a instrução RESTORE DATABASE contenha a cláusula WITH REPLACE ou WITH STOPAT, que deve especificar um momento ou transação que ocorreu após o final do backup de dados. Para obter mais informações sobre backups da parte final do log, veja [Backups da parte final do log &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md).  
  
### <a name="comparison-of-recovery-and-norecovery"></a>Comparação de RECOVERY e NORECOVERY  
 A reversão é controlada pela instrução RESTORE nas opções [ RECOVERY | NORECOVERY ]:  
  
-   NORECOVERY especifica que a reversão não ocorre. Isso permite que o roll forward continue com a próxima instrução na sequência.  
  
     Nesse caso, a sequência de restauração pode restaurar outros backups e efetuar roll forward neles.  
  
-   RECOVERY (o padrão) indica que a reversão deve ser executada após a conclusão do roll forward no backup atual.  
  
     Recuperando o banco de dados requer que todo o conjunto de dados que está sendo restaurados (o *conjunto de roll forward*) é consistente com o banco de dados. Se o conjunto de roll forward não tiver ido longe o suficiente para ficar consistente com o banco de dados e RECOVERY estiver especificado, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] emitirá um erro.  
  
## <a name="compatibility-support"></a>Suporte de compatibilidade  
 Backups de **mestre**, **modelo** e **msdb** que foram criados usando uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode ser restaurado por [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
> **Observação:** não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] backup ser restaurado para uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que a versão na qual o backup foi criado.  
  
 Cada versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa um caminho padrão diferente das versões anteriores. Assim, para restaurar um banco de dados que foi criado no local padrão dos backups de versões anteriores, você deve usar a opção MOVE. Para obter informações sobre o novo caminho padrão, consulte [locais de arquivo padrão e nomeadas instâncias do SQL Server](../../sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md).  
  
 Depois de você restaurar um banco de dados da versão anterior para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], o banco de dados será atualizado automaticamente. Normalmente, o banco de dados se torna disponível imediatamente. No entanto, se um banco de dados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] tiver índices de texto completo, o processo de atualização importará, redefinirá ou recriará esses índices, dependendo da configuração da propriedade de servidor  **upgrade_option** . Se a opção de atualização for definida como importar (**upgrade_option** = 2) ou recriar (**upgrade_option** = 0), os índices de texto completo permanecerão indisponíveis durante a atualização. Dependendo da quantidade de dados a serem indexados, a importação pode levar várias horas, e a recriação pode ser até dez vezes mais demorada. Lembre-se também de que, quando a opção de atualização estiver definida para importar, os índices de texto completo associados serão recriados se um catálogo de texto completo não estiver disponível. Para alterar a configuração da propriedade de servidor **upgrade_option** , use [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md).  
  
 Quando um banco de dados é anexado ou restaurado pela primeira vez a uma nova instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], uma cópia da chave mestra de banco de dados (criptografada pela chave mestra de serviço) ainda não está armazenada no servidor. É necessário usar a instrução **OPEN MASTER KEY** para descriptografar a DMK (chave mestra do banco de dados). Após a descriptografia da DMK, você tem a opção de habilitar a descriptografia automática no futuro usando a instrução **ALTER MASTER KEY REGENERATE** para provisionar o servidor com uma cópia da DMK criptografada com a SMK (chave mestra de serviço). Quando um banco de dados for atualizado de uma versão anterior, a DMK deverá ser regenerada para usar o algoritmo AES mais recente. Para obter mais informações sobre como regenerar a DMK, veja [ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md). O tempo necessário para regenerar a chave DMK para atualizar o AES depende do número de objetos protegidos pela DMK. É necessário regenerar a chave DMK para atualizar o AES somente uma vez, isso não tem impacto sobre regenerações futuras como parte de uma estratégia de rotação de chave.  
  
## <a name="general-remarks"></a>Comentários gerais  
 Durante uma restauração offline, se o banco de dados especificado estiver em uso, RESTORE forçará a saída do usuário depois de um pequeno atraso. Para restauração online de um grupo de arquivos não primário, o banco de dados pode permanecer em uso, exceto quando o grupo de arquivos que está sendo restaurado for colocado offline. Todos os dados no banco de dados especificado são substituídos pelos dados restaurados.  
  
 Para obter mais informações sobre a recuperação de banco de dados, consulte [visão geral de recuperação e restauração &#40; SQL Server &#41; ](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md).  
  
 As operações de restauração entre plataformas, mesmo entre tipos diferentes de processadores, podem ser executadas desde que o agrupamento do banco de dados tenha suporte no sistema operacional.  
  
 RESTORE pode ser reiniciado depois de um erro. Além disso, você pode instruir RESTORE a prosseguir, apesar dos erros, e ele restaura o máximo possível de dados (consulte a opção CONTINUE_AFTER_ERROR).  
  
 RESTORE não é permitido em uma transação explícita ou implícita.  
  
 Restaurando um danificado **mestre** banco de dados é executado usando um procedimento especial. Para obter mais informações, consulte [Fazer backup e restaurar bancos de dados do sistema &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md).  
  
 A restauração de um banco de dados limpa o cache de planos da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A limpeza do cache de planos gera uma recompilação de todos os planos de execução subsequentes e pode provocar uma redução repentina e temporária do desempenho de consultas. Para cada armazenamento em cache limpo no cache de planos, o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contém a seguinte mensagem informativa: "O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] encontrou %d ocorrência(s) de liberação de armazenamento em cache '% s' (parte do cache de planos) devido à manutenção do banco de dados ou operações de reconfiguração". Essa mensagem é registrada a cada cinco minutos, contanto que o cache seja liberado dentro desse intervalo de tempo.  
  
 Para restaurar um banco de dados de disponibilidade, primeiro restaure o banco de dados à instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], em seguida, adicione o banco de dados ao grupo de disponibilidade.  
  
## <a name="interoperability"></a>Interoperabilidade  
  
### <a name="database-settings-and-restoring"></a>Restauração e configuração do banco de dados  
 Durante uma restauração, a maioria das opções do banco de dados que são configuráveis com ALTER DATABASE é redefinida com os valores em vigor no momento do término do backup.  
  
 Porém, o uso da opção WITH RESTRICTED_USER substitui esse comportamento pela configuração da opção de acesso do usuário. Essa configuração sempre é definida seguindo uma instrução RESTORE que inclui a opção WITH RESTRICTED_USER.  
  
### <a name="restoring-an-encrypted-database"></a>Restaurando um banco de dados criptografado  
 Para restaurar um banco de dados criptografado, é necessário ter acesso ao certificado ou à chave assimétrica usada para criptografar o banco de dados. Sem o certificado ou a chave assimétrica, o banco de dados não pode ser restaurado. Como resultado, o certificado usado para criptografar a chave de criptografia do banco de dados deverá ser retido enquanto o backup for necessário. Para obter mais informações, consulte [SQL Server Certificates and Asymmetric Keys](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md).  
  
### <a name="restoring-a-database-enabled-for-vardecimal-storage"></a>Restaurando um bancos de dados habilitado para armazenamento vardecimal  
 Backup e restauração funcionam corretamente com o **vardecimal** o formato de armazenamento. Para obter mais informações sobre **vardecimal** formato de armazenamento, consulte [sp_db_vardecimal_storage_format &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-db-vardecimal-storage-format-transact-sql.md).  
  
### <a name="restore-full-text-data"></a>Restaurar dados de texto completo  
 Dados de texto completo são restaurados com outros dados do banco de dados durante uma restauração completa. Usando a sintaxe `RESTORE DATABASE database_name FROM backup_device` comum, os arquivos de texto completo são restaurados como parte da restauração de arquivo de banco de dados.  
  
 A instrução RESTORE também pode ser usada para executar restaurações em locais alternados, restaurações diferenciais, restaurações de arquivos e grupos de arquivos e restaurações de arquivos e grupos de arquivos diferenciais de dados de texto completo. Além disso, RESTORE pode restaurar apenas arquivos de texto completo, assim como dados de banco de dados.  
  
> **Observação:** catálogos de texto completo importados de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ainda são tratados como arquivos de banco de dados. Nesse caso, o procedimento usado pelo [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] para fazer backup de catálogos de texto completo ainda se aplica, exceto pelo fato de que não é mais necessário pausar e retomar a operação de backup. Para obter mais informações, consulte [fazendo backup e restauração de catálogos de texto completo](http://go.microsoft.com/fwlink/?LinkId=107381).  
  
## <a name="metadata"></a>Metadados  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inclui tabelas de histórico de backup e restauração que controlam a atividade de backup e restauração de cada instância de servidor. Quando uma restauração é executada, as tabelas de histórico de backup também são modificadas. Para obter informações sobre essas tabelas, consulte [histórico de Backup e informações de cabeçalho &#40; SQL Server &#41; ](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md).  
  
##  <a name="REPLACEoption"></a>Impacto da opção REPLACE  
 REPLACE raramente deve ser usado e só depois de cuidadosa consideração. Normalmente a restauração evita a substituição acidental de um banco de dados por um banco de dados diferente. Se o banco de dados especificado em uma instrução RESTORE já existir no servidor atual e a GUID de família do banco de dados especificado for diferente da GUID de família do banco de dados registrado no conjunto de backup, o banco de dados não será restaurado. Essa é uma proteção importante.  
  
 A opção REPLACE substitui várias verificações de segurança importantes que a restauração geralmente executa. As verificações substituídas são as seguintes:  
  
-   Restauração de um banco de dados existente com um backup tirado de outro banco de dados.  
  
     Com a opção REPLACE, a restauração permite que você substitua um banco de dados existente por qualquer banco de dados do conjunto de backup, mesmo que o nome do banco de dados especificado seja diferente do nome de banco de dados registrado no conjunto de backup. Isso pode resultar na substituição acidental de um banco de dados por um banco de dados diferente.  
  
-   Restauração de um banco de dados que usa o modelo de recuperação bulk-logged onde um backup do final do log não foi feito e a opção STOPAT não é usada.  
  
     Com a opção REPLACE, você pode perder trabalho confirmado porque não foi feito backup do log gravado mais recentemente.  
  
-   Substituição de arquivos existentes.  
  
     Por exemplo, um engano poderia permitir a substituição de arquivos do tipo errado, como arquivos .xls, ou que estivessem sendo usados por outro banco de dados que não estivesse online. A perda de dados arbitrária é possível se arquivos existentes forem substituídos, embora o banco de dados restaurado esteja completo.  
  
## <a name="redoing-a-restore"></a>Refazendo uma restauração  
 Não é possível desfazer os efeitos de uma restauração; no entanto, você pode recusar os efeitos de roll forward e de cópia dos dados reiniciando em uma base de um arquivo por vez. Para recomeçar, restaure o arquivo desejado e execute o roll forward novamente. Por exemplo, se você restaurou muitos backups de log acidentalmente e excedeu o ponto de parada pretendido, reinicie a sequência.  
  
 Uma sequência de restauração pode ser anulada e reiniciada com a restauração de todo o conteúdo dos arquivos afetados.  
  
## <a name="reverting-a-database-to-a-database-snapshot"></a>Revertendo um banco de dados para um instantâneo de banco de dados  
 Um *reverter a operação de banco de dados* (especificado com a opção DATABASE_SNAPSHOT) usa um banco de dados do código-fonte completo de volta no tempo, ou seja, revertendo-o para a hora de um instantâneo de banco de dados, substituindo o banco de dados de origem com dados do ponto no tempo mantido no instantâneo de banco de dados especificado. Só o instantâneo para o qual você está revertendo pode existir atualmente. A operação de reversão, então, reconstrói o log (portanto, você não poderá efetuar roll forward em um banco de dados revertido até o ponto do erro do usuário).  
  
 A perda de dados é limitada às atualizações no banco de dados desde a criação do instantâneo. Os metadados de um banco de dados revertido são iguais aos metadados no momento da criação do instantâneo. No entanto, a reversão para um instantâneo descarta todos os catálogos de texto completo.  
  
 A reversão a partir de um instantâneo do banco de dados não é destinada à recuperação de mídia. Ao contrário de um conjunto de backup regular, o instantâneo de banco de dados é uma cópia incompleta dos arquivos do banco de dados. Se o banco de dados ou o instantâneo do banco de dados está corrompido, é provável que a reversão a partir de um instantâneo seja impossível. Além disso, mesmo quando possível, é improvável que a reversão corrija o problema no caso de corrupção.  
  
### <a name="restrictions-on-reverting"></a>Restrições na reversão  
 Não há suporte para a reversão nas seguintes condições:  
  
-   O banco de dados de origem contém algum grupo de arquivos somente leitura ou compactado.  
  
-   Há algum arquivo offline que estava online quando o instantâneo foi criado.  
  
-   Existe mais de um instantâneo do banco de dados atualmente.  
  
 Para obter mais informações, consulte [reverter um banco de dados para um instantâneo do banco de dados](../../relational-databases/databases/revert-a-database-to-a-database-snapshot.md).  
  
## <a name="security"></a>Segurança  
 Uma operação de backup pode, opcionalmente, especificar senhas para um conjunto de mídias, um conjunto de backup ou ambos. Quando uma senha tiver sido definida em um conjunto de backup ou de mídias, será preciso especificar a senha ou as senhas corretas na instrução RESTORE. Essas senhas impedem operações de restauração não autorizadas e anexações não autorizadas de conjuntos de backup para mídia usando ferramentas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Porém, mídia protegida por senha pode ser substituída pela opção FORMAT da instrução BACKUP.  
  
> [!IMPORTANT]  
>  A proteção fornecida por esta senha é fraca. Destina-se a evitar uma restauração incorreta com o uso de ferramentas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por usuários autorizados ou não autorizados. Não impede a leitura dos dados de backup por outros meios ou a substituição da senha. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]A prática recomendada para proteger backups é armazenar as fitas de backup em um local seguro ou fazer backup de arquivos de disco que são protegidos por listas de controle de acesso adequadas (ACLs). As ACLs devem ser definidas no diretório raiz em que os backups são criados.  
>   
>  Para obter informações específicas para o backup do SQL Server e a restauração com o armazenamento de Blob do Windows Azure, consulte [SQL Server Backup e restauração com o serviço de armazenamento de BLOBs do Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  
  
### <a name="permissions"></a>Permissões  
 Se o banco de dados que está sendo restaurado não existir, o usuário deverá ter permissões CREATE DATABASE para poder executar o comando RESTORE. Se o banco de dados existir, as permissões RESTORE usarão como padrão os membros das funções de servidor fixas **sysadmin** e **dbcreator** e o proprietário (**dbo**) do banco de dados (para a opção FROM DATABASE_SNAPSHOT, o banco de dados sempre existe).  
  
 As permissões RESTORE são concedidas a funções nas quais as informações de associação estão sempre disponíveis para o servidor. Como a associação da função de banco de dados fixa pode ser verificada apenas quando o banco de dados está acessível e não danificado, o que nem sempre é o caso quando RESTORE é executado, os membros da função de banco de dados fixa **db_owner** não têm permissões RESTORE.  
  
##  <a name="examples"></a> Exemplos  
 Todos os exemplos presumem que um backup de banco de dados completo foi executado.  
  
 Os exemplos de RESTORE incluem o seguinte:  
  
-   A. [Restaurando um banco de dados completo](#restoring_full_db)  
  
-   B. [Restauração de backups de banco de dados completo e diferencial](#restoring_full_n_differential_db_backups)  
  
-   C. [Restaurando um banco de dados usando a sintaxe RESTART](#restoring_db_using_RESTART)  
  
-   D. [Restaurando um banco de dados e movendo arquivos](#restoring_db_n_move_files)  
  
-   E. [Copiar um banco de dados usando BACKUP e restauração](#copying_db_using_bnr)  
  
-   F. [Restauração pontual usando STOPAT](#restoring_to_pit_using_STOPAT)  
  
-   G. [Restaurando o log de transações até uma marca](#restoring_transaction_log_to_mark)  
  
-   H. [Restaurando usando a sintaxe de fita](#restoring_using_TAPE)  
  
-   I. [Restaurando usando a sintaxe FILE e FILEGROUP](#restoring_using_FILE_n_FG)  
  
-   J. [Revertendo de um instantâneo de banco de dados](#reverting_from_db_snapshot)  
  
-   K. [Restauração do serviço de armazenamento de BLOBs do Microsoft Azure](#Azure_Blob)  
  
> **Observação:** para obter exemplos adicionais, consulte os tópicos de instruções de restauração que são listados na [visão geral de recuperação e restauração &#40; SQL Server &#41; ](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md).  
  
###  <a name="restoring_full_db"></a> A. Restaurando um banco de dados completo  
 O exemplo a seguir restaura um backup de banco de dados completo do dispositivo de backup lógico `AdventureWorksBackups`. Para obter um exemplo de criação desse dispositivo, consulte [dispositivos de Backup](../../relational-databases/backup-restore/backup-devices-sql-server.md).  
  
```  
RESTORE DATABASE AdventureWorks2012   
   FROM AdventureWorks2012Backups;  
```  
  
> **Observação:** para um banco de dados usando o modelo de recuperação completa ou bulk-logged [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requer na maioria dos casos você fazer backup da parte final do log antes de restaurar o banco de dados. Para obter mais informações, veja [Backups da parte final do log &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md).  
  
 [&#91; Início do exemplos &#93;](#examples)  
  
###  <a name="restoring_full_n_differential_db_backups"></a> B. Restaurando backups de banco de dados diferenciais e completos  
 O exemplo a seguir restaura um backup de banco de dados completo seguido por um backup diferencial do dispositivo de backup `Z:\SQLServerBackups\AdventureWorks2012.bak`, que contém os dois backups. O backup de banco de dados completo a ser restaurado é o sexto conjunto de backup no dispositivo (`FILE = 6`), e o backup de banco de dados diferencial é o nono no dispositivo (`FILE = 9`). Assim que o backup diferencial é recuperado, o banco de dados é recuperado.  
  
```  
RESTORE DATABASE AdventureWorks2012  
   FROM DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak'  
   WITH FILE = 6  
      NORECOVERY;  
RESTORE DATABASE AdventureWorks2012  
   FROM DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak'  
   WITH FILE = 9  
      RECOVERY;  
```  
  
 [&#91; Início do exemplos &#93;](#examples)  
  
###  <a name="restoring_db_using_RESTART"></a> C. Restaurando um banco de dados usando a sintaxe RESTART  
 O exemplo a seguir usa a opção `RESTART` para reiniciar uma operação `RESTORE` interrompida por uma deficiência de força no servidor.  
  
```  
-- This database RESTORE halted prematurely due to power failure.  
RESTORE DATABASE AdventureWorks2012  
   FROM AdventureWorksBackups;  
-- Here is the RESTORE RESTART operation.  
RESTORE DATABASE AdventureWorks2012   
   FROM AdventureWorksBackups WITH RESTART;  
```  
  
 [&#91; Início do exemplos &#93;](#examples)  
  
###  <a name="restoring_db_n_move_files"></a> D. Restaurando um banco de dados e movendo arquivos  
 O exemplo a seguir restaura um banco de dados completo e log de transações e move o banco de dados restaurado para o diretório `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data`.  
  
```  
RESTORE DATABASE AdventureWorks2012  
   FROM AdventureWorksBackups  
   WITH NORECOVERY,   
      MOVE 'AdventureWorks2012_Data' TO   
'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\NewAdvWorks.mdf',   
      MOVE 'AdventureWorks2012_Log'   
TO 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\NewAdvWorks.ldf';  
RESTORE LOG AdventureWorks2012  
   FROM AdventureWorksBackups  
   WITH RECOVERY;  
```  
  
 [&#91; Início do exemplos &#93;](#examples)  
  
###  <a name="copying_db_using_bnr"></a> E. Copiando um banco de dados usando BACKUP e RESTORE  
 O exemplo a seguir usa as instruções `BACKUP` e `RESTORE` para fazer uma cópia do banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. A instrução `MOVE` causa a restauração dos dados e do arquivo de log nos locais especificados. A instrução `RESTORE FILELISTONLY` é usada para determinar o número e os nomes dos arquivos no banco de dados que está sendo restaurado. A nova cópia do banco de dados é nomeada `TestDB`. Para obter mais informações, veja [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md).  
  
```  
BACKUP DATABASE AdventureWorks2012   
   TO AdventureWorksBackups ;  
  
RESTORE FILELISTONLY   
   FROM AdventureWorksBackups ;  
  
RESTORE DATABASE TestDB   
   FROM AdventureWorksBackups   
   WITH MOVE 'AdventureWorks2012_Data' TO 'C:\MySQLServer\testdb.mdf',  
   MOVE 'AdventureWorks2012_Log' TO 'C:\MySQLServer\testdb.ldf';  
GO  
```  
  
 [&#91; Início do exemplos &#93;](#examples)  
  
###  <a name="restoring_to_pit_using_STOPAT"></a> F. Restauração pontual usando STOPAT  
 O exemplo a seguir restaura um banco de dados para seu estado de `12:00 AM` em `April 15, 2020` e mostra uma operação de restauração que envolve vários backups de log. No dispositivo de backup, `AdventureWorksBackups`, o backup de banco de dados completo a ser restaurado é o terceiro conjunto de backup no dispositivo (`FILE = 3`), o primeiro backup de log é o quarto conjunto de backup (`FILE = 4`), e o segundo backup de log é o quinto conjunto de backup (`FILE = 5`).  
  
```  
RESTORE DATABASE AdventureWorks2012  
   FROM AdventureWorksBackups  
   WITH FILE=3, NORECOVERY;  
  
RESTORE LOG AdventureWorks2012  
   FROM AdventureWorksBackups  
   WITH FILE=4, NORECOVERY, STOPAT = 'Apr 15, 2020 12:00 AM';  
  
RESTORE LOG AdventureWorks2012  
   FROM AdventureWorksBackups  
   WITH FILE=5, NORECOVERY, STOPAT = 'Apr 15, 2020 12:00 AM';  
RESTORE DATABASE AdventureWorks2012 WITH RECOVERY;  
  
```  
  
 [&#91; Início do exemplos &#93;](#examples)  
  
###  <a name="restoring_transaction_log_to_mark"></a>G. Restaurando o log de transações até uma marca  
 O exemplo a seguir restaura o log de transações até a marca na transação marcada denominada `ListPriceUpdate`.  
  
```  
USE AdventureWorks2012  
GO  
BEGIN TRANSACTION ListPriceUpdate  
   WITH MARK 'UPDATE Product list prices';  
GO  
  
UPDATE Production.Product  
   SET ListPrice = ListPrice * 1.10  
   WHERE ProductNumber LIKE 'BK-%';  
GO  
  
COMMIT TRANSACTION ListPriceUpdate;  
GO  
  
-- Time passes. Regular database   
-- and log backups are taken.  
-- An error occurs in the database.  
USE master;  
GO  
  
RESTORE DATABASE AdventureWorks2012  
FROM AdventureWorksBackups  
WITH FILE = 3, NORECOVERY;  
GO  
  
RESTORE LOG AdventureWorks2012  
   FROM AdventureWorksBackups   
   WITH FILE = 4,  
   RECOVERY,   
   STOPATMARK = 'UPDATE Product list prices';  
```  
  
 [&#91; Início do exemplos &#93;](#examples)  
  
###  <a name="restoring_using_TAPE"></a>H. Restaurando com o uso da sintaxe de TAPE  
 O exemplo a seguir restaura um backup de banco de dados completo de um dispositivo de backup `TAPE`.  
  
```  
RESTORE DATABASE AdventureWorks2012   
   FROM TAPE = '\\.\tape0';  
```  
  
 [&#91; Início do exemplos &#93;](#examples)  
  
###  <a name="restoring_using_FILE_n_FG"></a>I. Restaurando usando a sintaxe FILE e FILEGROUP  
 O exemplo a seguir restaura um banco de dados nomeado `MyDatabase` que tem dois arquivos, um grupo de arquivos secundário e um log de transações. O banco de dados usa o modelo de recuperação completa.  
  
 O backup do banco de dados é o nono conjunto de backup no conjunto de mídias em um dispositivo de backup lógico nomeado `MyDatabaseBackups`. Depois, três backups de log, que estão nos próximos três conjuntos de backup (`10`, `11` e `12`) no dispositivo `MyDatabaseBackups`, são restaurados usando `WITH NORECOVERY`. Depois de restaurar o último backup de log, o banco de dados é recuperado.  
  
> **Observação:** recuperação é executada como uma etapa separada para reduzir a possibilidade de recuperação antecipada, antes que o log de todos os backups foram restaurados.  
  
 No `RESTORE DATABASE`, observe que há dois tipos de opções de `FILE`. As opções `FILE` que precedem o nome do dispositivo de backup especificam os nomes de arquivos lógicos dos arquivos de banco de dados restaurados do conjunto de backup; por exemplo, `FILE = 'MyDatabase_data_1'`. Esse conjunto de backups não é o primeiro backup de banco de dados no conjunto de mídias; portanto, sua posição no conjunto de mídias é indicada com a opção `FILE` na cláusula `WITH`, `FILE=9`.  
  
```  
RESTORE DATABASE MyDatabase  
   FILE = 'MyDatabase_data_1',  
   FILE = 'MyDatabase_data_2',  
   FILEGROUP = 'new_customers'  
   FROM MyDatabaseBackups  
   WITH   
      FILE = 9,  
      NORECOVERY;  
GO  
-- Restore the log backups.  
RESTORE LOG MyDatabase  
   FROM MyDatabaseBackups  
   WITH FILE = 10,   
      NORECOVERY;  
GO  
RESTORE LOG MyDatabase  
   FROM MyDatabaseBackups  
   WITH FILE = 11,   
      NORECOVERY;  
GO  
RESTORE LOG MyDatabase  
   FROM MyDatabaseBackups  
   WITH FILE = 12,   
      NORECOVERY;  
GO  
--Recover the database:  
RESTORE DATABASE MyDatabase WITH RECOVERY;  
GO  
```  
  
 [&#91; Início do exemplos &#93;](#examples)  
  
###  <a name="reverting_from_db_snapshot"></a>J. Revertendo de um instantâneo do banco de dados  
 O exemplo a seguir reverte um banco de dados para um instantâneo do banco de dados. O exemplo presume que existe apenas um instantâneo atualmente no banco de dados. Para obter um exemplo de como criar esse instantâneo de banco de dados, consulte [criar um instantâneo de banco de dados &#40; Transact-SQL &#41; ](../../relational-databases/databases/create-a-database-snapshot-transact-sql.md).  
  
> **Observação:** reverter para um instantâneo descarta todos os catálogos de texto completo.  
  
```  
USE master;    
RESTORE DATABASE AdventureWorks2012 FROM DATABASE_SNAPSHOT = 'AdventureWorks_dbss1800';  
GO  
```  
 Para obter mais informações, consulte [reverter um banco de dados para um instantâneo do banco de dados](../../relational-databases/databases/revert-a-database-to-a-database-snapshot.md).  

 [&#91; Início do exemplos &#93;](#examples)  
  
###  <a name="Azure_Blob"></a>K. Restauração do serviço de armazenamento de BLOBs do Microsoft Azure  
Os três exemplos a seguir envolvem o uso do serviço de armazenamento do Microsoft Azure.  O nome da Conta de armazenamento é `mystorageaccount`.  O contêiner para arquivos de dados é chamado `myfirstcontainer`.  O contêiner para arquivos de backup é chamado `mysecondcontainer`.  Uma política de acesso armazenado foi criada com direitos de leitura, gravação, exclusão e lista, para cada contêiner.  Credenciais do SQL Server foram criadas usando assinaturas de acesso compartilhado que estão associados com as políticas de acesso armazenado.  Para obter informações específicas para o backup do SQL Server e a restauração com o armazenamento de BLOBs do Microsoft Azure, consulte [SQL Server Backup e restauração com o serviço de armazenamento de BLOBs do Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  

**K1.  Restaurar um backup completo do banco de dados de serviço de armazenamento do Microsoft Azure**  
Um backup de banco de dados completo, localizado em `mysecondcontainer`, de `Sales` será restaurado `myfirstcontainer`.  `Sales`não existem no servidor. 
```
RESTORE DATABASE Sales
  FROM URL = 'https://mystorageaccount.blob.core.windows.net/mysecondcontainer/Sales.bak'   
  WITH  MOVE 'Sales_Data1' to 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer/Sales_Data1.mdf', 
  MOVE 'Sales_log' to 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer/Sales_log.ldf', 
  STATS = 10;
```

**K2. Restaurar um backup de banco de dados completo do serviço de armazenamento do Microsoft Azure para armazenamento local**  
Um backup de banco de dados completo, localizado em `mysecondcontainer`, de `Sales` será restaurado para o armazenamento local.  `Sales`não existem no servidor.
```
RESTORE DATABASE Sales
  FROM URL = 'https://mystorageaccount.blob.core.windows.net/mysecondcontainer/Sales.bak'   
  WITH  MOVE 'Sales_Data1' to 'H:\DATA\Sales_Data1.mdf', 
  MOVE 'Sales_log' to 'O:\LOG\Sales_log.ldf', 
  STATS = 10;
```
  
**K3. Restaurar um backup completo do banco de dados do armazenamento local para o serviço de armazenamento do Microsoft Azure**  
```
RESTORE DATABASE Sales
  FROM DISK = 'E:\BAK\Sales.bak'
  WITH  MOVE 'Sales_Data1' to 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer/Sales_Data1.mdf', 
  MOVE 'Sales_log' to 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer/Sales_log.ldf', 
  STATS = 10;
```  
  

  
 [&#91; Início do exemplos &#93;](#examples)  
  
## <a name="much-more-information"></a>Muito mais informações!!  
 - [Fazer backup e restaurar bancos de dados do SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md) 
- [Backup e restauração de bancos de dados do sistema (SQL Server)](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md) 
 - [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)
 - [Fazer backup e restaurar índices e catálogos de texto completo](../../relational-databases/search/back-up-and-restore-full-text-catalogs-and-indexes.md)   
 - [Fazer backup e restaurar bancos de dados replicados](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
 - [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 - [Conjuntos de mídias, famílias de mídia e conjuntos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 - [RESTORE REWINDONLY &#40; Transact-SQL &#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)   
 - [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)   
 - [RESTORE FILELISTONLY (Transact-SQL)](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)  
 - [RESTORE HEADERONLY (Transact-SQL)](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)  
 - [Informações de histórico e cabeçalho de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)  
  
  

