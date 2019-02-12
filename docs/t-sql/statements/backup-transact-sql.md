---
title: BACKUP (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/02/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- BACKUP_TSQL
- BACKUP
- BACKUP_DATABASE_TSQL
- BACKUP_LOG_TSQL
- BACKUP LOG
- BACKUP DATABASE
dev_langs:
- TSQL
helpviewer_keywords:
- backup media [SQL Server], BACKUP statement
- backing up filegroups [SQL Server]
- backup file formats [SQL Server]
- backups [SQL Server]
- database backups [SQL Server], BACKUP statement
- multifamily media sets [SQL Server]
- mirrored media sets [SQL Server]
- backing up files [SQL Server]
- backup sets [SQL Server], BACKUP statement
- backup compression [SQL Server], BACKUP statement
- BACKUP statement
- backups [SQL Server], BACKUP statement
- backup history tables [SQL Server]
- transaction log backups [SQL Server], BACKUP LOG statement
- READ_WRITE_FILEGROUPS option
- BACKUP DATABASE statement
- concurrency [SQL Server], backups
- backing up databases [SQL Server]
- passwords [SQL Server], backups
- security [SQL Server], backups
- media families [SQL Server]
- BACKUP LOG statement
- backing up transaction logs [SQL Server]
- stripe sets [SQL Server]
- cross-platform backups
ms.assetid: 89a4658a-62f1-4289-8982-f072229720a1
author: mashamsft
ms.author: mathoma
manager: craigg
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current||>=aps-pdw-2016||=sqlallproducts-allversions'
ms.openlocfilehash: a098756919cec261d9416149a508b311c48cd147
ms.sourcegitcommit: 97340deee7e17288b5eec2fa275b01128f28e1b8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/30/2019
ms.locfileid: "55421493"
---
# <a name="backup-transact-sql"></a>BACKUP (Transact-SQL)

Faz o backup de um Banco de Dados SQL. 

Clique em uma das guias a seguir para ver sintaxe, argumentos, comentários, permissões e exemplos de uma versão específica do SQL com a qual você está trabalhando.

Para obter mais informações sobre as convenções de sintaxe, consulte [Convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md). 

## <a name="click-a-product"></a>Clique em um produto!

Na linha a seguir, clique em qualquer nome de produto de seu interesse. O clique exibe conteúdo diferente aqui, apropriado para qualquer produto no qual você clicar:

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions"

> [!div class="mx-tdCol2BreakAll"]  
> |||| 
> |---|---|---| 
> |**_\* SQL Server \*_** &nbsp;|[Instância gerenciada<br />do Banco de Dados SQL](backup-transact-sql.md?view=azuresqldb-mi-current)|[Parallel<br />Data Warehouse](backup-transact-sql.md?view=aps-pdw-2016)|  

&nbsp;

## <a name="sql-server"></a>SQL Server

Faz backup de um banco de dados completo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para criar um backup de banco de dados ou um ou mais arquivos ou grupos de arquivos do banco de dados para criar um backup de arquivo (BACKUP DATABASE). Além disso, no modelo de recuperação completa ou no modelo de recuperação bulk-logged, faz o backup do log de transações do banco de dados para criar um backup de log (BACKUP LOG). 
  
## <a name="syntax"></a>Sintaxe  
  
```sql 
--Backing Up a Whole Database   
BACKUP DATABASE { database_name | @database_name_var }   
  TO <backup_device> [ ,...n ]   
  [ <MIRROR TO clause> ] [ next-mirror-to ]  
  [ WITH { DIFFERENTIAL 
           | <general_WITH_options> [ ,...n ] } ]  
[;]  
  
--Backing Up Specific Files or Filegroups  
BACKUP DATABASE { database_name | @database_name_var }   
 <file_or_filegroup> [ ,...n ]   
  TO <backup_device> [ ,...n ]   
  [ <MIRROR TO clause> ] [ next-mirror-to ]  
  [ WITH { DIFFERENTIAL | <general_WITH_options> [ ,...n ] } ]  
[;]  
  
--Creating a Partial Backup  
BACKUP DATABASE { database_name | @database_name_var }   
 READ_WRITE_FILEGROUPS [ , <read_only_filegroup> [ ,...n ] ]  
  TO <backup_device> [ ,...n ]   
  [ <MIRROR TO clause> ] [ next-mirror-to ]  
  [ WITH { DIFFERENTIAL | <general_WITH_options> [ ,...n ] } ]  
[;]  
  
--Backing Up the Transaction Log (full and bulk-logged recovery models)  
BACKUP LOG 
  { database_name | @database_name_var }  
  TO <backup_device> [ ,...n ]   
  [ <MIRROR TO clause> ] [ next-mirror-to ]  
  [ WITH { <general_WITH_options> | \<log-specific_optionspec> } [ ,...n ] ]  
[;]  
  
<backup_device>::=   
 {  
   { logical_device_name | @logical_device_name_var }   
 | {   DISK 
     | TAPE 
     | URL } =   
     { 'physical_device_name' | @physical_device_name_var | 'NUL' }  
 }   
  
<MIRROR TO clause>::=  
 MIRROR TO <backup_device> [ ,...n ]  
  
<file_or_filegroup>::=  
 {  
   FILE = { logical_file_name | @logical_file_name_var }   
 | FILEGROUP = { logical_filegroup_name | @logical_filegroup_name_var }  
 }   
  
<read_only_filegroup>::=  
FILEGROUP = { logical_filegroup_name | @logical_filegroup_name_var }  
  
<general_WITH_options> [ ,...n ]::=   
--Backup Set Options  
   COPY_ONLY   
 | { COMPRESSION | NO_COMPRESSION }   
 | DESCRIPTION = { 'text' | @text_variable }   
 | NAME = { backup_set_name | @backup_set_name_var }   
 | CREDENTIAL  
 | ENCRYPTION  
 | FILE_SNAPSHOT  
 | { EXPIREDATE = { 'date' | @date_var }   
        | RETAINDAYS = { days | @days_var } }   
  
--Media Set Options  
   { NOINIT | INIT }   
 | { NOSKIP | SKIP }   
 | { NOFORMAT | FORMAT }   
 | MEDIADESCRIPTION = { 'text' | @text_variable }   
 | MEDIANAME = { media_name | @media_name_variable }   
 | BLOCKSIZE = { blocksize | @blocksize_variable }   
  
--Data Transfer Options  
   BUFFERCOUNT = { buffercount | @buffercount_variable }   
 | MAXTRANSFERSIZE = { maxtransfersize | @maxtransfersize_variable }  
  
--Error Management Options  
   { NO_CHECKSUM | CHECKSUM }  
 | { STOP_ON_ERROR | CONTINUE_AFTER_ERROR }  
  
--Compatibility Options  
   RESTART   
  
--Monitoring Options  
   STATS [ = percentage ]   
  
--Tape Options. 
   { REWIND | NOREWIND }   
 | { UNLOAD | NOUNLOAD }   
  
--Log-specific Options. 
   { NORECOVERY | STANDBY = undo_file_name }  
 | NO_TRUNCATE  
  
--Encryption Options  
 ENCRYPTION (ALGORITHM = { AES_128 | AES_192 | AES_256 | TRIPLE_DES_3KEY } , encryptor_options ) <encryptor_options> ::=   
   SERVER CERTIFICATE = Encryptor_Name | SERVER ASYMMETRIC KEY = Encryptor_Name   
```  
  
## <a name="arguments"></a>Argumentos  

DATABASE  
Especifica um backup completo do banco de dados. Se uma lista de arquivos e grupos de arquivos estiver especificada, será feito o backup apenas desses arquivos e grupos de arquivos. Durante um backup completo ou diferencial do banco de dados, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] faz backup suficiente do log de transações para produzir um banco de dados consistente quando o backup é restaurado.  
  
Ao restaurar um backup criado por BACKUP DATABASE (um *backup de dados*), o backup inteiro é restaurado. Somente um backup de log pode ser restaurado em uma transação ou momento específico dentro do backup.  
  
> [!NOTE]  
> Apenas um backup completo do banco de dados pode ser executado no banco de dados **mestre**.  
  
LOG 

Especifica um backup apenas do log de transações. O backup do log é feito a partir do último backup do log executado com êxito até o final do log atual. Para poder criar o primeiro backup de log, você deve criar um backup completo.  
  
É possível restaurar um backup de log em uma transação ou momento específico dentro do backup especificando `WITH STOPAT`, `STOPATMARK` ou `STOPBEFOREMARK` na instrução [RESTORE LOG](../../t-sql/statements/restore-statements-transact-sql.md).  
  
> [!NOTE]  
>  Após um backup de log típico, alguns registros do log de transações se tornam inativos, a menos que você especifique `WITH NO_TRUNCATE` ou `COPY_ONLY`. O log é truncado depois que todos os registros contidos em um ou mais arquivos de log virtual se tornam ativos. Se o log não estiver sendo truncado após backups de log de rotina, algo pode estar atrasando o truncamento do log. Para obter mais informações, consulte [Fatores que podem atrasar o truncamento de log](../../relational-databases/logs/the-transaction-log-sql-server.md#FactorsThatDelayTruncation).  
  
{ _database\_name_ | **@**_database\_name\_var_ }   
É o banco de dados do qual é feito o backup do log de transações, do banco de dados parcial ou do banco de dados completo. Se for fornecido como uma variável (**@**_database\_name\_var_), esse nome poderá ser especificado como uma constante de cadeia de caracteres (**@**_database\_name\_var_**=**_database name_) ou como uma variável de tipo de dados de cadeia de caracteres, exceto para os tipos de dados **ntext** ou **text**.  
  
> [!NOTE]  
> O backup do banco de dados espelho em uma parceria de espelhamento de banco de dados não pode ser feito.  
  
\<file_or_filegroup> [ **,**...*n* ]  
Usado apenas com BACKUP DATABASE, especifica um arquivo ou grupo de arquivos do banco de dados a ser incluído em um backup de arquivo, ou especifica um arquivo ou grupo de arquivos somente leitura a ser incluído em um backup parcial.  
  
FILE **=** { *logical_file_name* | **@**_logical\_file\_name\_var_ }  
É o nome lógico de um arquivo ou variável cujo valor é igual ao nome lógico de um arquivo que deve ser incluído no backup.  
  
FILEGROUP **=** { _logical\_filegroup\_name_ | **@**_logical\_filegroup\_name\_var_ }  
É o nome lógico de um grupo de arquivos ou variável cujo valor é igual ao nome lógico de um grupo de arquivos que deve ser incluído no backup. No modelo de recuperação simples, um backup de grupo de arquivos é permitido apenas para grupos de arquivos somente leitura.  
  
> [!NOTE]  
> Considere usar backups de arquivo quando o tamanho do banco de dados e as exigências de desempenho tornarem um backup de banco de dados impraticável. O dispositivo NUL pode ser usado para testar o desempenho dos backups, mas não deve ser usado em ambientes de produção.
  
*n*  
É um espaço reservado que indica que vários arquivos e grupos de arquivos podem ser especificados em uma lista separada por vírgulas. O número é ilimitado. 
  
Para obter mais informações, consulte [Backups completos de arquivos &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-file-backups-sql-server.md) e [Fazer backup de arquivos e grupos de arquivos &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md).  
  
READ_WRITE_FILEGROUPS [ **,** FILEGROUP = { _logical\_filegroup\_name_ | **@**_logical\_filegroup\_name\_var_ } [ **,**..._n_ ] ]  
Especifica um backup parcial. Um backup parcial inclui todos os arquivos de leitura/gravação em um banco de dados: o grupo de arquivos primário e quaisquer grupos de arquivos secundários de leitura/gravação e também quaisquer arquivos ou grupos de arquivos somente leitura especificados.  
  
READ_WRITE_FILEGROUPS  
Especifica que o backup de todos os grupos de arquivos de leitura/gravação seja feito no backup parcial. Se o banco de dados for somente leitura, READ_WRITE_FILEGROUPS incluirá apenas o grupo de arquivos primário.  
  
> [!IMPORTANT]  
> A listagem explícita de grupos de arquivos de leitura/gravação usando FILEGROUP em vez de READ_WRITE_FILEGROUPS cria um backup de arquivo.  
  
FILEGROUP = { *logical_filegroup_name* | **@**_logical\_filegroup\_name\_var_ }  
É o nome lógico de um grupo de arquivos somente leitura ou de uma variável cujo valor é igual ao nome lógico de um grupo de arquivos somente leitura que deve ser incluído no backup parcial. Para obter mais informações, consulte "\<file_or_filegroup>", anteriormente neste tópico.
  
*n*  
É um espaço reservado que indica que vários grupos de arquivos somente leitura podem ser especificados em uma lista separada por vírgulas.  
  
Para obter mais informações sobre backups parciais, consulte [Backups parciais &#40;SQL Server&#41;](../../relational-databases/backup-restore/partial-backups-sql-server.md).  
  
TO \<backup_device> [ **,**...*n* ] Indica que o conjunto complementar de [dispositivos de backup](../../relational-databases/backup-restore/backup-devices-sql-server.md) é um conjunto de mídias não espelhado ou o primeiro dos espelhos dentro de um conjunto de mídias espelhado (para o qual uma ou mais cláusulas MIRROR TO são declaradas).  
  
\<backup_device>

Especifica um dispositivo de backup lógico ou físico a ser usado para a operação de backup.  
  
{ *nome_dispositivo_lógico* | **@**_nome\_dispositivo\_lógico\_var_ } **Aplica-se a:** SQL Server   
É o nome lógico do dispositivo de backup no qual o backup do banco de dados é feito. O nome lógico deve seguir as regras para identificadores. Se for fornecida como uma variável (@*logical_device_name_var*), o nome do dispositivo de backup poderá ser especificado como uma constante de cadeia de caracteres (nome do dispositivo de backup lógico de @_logical\_device\_name\_var_**=**) ou como uma variável de qualquer tipo de dados de cadeia de caracteres, com exceção dos tipos de dados **ntext** ou **text**.  
  
{ DISK | TAPE | URL} **=** { **'**_nome\_dispositivo\_físico_**'** | **@**_nome\_dispositivo\_físico\_var_ | 'NUL' } **Aplica-se a:** DISK, TAPE e URL se aplicam ao SQL Server. 
Especifica um arquivo de disco ou dispositivo de fita, ou um serviço de Armazenamento de Blobs do Microsoft Azure. O formato da URL é usado para criar backups no serviço de armazenamento do Microsoft Azure. Para obter mais informações e exemplos, consulte [Backup e restauração do SQL Server com o serviço de Armazenamento de Blobs do Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md). Para obter um tutorial, confira [Tutorial: Backup e restauração do SQL Server no serviço de Armazenamento de Blobs do Microsoft Azure](~/relational-databases/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md). 

> [!NOTE] 
> O dispositivo de disco NUL descartará todas as informações enviadas para ele e apenas deve ser usado para teste. Isso não se destina ao uso em produção.
  
> [!IMPORTANT]  
> Começando pelo [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2 ao [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], somente é possível fazer backup em um único dispositivo durante o backup em uma URL. Para fazer backup em vários dispositivos ao fazer backup em uma URL, é necessário usar o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] por meio do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e usar tokens SAS (Assinatura de Acesso Compartilhado). Para obter exemplos sobre como criar uma Assinatura de Acesso Compartilhado, consulte [Backup do SQL Server em uma URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md) e [Simplificando a criação de credenciais do SQL com tokens SAS (Assinatura de Acesso Compartilhado) no Armazenamento do Azure com o PowerShell](https://blogs.msdn.com/b/sqlcat/archive/2015/03/21/simplifying-creation-sql-credentials-with-shared-access-signature-sas-keys-on-azure-storage-containers-with-powershell.aspx).  
  
**URL aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2 ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
  
Um dispositivo de disco não precisa existir antes de ser especificado em uma instrução BACKUP. Se o dispositivo físico existir e a opção INIT não estiver especificada na instrução BACKUP, o backup será anexado ao dispositivo.  
 
> [!NOTE] 
> O dispositivo NUL descartará todas as entradas enviadas para esse arquivo; no entanto, o backup ainda marcará todas as páginas como copiadas em backup.
  
Para obter mais informações, consulte [Dispositivos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).  
  
> [!NOTE]  
> A opção TAPE será removida em uma futura versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam.  
  
*n*  
É um espaço reservado que indica que até 64 dispositivos de backup podem ser especificados em uma lista separada por vírgulas.  
  
MIRROR TO \<backup_device> [ **,**...*n* ] Especifica um conjunto de até três dispositivos de backup secundário, que espelharão os dispositivos de backup especificados na cláusula TO. A cláusula MIRROR TO deve especificar o mesmo número e tipo dos dispositivos de backup que a cláusula TO. O número máximo de cláusulas MIRROR TO é três.  
  
Essa opção está disponível somente na edição Enterprise do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
> Para que MIRROR TO = DISK, BACKUP determine automaticamente o tamanho do bloco apropriado para dispositivos de disco, com base no tamanho do setor do disco. Se o disco MIRROR TO for formatado com um tamanho de setor diferente que o disco especificado como o dispositivo de backup principal, o comando de backup falhará.  Para espelhar os backups em dispositivos que têm diferentes tamanhos de setor, o parâmetro BLOCKSIZE deve ser especificado e definido como o maior tamanho de setor entre todos os dispositivos de destino.  Para saber mais sobre o tamanho de bloco, confira "BLOCKSIZE", mais adiante neste tópico.  
  
\<backup_device> Consulte "\<backup_device>", anteriormente nesta seção.
  
*n*  
É um espaço reservado que indica que até 64 dispositivos de backup podem ser especificados em uma lista separada por vírgulas. O número de dispositivos na cláusula MIRROR TO deve ser igual ao número de dispositivos na cláusula TO.  
  
Para obter mais informações, consulte "Famílias de mídia em conjunto de mídia espelhados", na seção [Comentários](#general-remarks), mais adiante neste tópico.  
  
[ *next-mirror-to* ]  
É um espaço reservado que indica que uma única instrução BACKUP pode conter até três cláusulas MIRROR TO, além da única cláusula TO.  
  
### <a name="with-options"></a>Opções WITH  
Especifica opções a serem usadas com uma operação de backup.  
  
CREDENTIAL  
**Aplica-se ao**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2 ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
Usado somente durante a criação de um backup no serviço de Armazenamento de Blobs do Microsoft Azure.  
  
FILE_SNAPSHOT **Aplica-se**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).

Usado para criar um instantâneo do Azure dos arquivos de banco de dados quando todos os arquivos de banco de dados do SQL Server são armazenados com o serviço de Armazenamento de Blobs do Azure. Para obter mais informações, consulte [Arquivos de dados do SQL Server no Microsoft Azure](../../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md). Backup de Instantâneo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa instantâneos do Azure dos arquivos de banco de dados (arquivos de log e de dados) em um estado consistente. Um conjunto consistente de instantâneos do Azure compõem um backup e são registrados no arquivo de backup. A única diferença entre o `BACKUP DATABASE TO URL WITH FILE_SNAPSHOT` e o `BACKUP LOG TO URL WITH FILE_SNAPSHOT` é que o último também trunca o log de transações, ao contrário do primeiro. Com o Backup do Instantâneo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], após o backup completo inicial exigido pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para estabelecer a cadeia de backup, somente um único backup de log de transações é necessário para restaurar um banco de dados para o ponto no tempo do backup de log de transações. Além disso, apenas dois backups de log de transações são necessários para restaurar um banco de dados para um ponto no tempo entre a hora dos dois backups de log de transações.  
    
DIFFERENTIAL  

Usado apenas com BACKUP DATABASE, especifica que o backup de banco de dados ou de arquivo deve consistir apenas das partes do banco de dados ou arquivo alterado desde o último backup completo. Um backup diferencial normalmente usa menos espaço do que um backup completo. Use essa opção para que todos os backups de log individuais executados desde o último backup não precisem ser aplicados.  
  
> [!NOTE]  
> Por padrão, `BACKUP DATABASE` cria um backup completo.  
  
Para obter mais informações, veja [Backups diferenciais &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md).  
  
ENCRYPTION  
Usado para especificar a criptografia de um backup. Você pode especificar um algoritmo de criptografia para criptografar o backup ou especificar `NO_ENCRYPTION` para que o backup não seja criptografado. A criptografia é a prática recomendada para ajudar a proteger arquivos de backup. A lista de algoritmos que você pode especificar é:  
  
- `AES_128`  
- `AES_192`  
- `AES_256`  
- `TRIPLE_DES_3KEY`  
- `NO_ENCRYPTION`    

Se você optar pela criptografia, também precisará especificar o criptografador usando as opções do criptografador:  
  
- SERVER CERTIFICATE = Encryptor_Name  
- SERVER ASYMMETRIC KEY = Encryptor_Name  
  
> [!WARNING]  
> Quando a criptografia é usada em conjunto com o argumento `FILE_SNAPSHOT`, o próprio arquivo de metadados é criptografado com o algoritmo de criptografia especificado e o sistema verifica se a [TDE (Transparent Data Encryption)](../../relational-databases/security/encryption/transparent-data-encryption.md) foi concluída para o banco de dados. Nenhuma criptografia adicional ocorre para os dados em si. O backup falhará se o banco de dados não tiver sido criptografado ou se a criptografia não tiver sido concluída antes da emissão da instrução de backup.  
  
**Opções de conjunto de backup**  
  
Essas opções funcionam no conjunto de backup criado por esta operação de backup.  
  
> [!NOTE]  
> Para especificar um conjunto de backup para uma operação de restauração, use a opção `FILE = <backup_set_file_number>`. Para obter mais informações sobre como especificar um conjunto de backup, consulte "Especificando um conjunto de backup" em [Argumentos de RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md).
  
COPY_ONLY Especifica que o backup é um *backup somente cópia*, o que não afeta a sequência normal de backups. Um backup somente cópia é criado independentemente de seus backups convencionais agendados regularmente. Um backup somente cópia não afeta o backup global e restaura procedimentos do banco de dados.  
  
Backups somente cópia devem ser usados em situações em que um backup é feito com um objetivo especial, como fazer backup de log antes de uma restauração de arquivo online. Normalmente, um backup de log somente cópia é usado uma vez e excluído em seguida.  
  
- Quando usado com `BACKUP DATABASE`, a opção `COPY_ONLY` cria um backup completo que não pode servir como uma base diferencial. O bitmap diferencial não é atualizado e backups diferenciais se comportam como se o backup somente cópia não existisse. Backups diferenciais subseqüentes usam o backup completo convencional mais recente como base.  
  
    > [!IMPORTANT]  
    > Se `DIFFERENTIAL` e `COPY_ONLY` são usados juntos, `COPY_ONLY` é ignorado e um backup diferencial é criado.  
  
- Quando usada com `BACKUP LOG`, a opção `COPY_ONLY` cria um *backup de log somente cópia*, que não trunca o log de transações. O backup de log somente cópia não tem nenhum efeito na cadeia de logs e outros backups de log se comportam como se o backup somente cópia não existisse.  
  
Para obter mais informações, veja [Backups somente cópia &#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md).  
  
{ COMPRESSION | NO_COMPRESSION }  
No [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] e em versões posteriores somente, especifica se a [compactação de backup](../../relational-databases/backup-restore/backup-compression-sql-server.md) é executada neste backup, substituindo o padrão no nível do servidor.  
  
Na instalação, o comportamento padrão é sem compactação de backup. No entanto, esse padrão pode ser alterado com a definição da opção [backup compression default](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md) de configuração do servidor. Para obter informações sobre como exibir o valor atual dessa opção, consulte [Exibir ou alterar propriedades do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/view-or-change-server-properties-sql-server.md).  

Para obter informações sobre como usar a compactação de backup com bancos de dados habilitados para [TDE (Transparent Data Encryption)](../../relational-databases/security/encryption/transparent-data-encryption.md), consulte a seção [Comentários](#general-remarks).
  
COMPRESSION  
Habilita explicitamente a compactação de backup.  
  
NO_COMPRESSION  
Desabilita explicitamente a compactação de backup.  
  
DESCRIPTION **=** { **'**_text_**'** | **@**_text\_variable_ }  
Especifica o texto de forma livre que descreve o conjunto de backup. A cadeia de caracteres pode conter um máximo de 255 caracteres.  
  
NAME **=** { *backup_set_name* | **@**_backup\_set\_var_ }  
Especifica o nome do conjunto de backup. Os nomes podem ter no máximo de 128 caracteres. Se NAME não estiver especificado, ele estará em branco.  
  
{ EXPIREDATE **='**_date_**'** | RETAINDAYS **=** _days_ }  
Especifica quando o conjunto de backup desse backup pode ser substituído. Se essas duas opções forem usadas, RETAINDAYS terá precedência sobre EXPIREDATE.  
  
Se nenhuma opção for especificada, a data de expiração será determinada pela definição da configuração de **mediaretention**. Para obter mais informações, veja [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).   
  
> [!IMPORTANT]  
> Essas opções apenas impedem que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] substitua um arquivo. Fitas podem ser apagadas por outros métodos e os arquivos de disco podem ser excluídos pelo sistema operacional. Para obter mais informações sobre verificação de validade, consulte SKIP e FORMAT neste tópico.  
  
EXPIREDATE **=** { **'**_date_**'** | **@**_date\_var_ }  
Especifica quando o conjunto de backup vence e pode ser substituído. Se for fornecida como uma variável (@_date\_var_), essa data deverá seguir o formato de **datetime** do sistema configurado e ser especificado como um dos seguintes:  
  
- Uma constante de cadeia de caracteres (@_date\_var_ **=** date)  
- Uma variável do tipo de dados de cadeia de caracteres (exceto para os tipos de dados **ntext** ou **text**)  
- Um **smalldatetime**  
- Uma variável **datetime**  
  
Por exemplo:  
  
- `'Dec 31, 2020 11:59 PM'`  
- `'1/1/2021'`  
  
Para obter informações sobre como especificar valores de **datetime**, consulte [Tipos de data e hora](../../t-sql/data-types/date-and-time-types.md).  
  
> [!NOTE]  
> Para ignorar a data de expiração, use a opção `SKIP`.  
  
RETAINDAYS **=** { *days* | **@**_days\_var_ }  
Especifica o número de dias que devem decorrer para que este conjunto de mídias de backup possa ser substituído. Se for fornecida como uma variável (**@**_days\_var_), ela deverá ser especificada como um inteiro.  
  
**Opções de conjunto de mídias**  
  
Essas opções funcionam no conjunto de mídias como um todo.  
  
{ **NOINIT** | INIT }  
Controla se a operação de backup anexa ou substitui os conjuntos de backup existentes na mídia de backup. O padrão é anexar ao backup mais recente definido na mídia (NOINIT).  
  
> [!NOTE]  
> Para obter informações sobre as interações entre { **NOINIT** | INIT } e { **NOSKIP** | SKIP }, consulte [Comentários](#general-remarks), mais adiante neste tópico.  
  
NOINIT  
Indica que o conjunto de backup é anexado ao conjunto de mídias especificado, preservando conjuntos de backup existentes. Se uma senha de mídia estiver definida para o conjunto de mídias, a senha deverá ser fornecida. NOINIT é o padrão.  
  
Para obter mais informações, veja [Conjuntos de mídias, famílias de mídia e conjuntos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md).  
  
INIT  
Especifica que todos os conjuntos de backup devem ser substituídos, mas preserva o cabeçalho de mídia. Se INIT estiver especificado, qualquer conjunto de backup existente naquele dispositivo será substituído, se as condições permitirem. Por padrão, BACKUP verificará as seguintes condições e não substituirá a mídia de backup se qualquer uma delas existir:  
  
- Um conjunto de backup ainda não expirou. Para obter mais informações, consulte as opções `EXPIREDATE` e `RETAINDAYS`.  
- O nome do conjunto de backup fornecido na instrução BACKUP, se fornecido, não corresponde ao nome na mídia de backup. Para obter mais informações, consulte a opção NAME, anteriormente nesta seção.  
  
Para substituir essas verificações, use a opção `SKIP`.  
  
Para obter mais informações, veja [Conjuntos de mídias, famílias de mídia e conjuntos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md).  
  
{ **NOSKIP** | SKIP }  
Controla se a operação de backup verifica a data e a hora de validade dos conjuntos de backup existentes na mídia antes de substituí-los.  
  
> [!NOTE]  
> Para obter informações sobre as interações entre { **NOINIT** | INIT } e { **NOSKIP** | SKIP }, consulte "Comentários", mais adiante neste tópico.  
  
NOSKIP  
Instrui a instrução BACKUP a verificar a data de validade de todos os conjuntos de backup na mídia antes de permitir que eles sejam substituídos. Esse é o comportamento padrão.  
  
SKIP  
Desabilita a verificação de validade e nome do conjunto de backup que normalmente é executada pela instrução BACKUP para impedir a substituição de conjuntos de backup. Para obter informações sobre as interações entre { INIT | NOINIT } e { NOSKIP | SKIP }, consulte "Comentários", mais adiante neste tópico.  
Para exibir as datas de validade de conjuntos de backup, consulte a coluna **expiration_date** da tabela de histórico [backupset](../../relational-databases/system-tables/backupset-transact-sql.md).  
  
{ **NOFORMAT** | FORMAT }  
Especifica se o cabeçalho da mídia deve ser gravado nos volumes usados para esta operação de backup, substituindo qualquer cabeçalho de mídia e conjuntos de backup existentes.  
  
NOFORMAT  
Especifica que a operação de backup preserva o cabeçalho da mídia e os conjuntos de backup existentes nos volumes de mídia usados para esta operação de backup. Esse é o comportamento padrão.  
  
FORMAT  
Especifica que um novo conjunto de mídias deve ser criado. FORMAT faz com que a operação de backup grave um novo cabeçalho de mídia em todos os volumes de mídia usados para a operação de backup. O conteúdo existente do volume se torna inválido, porque qualquer cabeçalho de mídia e conjuntos de backup existentes são substituídos.  
  
> [!IMPORTANT]  
> Use `FORMAT` com cautela. A formatação de qualquer volume de um conjunto de mídias renderiza todo o conjunto de mídias como inutilizável. Por exemplo, se você iniciar uma única fita pertencente a um conjunto de mídias distribuído existente, todo o conjunto de mídias será renderizado como inútil.  
  
A especificação de FORMAT implica `SKIP`; `SKIP` não precisa ser declarado explicitamente.  
  
MEDIADESCRIPTION **=** { *text* | **@**_text\_variable_ }  
Especifica a descrição de texto de forma livre do conjunto de mídias, com um máximo de 255 caracteres.  
  
MEDIANAME **=** { *media_name* | **@**_media\_name\_variable_ }  
Especifica o nome da mídia de todo o conjunto de mídias de backup. O nome da mídia não deve ter mais de 128 caracteres. Se `MEDIANAME` for especificado, ele deverá corresponder ao nome da mídia especificado anteriormente já existente nos volumes de backup. Se não estiver especificado ou se a opção SKIP estiver especificada, não haverá nenhuma verificação do nome da mídia.  
  
BLOCKSIZE **=** { *blocksize* | **@**_blocksize\_variable_ }  
Especifica o tamanho do bloco físico, em bytes. Os tamanhos com suporte são 512, 1024, 2048, 4096, 8192, 16384, 32768 e 65536 (64 KB) bytes. O padrão é 65536 para dispositivos de fita e 512 para outros dispositivos. Normalmente, essa opção é desnecessária porque BACKUP seleciona automaticamente um tamanho de bloco apropriado ao dispositivo. A declaração explícita de um tamanho de bloco substitui a seleção automática de tamanho de bloco.  
  
Se estiver fazendo um backup que planeja copiar e restaurar de um CD-ROM, especifique BLOCKSIZE=2048.  
  
> [!NOTE]  
> Normalmente, essa opção afeta o desempenho apenas durante a gravação em dispositivos de fita.  
  
**Opções de transferência de dados**  
  
BUFFERCOUNT **=** { *buffercount* | **@**_buffercount\_variable_ }  
Especifica o número total de buffers de E/S a ser usado para a operação de backup. É possível especificar qualquer inteiro positivo. No entanto, grandes números de buffers podem provocar erros de "memória insuficiente" devido a espaço de endereço virtual inadequado no processo Sqlservr.exe.  
  
O espaço total usado pelos buffers é determinado por: *buffercount/maxtransfersize*.  
  
> [!NOTE]  
> Para obter informações importantes sobre como usar a opção `BUFFERCOUNT`, confira o blog [BufferCount data transfer option can lead to OOM condition](https://blogs.msdn.com/b/sqlserverfaq/archive/2010/05/06/incorrect-buffercount-data-transfer-option-can-lead-to-oom-condition.aspx) (Opção incorreta de transferência de dados de BufferCount pode levar à condição OOM).  
  
MAXTRANSFERSIZE **=** { *maxtransfersize* | _**@** maxtransfersize\_variable_ } Especifica a maior unidade de transferência em bytes a ser usada entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e a mídia de backup. Os valores possíveis são múltiplos de 65536 bytes (64 KB), estendendo-se até 4194304 bytes (4 MB).  

> [!NOTE]  
> Durante a criação de backups usando o Serviço Gravador do SQL, se o banco de dados tiver configurado [FILESTREAM](../../relational-databases/blob/filestream-sql-server.md) ou incluir [grupos de arquivos com otimização de memória](../../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md), o `MAXTRANSFERSIZE` no momento de uma restauração deverá ser maior ou igual a `MAXTRANSFERSIZE` que foi usado quando o backup foi criado. 

> [!NOTE]  
> Para bancos de dados habilitados para [TDE (Transparent Data Encryption)](../../relational-databases/security/encryption/transparent-data-encryption.md) com um único arquivo de dados, o `MAXTRANSFERSIZE` padrão é 65.536 (64 KB). Para bancos de dados não criptografados com TDE, o `MAXTRANSFERSIZE` padrão é 1048576 (1 MB) ao usar o backup em DISK e 65536 (64 KB) ao usar VDI ou TAPE.
> Para obter mais informações sobre como usar a compactação de backup com bancos de dados criptografados com TDE, consulte a seção [Comentários](#general-remarks).
  
**Opções de gerenciamento de erros**  
  
Essas opções permitem determinar se as somas de verificação de backup estão habilitadas para a operação de backup e se a operação é interrompida quando um erro é encontrado.  
  
{ **NO_CHECKSUM** | CHECKSUM }  
Controla se somas de verificação de backup estão habilitadas.  
  
NO_CHECKSUM  
Desabilita explicitamente a geração de somas de verificação de backup (e a validação de somas de verificação de página). Esse é o comportamento padrão.  
  
CHECKSUM  
Especifica que a operação de backup verifica cada página quanto à soma de verificação e a página interrompida, se estiver habilitada e disponível, e gera uma soma de verificação para o backup inteiro.  
  
O uso de somas de verificação de backup pode afetar uma carga de trabalho e a taxa de transferência do backup.  
  
Para obter mais informações, consulte [Possíveis erros de mídia durante backup e restauração &#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md).  
  
{ **STOP_ON_ERROR** | CONTINUE_AFTER_ERROR }  
Controla se uma operação de backup para ou continua depois de encontrar um erro de soma de verificação de página.  
  
STOP_ON_ERROR  
Instrui BACKUP a falhar se uma soma de verificação de página não estiver correta. Esse é o comportamento padrão.  
  
CONTINUE_AFTER_ERROR  
Instrui BACKUP a continuar apesar de encontrar erros como somas de verificação inválidas ou páginas interrompidas.  
  
Se você não conseguir fazer backup da parte final do log usando a opção NO_TRUNCATE quando o banco de dados estiver danificado, tente fazer um [backup da parte final do log](../../relational-databases/backup-restore/tail-log-backups-sql-server.md) especificando CONTINUE_AFTER_ERROR em vez de NO_TRUNCATE.  
  
Para obter mais informações, consulte [Possíveis erros de mídia durante backup e restauração &#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md).  
  
**Opções de compatibilidade**  
  
RESTART  
A partir do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], não tem nenhum efeito. Esta opção é aceita pela versão para compatibilidade com versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
**Opções de monitoramento**  
  
STATS [ **=** _percentage_ ]  
Exibe uma mensagem sempre que outro *percentual* for concluída e é usado para medir o progresso. Se *percentage* for omitido, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exibirá uma mensagem após a conclusão de cada 10%.  
  
A opção STATS informa a porcentagem concluída de acordo com o limite de relatório do próximo intervalo. Esse limite é aproximadamente a porcentagem especificada. Por exemplo, com STATS=10, se a quantidade concluída for 40%, a opção poderá exibir 43%. Para conjuntos de backup grandes, isso não é um problema, porque a porcentagem concluída muda muito lentamente entre chamadas de E/S concluídas.  
  
**Opções de fita**  

Essas opções são usadas apenas para dispositivos TAPE. Se um dispositivo que não seja de fita estiver sendo usado, essas opções serão ignoradas.  
  
{ **REWIND** | NOREWIND }  
REWIND

Especifica que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solta e rebobina a fita. REWIND é o padrão.  
  
NOREWIND

Especifica que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mantém a fita aberta após a operação de backup. É possível usar essa opção para ajudar a melhorar o desempenho ao executar várias operações de backup em uma fita.  
  
NOREWIND implica NOUNLOAD e essas opções são incompatíveis dentro de uma única instrução BACKUP.  
  
> [!NOTE]  
> Se você usar `NOREWIND`, a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reterá a propriedade da unidade de fita até que uma instrução BACKUP ou RESTORE em execução no mesmo processo use a opção `REWIND` ou `UNLOAD` ou que a instância do servidor seja encerrada. Manter a fita aberta evita que outros processos a acessem. Para obter informações sobre como exibir uma lista de fitas abertas e fechar uma fita aberta, consulte [Dispositivos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).  
  
{ **UNLOAD** | NOUNLOAD }    

> [!NOTE]  
> `UNLOAD` e `NOUNLOAD` são configurações de sessão que persistem durante a vida da sessão ou até que ela seja redefinida com a especificação da alternativa.  
  
UNLOAD

Especifica que a fita é rebobinada e descarregada automaticamente quando o backup for concluído. UNLOAD é o padrão quando uma sessão começa. 
  
NOUNLOAD

Especifica que, após a operação BACKUP, a fita permanece carregada na unidade de fita.  
  
> [!NOTE]  
> Para um backup em um dispositivo de backup em fita, a opção `BLOCKSIZE` afeta o desempenho da operação de backup. Normalmente, essa opção afeta o desempenho apenas durante a gravação em dispositivos de fita.  
  
**Opções específicas de log**  

Essas opções são usadas apenas com `BACKUP LOG`.  
  
> [!NOTE]  
> Se você não quiser fazer backups de log, use o modelo de recuperação simples. Para obter mais informações, veja [Modelos de recuperação &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md).  
  
{ NORECOVERY | STANDBY **=** _undo_file_name_ }  
  NORECOVERY 

Faz backup do final do log e deixa o banco de dados no estado de RESTORING. NORECOVERY é útil ao executar failover em um banco de dados secundário ou ao salvar o final do log antes de uma operação RESTORE.  
  
Para executar um backup de log de melhor esforço que ignora o truncamento do log e, em seguida, coloca o banco de dados no estado RESTORING atomicamente, use as opções `NO_TRUNCATE` e `NORECOVERY` em conjunto.  
  
STANDBY **=** _standby_file_name_ 

Faz BACKUP do final do log e deixa o banco de dados em um estado STANDBY e somente leitura. A cláusula STANDBY grava dados em espera (executando reversão, mas com a opção de restaurações adicionais). O uso da opção STANDBY é equivalente a BACKUP LOG WITH NORECOVERY seguido por um RESTORE WITH STANDBY.  
  
O uso do modo em espera exige um arquivo em espera, especificado por *standby_file_name*, cujo local é armazenado no log do banco de dados. Se o arquivo especificado já existir, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] o substituirá. Se o arquivo não existir, ele será criado pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)]. O arquivo em espera se torna parte do banco de dados.  
  
Esse arquivo contém as alterações revertidas que deverão ser revertidas se operações RESTORE LOG forem aplicadas subseqüentemente. Deve haver espaço em disco suficiente para que o arquivo em espera cresça para que possa conter todas as páginas distintas do banco de dados que foi modificado pela reversão de transações não confirmadas.  
  
NO_TRUNCATE  

Especifica que o log não é truncado e faz com que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] tente fazer backup, independentemente do estado do banco de dados. Consequentemente, um backup feito com `NO_TRUNCATE` pode conter metadados incompletos. Essa opção permite fazer backup do log em situações em que o banco de dados está danificado.  
  
A opção NO_TRUNCATE de BACKUP LOG é equivalente a especificar COPY_ONLY e CONTINUE_AFTER_ERROR.  
  
Sem a opção `NO_TRUNCATE`, o banco de dados deve estar no estado ONLINE. Se o banco de dados estiver no estado SUSPENDED, você poderá criar um backup especificando `NO_TRUNCATE`. Mas se o banco de dados estiver no estado OFFLINE ou EMERGENCY, BACKUP não terá permissão, mesmo com `NO_TRUNCATE`. Para obter mais informações sobre estados do banco de dados, consulte [Estados do banco de dados](../../relational-databases/databases/database-states.md).  
  
## <a name="about-working-with-sql-server-backups"></a>Sobre o trabalho com backups do SQL Server  
Esta seção introduz os seguintes conceitos de backup essenciais:  
  
[Tipos de backup](#Backup_Types)  
[Truncamento do log de transações](#Tlog_Truncation)  
[Formatando uma mídia de backup](#Formatting_Media)  
[Trabalhando com dispositivos de backup e conjuntos de mídias](#Backup_Devices_and_Media_Sets)  
[Restaurando backups de SQL Server](#Restoring_Backups)  
  
> [!NOTE]  
> Para obter uma introdução ao backup no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Visão geral de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md).  
  
###  <a name="Backup_Types"></a> Tipos de backup  
Os tipos de backup com suporte dependem do modelo de recuperação do banco de dados, da seguinte maneira:  
  
- Todos os modelos de recuperação oferecem suporte a backups completos e diferenciais de dados.  
  
    |Escopo do backup|Tipos de backup|  
    |---------------------|------------------|  
    |Banco de dados inteiro|[Backups de banco de dados](../../relational-databases/backup-restore/full-database-backups-sql-server.md) abrangem o banco de dados inteiro.<br /><br /> Opcionalmente, cada backup de banco de dados pode servir como a base de uma série de um ou mais [backups de banco de dados diferenciais](../../relational-databases/backup-restore/differential-backups-sql-server.md).|  
    |Banco de dados parcial|[Backups parciais](../../relational-databases/backup-restore/partial-backups-sql-server.md) abrangem grupos de arquivos de leitura/gravação e, possivelmente, um ou mais arquivos ou grupos de arquivos somente leitura.<br /><br /> Opcionalmente, cada backup parcial pode servir como a base de uma série de um ou mais [backups parciais diferenciais](../../relational-databases/backup-restore/differential-backups-sql-server.md).|  
    |Arquivo ou grupo de arquivos|[Backups de arquivos](../../relational-databases/backup-restore/full-file-backups-sql-server.md) abrangem um ou mais arquivos ou grupos de arquivos e são relevantes apenas para bancos de dados que contêm vários grupos de arquivos. No modelo de recuperação simples, os backups de arquivos são essencialmente restritos a grupos de arquivos secundários somente leitura.<br /> Opcionalmente, cada backup de arquivo pode servir como a base de uma série de um ou mais [backups de arquivos diferenciais](../../relational-databases/backup-restore/differential-backups-sql-server.md).|  
  
- No modelo de recuperação completa ou modelo de recuperação bulk-logged, os backups convencionais também incluem *backups de log de transações* sequenciais (ou *backups de log*), que são obrigatórios. Cada backup de log abrange a parte do log de transações que estava ativa quando o backup foi criado e inclui todos os registros de log cujo backup não foi feito em um backup de log anterior.  
  
     Para minimizar a exposição de perda de trabalho, à custa de sobrecarga administrativa, você deve agendar backups de log freqüentes. O agendamento de backups diferenciais entre backups completos pode reduzir o tempo de restauração reduzindo o número de backups de log a serem restaurados após a restauração dos dados.  
  
     Recomendamos que você coloque backups de log em um volume separado dos backups de banco de dados.  
  
    > [!NOTE]  
    > Para poder criar o primeiro backup de log, você deve criar um backup completo.  
  
- Um *backup somente cópia* é um backup completo para finalidades especiais ou um backup de log que é independente da sequência normal de backups convencionais. Para criar um backup somente cópia, especifique a opção COPY_ONLY na instrução BACKUP. Para obter mais informações, veja [Backups somente cópia &#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md).  
  
###  <a name="Tlog_Truncation"></a> Truncamento do log de transações  
Para evitar o preenchimento do log de transações de um banco de dados, os backups rotineiros são essenciais. No modelo de recuperação simples, o truncamento do log ocorre automaticamente depois que o backup do banco de dados é feito, e no modelo de recuperação completa, depois que o backup do log de transações é feito. No entanto, às vezes o processo de truncamento pode ser demorado. Para ver informações sobre os fatores que podem adiar o truncamento de log, consulte [O log de transações &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md).  
  
> [!NOTE]  
> As opções `BACKUP LOG WITH NO_LOG` e `WITH TRUNCATE_ONLY` foram descontinuadas. Se você estiver usando o modelo de recuperação completa ou bulk-logged e dever remover a cadeia de backup de log de um banco de dados, alterne para o modelo de recuperação simples. Para obter mais informações, veja [Exibir ou alterar o modelo de recuperação de um banco de dados &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md).  
  
###  <a name="Formatting_Media"></a> Formatando uma mídia de backup  
A mídia de backup será formatada por uma instrução BACKUP se, e apenas se, qualquer uma das seguintes situações for verdadeira:  
  
- A opção `FORMAT` foi especificada.  
- A mídia estiver vazia.  
- A operação estiver gravando uma fita de continuação.  
  
###  <a name="Backup_Devices_and_Media_Sets"></a> Trabalhando com dispositivos de backup e conjuntos de mídias  
  
#### <a name="backup-devices-in-a-striped-media-set-a-stripe-set"></a>Dispositivos de backup em um conjunto de mídias distribuído (um conjunto de distribuição)  
Um *conjunto de distribuição* é um conjunto de arquivos de disco nos quais os dados são divididos em blocos e distribuídos em uma ordem fixa. O número de dispositivos de backup usados em um conjunto de distribuição deve permanecer o mesmo (a não ser que a mídia seja reinicializada com `FORMAT`).  
  
O exemplo a seguir grava um backup do banco de dados [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] em um novo conjunto de mídias distribuído que usa três arquivos de disco.  
  
```sql  
BACKUP DATABASE AdventureWorks2012  
TO DISK='X:\SQLServerBackups\AdventureWorks1.bak',   
DISK='Y:\SQLServerBackups\AdventureWorks2.bak',   
DISK='Z:\SQLServerBackups\AdventureWorks3.bak'  
WITH FORMAT,  
   MEDIANAME = 'AdventureWorksStripedSet0',  
   MEDIADESCRIPTION = 'Striped media set for AdventureWorks2012 database;  
GO  
```  
  
Após a definição de um dispositivo de backup como parte de um conjunto de distribuição, ele não pode ser usado como um backup de dispositivo único a menos que FORMAT seja especificado. Do mesmo modo, um dispositivo de backup que contém backups não distribuídos não pode ser usado em um conjunto de distribuição a menos que FORMAT seja especificado. Para dividir um conjunto de backup distribuído, use FORMAT.  
  
Se MEDIANAME nem MEDIADESCRIPTION estiver especificado quando um cabeçalho de mídia for gravado, o campo de cabeçalho de mídia correspondente ao item em branco estará vazio.  
  
#### <a name="working-with-a-mirrored-media-set"></a>Trabalhando com um conjunto de mídias espelhado  
Normalmente, backups não são espelhados e instruções BACKUP simplesmente incluem uma cláusula TO. No entanto, um total de quatro espelhos é possível por conjunto de mídias. Em um conjunto de mídias espelhado, a operação de backup grava em vários grupos de dispositivos de backup. Cada grupo de dispositivos de backup compõe um único espelho dentro do conjunto de mídias espelhado. Todos os espelhos devem usar a mesma quantidade e tipo de dispositivos físicos de backup que devem ter as mesmas propriedades.  
  
Para fazer backup em um conjunto de mídias espelhado, todos os espelhos devem estar presentes. Para fazer backup em um conjunto de mídias espelhado, especifique a cláusula `TO` para especificar o primeiro espelho e especifique uma cláusula `MIRROR TO` para cada espelho adicional.  
  
Para um conjunto de mídias espelhado, cada cláusula `MIRROR TO` deve listar o mesmo número e tipo de dispositivos que a cláusula TO. O exemplo a seguir grava em um conjunto de mídias espelhado que contém dois espelhos e usa três dispositivos por espelho:  
  
```sql  
BACKUP DATABASE AdventureWorks2012  
TO DISK='X:\SQLServerBackups\AdventureWorks1a.bak',   
  DISK='Y:\SQLServerBackups\AdventureWorks2a.bak',   
  DISK='Z:\SQLServerBackups\AdventureWorks3a.bak'  
MIRROR TO DISK='X:\SQLServerBackups\AdventureWorks1b.bak',   
  DISK='Y:\SQLServerBackups\AdventureWorks2b.bak',   
  DISK='Z:\SQLServerBackups\AdventureWorks3b.bak';  
GO  
```  
  
> [!IMPORTANT]  
> Este exemplo foi criado para permitir teste em seu sistema local. Na prática, fazer backup em vários dispositivos na mesma unidade deve afetar o desempenho e eliminar a redundância para a qual conjuntos de mídias espelhados foram projetados.  
  
##### <a name="media-families-in-mirrored-media-sets"></a>Famílias de mídia em conjuntos de mídia espelhados  
Cada dispositivo de backup especificado na cláusula `TO` de uma instrução BACKUP corresponde a uma família de mídia. Por exemplo, se as cláusulas `TO` listarem três dispositivos, a instrução BACKUP gravará dados nas três famílias de mídia. Em um conjunto de mídias espelhado, cada espelho deve conter uma cópia de cada família de mídia. É por isso que o número de dispositivos deve ser idêntico em cada espelho.  
  
Quando vários dispositivos são listados para cada espelho, a ordem dos dispositivos determina qual família de mídia é gravada em um determinado dispositivo. Por exemplo, em cada uma das listas de dispositivos, o segundo dispositivo corresponde à segunda família de mídia. Para os dispositivos do exemplo acima, a correspondência entre dispositivos e famílias de mídia é mostrada na tabela a seguir.  
  
|Espelho|Família de mídia 1|Família de mídia 2|Família de mídia 3|  
|---------|---------|---------|---------|  
|0|`Z:\AdventureWorks1a.bak`|`Z:\AdventureWorks2a.bak`|`Z:\AdventureWorks3a.bak`|  
|1|`Z:\AdventureWorks1b.bak`|`Z:\AdventureWorks2b.bak`|`Z:\AdventureWorks3b.bak`|  
  
 O backup de uma família de mídia sempre deve ser feito no mesmo dispositivo dentro de um espelho específico. Portanto, a cada vez que você usar um conjunto de mídias existente, liste os dispositivos de cada espelho na mesma ordem em que foram especificados quando o conjunto de mídias foi criado.  
  
Para obter mais informações sobre conjuntos de mídia espelhadas, consulte [Conjuntos de mídias de backup espelhadas &#40;SQL Server&#41;](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md). Para obter mais informações sobre conjuntos de mídias e famílias de mídia em geral, consulte [Conjuntos de mídias, famílias de mídia e conjuntos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md).  
  
###  <a name="Restoring_Backups"></a> Restaurando backups do SQL Server  
Para restaurar um banco de dados e, opcionalmente, recuperá-lo para fazê-lo ficar online ou restaurar um arquivo ou grupo de arquivos, use a instrução [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) do [!INCLUDE[tsql](../../includes/tsql-md.md)] ou as tarefas **Restore** do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obter mais informações, consulte [Visão geral de restauração e recuperação &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md).  
  
##  <a name="Additional_Considerations"></a> Considerações adicionais sobre as opções de BACKUP  
  
###  <a name="Interactions_SKIP_etc"></a> Interação de SKIP, NOSKIP, INIT e NOINIT  
Esta tabela descreve interações entre as opções { **NOINIT** | INIT } e { **NOSKIP** | SKIP }.  
  
> [!NOTE]  
> Se a mídia de fita estiver vazia ou se o arquivo de backup em disco não existir, todas essas interações gravarão um cabeçalho de mídia e continuarão. Se a mídia não estiver vazia e não tiver um cabeçalho de mídia válido, essas operações fornecerão comentários informando que essa não é uma mídia MTF válida e terminarão a operação de backup.  
  
||NOINIT|INIT|  
|------|------------|----------|  
|NOSKIP|Se o volume contiver um cabeçalho de mídia válido, ele verificará o nome da mídia correspondente ao `MEDIANAME` fornecido, se houver. Se houver correspondência, anexará o conjunto de backup preservando todos os conjuntos de backup existentes.<br /> Se o volume não contiver um cabeçalho de mídia válido, ocorrerá um erro.|Se o volume contiver um cabeçalho de mídia válido, executará as seguintes verificações:<br /><ul><li>Se `MEDIANAME` for especificado, ele verificará se o nome da mídia fornecido corresponde ao nome do cabeçalho de mídia.<sup>1</sup></li><li>Verifica se não há nenhum conjunto de backup vigente na mídia. Se houver, terminará o backup.</li></ul><br />Se essas verificações passarem, substituirá qualquer conjunto de backup na mídia preservando apenas o cabeçalho da mídia.<br /> Se o volume não contiver um cabeçalho de mídia válido, ele gerará um cabeçalho com o uso do `MEDIANAME` e `MEDIADESCRIPTION` especificados, se houver.|  
|SKIP|Se o volume contiver um cabeçalho de mídia válido, acrescentará o conjunto de backup, preservando todos os conjuntos de backup existentes.|Se o volume contiver um cabeçalho de mídia válido<sup>2</sup>, ele substituirá todos os conjuntos de backup na mídia, preservando apenas o cabeçalho da mídia.<br /> Se a mídia estiver vazia, ela gerará um cabeçalho de mídia usando o `MEDIANAME` e `MEDIADESCRIPTION` especificados, se houver.|  

<sup>1</sup> O usuário deve pertencer à função de banco de dados ou de servidor fixa apropriada para executar uma operação de backup.    

<sup>2</sup> A validade inclui o número de versão de MTF e outras informações de cabeçalho. Se a versão especificada não tiver suporte ou for um valor inesperado, ocorrerá um erro.  
  
## <a name="compatibility"></a>Compatibilidade  
  
> [!CAUTION]  
> Os backups criados por uma versão mais recente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não podem ser restaurados em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
BACKUP dá suporte à opção `RESTART` para fornecer compatibilidade com versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Mas RESTART não tem nenhum efeito.  
  
## <a name="general-remarks"></a>Comentários gerais  
Backups de banco de dados ou de log podem ser anexados a qualquer dispositivo de disco ou de fita, permitindo que um banco de dados e seus logs de transações sejam mantidos em um local físico.  
  
A instrução BACKUP não é permitida em uma transação explícita ou implícita.  
  
Operações de backup entre plataformas, mesmo entre tipos diferentes de processadores, podem ser executadas desde que a ordenação do banco de dados tenha suporte no sistema operacional.  
 
Ao usar a compactação de backup com bancos de dados habilitados para [TDE (Transparent Data Encryption)](../../relational-databases/security/encryption/transparent-data-encryption.md) com um único arquivo de dados, é recomendável usar uma `MAXTRANSFERSIZE` configuração **maior que 65.536 (64 KB)**.   
Começando pelo [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], isto permite um algoritmo de compactação otimizada para bancos de dados criptografados com TDE que primeiro descriptografa uma página, compacta-a e, em seguida, criptografa-a novamente. Se você estiver usando `MAXTRANSFERSIZE = 65536` (64 KB), a compactação de backup com bancos de dados criptografados com TDE compactará diretamente as páginas criptografadas e poderá não resultar em taxas de compactação satisfatórias. Para obter mais informações, consulte [Compactação de backup para bancos de dados habilitados para TDE](https://blogs.msdn.microsoft.com/sqlcat/2016/06/20/sqlsweet16-episode-1-backup-compression-for-tde-enabled-databases/).

> [!NOTE]  
> Há alguns casos em que o padrão `MAXTRANSFERSIZE` é maior que 64 K:
> * Quando o banco de dados tem vários arquivos de dados criados, ele usa `MAXTRANSFERSIZE` >64 K
> * Ao executar backup para URL, o padrão `MAXTRANSFERSIZE = 1048576` (1 MB)
>   
> Mesmo que uma destas condições se aplique, você deverá definir explicitamente `MAXTRANSFERSIZE` como maior que 64 K no comando de backup para obter o novo algoritmo de compactação de backup.
  
Por padrão, toda operação de backup bem-sucedida acrescenta uma entrada ao log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e ao log de eventos do sistema. Se você fizer backup do log com muita frequência, essas mensagens de êxito se acumularão muito rapidamente, resultando em logs de erros imensos que podem dificultar a localização de outras mensagens. Em tais situações, você pode suprimir essas entradas de log usando o sinalizador de rastreamento 3226, caso nenhum dos seus scripts dependa dessas entradas. Para obter mais informações, veja, [Sinalizadores de rastreamento &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).  
  
## <a name="interoperability"></a>Interoperabilidade  
O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa um processo de backup online para permitir que um backup de banco de dados seja feito enquanto o banco de dados ainda está uso. Durante um backup, a maior parte das operações é possível. Por exemplo, instruções INSERT, UPDATE ou DELETE são permitidas durante uma operação de backup  
  
Operações que não podem ser executadas durante um backup de banco de dados ou de log de transações incluem:  
  
- Operações de gerenciamento de arquivos, como a instrução `ALTER DATABASE` com as opções `ADD FILE` ou `REMOVE FILE`.  
  
- Operações de redução do banco de dados ou de arquivos. Isso inclui operações de redução automática.  
  
Se uma operação de backup for sobreposta por uma operação de gerenciamento ou de redução de arquivos, um conflito será gerado. Independentemente de qual operação em conflito começou primeiro, a segunda operação aguardará até que o tempo limite do bloqueio definido pela primeira operação seja esgotado (o período limite é controlado pela configuração de tempo limite de uma sessão). Se o bloqueio for liberado durante o período de tempo limite, a segunda operação continuará. Se o tempo limite do bloqueio for esgotado, a segunda operação falhará.  
 
## <a name="metadata"></a>Metadados  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inclui as seguintes tabelas de histórico de backup que controlam as atividades do banco de dados:  
  
- [backupfile &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)  
- [backupfilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)  
- [backupmediafamily &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)  
- [backupmediaset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediaset-transact-sql.md)  
- [conjunto de backup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)  
  
Quando uma restauração é executada, se o conjunto de backup ainda não tiver sido registrado no banco de dados **msdb**, as tabelas de histórico de backup poderão ser modificadas.  
  
## <a name="security"></a>Segurança  
Começando pelo [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], as opções `PASSWORD` e `MEDIAPASSWORD` foram descontinuadas para a criação de backups. Ainda é possível restaurar backups criados com senhas.  
  
### <a name="permissions"></a>Permissões  
As permissões BACKUP DATABASE e BACKUP LOG usam como padrão os membros da função de servidor fixa **sysadmin** e as funções de banco de dados fixas **db_owner** e **db_backupoperator** .  
  
Os problemas de propriedade e permissão no arquivo físico do dispositivo de backup podem interferir em uma operação de backup. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser capaz de ler e gravar no dispositivo; a conta sob a qual o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executa deve ter permissões de gravação. No entanto, [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md), que adiciona uma entrada para um dispositivo de backup nas tabelas do sistema, não verifica permissões de acesso a arquivos. Esses problemas no arquivo físico do dispositivo de backup podem não aparecer até que o recurso físico seja acessado quando o backup ou restauração é tentado.  
  
##  <a name="examples"></a> Exemplos  
Esta seção contém os seguintes exemplos:  
  
- A. [Fazendo backup de um banco de dados completo](#backing_up_db)  
- b. [Fazendo backup do banco de dados e do log](#backing_up_db_and_log)  
- C. [Criando um backup completo de arquivos dos grupos de arquivos secundários](#full_file_backup)  
- D. [Criando um backup diferencial de arquivos dos grupos de arquivos secundários](#differential_file_backup)  
- E. [Criando e fazendo backup em um conjunto de mídias espelhado de uma única família](#create_single_family_mirrored_media_set)  
- F. [Criando e fazendo backup em um conjunto de mídias espelhado de várias famílias](#create_multifamily_mirrored_media_set)  
- G [Fazendo backup em um conjunto de mídias espelhado existente](#existing_mirrored_media_set)  
- H. [Criando um backup compactado em um novo conjunto de mídias](#creating_compressed_backup_new_media_set)  
- I. [Fazendo backup no serviço de Armazenamento de Blobs do Microsoft Azure](#url)  
  
> [!NOTE]  
> Os tópicos de instruções de backup contêm exemplos adicionais. Para obter mais informações, veja [Visão geral do backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md).  
  
###  <a name="backing_up_db"></a> A. Fazendo backup de um banco de dados completo  
O exemplo a seguir faz backup do banco de dados [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] em um arquivo de disco.  
  
```sql  
BACKUP DATABASE AdventureWorks2012   
 TO DISK = 'Z:\SQLServerBackups\AdvWorksData.bak'  
   WITH FORMAT;  
GO  
```  
  
###  <a name="backing_up_db_and_log"></a> B. Fazendo backup do banco de dados e do log  
O exemplo a seguir faz backup do banco de dados de exemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] que, por padrão, usa o modelo de recuperação simples. Para oferecer suporte a backups de log, o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] é modificado para usar o modelo de recuperação completa.  
  
Em seguida, o exemplo usa [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md) para criar um [dispositivo de backup](../../relational-databases/backup-restore/backup-devices-sql-server.md) lógico para fazer backup dos dados, `AdvWorksData`, e cria outro dispositivo de backup lógico para fazer backup do log, `AdvWorksLog`.  
  
Em seguida, o exemplo cria um backup de dados completo em `AdvWorksData` e, após um período de atividades de atualização, faz o backup do log em `AdvWorksLog`.  
  
```sql  
-- To permit log backups, before the full database backup, modify the database   
-- to use the full recovery model.  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
   SET RECOVERY FULL;  
GO  
-- Create AdvWorksData and AdvWorksLog logical backup devices.   
USE master  
GO  
EXEC sp_addumpdevice 'disk', 'AdvWorksData',   
'Z:\SQLServerBackups\AdvWorksData.bak';  
GO  
EXEC sp_addumpdevice 'disk', 'AdvWorksLog',   
'X:\SQLServerBackups\AdvWorksLog.bak';  
GO  
  
-- Back up the full AdventureWorks2012 database.  
BACKUP DATABASE AdventureWorks2012 TO AdvWorksData;  
GO  
-- Back up the AdventureWorks2012 log.  
BACKUP LOG AdventureWorks2012  
   TO AdvWorksLog;  
GO  
```  
  
> [!NOTE]  
>  Para um banco de dados de produção, faça backup do log regularmente. Os backups de log devem ser frequentes o suficiente para fornecer proteção contra perda de dados.  
  
###  <a name="full_file_backup"></a> C. Criando um backup completo de arquivos dos grupos de arquivos secundários  
O exemplo a seguir cria um backup de arquivo completo de todos os arquivos dos dois grupos de arquivos secundários.  
  
```sql  
--Back up the files in SalesGroup1:  
BACKUP DATABASE Sales  
   FILEGROUP = 'SalesGroup1',  
   FILEGROUP = 'SalesGroup2'  
   TO DISK = 'Z:\SQLServerBackups\SalesFiles.bck';  
GO  
```  
  
###  <a name="differential_file_backup"></a> D. Criando um backup diferencial de arquivos dos grupos de arquivos secundários  
O exemplo a seguir cria um backup diferencial de cada arquivo nos dois grupos de arquivos secundários.  
  
```sql  
--Back up the files in SalesGroup1:  
BACKUP DATABASE Sales  
   FILEGROUP = 'SalesGroup1',  
   FILEGROUP = 'SalesGroup2'  
   TO DISK = 'Z:\SQLServerBackups\SalesFiles.bck'  
   WITH   
      DIFFERENTIAL;  
GO  
```  
  
###  <a name="create_single_family_mirrored_media_set"></a> E. Criando e fazendo backup em um conjunto de mídias espelhado de uma única família  
O exemplo a seguir cria um conjunto de mídias espelhado que contêm uma única família de mídia e quatro espelhos nos quais faz backup do banco de dados [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)].  
  
```sql  
BACKUP DATABASE AdventureWorks2012  
TO TAPE = '\\.\tape0'  
MIRROR TO TAPE = '\\.\tape1'  
MIRROR TO TAPE = '\\.\tape2'  
MIRROR TO TAPE = '\\.\tape3'  
WITH  
   FORMAT,  
   MEDIANAME = 'AdventureWorksSet0';  
```  
  
###  <a name="create_multifamily_mirrored_media_set"></a> F. Criando e fazendo backup em um conjunto de mídias espelhado de várias famílias  
O exemplo a seguir cria um conjunto de mídias espelhado no qual cada espelho consiste em duas famílias de mídia. Em seguida, o exemplo faz backup do banco de dados [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] nos dois espelhos.  
  
```sql  
BACKUP DATABASE AdventureWorks2012  
TO TAPE = '\\.\tape0', TAPE = '\\.\tape1'  
MIRROR TO TAPE = '\\.\tape2', TAPE = '\\.\tape3'  
WITH  
   FORMAT,  
   MEDIANAME = 'AdventureWorksSet1';  
```  
  
###  <a name="existing_mirrored_media_set"></a> G. Fazendo backup em um conjunto de mídias espelhado existente  
O exemplo a seguir anexa um conjunto de backup ao conjunto de mídias criado no exemplo anterior.  
  
```sql  
BACKUP LOG AdventureWorks2012  
TO TAPE = '\\.\tape0', TAPE = '\\.\tape1'  
MIRROR TO TAPE = '\\.\tape2', TAPE = '\\.\tape3'  
WITH   
   NOINIT,  
   MEDIANAME = 'AdventureWorksSet1';  
```  
  
> [!NOTE]  
>  NOINIT, que é o padrão, é mostrado aqui para maior clareza.  
  
###  <a name="creating_compressed_backup_new_media_set"></a> H. Criando um backup compactado em um novo conjunto de mídias  
O exemplo a seguir formata a mídia, criando um novo conjunto de mídias e executa um backup completo compactado do banco de dados [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)].  
  
```sql  
BACKUP DATABASE AdventureWorks2012 TO DISK='Z:\SQLServerBackups\AdvWorksData.bak'   
WITH   
   FORMAT,   
   COMPRESSION;  
```  

###  <a name="url"></a> I. Fazer backup do serviço de Armazenamento de Blobs do Microsoft Azure 
O exemplo faz um backup completo do banco de dados do `Sales` no serviço de Armazenamento de Blobs do Microsoft Azure.  O nome da Conta de armazenamento é `mystorageaccount`.  O contêiner é chamado `myfirstcontainer`.  Uma política de acesso armazenado foi criada com direitos de leitura, gravação, exclusão e lista.  A credencial do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`, foi criada usando uma Assinatura de Acesso Compartilhado associada à Política de Acesso Armazenado.  Para obter informações sobre o backup do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no serviço de Armazenamento de Blobs do Microsoft Azure, consulte [Backup e restauração do SQL Server com o serviço de Armazenamento de Blobs do Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md) e [Backup do SQL Server em uma URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md).

```sql  
BACKUP DATABASE Sales
TO URL = 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer/Sales_20160726.bak'
WITH STATS = 5;
```
  
## <a name="see-also"></a>Consulte Também  
[Dispositivos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
[Conjuntos de mídias, famílias de mídia e conjuntos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
[Backups da parte final do log &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)   
[ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
[DBCC SQLPERF &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md)   
[RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
[RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)   
[RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)   
[RESTORE LABELONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)   
[RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)   
[sp_addumpdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
[sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
[sp_helpfile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpfile-transact-sql.md)   
[sp_helpfilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpfilegroup-transact-sql.md)   
[Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
[Restauração por etapas de bancos de dados com tabelas com otimização de memória](../../relational-databases/in-memory-oltp/piecemeal-restore-of-databases-with-memory-optimized-tables.md)  
  
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"

> [!div class="mx-tdCol2BreakAll"]  
> |||| 
> |---|---|---| 
> |[SQL Server](backup-transact-sql.md?view=sql-server-2016)|**_\* Instância gerenciada<br />do Banco de Dados SQL \*_** &nbsp;|[Parallel<br />Data Warehouse](backup-transact-sql.md?view=aps-pdw-2016)|  

&nbsp;

## <a name="azure-sql-database-managed-instance"></a>Instância gerenciada do Banco de Dados SQL do Azure

Faz backup de um Banco de Dados SQL colocado/hospedado em uma instância gerenciada do Banco de Dados SQL do Azure. A [instância gerenciada](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) do Banco de Dados SQL tem backups automáticos e permite aos usuários criar backups `COPY_ONLY` de bancos de dados completos. Não há suporte para backups de instantâneo de arquivo, log e diferencial.  

## <a name="syntax"></a>Sintaxe  
  
```sql 
BACKUP DATABASE { database_name | @database_name_var }   
  TO URL = { 'physical_device_name' | @physical_device_name_var }   [ ,...n ] 
  WITH COPY_ONLY [, { <general_WITH_options> } ]  
[;]  

<general_WITH_options> [ ,...n ]::=  
 
--Media Set Options  
   MEDIADESCRIPTION = { 'text' | @text_variable }   
 | MEDIANAME = { media_name | @media_name_variable }   
 | BLOCKSIZE = { blocksize | @blocksize_variable }
  
--Data Transfer Options  
   BUFFERCOUNT = { buffercount | @buffercount_variable }   
 | MAXTRANSFERSIZE = { maxtransfersize | @maxtransfersize_variable }  
  
--Error Management Options  
   { NO_CHECKSUM | CHECKSUM }  
 | { STOP_ON_ERROR | CONTINUE_AFTER_ERROR }  
  
--Compatibility Options  
   RESTART   
  
--Monitoring Options  
   STATS [ = percentage ]   
   
--Encryption Options  
 ENCRYPTION (ALGORITHM = { AES_128 | AES_192 | AES_256 | TRIPLE_DES_3KEY } , encryptor_options ) <encryptor_options> ::=   
   SERVER CERTIFICATE = Encryptor_Name | SERVER ASYMMETRIC KEY = Encryptor_Name   
```  
  
## <a name="arguments"></a>Argumentos  

DATABASE  
Especifica um backup completo do banco de dados. Durante um backup de banco de dados, a instância gerenciada faz backup suficiente do log de transações para produzir um banco de dados consistente quando o backup é restaurado.  

> [!IMPORTANT]
> Um backup de banco de dados criado em uma instância gerenciada só pode ser restaurado em outra instância gerenciada. Ele não pode ser restaurado para uma instância local do SQL Server (semelhante ao modo como um backup de um banco de dados do SQL Server 2016 não pode ser restaurado para uma instância do SQL Server 2012).
  
Ao restaurar um backup criado por BACKUP DATABASE (um *backup de dados*), o backup inteiro é restaurado. Para restaurar por meio de backups automáticos da instância gerenciada do Banco de Dados SQL do Azure, confira [Restauração do Banco de Dados SQL](https://docs.microsoft.com/azure/sql-database/sql-database-restore)  
  
{ *database_name* | **@**_database\_name\_var_ }   
É o banco de dados do qual é feito o backup do banco de dados completo. Se for fornecido como uma variável (**@**_database\_name\_var_), esse nome poderá ser especificado como uma constante de cadeia de caracteres (**@**_database\_name\_var_**=**_database name_) ou como uma variável de tipo de dados de cadeia de caracteres, exceto para os tipos de dados **ntext** ou **text**.  
  
Para obter mais informações, consulte [Backups completos de arquivos &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-file-backups-sql-server.md) e [Fazer backup de arquivos e grupos de arquivos &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md).  
  
  
TO URL

Especifica a URL a ser usada para a operação de backup. O formato da URL é usado para criar backups no serviço de armazenamento do Microsoft Azure. 

> [!IMPORTANT]  
> Para fazer backup em vários dispositivos ao fazer backup em uma URL, é necessário usar os tokens SAS (Assinatura de Acesso Compartilhado). Para obter exemplos sobre como criar uma Assinatura de Acesso Compartilhado, consulte [Backup do SQL Server em uma URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md) e [Simplificando a criação de credenciais do SQL com tokens SAS (Assinatura de Acesso Compartilhado) no Armazenamento do Azure com o PowerShell](https://blogs.msdn.com/b/sqlcat/archive/2015/03/21/simplifying-creation-sql-credentials-with-shared-access-signature-sas-keys-on-azure-storage-containers-with-powershell.aspx).  
  
*n*  
É um espaço reservado que indica que até 64 dispositivos de backup podem ser especificados em uma lista separada por vírgulas.  
  
### <a name="with-options"></a>Opções WITH  
Especifica opções a serem usadas com uma operação de backup.  
  
CREDENTIAL  
Usado somente durante a criação de um backup no serviço de Armazenamento de Blobs do Microsoft Azure.  
  
ENCRYPTION  
Usado para especificar a criptografia de um backup. Você pode especificar um algoritmo de criptografia para criptografar o backup ou especificar `NO_ENCRYPTION` para que o backup não seja criptografado. A criptografia é a prática recomendada para ajudar a proteger arquivos de backup. A lista de algoritmos que você pode especificar é:  
  
- `AES_128`  
- `AES_192`  
- `AES_256`  
- `TRIPLE_DES_3KEY`  
- `NO_ENCRYPTION`    

Se você optar pela criptografia, também precisará especificar o criptografador usando as opções do criptografador:  
  
- SERVER CERTIFICATE = Encryptor_Name  
- SERVER ASYMMETRIC KEY = Encryptor_Name  
  
**Opções de conjunto de backup**  
  
COPY_ONLY Especifica que o backup é um *backup somente cópia*, o que não afeta a sequência normal de backups. Um backup somente cópia é criado independentemente dos backups automáticos do Banco de Dados SQL do Azure. Para obter mais informações, veja [Backups somente cópia &#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md).  
  
{ COMPRESSION | NO_COMPRESSION }  
Especifica se a [compactação de backup](../../relational-databases/backup-restore/backup-compression-sql-server.md) é executada neste backup, substituindo o padrão de nível de servidor.  
  
O comportamento padrão é sem compactação de backup. No entanto, esse padrão pode ser alterado com a definição da opção [backup compression default](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md) de configuração do servidor. Para obter informações sobre como exibir o valor atual dessa opção, consulte [Exibir ou alterar propriedades do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/view-or-change-server-properties-sql-server.md).  

Para obter informações sobre como usar a compactação de backup com bancos de dados habilitados para [TDE (Transparent Data Encryption)](../../relational-databases/security/encryption/transparent-data-encryption.md), consulte a seção [Comentários](#general-remarks).
  
COMPRESSION  
Habilita explicitamente a compactação de backup.  
  
NO_COMPRESSION  
Desabilita explicitamente a compactação de backup.  
  
DESCRIPTION **=** { **'**_text_**'** | **@**_text\_variable_ }  
Especifica o texto de forma livre que descreve o conjunto de backup. A cadeia de caracteres pode conter um máximo de 255 caracteres.  
  
NAME **=** { *backup_set_name* | **@**_backup\_set\_var_ }  
Especifica o nome do conjunto de backup. Os nomes podem ter no máximo de 128 caracteres. Se NAME não estiver especificado, ele estará em branco.  
  
MEDIADESCRIPTION **=** { *text* | **@**_text\_variable_ }  
Especifica a descrição de texto de forma livre do conjunto de mídias, com um máximo de 255 caracteres.  
  
MEDIANAME **=** { *media_name* | **@**_media\_name\_variable_ }  
Especifica o nome da mídia de todo o conjunto de mídias de backup. O nome da mídia não deve ter mais de 128 caracteres. Se `MEDIANAME` for especificado, ele deverá corresponder ao nome da mídia especificado anteriormente já existente nos volumes de backup. Se não estiver especificado ou se a opção SKIP estiver especificada, não haverá nenhuma verificação do nome da mídia.  
  
BLOCKSIZE **=** { *blocksize* | **@**_blocksize\_variable_ }  
Especifica o tamanho do bloco físico, em bytes. Os tamanhos com suporte são 512, 1024, 2048, 4096, 8192, 16384, 32768 e 65536 (64 KB) bytes. O padrão é 65536 para dispositivos de fita e 512 para outros dispositivos. Normalmente, essa opção é desnecessária porque BACKUP seleciona automaticamente um tamanho de bloco apropriado ao dispositivo. A declaração explícita de um tamanho de bloco substitui a seleção automática de tamanho de bloco.  
  
**Opções de transferência de dados**  
  
BUFFERCOUNT **=** { *buffercount* | **@**_buffercount\_variable_ }  
Especifica o número total de buffers de E/S a ser usado para a operação de backup. É possível especificar qualquer inteiro positivo. No entanto, grandes números de buffers podem provocar erros de "memória insuficiente" devido a espaço de endereço virtual inadequado no processo Sqlservr.exe.  
  
O espaço total usado pelos buffers é determinado por: *buffercount/maxtransfersize*.  
  
> [!NOTE]  
> Para obter informações importantes sobre como usar a opção `BUFFERCOUNT`, confira o blog [BufferCount data transfer option can lead to OOM condition](https://blogs.msdn.com/b/sqlserverfaq/archive/2010/05/06/incorrect-buffercount-data-transfer-option-can-lead-to-oom-condition.aspx) (Opção incorreta de transferência de dados de BufferCount pode levar à condição OOM).  
  
MAXTRANSFERSIZE **=** { *maxtransfersize* | _**@** maxtransfersize\_variable_ } Especifica a maior unidade de transferência em bytes a ser usada entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e a mídia de backup. Os valores possíveis são múltiplos de 65536 bytes (64 KB), estendendo-se até 4194304 bytes (4 MB).  

> [!NOTE]  
> Para bancos de dados habilitados para [TDE (Transparent Data Encryption)](../../relational-databases/security/encryption/transparent-data-encryption.md) com um único arquivo de dados, o `MAXTRANSFERSIZE` padrão é 65.536 (64 KB). Para bancos de dados não criptografados com TDE, o `MAXTRANSFERSIZE` padrão é 1048576 (1 MB) ao usar o backup em DISK e 65536 (64 KB) ao usar VDI ou TAPE.
> Para obter mais informações sobre como usar a compactação de backup com bancos de dados criptografados com TDE, consulte a seção [Comentários](#general-remarks).
  
**Opções de gerenciamento de erros**  
  
Essas opções permitem determinar se as somas de verificação de backup estão habilitadas para a operação de backup e se a operação é interrompida quando um erro é encontrado.  
  
{ **NO_CHECKSUM** | CHECKSUM }  
Controla se somas de verificação de backup estão habilitadas.  
  
NO_CHECKSUM  
Desabilita explicitamente a geração de somas de verificação de backup (e a validação de somas de verificação de página). Esse é o comportamento padrão.  
  
CHECKSUM  
Especifica que a operação de backup verifica cada página quanto à soma de verificação e a página interrompida, se estiver habilitada e disponível, e gera uma soma de verificação para o backup inteiro.  
  
O uso de somas de verificação de backup pode afetar uma carga de trabalho e a taxa de transferência do backup.  
  
Para obter mais informações, consulte [Possíveis erros de mídia durante backup e restauração &#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md).  
  
{ **STOP_ON_ERROR** | CONTINUE_AFTER_ERROR }  
Controla se uma operação de backup para ou continua depois de encontrar um erro de soma de verificação de página.  
  
STOP_ON_ERROR  
Instrui BACKUP a falhar se uma soma de verificação de página não estiver correta. Esse é o comportamento padrão.  
  
CONTINUE_AFTER_ERROR  
Instrui BACKUP a continuar apesar de encontrar erros como somas de verificação inválidas ou páginas interrompidas.  
  
Se você não conseguir fazer backup da parte final do log usando a opção NO_TRUNCATE quando o banco de dados estiver danificado, tente fazer um [backup da parte final do log](../../relational-databases/backup-restore/tail-log-backups-sql-server.md) especificando CONTINUE_AFTER_ERROR em vez de NO_TRUNCATE.  
  
Para obter mais informações, consulte [Possíveis erros de mídia durante backup e restauração &#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md).  
  
**Opções de compatibilidade**  
  
RESTART  
Não tem nenhum efeito. Esta opção é aceita pela versão para compatibilidade com versões anteriores do SQL Server. 
  
**Opções de monitoramento**  
  
STATS [ **=** _percentage_ ]  
Exibe uma mensagem sempre que outro *percentual* for concluída e é usado para medir o progresso. Se *percentage* for omitido, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exibirá uma mensagem após a conclusão de cada 10%.  
  
A opção STATS informa a porcentagem concluída de acordo com o limite de relatório do próximo intervalo. Esse limite é aproximadamente a porcentagem especificada. Por exemplo, com STATS=10, se a quantidade concluída for 40%, a opção poderá exibir 43%. Para conjuntos de backup grandes, isso não é um problema, porque a porcentagem concluída muda muito lentamente entre chamadas de E/S concluídas.  
  
## <a name="limitations-for-sql-database-managed-instance"></a>Limitações para a instância gerenciada do Banco de Dados SQL
O tamanho máximo da faixa de backup é 195 GB (tamanho máximo do blob). Aumente o número de faixas no comando de backup para reduzir o tamanho da faixa individual e permaneça dentro desse limite.

## <a name="security"></a>Segurança  

### <a name="permissions"></a>Permissões  
As permissões BACKUP DATABASE usam como padrão os membros da função de servidor fixa **sysadmin** e as funções de banco de dados fixas **db_owner** e **db_backupoperator**.  
  
Os problemas de propriedade e permissão na URL podem interferir em uma operação de backup. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser capaz de ler e gravar no dispositivo; a conta sob a qual o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executa deve ter permissões de gravação.   
  
##  <a name="examples"></a> Exemplos  
O exemplo faz um backup COPY_ONLY do `Sales` no serviço de Armazenamento de Blobs do Microsoft Azure.  O nome da Conta de armazenamento é `mystorageaccount`.  O contêiner é chamado `myfirstcontainer`.  Uma política de acesso armazenado foi criada com direitos de leitura, gravação, exclusão e lista.  A credencial do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`, foi criada usando uma Assinatura de Acesso Compartilhado associada à Política de Acesso Armazenado.  Para obter informações sobre o backup do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no serviço de Armazenamento de Blobs do Microsoft Azure, consulte [Backup e restauração do SQL Server com o serviço de Armazenamento de Blobs do Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md) e [Backup do SQL Server em uma URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md).

```sql  
BACKUP DATABASE Sales
TO URL = 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer/Sales_20160726.bak'
WITH STATS = 5, COPY_ONLY;
```

  
## <a name="see-also"></a>Consulte Também  
  
[Restaurar banco de dados](restore-statements-transact-sql.md)

::: moniker-end
::: moniker range=">=aps-pdw-2016||=sqlallproducts-allversions"

> [!div class="mx-tdCol2BreakAll"]  
> |||| 
> |---|---|---| 
> |[SQL Server](backup-transact-sql.md?view=sql-server-2016)|[Instância gerenciada<br />do Banco de Dados SQL](backup-transact-sql.md?view=azuresqldb-mi-current)|**_\* Parallel<br />Data Warehouse \*_** &nbsp;|  

&nbsp;

## <a name="parallel-data-warehouse"></a>Parallel Data Warehouse

Cria um backup de um banco de dados do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] e armazena o backup fora do dispositivo em um local de rede especificado pelo usuário. Use esta instrução com [RESTORE DATABASE &#40;Parallel Data Warehouse&#41;](../../t-sql/statements/restore-statements-transact-sql.md) para recuperação de desastre ou para copiar um banco de dados de um dispositivo para outro.  
  
**Antes de começar a**, confira "Adquirir e configurar um servidor de backup" no [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
Há dois tipos de backup no [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. Um *backup completo de banco de dados* é um backup de um banco de dados inteiro do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. Um *backup diferencial de banco de dados* inclui apenas as alterações feitas desde o último backup completo. Um backup de um banco de dados de usuário inclui os usuários do banco de dados e as funções do banco de dados. Um backup do banco de dados mestre inclui os logons.  
  
Para obter mais informações sobre backups de banco de dados do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], confira "Backup e restauração" no [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
--Create a full backup of a user database or the master database.  
BACKUP DATABASE database_name  
    TO DISK = '\\UNC_path\backup_directory'  
    [ WITH [ ( ]  <with_options> [ ,...n ]  [ ) ] ]  
[;]  
  
--Create a differential backup of a user database.  
BACKUP DATABASE database_name  
    TO DISK = '\\UNC_path\backup_directory'  
    WITH [ ( ] DIFFERENTIAL   
    [ , <with_options> [ ,...n ] [ ) ]  
[;]  
  
<with_options> ::=  
    DESCRIPTION = 'text'  
    | NAME = 'backup_name'  
```  
  
## <a name="arguments"></a>Argumentos  
*database_name*  
O nome do banco de dados no qual o backup será criado. O banco de dados pode ser o banco de dados mestre ou um banco de dados de usuário.  
  
TO DISK = '\\\\*UNC_path*\\*backup_directory*'  
O caminho e o diretório de rede em que o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] gravará os arquivos de backup. Por exemplo, '\\\xxx.xxx.xxx.xxx\backups\2012\Monthly\08.2012.Mybackup'.  
  
- O caminho para o nome do diretório de backup já precisa existir e estar especificado como um caminho UNC totalmente qualificado.  
- O diretório de backup, *backup_directory*, não pode existir antes da execução do comando de backup. O [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] criará o diretório de backup.  
- O caminho para o diretório de backup não pode ser um caminho local e não pode ser um local em um dos nós de dispositivo do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
- O tamanho máximo do caminho UNC e do nome do diretório de backup é de 200 caracteres.  
- O servidor ou o host precisa ser especificado como um endereço IP.  Não é possível especificá-lo como o nome de host ou do servidor.  
  
DESCRIPTION = **'**_text_**'**  
Especifica uma descrição textual do backup. O comprimento máximo do texto é de 255 caracteres.  
  
A descrição é armazenada nos metadados e será exibida quando o cabeçalho do backup for restaurado com RESTORE HEADERONLY.  
  
NAME = **'**_backup \_name_**'**  
Especifica o nome do backup. O nome do backup pode ser diferente do nome do banco de dados.  
  
- Os nomes podem ter no máximo de 128 caracteres.  
- Não é possível incluir um caminho.  
- É necessário começar com um caractere de letra ou de número ou com um sublinhado (_). Os caracteres especiais permitidos são sublinhado (\_), hífen (-) ou espaço (). Os nomes de backup não podem terminar com um caractere de espaço.  
- A instrução falhará se *backup_name* já existir no local especificado.  
  
Esse nome é armazenado nos metadados e será exibido quando o cabeçalho do backup for restaurado com RESTORE HEADERONLY.  
  
DIFFERENTIAL  
Especifica a execução de um backup diferencial de um banco de dados de usuário. Se omitido, o padrão será um backup completo do banco de dados. O nome do backup diferencial não precisa corresponder ao nome do backup completo. Para controlar o diferencial e seu backup completo correspondente, considere usar o mesmo nome com 'completo' ou 'diferencial' anexado.  
  
Por exemplo:  
  
`BACKUP DATABASE Customer TO DISK = '\\xxx.xxx.xxx.xxx\backups\CustomerFull';`  
  
`BACKUP DATABASE Customer TO DISK = '\\xxx.xxx.xxx.xxx\backups\CustomerDiff' WITH DIFFERENTIAL;`  
  
## <a name="permissions"></a>Permissões  
Requer a permissão **BACKUP DATABASE** ou a associação à função de banco de dados fixa **db_backupoperator**. O banco de dados mestre não pode ser submetido a backup simplesmente por um usuário normal que tenha sido adicionado à função de banco de dados fixa **db_backupoperator**. O banco de dados mestre somente pode ser submetido a backup pela **SA**, pelo administrador da malha ou pelos membros da função de servidor fixa **sysadmin**.  
  
Requer uma conta do Windows que tenha permissão para acessar, criar e gravar no diretório de backup. O nome de conta do Windows e a senha também precisam ser armazenados no [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. Para adicionar essas credenciais de rede no [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o procedimento armazenado [sp_pdw_add_network_credentials &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md).  
  
Para obter mais informações sobre o gerenciamento de credenciais no [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], confira a seção [Segurança](#Security).  
  
## <a name="error-handling"></a>Tratamento de erros  
Erros de BACKUP DATABASE nas seguintes condições:  
  
- As permissões de usuário não são suficientes para executar um backup.  
- O [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] não tem as permissões corretas para o local de rede no qual backup será armazenado.
- O banco de dados não existe.  
- O diretório de destino já existe no compartilhamento de rede.  
- O compartilhamento de rede de destino não está disponível.  
- O compartilhamento de rede de destino não tem espaço suficiente para o backup. O comando BACKUP DATABASE não confirma a existência de espaço em disco suficiente antes de iniciar o backup, possibilitando a geração de um erro de falta de espaço em disco durante a execução de BACKUP DATABASE. Quando ocorrer falta de espaço em disco suficiente, o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] reverterá o comando BACKUP DATABASE. Para diminuir o tamanho do banco de dados, execute [DBCC SHRINKLOG (SQL Data Warehouse do Azure)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md)  
- Tentativa de iniciar um backup em uma transação.  
  
## <a name="general-remarks"></a>Comentários gerais  
Antes de executar um backup de banco de dados, use [DBCC SHRINKLOG (SQL Data Warehouse do Azure)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md) para diminuir o tamanho do banco de dados. 
 
Um backup do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] é armazenado como um conjunto de vários arquivos no mesmo diretório.  
  
Um backup diferencial geralmente leva menos tempo do que um backup completo e pode ser executado com mais frequência. Quando vários backups diferenciais se baseiam no mesmo backup completo, cada diferencial inclui todas as alterações do backup diferencial anterior.  
  
Se você cancelar um comando BACKUP, o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] removerá o diretório de destino e todos os arquivos criados para o backup. Se o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] perder a conectividade de rede com o compartilhamento, não será possível concluir a reversão.  
  
Os backups completos e os backups diferenciais são armazenados em diretórios separados. Não são impostas convenções de nomenclatura para especificar que um backup completo e um backup diferencial se pertencem. Controle isso usando suas próprias convenções de nomenclatura. Como alternativa, você pode controlar isso usando a opção WITH DESCRIPTION para adicionar uma descrição e, em seguida, usando a instrução RESTORE HEADERONLY para recuperar a descrição.  
  
## <a name="limitations-and-restrictions"></a>Limitações e Restrições  
Não é possível executar um backup diferencial do banco de dados mestre. Apenas os backups completos do banco de dados mestre são compatíveis.  
  
Os arquivos de backup são armazenados em um formato adequado para a restauração do backup em um dispositivo do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] usando a instrução [RESTORE DATABASE &#40;Parallel Data Warehouse&#41;](../../t-sql/statements/restore-statements-transact-sql.md).  
  
O backup com a instrução BACKUP DATABASE não pode ser usado para transferir dados ou informações de usuário para bancos de dados de SMP do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para essa funcionalidade, você pode usar o recurso de cópia de tabela remota. Para obter mais informações, consulte "Cópia de tabela remota" na [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
O [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] usa a tecnologia de backup do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para fazer backup e restaurar bancos de dados. As opções de backup do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são pré-configuradas para usar a compactação de backup. Não é possível definir as opções de backup, como compactação, soma de verificação, tamanho de bloco e contagem de buffer.  
  
Apenas um backup de banco de dados ou uma restauração pode ser executada no dispositivo de cada vez. O [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] coloca os comandos de backup ou restauração na fila até que o comando de backup ou de restauração atual seja concluído.  
  
O dispositivo de destino para restaurar o backup precisa ter pelo menos o mesmo número de nós de computação que o dispositivo de origem. O destino pode ter mais nós de computação do que o dispositivo de origem, mas não pode ter menos.  
  
O [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] não rastreia o local e os nomes de backups, pois os backups são armazenados fora do dispositivo.  
  
O [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] acompanha o êxito ou a falha dos backups de banco de dados.  
  
Um backup diferencial só será permitido se o último backup completo tiver sido concluído com êxito. Por exemplo, suponha que na segunda-feira você crie um backup completo do banco de dados de vendas e o backup seja concluído com êxito. Na terça-feira, você cria um backup completo do banco de dados de vendas e ele falha. Após essa falha, não será possível criar um backup diferencial com base no backup completo de segunda-feira. Primeiro você deverá criar um backup completo com êxito antes de criar um backup diferencial.  
  
## <a name="metadata"></a>Metadados  
Essas exibições de gerenciamento dinâmico contêm informações sobre todos os backup, as restauração e as operações de carregamento. As informações persistem entre os reinícios do sistema.  
  
- [sys.pdw_loader_backup_runs &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)  
- [sys.pdw_loader_backup_run_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)  
- [sys.pdw_loader_run_stages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-run-stages-transact-sql.md)  
## <a name="performance"></a>Desempenho  
Para executar um backup, o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] primeiro faz backup dos metadados e, em seguida, executa um backup paralelo dos dados do banco de dados armazenados nos nós de computação. Os dados são copiados diretamente de cada nó de computação para o diretório de backup. Para obter o melhor desempenho para mover dados dos nós de computação para o diretório de backup, o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] controla o número de nós de computação que estão copiando dados simultaneamente.  
  
## <a name="locking"></a>Bloqueio  
Coloca um bloqueio ExclusiveUpdate no objeto DATABASE.  
  
##  <a name="Security"></a> Segurança  
Os backups do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] não são armazenados no dispositivo. Portanto, sua equipe de TI é responsável por gerenciar todos os aspectos de segurança do backup. Por exemplo, isso inclui gerenciar a segurança dos dados de backup, a segurança do servidor usado para armazenar os backups e a segurança da infraestrutura de rede que conecta o servidor de backup ao dispositivo do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
**Gerenciar credenciais de rede**  
  
O acesso da rede ao diretório de backup baseia-se na segurança de compartilhamento de arquivos padrão do Windows. Antes de executar um backup, você precisa criar ou designar uma conta do Windows que será usada para autenticar o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] no diretório de backup. Essa conta do Windows precisa ter permissão para acessar, criar e gravar no diretório de backup.  
  
> [!IMPORTANT]  
> Para reduzir os riscos de segurança para seus dados, é recomendável designar uma conta do Windows exclusivamente para a finalidade de executar operações de backup e restauração. Permita que essa conta tenha permissões para o local de backup e não tenha para nenhum outro lugar.  
  
Você precisa armazenar o nome de usuário e a senha no [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] executando o procedimento armazenado [sp_pdw_add_network_credentials &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md). O [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] usa o Gerenciador de Credenciais do Windows para armazenar e criptografar os nomes de usuário e as senhas no nó de controle e nos nós de computação. As credenciais não são submetidas a backup com o comando BACKUP DATABASE.  
  
Para remover as credenciais de rede do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], confira [sp_pdw_remove_network_credentials &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md).  
  
Para listar todas as credenciais de rede armazenadas no [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use a exibição de gerenciamento dinâmico [sys.dm_pdw_network_credentials &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-add-network-credentials-for-the-backup-location"></a>A. Adicionar as credenciais de rede para o local de backup  
Para criar um backup, o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] precisa ter permissão de leitura/gravação para o diretório de backup. O exemplo a seguir mostra como adicionar as credenciais para um usuário. O [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] armazenará essas credenciais e as usará para as operações de backup e restauração.  
  
> [!IMPORTANT]  
> Por motivos de segurança, é recomendável criar uma conta de domínio exclusivamente para a finalidade de executar backups.  
  
```sql  
EXEC sp_pdw_add_network_credentials 'xxx.xxx.xxx.xxx', 'domain1\backupuser', '*****';  
```  
  
### <a name="b-remove-network-credentials-for-the-backup-location"></a>b. Remover as credenciais de rede do local de backup  
O exemplo a seguir mostra como remover as credenciais de um usuário de domínio do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
```sql  
EXEC sp_pdw_remove_network_credentials 'xxx.xxx.xxx.xxx';  
```  
  
### <a name="c-create-a-full-backup-of-a-user-database"></a>C. Criar um backup completo de um banco de dados de usuário  
O exemplo a seguir cria um backup completo do banco de dados de usuário de faturas. O [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] criará o diretório Invoices2013 e salvará os arquivos de backup no diretório \\\10.192.63.147\backups\yearly\Invoices2013Full.  
  
```sql  
BACKUP DATABASE Invoices TO DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full';  
```  
  
### <a name="d-create-a-differential-backup-of-a-user-database"></a>D. Criar um backup diferencial de um banco de dados de usuário  
O exemplo a seguir cria um backup diferencial, que inclui todas as alterações feitas desde o último backup completo do banco de dados de faturas. O [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] criará o diretório \\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff no qual armazenará os arquivos. A descrição 'Invoices 2013 differential backup' será armazenada com as informações de cabeçalho do backup.  
  
O backup diferencial só será executado com êxito se o último backup completo do banco de dados de faturas for concluído com êxito.  
  
```sql  
BACKUP DATABASE Invoices TO DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff'  
    WITH DIFFERENTIAL,   
    DESCRIPTION = 'Invoices 2013 differential backup';  
```  
  
### <a name="e-create-a-full-backup-of-the-master-database"></a>E. Criar um backup completo do banco de dados mestre  
O exemplo a seguir cria um backup completo do banco de dados mestre e armazena-o no diretório '\\\10.192.63.147\backups\2013\daily\20130722\master'.  
  
```sql  
BACKUP DATABASE master TO DISK = '\\xxx.xxx.xxx.xxx\backups\2013\daily\20130722\master';  
```  
  
### <a name="f-create-a-backup-of-appliance-login-information"></a>F. Criar um backup das informações de logon do dispositivo.  
O banco de dados mestre armazena as informações de logon do dispositivo. Para fazer backup das informações de logon do dispositivo é necessário fazer o backup do mestre.  
  
O exemplo a seguir cria um backup completo do banco de dados mestre.  
  
```sql  
BACKUP DATABASE master TO DISK = '\\xxx.xxx.xxx.xxx\backups\2013\daily\20130722\master'  
WITH (   
    DESCRIPTION = 'Master Backup 20130722',  
    NAME = 'login-backup'  
)  
;  
```  
  
## <a name="see-also"></a>Consulte Também  
[RESTORE DATABASE &#40;Parallel Data Warehouse&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   

::: moniker-end
