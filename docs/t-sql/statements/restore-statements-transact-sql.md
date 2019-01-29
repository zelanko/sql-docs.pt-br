---
title: RESTORE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: mashamsft
ms.author: mathoma
manager: craigg
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current||>=aps-pdw-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 72d978967591fbffa8d25b3954c78256149f7592
ms.sourcegitcommit: 1e28f923cda9436a4395a405ebda5149202f8204
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "55045089"
---
# <a name="restore-statements-transact-sql"></a>Instruções RESTORE (Transact-SQL)
Restaura backups do banco de dados SQL feitos usando o comando BACKUP. 

Clique em uma das guias a seguir para ver sintaxe, argumentos, comentários, permissões e exemplos de uma versão específica do SQL com a qual você está trabalhando.

Para obter mais informações sobre as convenções de sintaxe, consulte [Convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md). 

## <a name="click-a-product"></a>Clique em um produto!

Na linha a seguir, clique em qualquer nome de produto de seu interesse. O clique exibe conteúdo diferente aqui, apropriado para qualquer produto no qual você clicar:

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions"

> [!div class="mx-tdCol2BreakAll"]
> ||||
> |-|-|-|
> |**_\*SQL Server\*_**|[Banco de Dados SQL<br />Instância Gerenciada](restore-statements-transact-sql.md?view=azuresqldb-mi-current)|[Parallel<br />Data Warehouse](restore-statements-transact-sql.md?view=aps-pdw-2016)

&nbsp;

## <a name="sql-server"></a>SQL Server

Esse comando permite executar os seguintes cenários de restauração:  
  
- Restaurar um banco de dados inteiro de um backup de banco de dados completo (uma restauração completa).
- Restaurar parte de um banco de dados (uma restauração parcial).
- Restaurar arquivos ou grupos de arquivos específicos para um banco de dados (uma restauração de arquivo).
- Restaurar páginas específicas para um banco de dados (uma restauração de página).  
- Restaurar um log de transações em um banco de dados (uma restauração de log de transações).  
- Reverter um banco de dados ao momento determinado capturado por um instantâneo do banco de dados.  
  
Para obter informações sobre o cenários de restauração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Visão geral da restauração e recuperação &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md). Para obter mais informações sobre descrições dos argumentos, consulte [Argumentos de RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md). Ao restaurar um banco de dados de outra instância, considere as informações descritas em [Gerenciar metadados ao disponibilizar um banco de dados em outra instância do servidor (SQL Server)](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md).
  
> [!NOTE] 
> Para obter mais informações sobre a restauração por meio do serviço de Armazenamento de Blobs do Microsoft Azure, consulte [Backup e restauração do SQL Server com o serviço de Armazenamento de Blobs do Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
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
   | , \<point_in_time_WITH_options-RESTORE_DATABASE>   
   } [ ,...n ]  
 ]  
[;]  
  
--To perform the first step of the initial restore sequence of a piecemeal restore:  
RESTORE DATABASE { database_name | @database_name_var }   
   <files_or_filegroups> [ ,...n ]  
 [ FROM <backup_device> [ ,...n ] ]   
   WITH   
      PARTIAL, NORECOVERY   
      [  , <general_WITH_options> [ ,...n ]   
       | , \<point_in_time_WITH_options-RESTORE_DATABASE>   
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
    | , \<point_in_time_WITH_options-RESTORE_LOG>   
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
 | { DISK    
     | TAPE  
     | URL   
   } = { 'physical_backup_device_name' |  
      @physical_backup_device_name_var }   
}   
Note: URL is the format used to specify the location and the file name for the Microsoft Azure Blob. Although Microsoft Azure storage is a service, the implementation is similar to disk and tape to allow for a consistent and seamless restore experience for all the three devices.  
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
  
--Tape Options. 
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
  
\<point_in_time_WITH_options-RESTORE_DATABASE>::=   
 | {  
   STOPAT = { 'datetime'| @datetime_var }   
 | STOPATMARK = 'lsn:lsn_number'  
                 [ AFTER 'datetime']   
 | STOPBEFOREMARK = 'lsn:lsn_number'  
                 [ AFTER 'datetime']   
   }   
  
\<point_in_time_WITH_options-RESTORE_LOG>::=   
 | {  
   STOPAT = { 'datetime'| @datetime_var }   
 | STOPATMARK = { 'mark_name' | 'lsn:lsn_number' }  
                 [ AFTER 'datetime']   
 | STOPBEFOREMARK = { 'mark_name' | 'lsn:lsn_number' }  
                 [ AFTER 'datetime']   
   }  
```  
  
## <a name="arguments"></a>Argumentos  
Para obter descrições dos argumentos, consulte [Argumentos de RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md).  
  
## <a name="about-restore-scenarios"></a>Sobre cenários de restauração  
O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte a vários cenários de restauração:  
  
- restauração completa do banco de dados  
  
  Restaura todo o banco de dados, começando com um backup completo do banco de dados, que pode ser seguido pela restauração de um backup diferencial do banco de dados (e backups de log). Para obter mais informações, veja [Restaurações completas de banco de dados &#40;Modelo de recuperação simples#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md) ou [Restaurações completas de banco de dados &#40;Modelo de recuperação completa#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md).  
  
- Restauração de arquivo  
  
  Restaura um arquivo ou grupo de arquivos em um banco de dados com vários grupos de arquivos. Observe que no modelo de recuperação simples, o arquivo deve pertencer a um grupo de arquivos somente leitura. Depois de uma restauração completa do arquivo, um backup de arquivo diferencial pode ser restaurado. Para obter mais informações, consulte [Restaurações de arquivo &#40;modelo de recuperação completa&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md) e [Restaurações de arquivo &#40;modelo de recuperação simples&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md).  
  
- Restauração de página  
  
  Restaura páginas individuais. A restauração de página só está disponível nos modelos de recuperação completa e bulk-logged. Para obter mais informações, veja [Restaurar páginas &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md).  
  
- Restauração por etapas  
  
  Restaura o banco de dados por etapas, começando com o grupo de arquivos primário e um ou mais grupos de arquivos secundários. Uma restauração por etapas começa com um RESTORE DATABASE, usando a opção PARTIAL e especificando um ou mais grupos de arquivos secundários a serem restaurados. Para obter mais informações, veja [Restaurações por etapas &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md).  
  
- Somente recuperação  
  
  Recupera dados que já estão consistentes com o banco de dados e só precisam ser disponibilizados. Para obter mais informações, veja [Recuperar um banco de dados sem restaurar dados &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/recover-a-database-without-restoring-data-transact-sql.md).  
  
- Restauração de log de transações.  
  
  No modelo de recuperação completa ou bulk-logged, a restauração de backups de log é exigida para alcançar o ponto de recuperação desejado. Para obter mais informações sobre backups de log de restaurações, consulte [Aplicar backups de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md).  
  
- Preparar um banco de dados de disponibilidade para um Grupo de Disponibilidade AlwaysOn  
  
  Para obter mais informações, consulte [Preparar um banco de dados secundário manualmente para um grupo de disponibilidade &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md).  
  
- Preparar um banco de dados espelho para espelhamento de banco de dados  
  
  Para obter mais informações, veja [Preparar um banco de dados espelho para espelhamento &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md).  
  
- Restauração online  
  
  > [!NOTE] 
  > A restauração online é permitida somente na edição Enterprise do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
  Quando houver suporte para a restauração online, se o banco de dados estiver online, restaurações de páginas e de arquivos serão automaticamente restaurações online e, também, restaurações de grupos de arquivos secundários após o estágio inicial de uma restauração por etapas.  
  
  > [!NOTE] 
  > As restaurações online podem envolver [transações adiadas](../../relational-databases/backup-restore/deferred-transactions-sql-server.md).  
  
  Para obter mais informações, consulte [Restauração online &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md).  
  
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
  
> [!NOTE] 
> Para um banco de dados que usa o modelo de recuperação completa ou bulk-logged, na maioria dos casos é necessário fazer backup do final do log antes da restauração do banco de dados. Restaurar um banco de dados sem antes fazer backup do final do log resultará em um erro, a não ser que a instrução RESTORE DATABASE contenha a cláusula WITH REPLACE ou WITH STOPAT, que deve especificar um momento ou transação que ocorreu após o final do backup de dados. Para obter mais informações sobre backups da parte final do log, veja [Backups da parte final do log &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md).  
  
### <a name="comparison-of-recovery-and-norecovery"></a>Comparação de RECOVERY e NORECOVERY  
A reversão é controlada pela instrução RESTORE nas opções [ RECOVERY | NORECOVERY ]:  
  
- NORECOVERY especifica que a reversão não ocorre. Isso permite que o roll forward continue com a próxima instrução na sequência.  
  
Nesse caso, a sequência de restauração pode restaurar outros backups e efetuar roll forward neles.  
  
- RECOVERY (o padrão) indica que a reversão deve ser executada após a conclusão do roll forward no backup atual.  
  
A recuperação do banco de dados exige que todo o conjunto de dados que está sendo restaurado (o *conjunto de roll forward*) seja consistente com o banco de dados. Se o conjunto de roll forward não tiver ido longe o suficiente para ficar consistente com o banco de dados e RECOVERY estiver especificado, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] emitirá um erro.  
  
## <a name="compatibility-support"></a>Suporte de compatibilidade  
Backups do **master**, **model** e **msdb** que foram criados em uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não podem ser restaurados pelo [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
> [!NOTE]
> Nenhum backup do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ser restaurado para uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a não ser na versão na qual o backup foi criado.  
  
Cada versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa um caminho padrão diferente das versões anteriores. Assim, para restaurar um banco de dados que foi criado no local padrão dos backups de versões anteriores, você deve usar a opção MOVE. Para obter informações sobre o novo caminho padrão, consulte [Locais de arquivos para instâncias padrão e nomeadas do SQL Server](../../sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md).  
  
Depois de você restaurar um banco de dados da versão anterior para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], o banco de dados será atualizado automaticamente. Normalmente, o banco de dados se torna disponível imediatamente. No entanto, se um banco de dados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] tiver índices de texto completo, o processo de atualização importará, redefinirá ou recriará esses índices, dependendo da configuração da propriedade de servidor  **upgrade_option** . Se a opção de atualização for definida como importar (**upgrade_option** = 2) ou recriar (**upgrade_option** = 0), os índices de texto completo permanecerão indisponíveis durante a atualização. Dependendo da quantidade de dados a serem indexados, a importação pode levar várias horas, e a recriação pode ser até dez vezes mais demorada. Lembre-se também de que, quando a opção de atualização estiver definida para importar, os índices de texto completo associados serão recriados se um catálogo de texto completo não estiver disponível. Para alterar a configuração da propriedade de servidor **upgrade_option** , use [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md).  
  
Quando um banco de dados é anexado ou restaurado pela primeira vez a uma nova instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], uma cópia da chave mestra de banco de dados (criptografada pela chave mestra de serviço) ainda não está armazenada no servidor. É necessário usar a instrução **OPEN MASTER KEY** para descriptografar a DMK (chave mestra do banco de dados). Após a descriptografia da DMK, você tem a opção de habilitar a descriptografia automática no futuro usando a instrução **ALTER MASTER KEY REGENERATE** para provisionar o servidor com uma cópia da DMK criptografada com a SMK (chave mestra de serviço). Quando um banco de dados for atualizado de uma versão anterior, a DMK deverá ser regenerada para usar o algoritmo AES mais recente. Para obter mais informações sobre como regenerar a DMK, veja [ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md). O tempo necessário para regenerar a chave DMK para atualizar o AES depende do número de objetos protegidos pela DMK. É necessário regenerar a chave DMK para atualizar o AES somente uma vez, isso não tem impacto sobre regenerações futuras como parte de uma estratégia de rotação de chave.  
  
## <a name="general-remarks"></a>Comentários gerais  
Durante uma restauração offline, se o banco de dados especificado estiver em uso, RESTORE forçará a saída do usuário depois de um pequeno atraso. Para restauração online de um grupo de arquivos não primário, o banco de dados pode permanecer em uso, exceto quando o grupo de arquivos que está sendo restaurado for colocado offline. Todos os dados no banco de dados especificado são substituídos pelos dados restaurados.  
  
Para obter mais informações sobre a recuperação de banco de dados, consulte [Visão geral da restauração e recuperação &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md).  
  
As operações de restauração entre plataformas, mesmo entre tipos diferentes de processadores, podem ser executadas desde que a ordenação do banco de dados tenha suporte no sistema operacional.  
  
RESTORE pode ser reiniciado depois de um erro. Além disso, você pode instruir RESTORE a prosseguir, apesar dos erros, e ele restaura o máximo possível de dados (consulte a opção CONTINUE_AFTER_ERROR).  
  
RESTORE não é permitido em uma transação explícita ou implícita.  
  
A restauração de um banco de dados **mestre** danificado é executada por meio de um procedimento especial. Para obter mais informações, consulte [Fazer backup e restaurar bancos de dados do sistema &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md).  
  
A restauração de um banco de dados limpa o cache de planos da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A limpeza do cache de planos gera uma recompilação de todos os planos de execução subsequentes e pode provocar uma redução repentina e temporária do desempenho de consultas. Para cada armazenamento em cache limpo no cache de planos, o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contém a seguinte mensagem informativa: "[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] encontrou %d ocorrências de liberação de armazenamento em cache para o armazenamento em cache '%s' (parte do cache de planos) devido a operações de reconfiguração ou manutenção do banco de dados". Essa mensagem é registrada a cada cinco minutos, contanto que o cache seja liberado dentro desse intervalo de tempo.  
  
Para restaurar um banco de dados de disponibilidade, primeiro restaure o banco de dados à instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], em seguida, adicione o banco de dados ao grupo de disponibilidade.  

## <a name="interoperability"></a>Interoperabilidade  
  
### <a name="database-settings-and-restoring"></a>Restauração e configuração do banco de dados  
Durante uma restauração, a maioria das opções do banco de dados que são configuráveis com ALTER DATABASE é redefinida com os valores em vigor no momento do término do backup.  
  
Porém, o uso da opção WITH RESTRICTED_USER substitui esse comportamento pela configuração da opção de acesso do usuário. Essa configuração sempre é definida seguindo uma instrução RESTORE que inclui a opção WITH RESTRICTED_USER.  
  
### <a name="restoring-an-encrypted-database"></a>Restaurando um banco de dados criptografado  
Para restaurar um banco de dados criptografado, é necessário ter acesso ao certificado ou à chave assimétrica usada para criptografar o banco de dados. Sem o certificado ou a chave assimétrica, o banco de dados não pode ser restaurado. Como resultado, o certificado usado para criptografar a chave de criptografia do banco de dados deverá ser retido enquanto o backup for necessário. Para obter mais informações, consulte [SQL Server Certificates and Asymmetric Keys](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md).  
  
### <a name="restoring-a-database-enabled-for-vardecimal-storage"></a>Restaurando um bancos de dados habilitado para armazenamento vardecimal  
O backup e a restauração funcionam corretamente com o formato de armazenamento **vardecimal**. Para obter mais informações sobre o formato de armazenamento **vardecimal**, consulte [sp_db_vardecimal_storage_format &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-db-vardecimal-storage-format-transact-sql.md).  
  
### <a name="restore-full-text-data"></a>Restaurar dados de texto completo  
Dados de texto completo são restaurados com outros dados do banco de dados durante uma restauração completa. Usando a sintaxe `RESTORE DATABASE database_name FROM backup_device` comum, os arquivos de texto completo são restaurados como parte da restauração de arquivo de banco de dados.  
  
A instrução RESTORE também pode ser usada para executar restaurações em locais alternados, restaurações diferenciais, restaurações de arquivos e grupos de arquivos e restaurações de arquivos e grupos de arquivos diferenciais de dados de texto completo. Além disso, RESTORE pode restaurar apenas arquivos de texto completo, assim como dados de banco de dados.  
  
> [!NOTE] 
> Catálogos de texto completo importados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ainda são tratados como arquivos de banco de dados. Nesse caso, o procedimento usado pelo [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] para fazer backup de catálogos de texto completo ainda se aplica, exceto pelo fato de que não é mais necessário pausar e retomar a operação de backup. Para obter mais informações, consulte [Fazendo backup e restaurando catálogos de texto completo](https://go.microsoft.com/fwlink/?LinkId=107381).  
  
## <a name="metadata"></a>Metadados  
O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inclui tabelas de histórico de backup e restauração que controlam a atividade de backup e restauração de cada instância de servidor. Quando uma restauração é executada, as tabelas de histórico de backup também são modificadas. Para obter informações sobre essas tabelas, consulte [Histórico de backup e informações de cabeçalho &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md).  
  
##  <a name="REPLACEoption"></a> Impacto da opção REPLACE  
REPLACE raramente deve ser usado e só depois de cuidadosa consideração. Normalmente a restauração evita a substituição acidental de um banco de dados por um banco de dados diferente. Se o banco de dados especificado em uma instrução RESTORE já existir no servidor atual e a GUID de família do banco de dados especificado for diferente da GUID de família do banco de dados registrado no conjunto de backup, o banco de dados não será restaurado. Essa é uma proteção importante.  
  
A opção REPLACE substitui várias verificações de segurança importantes que a restauração geralmente executa. As verificações substituídas são as seguintes:  
  
- Restauração de um banco de dados existente com um backup tirado de outro banco de dados.  
  
  Com a opção REPLACE, a restauração permite que você substitua um banco de dados existente por qualquer banco de dados do conjunto de backup, mesmo que o nome do banco de dados especificado seja diferente do nome de banco de dados registrado no conjunto de backup. Isso pode resultar na substituição acidental de um banco de dados por um banco de dados diferente.  
  
- Restauração de um banco de dados que usa o modelo de recuperação bulk-logged onde um backup do final do log não foi feito e a opção STOPAT não é usada.  
  
  Com a opção REPLACE, você pode perder trabalho confirmado porque não foi feito backup do log gravado mais recentemente.  
  
- Substituição de arquivos existentes.  
  
  Por exemplo, um engano poderia permitir a substituição de arquivos do tipo errado, como arquivos .xls, ou que estivessem sendo usados por outro banco de dados que não estivesse online. A perda de dados arbitrária é possível se arquivos existentes forem substituídos, embora o banco de dados restaurado esteja completo.  
  
## <a name="redoing-a-restore"></a>Refazendo uma restauração  
Não é possível desfazer os efeitos de uma restauração; no entanto, você pode recusar os efeitos de roll forward e de cópia dos dados reiniciando em uma base de um arquivo por vez. Para recomeçar, restaure o arquivo desejado e execute o roll forward novamente. Por exemplo, se você restaurou muitos backups de log acidentalmente e excedeu o ponto de parada pretendido, reinicie a sequência.  
  
Uma sequência de restauração pode ser anulada e reiniciada com a restauração de todo o conteúdo dos arquivos afetados.  
  
## <a name="reverting-a-database-to-a-database-snapshot"></a>Revertendo um banco de dados para um instantâneo de banco de dados  
Uma *operação de reversão de banco de dados* (especificada com a opção DATABASE_SNAPSHOT) reverte um banco de dados de origem completo, revertendo-o para o momento de um instantâneo do banco de dados, ou seja, com a substituição do banco de dados de origem pelos dados do momento específico mantidos no instantâneo do banco de dados especificado. Só o instantâneo para o qual você está revertendo pode existir atualmente. A operação de reversão, então, reconstrói o log (portanto, você não poderá efetuar roll forward em um banco de dados revertido até o ponto do erro do usuário).  
  
A perda de dados é limitada às atualizações no banco de dados desde a criação do instantâneo. Os metadados de um banco de dados revertido são iguais aos metadados no momento da criação do instantâneo. No entanto, a reversão para um instantâneo descarta todos os catálogos de texto completo.  
  
A reversão a partir de um instantâneo do banco de dados não é destinada à recuperação de mídia. Ao contrário de um conjunto de backup regular, o instantâneo de banco de dados é uma cópia incompleta dos arquivos do banco de dados. Se o banco de dados ou o instantâneo do banco de dados está corrompido, é provável que a reversão a partir de um instantâneo seja impossível. Além disso, mesmo quando possível, é improvável que a reversão corrija o problema no caso de corrupção.  
  
### <a name="restrictions-on-reverting"></a>Restrições na reversão  
Não há suporte para a reversão nas seguintes condições:  
  
- O banco de dados de origem contém algum grupo de arquivos somente leitura ou compactado.  
- Há algum arquivo offline que estava online quando o instantâneo foi criado.  
- Existe mais de um instantâneo do banco de dados atualmente.  
  
Para obter mais informações, consulte [Reverter um banco de dados para um instantâneo do banco de dados](../../relational-databases/databases/revert-a-database-to-a-database-snapshot.md).  
  
## <a name="security"></a>Segurança  
Uma operação de backup pode, opcionalmente, especificar senhas para um conjunto de mídias, um conjunto de backup ou ambos. Quando uma senha tiver sido definida em um conjunto de backup ou de mídias, será preciso especificar a senha ou as senhas corretas na instrução RESTORE. Essas senhas impedem operações de restauração não autorizadas e anexações não autorizadas de conjuntos de backup para mídia usando ferramentas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Porém, mídia protegida por senha pode ser substituída pela opção FORMAT da instrução BACKUP.  
  
> [!IMPORTANT]  
>  A proteção fornecida por esta senha é fraca. Destina-se a evitar uma restauração incorreta com o uso de ferramentas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por usuários autorizados ou não autorizados. Não impede a leitura dos dados de backup por outros meios ou a substituição da senha. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]A melhor prática para proteger backups é armazenar as fitas de backup em um local seguro ou fazer backup em arquivos de disco protegidos por ACLs (listas de controle de acesso) adequadas. As ACLs devem ser definidas no diretório raiz em que os backups são criados.  
   
> [!NOTE]
> Para obter informações específicas sobre o backup e a restauração do SQL Server com o Armazenamento de Blobs do Microsoft Azure, consulte [Backup e restauração do SQL Server com o serviço de Armazenamento de Blobs do Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  
  
### <a name="permissions"></a>Permissões  
Se o banco de dados que está sendo restaurado não existir, o usuário deverá ter permissões CREATE DATABASE para poder executar o comando RESTORE. Se o banco de dados existir, as permissões RESTORE usarão como padrão os membros das funções de servidor fixas **sysadmin** e **dbcreator** e o proprietário (**dbo**) do banco de dados (para a opção FROM DATABASE_SNAPSHOT, o banco de dados sempre existe).  
  
As permissões RESTORE são concedidas a funções nas quais as informações de associação estão sempre disponíveis para o servidor. Como a associação da função de banco de dados fixa pode ser verificada apenas quando o banco de dados está acessível e não danificado, o que nem sempre é o caso quando RESTORE é executado, os membros da função de banco de dados fixa **db_owner** não têm permissões RESTORE.  
  
##  <a name="examples"></a> Exemplos  
Todos os exemplos presumem que um backup de banco de dados completo foi executado.  
  
Os exemplos de RESTORE incluem o seguinte:  
  
- A. [Restaurando um banco de dados completo](#restoring_full_db)  
- b. [Restaurando backups de banco de dados diferenciais e completos](#restoring_full_n_differential_db_backups)  
- C. [Restaurando um banco de dados usando a sintaxe RESTART](#restoring_db_using_RESTART)  
- D. [Restaurando um banco de dados e movendo arquivos](#restoring_db_n_move_files)  
- E. [Copiando um banco de dados usando BACKUP e RESTORE](#copying_db_using_bnr)  
- F. [Restauração pontual usando STOPAT](#restoring_to_pit_using_STOPAT)  
- G. [Restaurando o log de transações até uma marca](#restoring_transaction_log_to_mark)  
- H. [Restaurando com a sintaxe de TAPE](#restoring_using_TAPE)  
- I. [Restaurando com a sintaxe de FILE e FILEGROUP](#restoring_using_FILE_n_FG)  
- J. [Revertendo de um instantâneo do banco de dados](#reverting_from_db_snapshot)  
- K. [Restaurando do serviço de Armazenamento de Blobs do Microsoft Azure](#Azure_Blob)  
  
> [!NOTE] 
> Para obter outros exemplos, consulte os tópicos de instruções de restauração listados em [Visão geral de recuperação e restauração &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md).  
  
###  <a name="restoring_full_db"></a> A. Restaurando um banco de dados completo  
O exemplo a seguir restaura um backup de banco de dados completo do dispositivo de backup lógico `AdventureWorksBackups`. Para obter um exemplo de como criar esse dispositivo, consulte [Dispositivos de backup](../../relational-databases/backup-restore/backup-devices-sql-server.md).  
  
```sql  
RESTORE DATABASE AdventureWorks2012   
   FROM AdventureWorks2012Backups;  
```  
  
> [!NOTE] 
> Para um banco de dados que usa o modelo de recuperação completa ou bulk-logged, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requer que se faça backup do final do log antes da restauração do banco de dados. Para obter mais informações, veja [Backups da parte final do log &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md).  
  
[&#91;Início dos exemplos&#93;](#examples)  
  
###  <a name="restoring_full_n_differential_db_backups"></a> B. Restaurando backups de banco de dados diferenciais e completos  
O exemplo a seguir restaura um backup de banco de dados completo seguido por um backup diferencial do dispositivo de backup `Z:\SQLServerBackups\AdventureWorks2012.bak`, que contém os dois backups. O backup de banco de dados completo a ser restaurado é o sexto conjunto de backup no dispositivo (`FILE = 6`), e o backup de banco de dados diferencial é o nono no dispositivo (`FILE = 9`). Assim que o backup diferencial é recuperado, o banco de dados é recuperado.  
  
```sql  
RESTORE DATABASE AdventureWorks2012  
   FROM DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak'  
   WITH FILE = 6  
      NORECOVERY;  
RESTORE DATABASE AdventureWorks2012  
   FROM DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak'  
   WITH FILE = 9  
      RECOVERY;  
```  
  
[&#91;Início dos exemplos&#93;](#examples)  
  
###  <a name="restoring_db_using_RESTART"></a> C. Restaurando um banco de dados usando a sintaxe RESTART  
O exemplo a seguir usa a opção `RESTART` para reiniciar uma operação `RESTORE` interrompida por uma deficiência de força no servidor.  
  
```sql  
-- This database RESTORE halted prematurely due to power failure.  
RESTORE DATABASE AdventureWorks2012  
   FROM AdventureWorksBackups;  
-- Here is the RESTORE RESTART operation.  
RESTORE DATABASE AdventureWorks2012   
   FROM AdventureWorksBackups WITH RESTART;  
```  
  
[&#91;Início dos exemplos&#93;](#examples)  
  
###  <a name="restoring_db_n_move_files"></a> D. Restaurando um banco de dados e movendo arquivos  
O exemplo a seguir restaura um banco de dados completo e log de transações e move o banco de dados restaurado para o diretório `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data`.  
  
```sql  
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
  
[&#91;Início dos exemplos&#93;](#examples)  
  
###  <a name="copying_db_using_bnr"></a> E. Copiando um banco de dados usando BACKUP e RESTORE  
O exemplo a seguir usa as instruções `BACKUP` e `RESTORE` para fazer uma cópia do banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. A instrução `MOVE` causa a restauração dos dados e do arquivo de log nos locais especificados. A instrução `RESTORE FILELISTONLY` é usada para determinar o número e os nomes dos arquivos no banco de dados que está sendo restaurado. A nova cópia do banco de dados é nomeada `TestDB`. Para obter mais informações, veja [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md).  
  
```sql  
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
  
[&#91;Início dos exemplos&#93;](#examples)  
  
###  <a name="restoring_to_pit_using_STOPAT"></a> F. Restauração pontual usando STOPAT  
O exemplo a seguir restaura um banco de dados para seu estado de `12:00 AM` em `April 15, 2020` e mostra uma operação de restauração que envolve vários backups de log. No dispositivo de backup, `AdventureWorksBackups`, o backup de banco de dados completo a ser restaurado é o terceiro conjunto de backup no dispositivo (`FILE = 3`), o primeiro backup de log é o quarto conjunto de backup (`FILE = 4`), e o segundo backup de log é o quinto conjunto de backup (`FILE = 5`).  
  
```sql  
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
  
[&#91;Início dos exemplos&#93;](#examples)  
  
###  <a name="restoring_transaction_log_to_mark"></a> G. Restaurando o log de transações até uma marca  
O exemplo a seguir restaura o log de transações até a marca na transação marcada denominada `ListPriceUpdate`.  
  
```sql  
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
  
[&#91;Início dos exemplos&#93;](#examples)  
  
###  <a name="restoring_using_TAPE"></a> H. Restaurando com o uso da sintaxe de TAPE  
O exemplo a seguir restaura um backup de banco de dados completo de um dispositivo de backup `TAPE`.  
  
```sql  
RESTORE DATABASE AdventureWorks2012   
   FROM TAPE = '\\.\tape0';  
```  
  
[&#91;Início dos exemplos&#93;](#examples)  
  
###  <a name="restoring_using_FILE_n_FG"></a> I. Restaurando usando a sintaxe FILE e FILEGROUP  
O exemplo a seguir restaura um banco de dados nomeado `MyDatabase` que tem dois arquivos, um grupo de arquivos secundário e um log de transações. O banco de dados usa o modelo de recuperação completa.  
  
O backup do banco de dados é o nono conjunto de backup no conjunto de mídias em um dispositivo de backup lógico nomeado `MyDatabaseBackups`. Depois, três backups de log, que estão nos próximos três conjuntos de backup (`10`, `11` e `12`) no dispositivo `MyDatabaseBackups`, são restaurados usando `WITH NORECOVERY`. Depois de restaurar o último backup de log, o banco de dados é recuperado.  
  
> [!NOTE] 
> A recuperação é executada como uma etapa separada para reduzir a possibilidade de recuperação antecipada, antes que todos os backups de log tenham sido restaurados.  
  
No `RESTORE DATABASE`, observe que há dois tipos de opções de `FILE`. As opções `FILE` que precedem o nome do dispositivo de backup especificam os nomes de arquivos lógicos dos arquivos de banco de dados restaurados do conjunto de backup; por exemplo, `FILE = 'MyDatabase_data_1'`. Esse conjunto de backups não é o primeiro backup de banco de dados no conjunto de mídias; portanto, sua posição no conjunto de mídias é indicada com a opção `FILE` na cláusula `WITH`, `FILE=9`.  
  
```sql  
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
  
[&#91;Início dos exemplos&#93;](#examples)  
  
###  <a name="reverting_from_db_snapshot"></a> J. Revertendo de um instantâneo do banco de dados  
O exemplo a seguir reverte um banco de dados para um instantâneo do banco de dados. O exemplo presume que existe apenas um instantâneo atualmente no banco de dados. Para obter um exemplo de como criar esse instantâneo do banco de dados, consulte [Criar um instantâneo do banco de dados &#40;Transact-SQL&#41;](../../relational-databases/databases/create-a-database-snapshot-transact-sql.md).  
  
> [!NOTE] 
> A reversão para um instantâneo descarta todos os catálogos de texto completo.  
  
```sql  
USE master;    
RESTORE DATABASE AdventureWorks2012 FROM DATABASE_SNAPSHOT = 'AdventureWorks_dbss1800';  
GO  
```  
Para obter mais informações, consulte [Reverter um banco de dados para um instantâneo do banco de dados](../../relational-databases/databases/revert-a-database-to-a-database-snapshot.md).  

[&#91;Início dos exemplos&#93;](#examples)  
  
###  <a name="Azure_Blob"></a> K. Restaurando do serviço de Armazenamento de Blobs do Microsoft Azure  
Os três exemplos abaixo envolvem o uso do serviço de Armazenamento do Microsoft Azure.  O nome da Conta de armazenamento é `mystorageaccount`.  O contêiner para arquivos de dados é chamado `myfirstcontainer`.  O contêiner para arquivos de backup é chamado `mysecondcontainer`.  Uma política de acesso armazenada foi criada com direitos de leitura, gravação, exclusão e lista para cada contêiner.  As credenciais do SQL Server foram criadas usando Assinaturas de Acesso Compartilhado que estão associadas às Políticas de Acesso Armazenado.  Para obter informações específicas sobre o backup e a restauração do SQL Server com o Armazenamento de Blobs do Microsoft Azure, consulte [Backup e restauração do SQL Server com o serviço de Armazenamento de Blobs do Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  

**K1.  Restaurar um backup de banco de dados completo do serviço de Armazenamento do Microsoft Azure**  
Um backup de banco de dados completo, localizado em `mysecondcontainer`, de `Sales` será restaurado no `myfirstcontainer`.  Atualmente, o `Sales` não existe no servidor. 

```sql
RESTORE DATABASE Sales
  FROM URL = 'https://mystorageaccount.blob.core.windows.net/mysecondcontainer/Sales.bak'   
  WITH  MOVE 'Sales_Data1' to 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer/Sales_Data1.mdf', 
  MOVE 'Sales_log' to 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer/Sales_log.ldf', 
  STATS = 10;
```

**K2. Restaurar um backup de banco de dados completo do serviço de Armazenamento do Microsoft Azure para o armazenamento local**  
Um backup de banco de dados completo, localizado em `mysecondcontainer`, de `Sales` será restaurado no armazenamento local.  Atualmente, o `Sales` não existe no servidor.

```sql
RESTORE DATABASE Sales
  FROM URL = 'https://mystorageaccount.blob.core.windows.net/mysecondcontainer/Sales.bak'   
  WITH  MOVE 'Sales_Data1' to 'H:\DATA\Sales_Data1.mdf', 
  MOVE 'Sales_log' to 'O:\LOG\Sales_log.ldf', 
  STATS = 10;
```
  
**K3. Restaurar um backup de banco de dados completo do armazenamento local para o serviço de Armazenamento do Microsoft Azure**  
```sql
RESTORE DATABASE Sales
  FROM DISK = 'E:\BAK\Sales.bak'
  WITH  MOVE 'Sales_Data1' to 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer/Sales_Data1.mdf', 
  MOVE 'Sales_log' to 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer/Sales_log.ldf', 
  STATS = 10;
```  
  

  
[&#91;Início dos exemplos&#93;](#examples)  
  
## <a name="much-more-information"></a>Muito mais informações!  
- [Fazer backup e restaurar bancos de dados do SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md) 
- [Fazer backup e restaurar bancos de dados do sistema (SQL Server)](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md) 
- [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)
- [Fazer backup e restaurar índices e catálogos de texto completo](../../relational-databases/search/back-up-and-restore-full-text-catalogs-and-indexes.md)   
- [Fazer backup e restaurar bancos de dados replicados](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
- [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
- [Conjuntos de mídias, famílias de mídia e conjuntos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
- [RESTORE REWINDONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)   
- [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)   
- [RESTORE FILELISTONLY (Transact-SQL)](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)  
- [RESTORE HEADERONLY (Transact-SQL)](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)  
- [Informações de histórico e cabeçalho de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)  
  
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"

> [!div class="mx-tdCol2BreakAll"]
> ||||
> |-|-|-|
> |[SQL Server](restore-statements-transact-sql.md?view=sql-server-2016)|**_\* Banco de Dados SQL<br />Instância Gerenciada \*_**|[Parallel<br />Data Warehouse](restore-statements-transact-sql.md?view=aps-pdw-2016)

&nbsp;

## <a name="azure-sql-database-managed-instance"></a>Instância Gerenciada do Banco de Dados SQL do Azure

Esse comando permite restaurar um banco de dados inteiro de um backup de banco de dados completo (uma restauração completa) da conta do Armazenamento de Blobs do Azure.

Para outros comandos RESTORE com suporte, consulte:
- [RESTORE FILELISTONLY (Transact-SQL)](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)  
- [RESTORE HEADERONLY (Transact-SQL)](../../t-sql/statements/restore-statements-headeronly-transact-sql.md) 
- [RESTORE LABELONLY ONLY (Transact-SQL)](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)
- [RESTORE VERIFYONLY (Transact-SQL)](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)   

> [!IMPORTANT]
> Para restaurar por meio de backups automáticos da Instância Gerenciada do Banco de Dados SQL do Azure, consulte [Restauração do Banco de Dados SQL](https://docs.microsoft.com/azure/sql-database/sql-database-recovery-using-backups).
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
--To Restore an Entire Database from a Full database backup (a Complete Restore):  
RESTORE DATABASE { database_name | @database_name_var }   
 FROM URL = { 'physical_device_name' | @physical_device_name_var } [ ,...n ]   
[;]  
  
```  
   
## <a name="arguments"></a>Argumentos  

DATABASE  
  
Especifica o banco de dados de destino.  
  
FROM URL

Especifica um ou mais dispositivos de backup colocados em URLs que serão usados para a operação de restauração. O formato da URL é usado para restaurar os backups do serviço de armazenamento do Microsoft Azure. 

> [!IMPORTANT]  
> Para fazer uma restauração de vários dispositivos ao restaurar de uma URL, é necessário usar os tokens SAS (Assinatura de Acesso Compartilhado). Para obter exemplos sobre como criar uma Assinatura de Acesso Compartilhado, consulte [Backup do SQL Server em uma URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md) e [Simplificando a criação de credenciais do SQL com tokens SAS (Assinatura de Acesso Compartilhado) no Armazenamento do Azure com o PowerShell](https://blogs.msdn.com/b/sqlcat/archive/2015/03/21/simplifying-creation-sql-credentials-with-shared-access-signature-sas-keys-on-azure-storage-containers-with-powershell.aspx).  
  
*n*  
É um espaço reservado que indica que até 64 dispositivos de backup podem ser especificados em uma lista separada por vírgulas.  
 
## <a name="general-remarks"></a>Comentários gerais

Como pré-requisito, você precisa criar uma credencial com o nome que corresponda à URL da conta de armazenamento de blobs, e colocar a Assinatura de Acesso Compartilhado como secreta. O comando RESTORE pesquisará as credenciais usando a URL de armazenamento de blobs para localizar as informações necessárias para ler o dispositivo de backup.

A operação RESTORE é assíncrona: a restauração continua mesmo se a conexão de cliente é interrompida. Se sua conexão for interrompida, será possível marcar a exibição [sys.dm_operation_status](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md) para o status de uma operação de restauração (bem como para o banco de dados CREATE e DROP). 

As opções de banco de dados a seguir são definidas/substituídas e não podem ser alteradas posteriormente:

- NEW_BROKER (se o agente não estiver habilitado no arquivo .bak)
- ENABLE_BROKER (se o agente não estiver habilitado no arquivo .bak)
- AUTO_CLOSE=OFF (se um banco de dados no arquivo .bak tiver AUTO_CLOSE=ON)
- RECOVERY FULL (se um banco de dados no arquivo .bak tiver modo de recuperação SIMPLE ou BULK_LOGGED)
- O grupo de arquivos otimizado para memória será adicionado e o XTP, chamado, se ele não estiver no arquivo .bak de origem. Qualquer grupo de arquivos otimizado para memória existente é renomeado para XTP
- As opções SINGLE_USER e RESTRICTED_USER são convertidas em MULTI_USER

## <a name="limitations---sql-database-managed-instance"></a>Limitações – Instância Gerenciada do Banco de Dados SQL
Estas limitações se aplicam:

- Arquivos .BAK que contêm vários conjuntos de backup não podem ser restaurados.
- Arquivos .BAK que contêm vários arquivos de log não podem ser restaurados.
- A restauração falhará se o .bak contiver dados FILESTREAM.
- Os backups que contêm banco de dados que têm objetos na memória ativos não podem ser restaurados em uma instância gerenciada de Uso Geral.
- Os backups que contêm bancos de dados em modo somente leitura não podem ser restaurados no momento. Essa limitação será removida em breve.

Para obter mais informações, consulte [Instância gerenciada](/azure/sql-database/sql-database-managed-instance)

## <a name="restoring-an-encrypted-database"></a>Restaurando um banco de dados criptografado  
Para restaurar um banco de dados criptografado, é necessário ter acesso ao certificado ou à chave assimétrica usada para criptografar o banco de dados. Sem o certificado ou a chave assimétrica, o banco de dados não pode ser restaurado. Como resultado, o certificado usado para criptografar a chave de criptografia do banco de dados deverá ser retido enquanto o backup for necessário. Para obter mais informações, consulte [SQL Server Certificates and Asymmetric Keys](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md).  
    
## <a name="permissions"></a>Permissões  
O usuário deve ter permissões CREATE DATABASE para poder executar RESTORE.  
```
CREATE LOGIN mylogin WITH PASSWORD = 'Very Strong Pwd123!';
GRANT CREATE ANY DATABASE TO [mylogin];
```  
As permissões RESTORE são concedidas a funções nas quais as informações de associação estão sempre disponíveis para o servidor. Como a associação da função de banco de dados fixa pode ser verificada apenas quando o banco de dados está acessível e não danificado, o que nem sempre é o caso quando RESTORE é executado, os membros da função de banco de dados fixa **db_owner** não têm permissões RESTORE.  
  
##  <a name="examples"></a> Exemplos  
Os exemplos a seguir restauram um backup de banco de dados somente de cópia por meio da URL, incluindo a criação de uma credencial.  
  
###  <a name="restore-mi-database"></a> A. Restaure o banco de dados de quatro dispositivos de backup.   
```sql

-- Create credential
CREATE CREDENTIAL [https://mybackups.blob.core.windows.net/wide-world-importers]
WITH IDENTITY = 'SHARED ACCESS SIGNATURE',
       SECRET = 'sv=2017-11-09&ss=bq&srt=sco&sp=rl&se=2022-06-19T22:41:07Z&st=2018-06-01T14:41:07Z&spr=https&sig=s7wddcf0w%3D';
GO
-- Restore database
RESTORE DATABASE WideWorldImportersStandard
FROM URL = N'https://mybackups.blob.core.windows.net/wide-world-importers/00-WideWorldImporters-Standard.bak',
URL = N'https://mybackups.blob.core.windows.net/wide-world-importers/01-WideWorldImporters-Standard.bak',
URL = N'https://mybackups.blob.core.windows.net/wide-world-importers/02-WideWorldImporters-Standard.bak',
URL = N'https://mybackups.blob.core.windows.net/wide-world-importers/03-WideWorldImporters-Standard.bak'
```
O erro a seguir é mostrado se o banco de dados já existe:
```
Msg 1801, Level 16, State 1, Line 9
Database 'WideWorldImportersStandard' already exists. Choose a different database name.
```
###  <a name="restore-mi-database-variables"></a> B. Restaure o banco de dados especificado por meio da variável.  

```
DECLARE @db_name sysname = 'WideWorldImportersStandard';
DECLARE @url nvarchar(400) = N'https://mybackups.blob.core.windows.net/wide-world-importers/WideWorldImporters-Standard.bak';

RESTORE DATABASE @db_name 
FROM URL = @url
```  

### <a name="restore-mi-database-progress"></a> C. Acompanhe o progresso da instrução restore. 

```
SELECT  query = a.text, start_time, percent_complete,
        eta = dateadd(second,estimated_completion_time/1000, getdate()) 
FROM sys.dm_exec_requests r
    CROSS APPLY sys.dm_exec_sql_text(r.sql_handle) a 
WHERE r.command = 'RESTORE DATABASE'
```

> [!Note]
> Esta exibição provavelmente mostra duas solicitações de restore. Uma é a instrução RESTORE original enviada pelo cliente e a outra é a instrução RESTORE em segundo plano que está sendo executada, mesmo se houver falha na conexão do cliente.

::: moniker-end
::: moniker range=">=aps-pdw-2016||=sqlallproducts-allversions"

> [!div class="mx-tdCol2BreakAll"]
> ||||
> |-|-|-|
> |[SQL Server](restore-statements-transact-sql.md?view=sql-server-2016)|[Banco de Dados SQL<br />Instância Gerenciada](restore-statements-transact-sql.md?view=azuresqldb-mi-current)|**_\* Parallel<br />Data Warehouse \*_**

&nbsp;

## <a name="parallel-data-warehouse"></a>Parallel Data Warehouse


Restaura um banco de dados de usuário do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] por meio de um backup de banco de dados em um dispositivo do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. O banco de dados é restaurado por meio de um backup que foi criado anteriormente pelo comando [!INCLUDE[ssPDW](../../includes/sspdw-md.md)][BACKUP DATABASE &#40;Parallel Data Warehouse&#41;](../../t-sql/statements/backup-transact-sql.md). Use as operações de backup e restauração para criar um plano de recuperação de desastre ou mover bancos de dados de um dispositivo para outro.  
  
> [!NOTE]  
>  A restauração do mestre inclui a restauração das informações de logon do dispositivo. Para restaurar um mestre, use a página [Restaurar o banco de dados mestre &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-the-master-database-transact-sql.md) da ferramenta **Configuration Manager**. Um administrador com acesso ao nó de Controle pode executar essa operação.  
Para obter mais informações sobre backups de banco de dados do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], confira "Backup e restauração" no [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
  
-- Restore the master database  
-- Use the Configuration Manager tool.  
  
Restore a full user database backup.  
RESTORE DATABASE database_name   
    FROM DISK = '\\UNC_path\full_backup_directory'  
[;]  
  
--Restore a full user database backup and then a differential backup.  
RESTORE DATABASE database_name  
    FROM DISK = '\\UNC_path\differential_backup_directory'   
    WITH [ ( ] BASE = '\\UNC_path\full_backup_directory' [ ) ]   
[;]  
  
--Restore header information for a full or differential user database backup.  
RESTORE HEADERONLY   
    FROM DISK = '\\UNC_path\backup_directory'  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
RESTORE DATABASE *database_name*  
Especifica para restaurar um banco de dados de usuário para um banco de dados chamado *database_name*. O banco de dados restaurado pode ter um nome diferente do banco de dados de origem que foi copiado em backup. *database_name* ainda não pode existir como um banco de dados no dispositivo de destino. Para obter mais detalhes sobre nomes de banco de dados permitidos, consulte "Regras de nomenclatura de objeto" no [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
A restauração de um banco de dados de usuário restaura um backup de banco de dados completo e, opcionalmente, em seguida, restaura um backup diferencial no dispositivo. Uma restauração de um banco de dados de usuário inclui a restauração de usuários e funções de banco de dados.  
  
FROM DISK = '\\\\*UNC_path*\\*backup_directory*'  
O caminho de rede e o diretório do qual o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] restaurará os arquivos de backup. Por exemplo, FROM DISK = '\\\xxx.xxx.xxx.xxx\backups\2012\Monthly\08.2012.Mybackup'.  
  
*backup_directory*  
Especifica o nome de um diretório que contém o backup completo ou diferencial. Por exemplo, você pode executar uma operação RESTORE HEADERONLY em um backup completo ou diferencial.  
  
*full_backup_directory*  
Especifica o nome de um diretório que contém o backup completo.  
  
*differential_backup_directory*  
Especifica o nome do diretório que contém o backup diferencial.  
  
- O caminho e o diretório de backup já devem existir e devem ser especificados como um caminho UNC (convenção de nomenclatura de universal) totalmente qualificado.  
- O caminho para o diretório de backup não pode ser um caminho local e não pode ser um local em um dos nós de dispositivo do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
- O tamanho máximo do caminho UNC e do nome do diretório de backup é de 200 caracteres.  
- O servidor ou o host precisa ser especificado como um endereço IP.  
  
RESTORE HEADERONLY  
Especifica para retornar somente as informações de cabeçalho para um backup de banco de dados de usuário. Entre os outros campos, o cabeçalho inclui a descrição do texto do backup e o nome do backup. O nome do backup não precisa ter o mesmo nome do diretório que armazena os arquivos de backup.  
  
Os resultados de RESTORE HEADERONLY seguem o mesmo padrão dos resultados de RESTORE HEADERONLY do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O resultado tem mais de 50 colunas, e nem todas são usadas pelo [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. Para obter uma descrição das colunas nos resultados de RESTORE HEADERONLY do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
Requer a permissão **CREATE ANY DATABASE**.  
  
Exige uma conta do Windows que tem permissão para acessar e ler por meio do diretório de backup. O nome de conta do Windows e a senha também precisam ser armazenados no [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
- Para verificar se as credenciais já estão nesse local, use [sys.dm_pdw_network_credentials &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md).  
- Para adicionar ou atualizar as credenciais, use [sp_pdw_add_network_credentials &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md).  
- Para remover credenciais do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use [sp_pdw_remove_network_credentials &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md).  
  
## <a name="error-handling"></a>Tratamento de erros  
O comando RESTORE DATABASE resulta em erros nas seguintes condições:  
  
- O nome do banco de dados a ser restaurado já existe no dispositivo de destino. Para evitar isso, escolha um nome exclusivo de banco de dados ou remova o banco de dados existente antes de executar a restauração.  
- Há um conjunto inválido de arquivos de backup no diretório de backup.  
- As permissões de logon não são suficientes para restaurar um banco de dados.  
- O [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] não tem as permissões corretas para o local de rede em que os arquivos de backup estão localizados.  
- O local de rede para o diretório de backup não existe ou não está disponível.  
- Não há espaço em disco suficiente nos nós de Computação ou no nó de Controle. O [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] não confirma se o espaço em disco suficiente existe no dispositivo antes de iniciar a restauração. Portanto, é possível gerar um erro de espaço em disco insuficiente ao executar a instrução RESTORE DATABASE. Quando não há espaço em disco suficiente, o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] reverte a restauração.  
- O dispositivo de destino no qual o banco de dados está sendo restaurado tem menos nós de Computação que o dispositivo de origem do qual o banco de dados foi copiado em backup.  
- Houve uma tentativa de restauração do banco de dados em uma transação.  
  
## <a name="general-remarks"></a>Comentários gerais  
[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] acompanha o êxito das restaurações do banco de dados. Antes de restaurar um backup de banco de dados diferencial, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] verifica se a restauração do banco de dados completo foi concluída com êxito.  
  
Após uma restauração, o banco de dados de usuário terá o nível de compatibilidade 120 do banco de dados. Isso é verdadeiro para todos os bancos de dados, seja qual for seu nível de compatibilidade original.  
  
**Restaurando para um dispositivo com um número maior de nós de Computação**  
Execute [DBCC SHRINKLOG (SQL Data Warehouse do Azure)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md) depois de restaurar um banco de dados de um dispositivo menor até o maior, pois a redistribuição aumentará o log de transações.  

A restauração de um backup em um dispositivo com um número maior de nós de Computação aumenta o tamanho do banco de dados alocado proporcionalmente ao número de nós de Computação.  
  
Por exemplo, ao restaurar um banco de dados de 60 GB de um dispositivo de 2 nós (30 GB por nó) em um dispositivo de 6 nós, o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] cria um banco de dados de 180 GB (6 nós com 30 GB por nó) no dispositivo de 6 nós. Inicialmente, o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] restaura o banco de dados em dois nós para que isso corresponda à configuração de origem e, em seguida, redistribui os dados para todos os seis nós.  
  
Após a redistribuição, cada nó de Computação conterá menos dados reais e mais espaço livre do que cada nó de Computação no dispositivo de origem menor. Use o espaço adicional para adicionar mais dados ao banco de dados. Se o tamanho do banco de dados restaurado for maior do que o necessário, use [ALTER DATABASE &#40;Parallel Data Warehouse&#41;](../../t-sql/statements/alter-database-transact-sql.md?&tabs=sqlpdw) para reduzir os tamanhos de arquivos de banco de dados.  
  
## <a name="limitations-and-restrictions"></a>Limitações e Restrições  
Para essas limitações e restrições, o dispositivo de origem é o dispositivo por meio do qual o backup do banco de dados foi criado e o dispositivo de destino é o dispositivo no qual o banco de dados será restaurado.  
  
- A restauração de um banco de dados não recompila as estatísticas automaticamente.  
- Apenas uma instrução RESTORE DATABASE ou BACKUP DATABASE pode ser executada no dispositivo em determinado momento. Se várias instruções de backup e restauração forem enviadas simultaneamente, o dispositivo as colocará em uma fila e as processará uma por vez.  
- Apenas é possível restaurar um backup de banco de dados em um dispositivo de destino do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] que tenha o mesmo número ou mais nós de Computação do que o dispositivo de origem. O dispositivo de destino não pode ter menos nós de Computação que o dispositivo de origem.  
- Não é possível restaurar um backup que foi criado em um dispositivo que tem o hardware do SQL Server 2012 PDW em um dispositivo que tem o hardware do SQL Server 2008 R2. Isso se aplica mesmo se o dispositivo foi adquirido originalmente com o hardware do SQL Server 2008 R2 PDW e agora executa o software do SQL Server 2012 PDW.  
  
## <a name="locking"></a>Bloqueio  
Usa um bloqueio exclusivo no objeto DATABASE.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-simple-restore-examples"></a>A. Exemplos simples de RESTORE  
O exemplo a seguir restaura um backup completo para o banco de dados do `SalesInvoices2013`. Os arquivos de backup são armazenados no diretório \\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full. O banco de dados SalesInvoices2013 ainda não pode existir no dispositivo de destino ou esse comando falhará com um erro.  
  
```sql  
RESTORE DATABASE SalesInvoices2013  
FROM DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full';  
```  
  
### <a name="b-restore-a-full-and-differential-backup"></a>b. Restaurar um backup completo e diferencial  
O exemplo a seguir restaura um backup completo e, em seguida, um backup diferencial para o banco de dados SalesInvoices2013  
  
O backup completo do banco de dados é restaurado do backup completo que está armazenado no diretório '\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full'. Se a restauração for concluída com êxito, o backup diferencial será restaurado no banco de dados SalesInvoices2013.  O backup diferencial é armazenado no diretório '\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff'.  
  
```sql  
RESTORE DATABASE SalesInvoices2013  
    FROM DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff'  
    WITH BASE = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full'  
[;]  
  
```  
  
### <a name="c-restoring-the-backup-header"></a>C. Restaurando o cabeçalho do backup  
Este exemplo restaura as informações de cabeçalho para o backup de banco de dados '\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full'. Os resultados do comando em uma linha de informações para o backup de Invoices2013Full.  
  
```sql  
RESTORE HEADERONLY  
    FROM DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full'  
[;]  
```  
  
Use as informações de cabeçalho para verificar o conteúdo de um backup ou para garantir que o dispositivo de restauração de destino é compatível com o dispositivo de backup de origem antes de tentar restaurar o backup.  
  
## <a name="see-also"></a>Consulte Também  
[BACKUP DATABASE &#40;Parallel Data Warehouse&#41;](../../t-sql/statements/backup-transact-sql.md)  

::: moniker-end
