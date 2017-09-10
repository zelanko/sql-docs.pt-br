---
title: BACKUP (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/05/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 275
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 60272ce672c0a32738b0084ea86f8907ec7fc0a5
ms.openlocfilehash: ac638619fc3117551c774ecc26a43cae72826d39
ms.contentlocale: pt-br
ms.lasthandoff: 09/06/2017

---
# <a name="backup-transact-sql"></a>BACKUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Faz o backup completo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados para criar um backup de banco de dados, ou um ou mais arquivos ou grupos de arquivos do banco de dados para criar um backup de arquivo (banco de dados de BACKUP). Além disso, no modelo de recuperação completa ou no modelo de recuperação bulk-logged, faz o backup do log de transações do banco de dados para criar um backup de log (BACKUP LOG).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
``` 
Backing Up a Whole Database   
BACKUP DATABASE { database_name | @database_name_var }   
  TO <backup_device> [ ,...n ]   
  [ <MIRROR TO clause> ] [ next-mirror-to ]  
  [ WITH { DIFFERENTIAL | <general_WITH_options> [ ,...n ] } ]  
[;]  
  
Backing Up Specific Files or Filegroups  
BACKUP DATABASE { database_name | @database_name_var }   
 <file_or_filegroup> [ ,...n ]   
  TO <backup_device> [ ,...n ]   
  [ <MIRROR TO clause> ] [ next-mirror-to ]  
  [ WITH { DIFFERENTIAL | <general_WITH_options> [ ,...n ] } ]  
[;]  
  
Creating a Partial Backup  
BACKUP DATABASE { database_name | @database_name_var }   
 READ_WRITE_FILEGROUPS [ , <read_only_filegroup> [ ,...n ] ]  
  TO <backup_device> [ ,...n ]   
  [ <MIRROR TO clause> ] [ next-mirror-to ]  
  [ WITH { DIFFERENTIAL | <general_WITH_options> [ ,...n ] } ]  
[;]  
  
Backing Up the Transaction Log (full and bulk-logged recovery models)  
BACKUP LOG { database_name | @database_name_var }   
  TO <backup_device> [ ,...n ]   
  [ <MIRROR TO clause> ] [ next-mirror-to ]  
  [ WITH { <general_WITH_options> | \<log-specific_optionspec> } [ ,...n ] ]  
[;]  
  
<backup_device>::=   
 {  
   { logical_device_name | @logical_device_name_var }   
 | { DISK | TAPE | URL} =   
     { 'physical_device_name' | @physical_device_name_var }  
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
  
--Tape Options  
   { REWIND | NOREWIND }   
 | { UNLOAD | NOUNLOAD }   
  
--Log-specific Options  
   { NORECOVERY | STANDBY = undo_file_name }  
 | NO_TRUNCATE  
  
--Encryption Options  
 ENCRYPTION (ALGORITHM = { AES_128 | AES_192 | AES_256 | TRIPLE_DES_3KEY } , encryptor_options ) <encryptor_options> ::=   
   SERVER CERTIFICATE = Encryptor_Name | SERVER ASYMMETRIC KEY = Encryptor_Name   
```  
  
## <a name="arguments"></a>Argumentos  
 DATABASE  
 Especifica um backup completo do banco de dados. Se uma lista de arquivos e grupos de arquivos estiver especificada, será feito o backup apenas desses arquivos e grupos de arquivos. Durante um backup completo ou diferencial do banco de dados, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] faz backup suficiente do log de transações para produzir um banco de dados consistente quando o backup é restaurado.  
  
 Quando você restaurar um backup criado pelo BACKUP do banco de dados (um *backup de dados*), todo o backup é restaurado. Somente um backup de log pode ser restaurado em uma transação ou momento específico dentro do backup.  
  
> [!NOTE]  
>  Apenas um backup completo do banco de dados pode ser executado no **mestre** banco de dados.  
  
 LOG  
 Especifica um backup apenas do log de transações. O backup do log é feito a partir do último backup do log executado com êxito até o final do log atual. Para poder criar o primeiro backup de log, você deve criar um backup completo.  
  
 Você pode restaurar um backup de log em uma transação dentro do backup ou uma hora específica, especificando WITH STOPAT, STOPATMARK ou STOPBEFOREMARK em seu [RESTORE LOG](../../t-sql/statements/restore-statements-transact-sql.md) instrução.  
  
> [!NOTE]  
>  Após um backup de log típico, alguns registros do log de transações se tornam inativos, a menos que você especifique WITH NO_TRUNCATE ou COPY_ONLY. O log é truncado depois que todos os registros contidos em um ou mais arquivos de log virtual se tornam ativos. Se o log não estiver sendo truncado após backups de log de rotina, algo pode estar atrasando o truncamento do log. Para obter mais informações, consulte:  
  
 { *database_name*| **@**database_name_var *}  
 É o banco de dados do qual é feito o backup do log de transações, do banco de dados parcial ou do banco de dados completo. Se fornecido como uma variável (**@***database_name_var*), esse nome pode ser especificado como uma constante de cadeia de caracteres ( **@**   *database_name_var***=***nome do banco de dados*) ou como uma variável do tipo de dados de cadeia de caracteres, exceto para o **ntext** ou **texto** tipos de dados.  
  
> [!NOTE]  
>  O backup do banco de dados espelho em uma parceria de espelhamento de banco de dados não pode ser feito.  
  
\<file_or_filegroup > [ **,**...  *n*  ] Usado apenas com BACKUP DATABASE, especifica um arquivo de banco de dados ou grupo de arquivos para incluir em um backup de arquivo ou especifica um arquivo somente leitura ou um grupo de arquivos para incluir em um backup parcial.  
  
 ARQUIVO  **=**  { *logical_file_name*| **@***logical_file_name_var* }  
 É o nome lógico de um arquivo ou variável cujo valor é igual ao nome lógico de um arquivo que deve ser incluído no backup.  
  
 Grupo de arquivos  **=**  { *logical_filegroup_name*| **@***logical_filegroup_name_var* }  
 É o nome lógico de um grupo de arquivos ou variável cujo valor é igual ao nome lógico de um grupo de arquivos que deve ser incluído no backup. No modelo de recuperação simples, um backup de grupo de arquivos é permitido apenas para grupos de arquivos somente leitura.  
  
> [!NOTE]  
>  Considere usar backups de arquivo quando o tamanho do banco de dados e as exigências de desempenho tornarem um backup de banco de dados impraticável.  
  
 *n*  
 É um espaço reservado que indica que vários arquivos e grupos de arquivos podem ser especificados em uma lista separada por vírgulas. O número é ilimitado. 
  
 Para obter mais informações, consulte: [Backups completos de arquivos &#40; SQL Server &#41; ](../../relational-databases/backup-restore/full-file-backups-sql-server.md) e [fazer backup de arquivos e grupos de arquivos &#40; SQL Server &#41; ](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md).  
  
 READ_WRITE_FILEGROUPS [ **,** FILEGROUP = { *logical_filegroup_name*| **@***logical_filegroup_name_var* } [ **,**... *n* ] ]  
 Especifica um backup parcial. Um backup parcial inclui todos os arquivos de leitura/gravação em um banco de dados: o grupo de arquivos primário e quaisquer grupos de arquivos secundários de leitura/gravação e também quaisquer arquivos ou grupos de arquivos somente leitura especificados.  
  
 READ_WRITE_FILEGROUPS  
 Especifica que o backup de todos os grupos de arquivos de leitura/gravação seja feito no backup parcial. Se o banco de dados for somente leitura, READ_WRITE_FILEGROUPS incluirá apenas o grupo de arquivos primário.  
  
> [!IMPORTANT]  
>  A listagem explícita de grupos de arquivos de leitura/gravação usando FILEGROUP em vez de READ_WRITE_FILEGROUPS cria um backup de arquivo.  
  
 Grupo de arquivos = { *logical_filegroup_name*| **@***logical_filegroup_name_var* }  
É o nome lógico de um grupo de arquivos somente leitura ou de uma variável cujo valor é igual ao nome lógico de um grupo de arquivos somente leitura que deve ser incluído no backup parcial. Para obter mais informações, consulte "\<file_or_filegroup >," anteriormente neste tópico.
  
 *n*  
 É um espaço reservado que indica que vários grupos de arquivos somente leitura podem ser especificados em uma lista separada por vírgulas.  
  
 Para obter mais informações sobre backups parciais, consulte [Backups parciais &#40; SQL Server &#41; ](../../relational-databases/backup-restore/partial-backups-sql-server.md).  
  
PARA \<backup_device > [ **,**...  *n*  ] Indica que o conjunto de acompanhamento de [dispositivos de backup](../../relational-databases/backup-restore/backup-devices-sql-server.md) é um conjunto de mídias não espelhado ou o primeiro dos espelhos dentro de um conjunto (por que um ou mais MIRROR TO de mídias espelhado as cláusulas são declaradas).  
  
\<backup_device > especifica um dispositivo de backup lógico ou físico a ser usado para a operação de backup.  
  
 { *logical_device_name* | **@***logical_device_name_var* }  
 É o nome lógico do dispositivo de backup no qual o backup do banco de dados é feito. O nome lógico deve seguir as regras para identificadores. Se fornecido como uma variável (@*logical_device_name_var*), o nome de dispositivo de backup pode ser especificado como uma constante de cadeia de caracteres (@*logical_device_name_var*  **=**  nome de dispositivo de backup lógico) ou como uma variável de qualquer tipo de dados de cadeia de caracteres do caractere exceto para o **ntext** ou **texto** tipos de dados.  
  
 {DISK | FITA | URL}  **=**  { **'***physical_device_name***'**  |   **@**  *physical_device_name_var* }  
 Especifica um arquivo de disco ou dispositivo de fita, ou um serviço de armazenamento de Blob do Windows Azure. O formato de URL é usado para a criação de backups para o serviço de armazenamento do Windows Azure. Para obter mais informações e exemplos, consulte [SQL Server Backup e restauração com o serviço de armazenamento de BLOBs do Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md). Para obter um tutorial, consulte [Tutorial: SQL Server Backup e restauração para o serviço de armazenamento de Blob do Windows Azure](~/relational-databases/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md).  
  
> [!IMPORTANT]  
>  Com [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2 até [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], você pode somente fazer backup em um único dispositivo durante o backup para URL. Para fazer o backup em vários dispositivos ao fazer backup em URL, você deve usar [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e você deve usar os tokens de assinatura de acesso compartilhado (SAS). Para obter exemplos sobre como criar uma assinatura de acesso compartilhado, consulte [Backup do SQL Server para URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md) e [simplificando a criação de credenciais do SQL com tokens de assinatura de acesso compartilhado (SAS) no armazenamento do Azure com o Powershell](http://blogs.msdn.com/b/sqlcat/archive/2015/03/21/simplifying-creation-sql-credentials-with-shared-access-signature-sas-keys-on-azure-storage-containers-with-powershell.aspx).  
  
**URL se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2 até [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
  
 Um dispositivo de disco não precisa existir antes de ser especificado em uma instrução BACKUP. Se o dispositivo físico existir e a opção INIT não estiver especificada na instrução BACKUP, o backup será anexado ao dispositivo.  
  
 Para obter mais informações, consulte [Dispositivos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).  
  
> [!NOTE]  
>  A opção TAPE será removida em uma futura versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam.  
  
 *n*  
 É um espaço reservado que indica que até 64 dispositivos de backup podem ser especificados em uma lista separada por vírgulas.  
  
MIRROR TO \<backup_device > [ **,**...  *n*  ] Especifica um conjunto de até três dispositivos de backup secundários, cada um dos quais espelhos dispositivos backups especificados na cláusula TO. A cláusula MIRROR TO deve especificar o mesmo tipo e número de dispositivos de backup que a cláusula TO. O número máximo de cláusulas MIRROR TO é três.  
  
 Essa opção está disponível somente na edição Enterprise do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Para que MIRROR TO = DISK, BACKUP determine automaticamente o tamanho do bloco apropriado para dispositivos de disco. Para obter mais informações sobre tamanho de bloco, consulte "BLOCKSIZE", mais adiante nesta tabela.  
  
\<backup_device > consulte "\<backup_device >," anteriormente nesta seção.
  
 *n*  
 É um espaço reservado que indica que até 64 dispositivos de backup podem ser especificados em uma lista separada por vírgulas. O número de dispositivos na cláusula MIRROR TO deve ser igual ao número de dispositivos na cláusula TO.  
  
 Para obter mais informações, consulte "Famílias de Mídia em Conjunto de Mídia Espelhados", na seção "Comentários" posteriormente neste tópico.  
  
 [ *espelho Avançar para* ]  
 É um espaço reservado que indica que uma única instrução BACKUP pode conter até três cláusulas MIRROR TO, além da única cláusula TO.  
  
### <a name="with-options"></a>Opções WITH  
 Especifica opções a serem usadas com uma operação de backup.  
  
 CREDENTIAL  
 Usado somente durante a criação de um backup no serviço de armazenamento do Blob do Windows Azure.  
  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2 até [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
  
 FILE_SNAPSHOT  
 Usado para criar um instantâneo do Azure dos arquivos de banco de dados quando todos os arquivos de banco de dados do SQL Server são armazenados usando o serviço de armazenamento de BLOBs do Azure. Para obter mais informações, consulte [arquivos de dados do SQL Server no Microsoft Azure](../../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md). [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Backup de instantâneo usa instantâneos do Azure dos arquivos de banco de dados (arquivos de log e de dados) em um estado consistente. Um conjunto consistente de instantâneos do Azure compõem um backup e são registrados no arquivo de backup. A única diferença entre **BACKUP de banco de dados para URL com FILE_SNAPSHOT** e **BACKUP LOG para URL com FILE_SNAPSHOT** é que o último também trunca o log de transações enquanto o primeiro não. Com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Backup do instantâneo, após o backup inicial completo que é exigido pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para estabelecer a cadeia de backup, somente um backup de log de transações único é necessário para restaurar um banco de dados para o ponto no tempo do backup de log de transações. Além disso, apenas dois backups de log de transações são necessários para restaurar um banco de dados para um ponto no tempo entre a hora dos backups de log de transação de dois.  
  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
  
 DIFFERENTIAL  
 Usado apenas com BACKUP DATABASE, especifica que o backup de banco de dados ou de arquivo deve consistir apenas das partes do banco de dados ou arquivo alterado desde o último backup completo. Um backup diferencial normalmente usa menos espaço do que um backup completo. Use essa opção para que todos os backups de log individuais executados desde o último backup não precisem ser aplicados.  
  
> [!NOTE]  
>  Por padrão, o BACKUP DATABASE cria um backup completo.  
  
 Para obter mais informações, veja [Backups diferenciais &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md).  
  
 ENCRYPTION  
 Usado para especificar a criptografia de um backup. Você pode especificar um algoritmo de criptografia para criptografar o backup ou especificar ‘NO_ENCRYPION’ para que o backup não seja criptografado. A criptografia é a prática recomendada para ajudar a proteger arquivos de backup. A lista de algoritmos que você pode especificar é:  
  
-   AES_128  
  
-   AES_192  
  
-   AES_256  
  
-   TRIPLE_DES_3KEY  
  
-   NO_ENCRYPTION  
  
 Se você optar pela criptografia, também precisará especificar o criptografador usando as opções do criptografador:  
  
-   SERVER CERTIFICATE = Encryptor_Name  
  
-   SERVER ASYMMETRIC KEY = Encryptor_Name  
  
    > [!WARNING]  
    >  Quando a criptografia é usada em conjunto com o argumento FILE_SNAPSHOT, o arquivo de metadados é criptografado usando o algoritmo de criptografia especificado e o sistema verifica se a TDE foi concluída para o banco de dados. Nenhuma criptografia adicional ocorre para os dados em si. O backup falhará se o banco de dados não foi criptografado ou se a criptografia não foi concluída antes da instrução backup foi emitida.  
  
 **Opções de conjunto de backup**  
  
 Essas opções funcionam no conjunto de backup criado por esta operação de backup.  
  
> [!NOTE]  
>  Para especificar um conjunto de backup para uma operação de restauração, use o arquivo  **=**   *\<backup_set_file_number >* opção. Para obter mais informações sobre como especificar um conjunto de backup, consulte "Especificando um conjunto de Backup" no [argumentos RESTORE &#40; Transact-SQL &#41; ](../../t-sql/statements/restore-statements-arguments-transact-sql.md).
  
 COPY_ONLY  
 Especifica se o backup é um *backup somente cópia*, que não afeta a sequência normal de backups. Um backup somente cópia é criado independentemente de seus backups convencionais agendados regularmente. Um backup somente cópia não afeta o backup global e restaura procedimentos do banco de dados.  
  
 Backups somente cópia devem ser usados em situações em que um backup é feito com um objetivo especial, como fazer backup de log antes de uma restauração de arquivo online. Normalmente, um backup de log somente cópia é usado uma vez e excluído em seguida.  
  
-   Quando usado com BACKUP DATABASE, a opção COPY_ONLY cria um backup completo que não pode servir como uma base diferencial. O bitmap diferencial não é atualizado e backups diferenciais se comportam como se o backup somente cópia não existisse. Backups diferenciais subseqüentes usam o backup completo convencional mais recente como base.  
  
    > [!IMPORTANT]  
    >  Se as opções DIFFERENTIAL e COPY_ONLY forem usadas em conjunto, COPY_ONLY será ignorado e um backup diferencial será criado.  
  
-   Quando usado com o LOG de BACKUP, a opção COPY_ONLY cria um *backup de log somente cópia*, que não trunca o log de transações. O backup de log somente cópia não tem nenhum efeito na cadeia de logs e outros backups de log se comportam como se o backup somente cópia não existisse.  
  
 Para obter mais informações, veja [Backups somente cópia &#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md).  
  
 { COMPRESSION | NO_COMPRESSION }  
 Em [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] e versões posteriores somente, especifica se [compactação de backup](../../relational-databases/backup-restore/backup-compression-sql-server.md) é executada neste backup, substituindo o padrão de nível de servidor.  
  
 Na instalação, o comportamento padrão é sem compactação de backup. Mas esse padrão pode ser alterado definindo a [padrão de compactação de backup](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md) opção de configuração do servidor. Para obter informações sobre como exibir o valor atual dessa opção, consulte [exibir ou alterar propriedades do servidor &#40; SQL Server &#41; ](../../database-engine/configure-windows/view-or-change-server-properties-sql-server.md).  
  
 COMPRESSION  
 Habilita explicitamente a compactação de backup.  
  
 NO_COMPRESSION  
 Desabilita explicitamente a compactação de backup.  
  
 DESCRIPTION **=** { **'***text***'** | **@***text_variable* }  
 Especifica o texto de forma livre que descreve o conjunto de backup. A cadeia de caracteres pode conter um máximo de 255 caracteres.  
  
 NOME  **=**  { *backup_set_name*| **@***backup_set_var* }  
 Especifica o nome do conjunto de backup. Os nomes podem ter no máximo de 128 caracteres. Se NAME não estiver especificado, ele estará em branco.  
  
 {EXPIREDATE **='***data***'**| RETAINDAYS  **=**  *dias* }  
 Especifica quando o conjunto de backup desse backup pode ser substituído. Se essas duas opções forem usadas, RETAINDAYS terá precedência sobre EXPIREDATE.  
  
 Se nenhuma opção for especificada, a data de validade é determinada pelo **mediaretention** configuração. Para obter mais informações, consulte [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
> [!IMPORTANT]  
>  Essas opções apenas impedem que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] substitua um arquivo. Fitas podem ser apagadas por outros métodos e os arquivos de disco podem ser excluídos pelo sistema operacional. Para obter mais informações sobre verificação de validade, consulte SKIP e FORMAT neste tópico.  
  
 EXPIREDATE  **=**  { **'***data***'** |   **@**  *date_var* }  
 Especifica quando o conjunto de backup vence e pode ser substituído. Se fornecido como uma variável (@*date_var*), essa data deve seguir o sistema configurado **datetime** Formatar e ser especificado como um dos seguintes:  
  
-   Uma constante de cadeia de caracteres (@*date_var*  **=**  data)  
  
-   Uma variável de tipo de dados de cadeia de caracteres (exceto para o **ntext** ou **texto** tipos de dados)  
  
-   Um **smalldatetime**  
  
-   Um **datetime** variável  
  
 Por exemplo:  
  
-   `'Dec 31, 2020 11:59 PM'`  
  
-   `'1/1/2021'`  
  
 Para obter informações sobre como especificar **datetime** valores, consulte [tipos de data e hora](../../t-sql/data-types/date-and-time-types.md).  
  
> [!NOTE]  
>  Para ignorar a data de validade, use a opção SKIP.  
  
 RETAINDAYS  **=**  { *dias*| **@***days_var* }  
 Especifica o número de dias que devem decorrer para que este conjunto de mídias de backup possa ser substituído. Se fornecido como uma variável (**@***days_var*), ele deve ser especificado como um inteiro.  
  
 **Opções do conjunto de mídias**  
  
 Essas opções funcionam no conjunto de mídias como um todo.  
  
 { **NOINIT** | INIT}  
 Controla se a operação de backup anexa ou substitui os conjuntos de backup existentes na mídia de backup. O padrão é anexar ao backup mais recente definido na mídia (NOINIT).  
  
> [!NOTE]  
>  Para obter informações sobre as interações entre { **NOINIT** | INIT} e { **NOSKIP** | SKIP}, consulte "Comentários" mais adiante neste tópico.  
  
 NOINIT  
 Indica que o conjunto de backup é anexado ao conjunto de mídias especificado, preservando conjuntos de backup existentes. Se uma senha de mídia estiver definida para o conjunto de mídias, a senha deverá ser fornecida. NOINIT é o padrão.  
  
 Para obter mais informações, veja [Conjuntos de mídias, famílias de mídia e conjuntos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md).  
  
 INIT  
 Especifica que todos os conjuntos de backup devem ser substituídos, mas preserva o cabeçalho de mídia. Se INIT estiver especificado, qualquer conjunto de backup existente naquele dispositivo será substituído, se as condições permitirem. Por padrão, BACKUP verificará as seguintes condições e não substituirá a mídia de backup se qualquer uma delas existir:  
  
-   Um conjunto de backup ainda não expirou. Para obter mais informações, consulte as opções EXPIREDATE e RETAINDAYS.  
  
-   O nome do conjunto de backup fornecido na instrução BACKUP, se fornecido, não corresponde ao nome na mídia de backup. Para obter mais informações, consulte a opção NAME, anteriormente nesta seção.  
  
 Para substituir essas verificações, use a opção SKIP.  
  
 Para obter mais informações, veja [Conjuntos de mídias, famílias de mídia e conjuntos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md).  
  
 { **NOSKIP** | IGNORAR}  
 Controla se a operação de backup verifica a data e a hora de validade dos conjuntos de backup existentes na mídia antes de substituí-los.  
  
> [!NOTE]  
>  Para obter informações sobre as interações entre { **NOINIT** | INIT} e { **NOSKIP** | SKIP}, consulte "Comentários" mais adiante neste tópico.  
  
 NOSKIP  
 Instrui a instrução BACKUP a verificar a data de validade de todos os conjuntos de backup na mídia antes de permitir que eles sejam substituídos. Esse é o comportamento padrão.  
  
 SKIP  
 Desabilita a verificação de validade e nome do conjunto de backup que normalmente é executada pela instrução BACKUP para impedir a substituição de conjuntos de backup. Para obter informações sobre as interações entre { INIT | NOINIT } e { NOSKIP | SKIP }, consulte "Comentários", mais adiante neste tópico.  
  
 Para exibir as datas de expiração dos conjuntos de backup, consulte o **expiration_date** coluna o [backupset](../../relational-databases/system-tables/backupset-transact-sql.md) tabela de histórico.  
  
 { **NOFORMAT** | FORMATO}  
 Especifica se o cabeçalho da mídia deve ser gravado nos volumes usados para esta operação de backup, substituindo qualquer cabeçalho de mídia e conjuntos de backup existentes.  
  
 NOFORMAT  
 Especifica que a operação de backup preserva o cabeçalho da mídia e os conjuntos de backup existentes nos volumes de mídia usados para esta operação de backup. Esse é o comportamento padrão.  
  
 FORMAT  
 Especifica que um novo conjunto de mídias deve ser criado. FORMAT faz com que a operação de backup grave um novo cabeçalho de mídia em todos os volumes de mídia usados para a operação de backup. O conteúdo existente do volume se torna inválido, porque qualquer cabeçalho de mídia e conjuntos de backup existentes são substituídos.  
  
> [!IMPORTANT]  
>  Use FORMAT com cuidado. A formatação de qualquer volume de um conjunto de mídias renderiza todo o conjunto de mídias como inutilizável. Por exemplo, se você iniciar uma única fita pertencente a um conjunto de mídias distribuído existente, todo o conjunto de mídias será renderizado como inútil.  
  
 A especificação de FORMAT implica SKIP. SKIP não precisa ser declarado explicitamente.  
  
 MEDIADESCRIPTION  **=**  { *texto* | **@***text_variable* }  
 Especifica a descrição de texto de forma livre do conjunto de mídias, com um máximo de 255 caracteres.  
  
 MEDIANAME  **=**  { *media_name* | **@***media_name_variable* }  
 Especifica o nome da mídia de todo o conjunto de mídias de backup. O nome da mídia não deve ter mais de 128 caracteres. Se MEDIANAME estiver especificado, ele deverá corresponder ao nome da mídia especificado anteriormente já existente nos volumes de backup. Se não estiver especificado ou se a opção SKIP estiver especificada, não haverá nenhuma verificação do nome da mídia.  
  
 Tamanho de bloco  **=**  { *blocksize* | **@***blocksize_variable* }  
 Especifica o tamanho do bloco físico, em bytes. Os tamanhos com suporte são 512, 1024, 2048, 4096, 8192, 16384, 32768 e 65536 (64 KB) bytes. O padrão é 65536 para dispositivos de fita e 512 para outros dispositivos. Normalmente, essa opção é desnecessária porque BACKUP seleciona automaticamente um tamanho de bloco apropriado ao dispositivo. A declaração explícita de um tamanho de bloco substitui a seleção automática de tamanho de bloco.  
  
 Se estiver fazendo um backup que planeja copiar e restaurar de um CD-ROM, especifique BLOCKSIZE=2048.  
  
> [!NOTE]  
>  Normalmente, essa opção afeta o desempenho apenas durante a gravação em dispositivos de fita.  
  
 **Opções de transferência de dados**  
  
 BUFFERCOUNT  **=**  { *buffercount* | **@***buffercount_variable* }  
 Especifica o número total de buffers de E/S a ser usado para a operação de backup. É possível especificar qualquer inteiro positivo. No entanto, grandes números de buffers podem provocar erros de "memória insuficiente" devido a espaço de endereço virtual inadequado no processo Sqlservr.exe.  
  
 O espaço total usado pelos buffers é determinado por: *buffercount***\****maxtransfersize*.  
  
> [!NOTE]  
>  Para obter informações importantes sobre como usar a opção de BUFFERCOUNT, consulte o [opção de transferência de dados incorreto BufferCount pode levar à condição OOM](http://blogs.msdn.com/b/sqlserverfaq/archive/2010/05/06/incorrect-buffercount-data-transfer-option-can-lead-to-oom-condition.aspx) blog.  
  
 MAXTRANSFERSIZE  **=**  { *maxtransfersize* | **@***maxtransfersize_variable* }  
 Especifica a maior unidade de transferência em bytes a ser usada entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e a mídia de backup. Os valores possíveis são múltiplos de 65536 bytes (64 KB), estendendo-se até 4194304 bytes (4 MB).  
> [!NOTE]  
>  Quando o banco de dados tiver configurado o FILESTREAM, ou inclui ou grupos de arquivos OLTP em memória, `MAXTRANSFERSIZE` no momento da restauração deve ser maior ou igual ao que foi usado quando o backup foi criado.  
  
 **Opções de gerenciamento de erro**  
  
 Essas opções permitem determinar se somas de verificação de backup estão habilitadas para a operação de backup e se a operação para encontrar um erro.  
  
 { **NO_CHECKSUM** | SOMA DE VERIFICAÇÃO}  
 Controla se somas de verificação de backup estão habilitadas.  
  
 NO_CHECKSUM  
 Desabilita explicitamente a geração de somas de verificação de backup (e a validação de somas de verificação de página). Esse é o comportamento padrão.  
  
 CHECKSUM  
 Especifica que a operação de backup verifica cada página para soma de verificação e página interrompida, se estiver habilitado e disponível e gera uma soma de verificação para o backup inteiro.  
  
 O uso de somas de verificação de backup pode afetar uma carga de trabalho e a taxa de transferência do backup.  
  
 Para obter mais informações, consulte [erros de mídia possíveis durante Backup e restauração &#40; SQL Server &#41; ](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md).  
  
 { **STOP_ON_ERROR** | CONTINUE_AFTER_ERROR}  
 Controla se uma operação de backup para ou continua depois de encontrar um erro de soma de verificação de página.  
  
 STOP_ON_ERROR  
 Instrui BACKUP a falhar se uma soma de verificação de página não estiver correta. Esse é o comportamento padrão.  
  
 CONTINUE_AFTER_ERROR  
 Instrui BACKUP a continuar apesar de encontrar erros como somas de verificação inválidas ou páginas interrompidas.  
  
 Se não for possível fazer backup da parte final do log usando o NO_TRUNCATE opção quando o banco de dados está danificado, você pode tentar uma [backup do final do log](../../relational-databases/backup-restore/tail-log-backups-sql-server.md) especificando CONTINUE_AFTER_ERROR em vez de NO_TRUNCATE.  
  
 Para obter mais informações, consulte [erros de mídia possíveis durante Backup e restauração &#40; SQL Server &#41; ](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md).  
  
 **Opções de compatibilidade**  
  
 RESTART  
 A partir do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], não tem nenhum efeito. Esta opção é aceita pela versão para compatibilidade com versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Opções de monitoramento**  
  
 ESTATÍSTICAS [  **=**  *porcentagem* ]  
 Exibe uma mensagem sempre que outra *porcentagem* for concluída e é usado para medir o progresso. Se *porcentagem* for omitido, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exibe uma mensagem após a cada 10 por cento.  
  
 A opção STATS informa a porcentagem concluída de acordo com o limite de relatório do próximo intervalo. Esse limite é aproximadamente a porcentagem especificada. Por exemplo, com STATS=10, se a quantidade concluída for 40%, a opção poderá exibir 43%. Para conjuntos de backup grandes, isso não é um problema, porque a porcentagem concluída muda muito lentamente entre chamadas de E/S concluídas.  
  
 **Opções de fita**  
  
 Essas opções são usadas apenas para dispositivos TAPE. Se um dispositivo que não seja de fita estiver sendo usado, essas opções serão ignoradas.  
  
 { **REWIND** | NOREWIND }  
 REWIND  
 Especifica que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] libera e Rebobina a fita. REWIND é o padrão.  
  
 NOREWIND  
 Especifica que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mantém a fita aberta após a operação de backup. É possível usar essa opção para ajudar a melhorar o desempenho ao executar várias operações de backup em uma fita.  
  
 NOREWIND implica NOUNLOAD e essas opções são incompatíveis dentro de uma única instrução BACKUP.  
  
> [!NOTE]  
>  Se NOREWIND for usado, a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reterá a propriedade da unidade de fita até que uma instrução BACKUP ou RESTORE em execução no mesmo processo use a opção REWIND ou UNLOAD, ou que a instância do servidor seja encerrada. Manter a fita aberta evita que outros processos a acessem. Para obter informações sobre como exibir uma lista de fitas abertas e fechar uma fita aberta, consulte [dispositivos de Backup &#40; SQL Server &#41; ](../../relational-databases/backup-restore/backup-devices-sql-server.md).  
  
 { **UNLOAD** | NOUNLOAD}  
 > [!NOTE]  
>  UNLOAD/NOUNLOAD é uma configuração de sessão que persiste durante a vida útil da sessão ou até que ela seja redefinida especificando a alternativa.  
  
 UNLOAD  
 Especifica que a fita é rebobinada e descarregada automaticamente quando o backup for concluído. UNLOAD é o padrão quando uma sessão começa. 
  
 NOUNLOAD  
 Especifica que depois da operação de BACKUP a fita permanecerá carregada na unidade de fita.  
  
> [!NOTE]  
>  Para um backup em um dispositivo de backup de fita, a opção BLOCKSIZE afeta o desempenho da operação de backup. Normalmente, essa opção afeta o desempenho apenas durante a gravação em dispositivos de fita.  
  
 **Opções específicas de log**  
  
 Estas opções são usadas apenas com BACKUP LOG.  
  
> [!NOTE]  
>  Se você não quiser fazer backups de log, use o modelo de recuperação simples. Para obter mais informações, veja [Modelos de recuperação &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md).  
  
 {NORECOVERY | Modo de espera  **=**  *undo_file_name* }  
 NORECOVERY  
 Faz backup do final do log e deixa o banco de dados no estado de RESTORING. NORECOVERY é útil ao executar failover em um banco de dados secundário ou ao salvar o final do log antes de uma operação RESTORE.  
  
 Para executar um backup de log de melhor esforço que ignora o truncamento do log e coloca o banco de dados no estado RESTORING atomicamente, use as opções NO_TRUNCATE e NORECOVERY em conjunto.  
  
 Modo de espera  **=**  *standby_file_name*  
 Faz BACKUP do final do log e deixa o banco de dados em um estado STANDBY e somente leitura. A cláusula STANDBY grava dados em espera (executando reversão, mas com a opção de restaurações adicionais). O uso da opção STANDBY é equivalente a BACKUP LOG WITH NORECOVERY seguido por um RESTORE WITH STANDBY.  
  
 Usar o modo de espera requer um arquivo em espera, especificado por *standby_file_name*, cujo local é armazenado no log do banco de dados. Se o arquivo especificado já existir, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] o substituirá. Se o arquivo não existir, ele será criado pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)]. O arquivo em espera se torna parte do banco de dados.  
  
 Esse arquivo contém as alterações revertidas que deverão ser revertidas se operações RESTORE LOG forem aplicadas subseqüentemente. Deve haver espaço em disco suficiente para que o arquivo em espera cresça para que possa conter todas as páginas distintas do banco de dados que foi modificado pela reversão de transações não confirmadas.  
  
 NO_TRUNCATE  
 Especifica que o não log truncado e faz com que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] ao tentar fazer backup, independentemente do estado do banco de dados. Conseqüentemente, um backup feito com NO_TRUNCATE pode conter metadados incompletos. Essa opção permite fazer backup do log em situações em que o banco de dados está danificado.  
  
 A opção NO_TRUNCATE de BACKUP LOG é equivalente a especificar COPY_ONLY e CONTINUE_AFTER_ERROR.  
  
 Sem a opção NO_TRUNCATE, o banco de dados deve estar no estado ONLINE. Se o banco de dados estiver no estado SUSPENDED, talvez você possa criar um criar um backup especificando NO_TRUNCATE. Mas se o banco de dados estiver no estado OFFLINE ou EMERGENCY, BACKUP não será permitido mesmo com NO_TRUNCATE. Para obter informações sobre os estados de banco de dados, consulte [estados de banco de dados](../../relational-databases/databases/database-states.md).  
  
## <a name="about-working-with-sql-server-backups"></a>Sobre Trabalhando com backups do SQL Server  
 Esta seção introduz os seguintes conceitos de backup essenciais:  
  
 [Tipos de backup](#Backup_Types)  
  
 [Truncamento do Log de transações](#Tlog_Truncation)  
  
 [Formatação de mídia de Backup](#Formatting_Media)  
  
 [Trabalhando com dispositivos de Backup e conjuntos de mídias](#Backup_Devices_and_Media_Sets)  
  
 [Restauração de Backups do SQL Server](#Restoring_Backups)  
  
> [!NOTE]  
>  Para obter uma introdução ao backup no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [visão geral de Backup &#40; SQL Server &#41; ](../../relational-databases/backup-restore/backup-overview-sql-server.md).  
  
###  <a name="Backup_Types"></a>Tipos de backup  
 Os tipos de backup com suporte dependem do modelo de recuperação do banco de dados, da seguinte maneira:  
  
-   Todos os modelos de recuperação oferecem suporte a backups completos e diferenciais de dados.  
  
    |Escopo do backup|Tipos de backup|  
    |---------------------|------------------|  
    |Banco de dados inteiro|[Backups de banco de dados](../../relational-databases/backup-restore/full-database-backups-sql-server.md) abrangem todo o banco de dados.<br /><br /> Opcionalmente, cada backup de banco de dados pode servir como a base de uma série de um ou mais [backups de banco de dados diferencial](../../relational-databases/backup-restore/differential-backups-sql-server.md).|  
    |Banco de dados parcial|[Backups parciais](../../relational-databases/backup-restore/partial-backups-sql-server.md) cobertura de leitura/gravação de grupos de arquivos e, possivelmente, um ou mais arquivos somente leitura ou grupos de arquivos.<br /><br /> Opcionalmente, cada backup parcial pode servir como a base de uma série de um ou mais [backups diferenciais parciais](../../relational-databases/backup-restore/differential-backups-sql-server.md).|  
    |Arquivo ou grupo de arquivos|[Backups de arquivo](../../relational-databases/backup-restore/full-file-backups-sql-server.md) abrangem um ou mais arquivos ou grupos de arquivos e são relevantes apenas para bancos de dados que contêm vários grupos de arquivos. No modelo de recuperação simples, os backups de arquivos são essencialmente restritos a grupos de arquivos secundários somente leitura.<br /><br /> Opcionalmente, cada backup de arquivo pode servir como a base de uma série de um ou mais [backups de arquivos diferenciais](../../relational-databases/backup-restore/differential-backups-sql-server.md).|  
  
-   No modelo de recuperação completa ou modelo de recuperação bulk-logged, backups convencionais também incluem sequencial *backups de log de transação* (ou *backups de log*), que são necessário. Cada backup de log cobre a parte do log de transações que estava ativa quando o backup foi criado e inclui todos os registros de log sem backup em um backup de log anterior.  
  
     Para minimizar a exposição de perda de trabalho, à custa de sobrecarga administrativa, você deve agendar backups de log freqüentes. O agendamento de backups diferenciais entre backups completos pode reduzir o tempo de restauração reduzindo o número de backups de log a serem restaurados após a restauração dos dados.  
  
     Recomendamos que você coloque backups de log em um volume separado dos backups de banco de dados.  
  
    > [!NOTE]  
    >  Para poder criar o primeiro backup de log, você deve criar um backup completo.  
  
-   Um *backup somente cópia* é um backup completo de finalidade especial ou backup de log que é independente da sequência de backups convencionais. Para criar um backup somente cópia, especifique a opção COPY_ONLY na instrução BACKUP. Para obter mais informações, veja [Backups somente cópia &#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md).  
  
###  <a name="Tlog_Truncation"></a>Truncamento do Log de transações  
 Para evitar o preenchimento do log de transações de um banco de dados, os backups rotineiros são essenciais. No modelo de recuperação simples, o truncamento do log ocorre automaticamente depois que o backup do banco de dados é feito, e no modelo de recuperação completa, depois que o backup do log de transações é feito. No entanto, às vezes o processo de truncamento pode ser demorado. Para ver informações sobre os fatores que podem adiar o truncamento de log, consulte [O log de transações &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md).  
  
> [!NOTE]  
>  As opções BACKUP LOG WITH NO_LOG e WITH TRUNCATE_ONLY foram descontinuadas. Se você estiver usando o modelo de recuperação completa ou bulk-logged e dever remover a cadeia de backup de log de um banco de dados, alterne para o modelo de recuperação simples. Para obter mais informações, veja [Exibir ou alterar o modelo de recuperação de um banco de dados &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md).  
  
###  <a name="Formatting_Media"></a>Formatação de mídia de Backup  
 A mídia de backup será formatada por uma instrução BACKUP se, e apenas se, qualquer uma das seguintes situações for verdadeira:  
  
-   A opção FORMAT estiver especificada.  
  
-   A mídia estiver vazia.  
  
-   A operação estiver gravando uma fita de continuação.  
  
###  <a name="Backup_Devices_and_Media_Sets"></a>Trabalhando com dispositivos de Backup e conjuntos de mídias  
  
#### <a name="backup-devices-in-a-striped-media-set-a-stripe-set"></a>Dispositivos de backup em um conjunto de mídias distribuído (um conjunto de distribuição)  
 Um *distribuição* é um conjunto de arquivos do disco no qual os dados são divididos em blocos e distribuídos em uma ordem fixa. O número de dispositivos de backup usados em um conjunto de distribuição deve permanecer o mesmo (a não ser que a mídia seja reiniciada com FORMAT).  
  
 O exemplo a seguir grava um backup do banco de dados [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] em um novo conjunto de mídias distribuído que usa três arquivos de disco.  
  
```tsql  
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
  
 Se nem MEDIANAME nem MEDIADESCRIPTION for especificado quando um cabeçalho de mídia é gravado, o campo de cabeçalho de mídia correspondente ao item em branco está vazio.  
  
#### <a name="working-with-a-mirrored-media-set"></a>Trabalhando com um conjunto de mídias espelhado  
 Normalmente, backups não são espelhados e instruções BACKUP simplesmente incluem uma cláusula TO. No entanto, um total de quatro espelhos é possível por conjunto de mídias. Em um conjunto de mídias espelhado, a operação de backup grava em vários grupos de dispositivos de backup. Cada grupo de dispositivos de backup compõe um único espelho dentro do conjunto de mídias espelhado. Todos os espelhos devem usar a mesma quantidade e tipo de dispositivos físicos de backup que devem ter as mesmas propriedades.  
  
 Para fazer backup em um conjunto de mídias espelhado, todos os espelhos devem estar presentes. Para fazer backup em um conjunto de mídias espelhado, especifique a cláusula TO para especificar o primeiro espelho e especifique uma cláusula MIRROR TO para cada espelho adicional.  
  
 Para um conjunto de mídias espelhado, cada cláusula MIRROR TO deve listar o mesmo número e tipo de dispositivos que a cláusula TO. O exemplo a seguir grava em um conjunto de mídias espelhado que contém dois espelhos e usa três dispositivos por espelho:  
  
```tsql  
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
>  Este exemplo foi criado para permitir teste em seu sistema local. Na prática, fazer backup em vários dispositivos na mesma unidade deve afetar o desempenho e eliminar a redundância para a qual conjuntos de mídias espelhados foram projetados.  
  
##### <a name="media-families-in-mirrored-media-sets"></a>Famílias de mídia em conjuntos de mídia espelhados  
 Cada dispositivo de backup especificado na cláusula TO de uma instrução BACKUP corresponde a uma família de mídia. Por exemplo, se as cláusulas TO listarem três dispositivos, a instrução BACKUP gravará dados nas três famílias de mídia. Em um conjunto de mídias espelhado, cada espelho deve conter uma cópia de cada família de mídia. É por isso que o número de dispositivos deve ser idêntico em cada espelho.  
  
 Quando vários dispositivos são listados para cada espelho, a ordem dos dispositivos determina qual família de mídia é gravada em um determinado dispositivo. Por exemplo, em cada uma das listas de dispositivos, o segundo dispositivo corresponde à segunda família de mídia. Para os dispositivos do exemplo acima, a correspondência entre dispositivos e famílias de mídia é mostrada na tabela a seguir.  
  
|Espelho|Família de mídia 1|Família de mídia 2|Família de mídia 3|  
|------------|--------------------|--------------------|--------------------|  
|0|`Z:\AdventureWorks1a.bak`|`Z:\AdventureWorks2a.bak`|`Z:\AdventureWorks3a.bak`|  
|1|`Z:\AdventureWorks1b.bak`|`Z:\AdventureWorks2b.bak`|`Z:\AdventureWorks3b.bak`|  
  
 O backup de uma família de mídia sempre deve ser feito no mesmo dispositivo dentro de um espelho específico. Portanto, a cada vez que você usar um conjunto de mídias existente, liste os dispositivos de cada espelho na mesma ordem em que foram especificados quando o conjunto de mídias foi criado.  
  
 Para obter mais informações sobre conjuntos de mídia espelhadas, consulte [Conjuntos de mídias de backup espelhadas &#40;SQL Server&#41;](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md). Para obter mais informações sobre conjuntos de mídias e famílias de mídia em geral, consulte [conjuntos de mídias, famílias de mídia e conjuntos de Backup &#40; SQL Server &#41; ](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md).  
  
###  <a name="Restoring_Backups"></a>Restauração de Backups do SQL Server  
 Para restaurar um banco de dados e, opcionalmente, recuperá-lo para colocá-lo online, ou para restaurar um arquivo ou grupo de arquivos, use o [!INCLUDE[tsql](../../includes/tsql-md.md)] [RESTAURAR](../../t-sql/statements/restore-statements-transact-sql.md) instrução ou o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **restaurar** tarefas. Para obter mais informações, consulte [visão geral de recuperação e restauração &#40; SQL Server &#41; ](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md).  
  
##  <a name="Additional_Considerations"></a>Considerações adicionais sobre opções de BACKUP  
  
###  <a name="Interactions_SKIP_etc"></a>Interação de SKIP, NOSKIP, INIT e NOINIT  
 Esta tabela descreve as interações entre o { **NOINIT** | INIT} e { **NOSKIP** | Opções de ignorar}.  
  
> [!NOTE]  
>  Se a mídia de fita estiver vazia ou se o arquivo de backup em disco não existir, todas essas interações gravarão um cabeçalho de mídia e continuarão. Se a mídia não estiver vazia e não tiver um cabeçalho de mídia válido, essas operações fornecerão comentários informando que essa não é uma mídia MTF válida e terminarão a operação de backup.  
  
||NOINIT|INIT|  
|------|------------|----------|  
|NOSKIP|Se o volume contiver um cabeçalho de mídia válido, verificará o nome da mídia corresponde ao MEDIANAME fornecido, se houver. Se houver correspondência, anexará o conjunto de backup preservando todos os conjuntos de backup existentes.<br /><br /> Se o volume não contiver um cabeçalho de mídia válido, ocorrerá um erro.|Se o volume contiver um cabeçalho de mídia válido, executará as seguintes verificações:<br /><br /> -Se MEDIANAME estiver especificado, verifica se o nome da mídia fornecido corresponde mídia name.* * o cabeçalho de mídia<br /><br /> -Verifica se não há nenhum conjunto de backup vigente na mídia. Se houver, terminará o backup.<br /><br /> Se essas verificações passarem, substituirá qualquer conjunto de backup na mídia preservando apenas o cabeçalho da mídia.<br /><br /> Se o volume não contiver um cabeçalho de mídia válido, gerará um cabeçalho como uso do MEDIANAME e MEDIADESCRIPTION especificados, se houver.|  
|SKIP|Se o volume contiver um cabeçalho de mídia válido, acrescentará o conjunto de backup, preservando todos os conjuntos de backup existentes.|Se o volume contiver um válido * cabeçalho da mídia, substitui todos os conjuntos de backup na mídia, preservando apenas o cabeçalho de mídia.<br /><br /> Se a mídia estiver vazia, gerará um cabeçalho de mídia como uso de MEDIANAME e MEDIADESCRIPTION fornecidos, se houver.|  
  
 * Validade inclui o número de versão MTF e outras informações de cabeçalho. Se a versão especificada não tiver suporte ou for um valor inesperado, ocorrerá um erro.  
  
 * * O usuário deve pertencer às apropriadas funções fixas de banco de dados ou servidor para executar uma operação de backup.  
  
## <a name="compatibility"></a>Compatibilidade  
  
> [!CAUTION]  
>  Os backups criados por uma versão mais recente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não podem ser restaurados em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 BACKUP oferece suporte à opção RESTART para fornecer compatibilidade com versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Mas RESTART não tem nenhum efeito.  
  
## <a name="general-remarks"></a>Comentários gerais  
 Backups de banco de dados ou de log podem ser anexados a qualquer dispositivo de disco ou de fita, permitindo que um banco de dados e seus logs de transações sejam mantidos em um local físico.  
  
 A instrução BACKUP não é permitida em uma transação explícita ou implícita.  
  
 Operações de backup entre plataformas, mesmo entre tipos diferentes de processadores, podem ser executadas desde que o agrupamento do banco de dados tenha suporte no sistema operacional.  
  
> [!NOTE]  
>  Por padrão, toda operação de backup bem-sucedida acrescenta uma entrada ao log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e ao log de eventos do sistema. Se você fizer backup do log com muita frequência, essas mensagens de êxito se acumularão muito rapidamente, resultando em logs de erros imensos que podem dificultar a localização de outras mensagens. Em tais situações, você pode suprimir essas entradas de log usando o sinalizador de rastreamento 3226, caso nenhum dos seus scripts dependa dessas entradas. Para obter mais informações, veja, [Sinalizadores de rastreamento &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).  
  
## <a name="interoperability"></a>Interoperabilidade  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa um processo de backup online para permitir que um backup de banco de dados seja feito enquanto o banco de dados ainda está uso. Durante um backup, a maior parte das operações é possível. Por exemplo, instruções INSERT, UPDATE ou DELETE são permitidas durante uma operação de backup  
  
 As operações que não podem ser executadas durante um banco de dados ou backup de log de transações incluem:  
  
-   Operações de gerenciamento de arquivos, como a instrução ALTER DATABASE com as opções ADD FILE ou REMOVE.  
  
-   Operações de redução do banco de dados ou de arquivos. Isso inclui operações de redução automática.  
  
 Se uma operação de backup for sobreposta por uma operação de gerenciamento ou de redução de arquivos, um conflito será gerado. Independentemente de qual operação em conflito começou primeiro, a segunda operação aguardará até que o tempo limite do bloqueio definido pela primeira operação seja esgotado (o período limite é controlado pela configuração de tempo limite de uma sessão). Se o bloqueio for liberado durante o período de tempo limite, a segunda operação continuará. Se o tempo limite do bloqueio for esgotado, a segunda operação falhará.  
  
## <a name="metadata"></a>Metadados  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inclui as seguintes tabelas de histórico de backup que controlam as atividades do banco de dados:  
  
-   [backupfile &#40; Transact-SQL &#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)  
  
-   [backupfilegroup &#40; Transact-SQL &#41;](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)  
  
-   [backupmediafamily &#40; Transact-SQL &#41;](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)  
  
-   [backupmediaset &#40; Transact-SQL &#41;](../../relational-databases/system-tables/backupmediaset-transact-sql.md)  
  
-   [conjunto de backup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)  
  
 Quando uma restauração é executada, se o conjunto de backup não tiver sido registrado no **msdb** banco de dados, o histórico de backup tabelas podem ser modificadas.  
  
## <a name="security"></a>Segurança  
 Começando com [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], o **senha** e **MEDIAPASSWORD** opções foram descontinuadas para a criação de backups. Ainda é possível restaurar backups criados com senhas.  
  
### <a name="permissions"></a>Permissões  
 As permissões BACKUP DATABASE e BACKUP LOG usam como padrão os membros da função de servidor fixa **sysadmin** e as funções de banco de dados fixas **db_owner** e **db_backupoperator** .  
  
 Os problemas de propriedade e permissão no arquivo físico do dispositivo de backup podem interferir em uma operação de backup. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser capaz de ler e gravar no dispositivo; a conta sob a qual o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executa deve ter permissões de gravação. No entanto, [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md), que adiciona uma entrada para um dispositivo de backup nas tabelas do sistema, não verifica permissões de acesso a arquivos. Esses problemas no arquivo físico do dispositivo de backup podem não aparecer até que o recurso físico seja acessado quando o backup ou restauração é tentado.  
  
##  <a name="examples"></a> Exemplos  
 Esta seção contém os seguintes exemplos:  
  
-   A. [Fazendo backup de um banco de dados completo](#backing_up_db)  
  
-   B. [Fazendo backup do banco de dados e log](#backing_up_db_and_log)  
  
-   C. [Criando um backup de arquivo completo de grupos de arquivos secundários](#full_file_backup)  
  
-   D. [Criando um backup de arquivo diferencial dos grupos de arquivos secundários](#differential_file_backup)  
  
-   E. [Criando e fazendo backup em um única família de mídias espelhado conjunto](#create_single_family_mirrored_media_set)  
  
-   F. [Criando e fazendo backup em um várias famílias de mídias espelhado conjunto](#create_multifamily_mirrored_media_set)  
  
-   G [conjunto de mídias espelhado de backup existente](#existing_mirrored_media_set)  
  
-   H. [Criando um backup compactado em um novo conjunto de mídia](#creating_compressed_backup_new_media_set)  

- I.  [Fazendo backup para o serviço de armazenamento de BLOBs do Microsoft Azure](#url)
  
> [!NOTE]  
>  Os tópicos de instruções de backup contêm exemplos adicionais. Para obter mais informações, veja [Visão geral do backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md).  
  
###  <a name="backing_up_db"></a> A. Fazendo backup de um banco de dados completo  
 O exemplo a seguir faz backup de [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] banco de dados para um arquivo de disco.  
  
```tsql  
BACKUP DATABASE AdventureWorks2012   
 TO DISK = 'Z:\SQLServerBackups\AdvWorksData.bak'  
   WITH FORMAT;  
GO  
```  
  
###  <a name="backing_up_db_and_log"></a> B. Fazendo backup do banco de dados e do log  
 O exemplo a seguir faz backup do banco de dados de exemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] que, por padrão, usa o modelo de recuperação simples. Para oferecer suporte a backups de log, o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] é modificado para usar o modelo de recuperação completa.  
  
 Em seguida, o exemplo usa [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md) para criar uma lógica [dispositivo de backup](../../relational-databases/backup-restore/backup-devices-sql-server.md) para fazer backup de dados, `AdvWorksData`e cria outro dispositivo de backup lógico para fazer backup do log, `AdvWorksLog`.  
  
 Em seguida, o exemplo cria um backup de dados completo em `AdvWorksData` e, após um período de atividades de atualização, faz o backup do log em `AdvWorksLog`.  
  
```tsql  
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
  
```tsql  
--Back up the files in SalesGroup1:  
BACKUP DATABASE Sales  
   FILEGROUP = 'SalesGroup1',  
   FILEGROUP = 'SalesGroup2'  
   TO DISK = 'Z:\SQLServerBackups\SalesFiles.bck';  
GO  
```  
  
###  <a name="differential_file_backup"></a> D. Criando um backup diferencial de arquivos dos grupos de arquivos secundários  
 O exemplo a seguir cria um backup diferencial de cada arquivo nos dois grupos de arquivos secundários.  
  
```tsql  
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
  
```tsql  
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
  
```tsql  
BACKUP DATABASE AdventureWorks2012  
TO TAPE = '\\.\tape0', TAPE = '\\.\tape1'  
MIRROR TO TAPE = '\\.\tape2', TAPE = '\\.\tape3'  
WITH  
   FORMAT,  
   MEDIANAME = 'AdventureWorksSet1';  
```  
  
###  <a name="existing_mirrored_media_set"></a>G. Fazendo backup em um conjunto de mídias espelhado existente  
 O exemplo a seguir anexa um conjunto de backup ao conjunto de mídias criado no exemplo anterior.  
  
```tsql  
BACKUP LOG AdventureWorks2012  
TO TAPE = '\\.\tape0', TAPE = '\\.\tape1'  
MIRROR TO TAPE = '\\.\tape2', TAPE = '\\.\tape3'  
WITH   
   NOINIT,  
   MEDIANAME = 'AdventureWorksSet1';  
```  
  
> [!NOTE]  
>  NOINIT, que é o padrão, é mostrado aqui para maior clareza.  
  
###  <a name="creating_compressed_backup_new_media_set"></a>H. Criando um backup compactado em um novo conjunto de mídias  
 O exemplo a seguir formata a mídia, criando um novo conjunto de mídias e executa um backup completo compactado do banco de dados [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)].  
  
```tsql  
BACKUP DATABASE AdventureWorks2012 TO DISK='Z:\SQLServerBackups\AdvWorksData.bak'   
WITH   
   FORMAT,   
   COMPRESSION;  
```  

###  <a name="url"></a>I. Fazer backup do serviço de Armazenamento de Blobs do Microsoft Azure 
O exemplo executa um backup de banco de dados completo do `Sales` para o serviço de armazenamento de BLOBs do Microsoft Azure.  O nome da Conta de armazenamento é `mystorageaccount`.  O contêiner é chamado `myfirstcontainer`.  Uma política de acesso armazenado foi criada com direitos de leitura, gravação, exclusão e lista.  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] credencial, `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`, foi criado usando uma assinatura de acesso compartilhado que está associado com a política de acesso armazenada.  Para obter informações sobre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de backup para o serviço de armazenamento de Blob do Windows Azure, consulte [SQL Server Backup e restauração com o serviço de armazenamento de BLOBs do Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md) e [Backup do SQL Server para URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md).

```tsql  
BACKUP DATABASE Sales
TO URL = 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer/Sales_20160726.bak'
WITH STATS = 5;
```

  
## <a name="see-also"></a>Consulte também  
 [Dispositivos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [Conjuntos de mídias, famílias de mídia e conjuntos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [Backups da parte final do log &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [DBCC SQLPERF &#40; Transact-SQL &#41;](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)   
 [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)   
 [RESTORE LABELONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)   
 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)   
 [sp_addumpdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [sp_helpfile &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpfile-transact-sql.md)   
 [sp_helpfilegroup &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpfilegroup-transact-sql.md)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [Restauração por etapas de bancos de dados com tabelas com otimização de memória](../../relational-databases/in-memory-oltp/piecemeal-restore-of-databases-with-memory-optimized-tables.md)  
  
  

