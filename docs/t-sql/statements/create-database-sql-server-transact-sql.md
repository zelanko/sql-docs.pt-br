---
title: Criar banco de dados (SQL Server Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DATABASE_TSQL
- DATABASE
- CONTAINMENT_TSQL
- CREATE DATABASE
- CREATE_DATABASE_TSQL
- CONTAINS_FILESTREAM_TSQL
- CONTAINS FILESTREAM
- CONTAINMENT
dev_langs:
- TSQL
helpviewer_keywords:
- snapshots [SQL Server database snapshots], creating
- databases [SQL Server], creating
- model database [SQL Server], database creation
- mounted drives [SQL Server]
- CREATE DATABASE
- CREATE DATABASE statement
- file creation [SQL Server]
- creating databases
- containment
- filegroups [SQL Server], database creation
- database creation [SQL Server], CREATE DATABASE statement
- moving databases
- attaching databases [SQL Server], CREATE DATABASE...FOR ATTACH
ms.assetid: 29ddac46-7a0f-4151-bd94-75c1908c89f8
caps.latest.revision: 212
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: de8574d6d4f2322c63743828b7b8a03d4e6fa576
ms.contentlocale: pt-br
ms.lasthandoff: 10/24/2017

---
# <a name="create-database-sql-server-transact-sql"></a>CREATE DATABASE (SQL Server Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria um novo banco de dados e os arquivos usados para armazená-lo, um instantâneo de banco de dados ou anexa um banco de dados dos arquivos desanexados de um banco de dados criado anteriormente.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
      Create a database  
CREATE DATABASE database_name   
[ CONTAINMENT = { NONE | PARTIAL } ]  
[ ON   
      [ PRIMARY ] <filespec> [ ,...n ]   
      [ , <filegroup> [ ,...n ] ]   
      [ LOG ON <filespec> [ ,...n ] ]   
]   
[ COLLATE collation_name ]  
[ WITH  <option> [,...n ] ]  
[;]  
  
<option> ::=  
{  
      FILESTREAM ( <filestream_option> [,...n ] )  
    | DEFAULT_FULLTEXT_LANGUAGE = { lcid | language_name | language_alias }  
    | DEFAULT_LANGUAGE = { lcid | language_name | language_alias }  
    | NESTED_TRIGGERS = { OFF | ON }  
    | TRANSFORM_NOISE_WORDS = { OFF | ON}  
    | TWO_DIGIT_YEAR_CUTOFF = <two_digit_year_cutoff>   
    | DB_CHAINING { OFF | ON }  
    | TRUSTWORTHY { OFF | ON }  
}  
  
<filestream_option> ::=  
{  
      NON_TRANSACTED_ACCESS = { OFF | READ_ONLY | FULL }  
    | DIRECTORY_NAME = 'directory_name'   
}  
  
<filespec> ::=   
{  
(  
    NAME = logical_file_name ,  
    FILENAME = { 'os_file_name' | 'filestream_path' }   
    [ , SIZE = size [ KB | MB | GB | TB ] ]   
    [ , MAXSIZE = { max_size [ KB | MB | GB | TB ] | UNLIMITED } ]   
    [ , FILEGROWTH = growth_increment [ KB | MB | GB | TB | % ] ]  
)  
}  
  
<filegroup> ::=   
{  
FILEGROUP filegroup name [ [ CONTAINS FILESTREAM ] [ DEFAULT ] | CONTAINS MEMORY_OPTIMIZED_DATA ]  
    <filespec> [ ,...n ]  
}  
  
<service_broker_option> ::=  
{  
    ENABLE_BROKER  
  | NEW_BROKER  
  | ERROR_BROKER_CONVERSATIONS  
}  
  
```  
  
```  
  
      Attach a database  
CREATE DATABASE database_name   
    ON <filespec> [ ,...n ]   
    FOR { { ATTACH [ WITH <attach_database_option> [ , ...n ] ] }  
        | ATTACH_REBUILD_LOG }  
[;]  
  
<attach_database_option> ::=  
{  
      <service_broker_option>  
    | RESTRICTED_USER  
    | FILESTREAM ( DIRECTORY_NAME = { 'directory_name' | NULL } )  
}  
  
```  
  
```  
  
      Create a database snapshot  
CREATE DATABASE database_snapshot_name   
    ON   
    (  
        NAME = logical_file_name,  
        FILENAME = 'os_file_name'   
    ) [ ,...n ]   
    AS SNAPSHOT OF source_database_name  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 É o nome do novo banco de dados. Nomes de banco de dados devem ser exclusivos dentro de uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e estar de acordo com as regras de [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
 *Database_Name* pode ter no máximo 128 caracteres, a menos que um nome lógico não é especificado para o arquivo de log. Se não for especificado um nome de arquivo de log lógico, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gera o *logical_file_name* e *os_file_name* para o log acrescentando um sufixo para *database_name*. Isso limita *database_name* para 123 caracteres para o nome de arquivo lógico gerado é não mais de 128 caracteres.  
  
 Se o nome do arquivo de dados não for especificado, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa *database_name* como o *logical_file_name* e como o *os_file_name*. O caminho padrão é obtido do Registro. O caminho padrão pode ser alterado usando o **propriedades do servidor (página de configurações do banco de dados)** em [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. A alteração do caminho padrão exige o reinício do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 CONTAINMENT = { NONE | PARTIAL }  

**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] por meio de[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Especifica o status de contenção do banco de dados. NONE = banco de dados dependente. PARTIAL = banco de dados parcialmente independente.  
  
 ON  
 Especifica que os arquivos em disco usados para armazenar as seções de dados do banco de dados, arquivos de dados, são definidos explicitamente. ON é necessário quando seguido por uma lista separada por vírgulas de \<filespec > itens que definem os arquivos de dados para o grupo de arquivos primário. A lista de arquivos no grupo de arquivos primário pode ser seguida por uma lista opcional separada por vírgulas de \<arquivos > itens que definem os grupos de arquivos e seus arquivos.  
  
 PRIMARY  
 Especifica que o associado \<filespec > lista define o arquivo primário. O primeiro arquivo especificado no \<filespec > entrada no grupo de arquivos primário se torna o arquivo primário. Um banco de dados pode ter apenas um arquivo primário. Para obter mais informações, consulte [Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md).  
  
 Se PRIMARY não estiver especificado, o primeiro arquivo listado na instrução CREATE DATABASE se tornará o arquivo primário.  
  
 LOG ON  
 Especifica que os arquivos em disco usados para armazenar o log do banco de dados, os arquivos de log, são definidos explicitamente. LOG ON é seguido por uma lista separada por vírgulas de \<filespec > itens que definem os arquivos de log. Se LOG ON não estiver especificado, um arquivo de log será criado automaticamente com um tamanho de 25 por cento da soma dos tamanhos de todos os arquivos de dados do banco de dados ou 512 KB, o que for maior. Esse arquivo é colocado no local padrão de arquivo de log. Para obter informações sobre esse local, consulte [exibir ou alterar os locais padrão de dados e arquivos de Log &#40; SQL Server Management Studio &#41; ](../../database-engine/configure-windows/view-or-change-the-default-locations-for-data-and-log-files.md).  
  
 LOG ON não pode ser especificado em um instantâneo do banco de dados.  
  
 COLLATE *collation_name*  
 Especifica o agrupamento padrão do banco de dados. O nome do agrupamento pode ser um nome de agrupamento do Windows ou um nome de agrupamento SQL. Se não estiver especificado, o agrupamento padrão da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será atribuído ao banco de dados. Um nome de agrupamento não pode ser especificado em um instantâneo do banco de dados.  
  
 Um nome de agrupamento não pode ser especificado com as cláusulas FOR ATTACH ou FOR ATTACH_REBUILD_LOG. Para obter informações sobre como alterar o agrupamento de um banco de dados anexado, visite [site da Microsoft](http://go.microsoft.com/fwlink/?linkid=16419&kbid=325335).  
  
 Para obter mais informações sobre os nomes de agrupamento do Windows e do SQL, consulte [COLLATE &#40; Transact-SQL &#41; ](~/t-sql/statements/collations.md).  
  
> [!NOTE]  
>  Os bancos de dados independentes são agrupados de maneira diferente dos bancos de dados dependente. Consulte [agrupamentos de banco de dados independentes](../../relational-databases/databases/contained-database-collations.md) para obter mais informações.  
  
 COM \<opção >  
 -   **\<filestream_options >** 
  
     NON_TRANSACTED_ACCESS = { **OFF** | READ_ONLY | COMPLETO}  
**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].
  
     Especifica o nível de acesso não transacional de FILESTREAM ao banco de dados.  
  
    |Valor|Descrição|  
    |-----------|-----------------|  
    |OFF|O acesso não transacional está desabilitado.|  
    |READONLY|Os dados FILESTREAM deste banco de dados podem ser lidos por processos não transacionais.|  
    |FULL|O acesso não transacional completo a FileTables FILESTREAM está habilitado.|  
  
     DIRECTORY_NAME = \<directory_name > **aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] por meio de[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
     Um nome de diretório compatível com o Windows. Esse nome deve ser exclusivo entre todos os nomes de Database_Directory na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A comparação de exclusividade não diferencia maiúsculas de minúsculas, independentemente das configurações de agrupamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa opção deve ser definida antes da criação de um FileTable neste banco de dados.  
  
 As opções a seguir são permitidas apenas quando CONTAINMENT estiver definido como PARTIAL. Se CONTAINMENT não for definida como NOME, ocorrerão erros.  
  
-   **DEFAULT_FULLTEXT_LANGUAGE = \<lcid > | \<nome de idioma > | \<alias de idioma >**  
  
**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] por meio de[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
     See [Configure the default full-text language Server Configuration Option](../../database-engine/configure-windows/configure-the-default-full-text-language-server-configuration-option.md) for a full description of this option.  
  
-   **DEFAULT_LANGUAGE = \<lcid > | \<nome de idioma > | \<alias de idioma >**  
  
**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] por meio de[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
     See [Configure the default language Server Configuration Option](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md) for a full description of this option.  
  
-   **NESTED_TRIGGERS = {OFF | ON}**  
  
**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] por meio de[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
     See [Configure the nested triggers Server Configuration Option](../../database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option.md) for a full description of this option.  
  
-   **TRANSFORM_NOISE_WORDS = {OFF | ON}**  
  
**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] por meio de[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
     See [transform noise words Server Configuration Option](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md)for a full description of this option.  
  
-   **TWO_DIGIT_YEAR_CUTOFF = {2049 | \<qualquer ano entre 1753 e 9999 >}**  
  
     Quatro dígitos que representam um ano. 2049 é o valor padrão. Consulte [configurar o ano de dois dígitos cutoff Server Configuration Option](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md) para obter uma descrição completa dessa opção.  
  
-   **DB_CHAINING {OFF | ON}**  
  
     Quando ON estiver especificado, o banco de dados poderá ser a origem ou o destino de um encadeamento de propriedades de bancos de dados.  
  
     Quando OFF, o banco de dados não poderá participar do encadeamento de propriedades de bancos de dados. O padrão é OFF.  
  
    > [!IMPORTANT]  
    >  A instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reconhecerá essa configuração quando a opção do servidor Encadeamento de Propriedades de Bancos de Dados for 0 (OFF). Quando Encadeamento de Propriedades de BD for 1 (ON), todos os bancos de dados de usuário poderão participar de cadeias de propriedades de bancos de dados, independentemente do valor dessa opção. Essa opção é definida usando [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
     A definição dessa opção requer associação à função de servidor fixa sysadmin. A opção DB_CHAINING não pode ser definida nesses bancos de dados do sistema: mestre, modelo, tempdb.  
  
-   **TRUSTWORTHY {OFF | ON}**  
  
     Quando ON estiver especificado, os módulos de banco de dados (por exemplo, exibições, funções definidas pelo usuário ou procedimentos armazenados) que usam um contexto de representação poderão acessar recursos fora do banco de dados.  
  
     Quando OFF, os módulos do banco de dados em um contexto de representação não poderão acessar recursos fora do banco de dados. O padrão é OFF.  
  
     TRUSTWORTHY será definido como OFF sempre que o banco de dados for anexado.  
  
     Por padrão, todos os bancos de dados do sistema, exceto o banco de dados msdb, têm TRUSTWORTHY definido como OFF. O valor não pode ser alterado para os bancos de dados modelo e tempdb. É recomendável nunca definir a opção TRUSTWORTHY como ON para o banco de dados mestre.  
  
     A definição dessa opção requer associação à função de servidor fixa sysadmin.  
  
 FOR ATTACH [WITH \< attach_database_option >] Especifica o banco de dados criado por [anexando](../../relational-databases/databases/database-detach-and-attach-sql-server.md) um conjunto existente de arquivos do sistema operacional. Deve haver um \<filespec > entrada que especifica o arquivo primário. A única outra \<filespec > entradas necessárias são aquelas para todos os arquivos que tenham um caminho diferente de quando o banco de dados foi inicialmente criado ou anexado pela última vez. Um \<filespec > entrada deve ser especificada para esses arquivos.  
  
 FOR ATTACH exige o seguinte:  
  
-   Todos os arquivos de dados (MDF e NDF) devem estar disponíveis.  
  
-   Se existirem vários arquivos de log, todos eles deverão estar disponíveis.  
  
 Se um banco de dados de leitura/gravação tiver um único arquivo de log que não esteja disponível no momento e se o banco de dados foi encerrado sem usuários ou transações abertas antes da operação de anexação, FOR ATTACH reconstruirá automaticamente o arquivo de log e atualizará o arquivo primário. Por outro lado, para um banco de dados somente leitura, o log não pode ser reconstruído porque o arquivo primário não pode ser atualizado. Portanto, ao anexar um banco de dados somente leitura com um log que não está disponível, você deve fornecer os arquivos de log ou os arquivos na cláusula FOR ATTACH.  
  
> [!NOTE]  
>  Um banco de dados criado por uma versão mais recente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode ser anexado em versões anteriores.  
  
 No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], todos os arquivos de texto completo que fazem parte do banco de dados que está sendo anexado serão anexados com o banco de dados. Para especificar um novo caminho do catálogo de texto completo, especifique o novo local sem o nome do arquivo do sistema operacional de texto completo. Para obter mais informações, consulte a seção Exemplos.  
  
 Anexando um banco de dados que contém uma opção de FILESTREAM de "Nome do diretório", em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância solicitará [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para verificar se o nome do Database_Directory é exclusivo. Se não for, a operação de anexação falha com o erro "nome do Database_Directory do FILESTREAM \<nome > não é exclusivo nesta instância do SQL Server". Para evitar esse erro, o parâmetro opcional, *directory_name*, deve ser passado para esta operação.  
  
 FOR ATTACH não pode ser especificado em um instantâneo do banco de dados.  
  
 FOR ATTACH pode especificar a opção de RESTRICTED_USER. RESTRICTED_USER permite que somente os membros da função de banco de dados fixa db_owner e das funções de servidor fixas dbcreator e sysadmin conectem-se ao banco de dados, mas não limita seu número. As tentativas de usuários não qualificados são recusadas.  
  
 Se o banco de dados usa [!INCLUDE[ssSB](../../includes/sssb-md.md)], use WITH \<service_broker_option > na cláusula FOR ATTACH: 
  
 \<service_broker_option > controles [!INCLUDE[ssSB](../../includes/sssb-md.md)] entrega de mensagens e o [!INCLUDE[ssSB](../../includes/sssb-md.md)] identificador para o banco de dados. As opções [!INCLUDE[ssSB](../../includes/sssb-md.md)] podem ser especificadas somente quando a cláusula FOR ATTACH é usada.  
  
 ENABLE_BROKER  
 Especifica que o [!INCLUDE[ssSB](../../includes/sssb-md.md)] está habilitado para o banco de dados especificado. Ou seja, a entrega de mensagens é iniciada e is_broker_enabled é definido como true na exibição do catálogo sys. Databases. O banco de dados retém o identificador do [!INCLUDE[ssSB](../../includes/sssb-md.md)] existente.  
  
 NEW_BROKER  
 Cria um novo valor de service_broker_guid no sys.databases e no banco de dados restaurado e encerra todos os pontos de extremidade de conversa com limpeza. O agente está habilitado, mas nenhuma mensagem é enviada aos pontos de extremidade de conversa remotos. Qualquer rota que referencia o antigo identificador do [!INCLUDE[ssSB](../../includes/sssb-md.md)] deve ser recriada novamente com o novo identificador.  
  
 ERROR_BROKER_CONVERSATIONS  
 Encerra todas as conversas com um erro que declara que o banco de dados está anexado ou restaurado. O agente é desabilitado até que essa operação seja concluída e, em seguida, é habilitado. O banco de dados retém o identificador do [!INCLUDE[ssSB](../../includes/sssb-md.md)] existente.  
  
 Ao anexar um banco de dados replicado que tenha sido copiado, em vez de desanexado, considere o seguinte:  
  
-   Se você anexar o banco de dados à mesma instância e versão de servidor como banco de dados original, nenhuma etapa adicional será necessária.  
  
-   Se você anexar o banco de dados para a mesma instância de servidor, mas com uma versão atualizada, você deve executar [sp_vupgrade_replication](../../relational-databases/system-stored-procedures/sp-vupgrade-replication-transact-sql.md) para atualizar a replicação após a conclusão da operação de anexação.  
  
-   Se você anexar o banco de dados a uma instância de servidor diferente, independentemente da versão, você deve executar [sp_removedbreplication](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) para remover a replicação após a conclusão da operação de anexação.  
  
> [!NOTE]  
>  Anexação funciona com o **vardecimal** formato de armazenamento, mas o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] devem ser atualizados para pelo menos [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 2. Não é possível anexar um banco de dados que usa formato de armazenamento vardecimal a uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações sobre o **vardecimal** formato de armazenamento, consulte [compactação de dados](../../relational-databases/data-compression/data-compression.md).  
  
 Quando um banco de dados é anexado ou restaurado pela primeira vez a uma nova instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], uma cópia da chave mestra de banco de dados (criptografada pela chave mestra de serviço) ainda não está armazenada no servidor. É necessário usar a instrução **OPEN MASTER KEY** para descriptografar a DMK (chave mestra do banco de dados). Após a descriptografia da DMK, você tem a opção de habilitar a descriptografia automática no futuro usando a instrução **ALTER MASTER KEY REGENERATE** para provisionar o servidor com uma cópia da DMK criptografada com a SMK (chave mestra de serviço). Quando um banco de dados for atualizado de uma versão anterior, a DMK deverá ser regenerada para usar o algoritmo AES mais recente. Para obter mais informações sobre como regenerar a DMK, veja [ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md). O tempo necessário para regenerar a chave DMK para atualizar o AES depende do número de objetos protegidos pela DMK. É necessário regenerar a chave DMK para atualizar o AES somente uma vez, isso não tem impacto sobre regenerações futuras como parte de uma estratégia de rotação de chave. Para obter informações sobre como atualizar um banco de dados usando anexar, consulte [atualizar um banco de dados utilizando desanexar e anexar &#40; Transact-SQL &#41; ](../../relational-databases/databases/upgrade-a-database-using-detach-and-attach-transact-sql.md).  
  
 **Observação de segurança** é recomendável não anexar bancos de dados de origens desconhecidas ou não confiáveis. Esses bancos de dados podem conter um código mal-intencionado que pode executar um código [!INCLUDE[tsql](../../includes/tsql-md.md)] inesperado ou provocar erros modificando o esquema ou a estrutura física do banco de dados. Antes de usar um banco de dados de uma origem desconhecida ou não confiável, execute [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) no banco de dados em um servidor de produção, além disso, examine o código, como procedimentos armazenados ou outro código definido pelo usuário, no banco de dados.  
  
> [!NOTE]  
>  O **TRUSTWORTHY** e **DB_CHAINING** opções não terão nenhum efeito quando anexar um banco de dados.  
  
 FOR ATTACH_REBUILD_LOG  
 Especifica que o banco de dados é criado pela anexação de um conjunto existente de arquivos do sistema operacional. Essa opção é limitada a bancos de dados de leitura/gravação. Deve haver uma  *\<filespec >* entrada especifica o arquivo primário. Se um ou mais arquivos de log de transações estiverem ausentes, o arquivo de log será reconstruído. O ATTACH_REBUILD_LOG cria automaticamente um novo arquivo de log de 1 MB. Esse arquivo é colocado no local padrão de arquivo de log. Para obter informações sobre esse local, consulte [exibir ou alterar os locais padrão de dados e arquivos de Log &#40; SQL Server Management Studio &#41; ](../../database-engine/configure-windows/view-or-change-the-default-locations-for-data-and-log-files.md).  
  
> [!NOTE]  
>  Se os arquivos de log estiverem disponíveis, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] usará esses arquivos em vez de reconstruir os arquivos de log.  
  
 FOR ATTACH_REBUILD_LOG exige o seguinte:  
  
-   Um desligamento correto do banco de dados.  
  
-   Todos os arquivos de dados (MDF e NDF) devem estar disponíveis.  
  
> [!IMPORTANT]  
>  Essa operação interrompe a cadeia de backup de log. É recomendável que um backup completo do banco de dados seja executado após a conclusão da operação. Para obter mais informações, veja [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md).  
  
 Normalmente, FOR ATTACH_REBUILD_LOG é usado quando você copia um banco de dados de leitura/gravação com um log grande em outro servidor onde a cópia será usada principalmente, ou apenas, para operações de leitura e, portanto, exige menos espaço de log do que o banco de dados original.  
  
 FOR ATTACH_REBUILD_LOG não pode ser especificado em um instantâneo do banco de dados.  
  
 Para obter mais informações sobre como anexar ou desanexar bancos de dados, consulte [anexar e desanexar bancos de dados &#40; SQL Server &#41; ](../../relational-databases/databases/database-detach-and-attach-sql-server.md).  
  
 \<filespec >  
 Controla as propriedades do arquivo.  
  
 NOME *logical_file_name*  
 Especifica o nome lógico do arquivo. NAME é exigido quando FILENAME está especificado, exceto ao especificar uma das cláusulas FOR ATTACH. Um grupo de arquivos FILESTREAM não pode ser denominado PRIMARY.  
  
 *logical_file_name*  
 É o nome lógico usado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao referenciar o arquivo. *Logical_file_name* devem ser exclusivos no banco de dados e estar em conformidade com as regras de [identificadores](../../relational-databases/databases/database-identifiers.md). O nome pode ser um caractere ou constante Unicode ou um identificador normal ou delimitado.  
  
 Nome do arquivo { **'***os_file_name***'** | **'***filestream_path* **'** }  
 Especifica o nome do arquivo (físico) do sistema operacional.  
  
 **'** *os_file_name* **'**  
 É o caminho e o nome do arquivo usados pelo sistema operacional quando o arquivo é criado. O arquivo deve residir em um dos seguintes dispositivos: o servidor local no qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está instalado, uma rede de área de armazenamento [SAN] ou em uma rede baseada em iSCSI. O caminho especificado deve existir antes da execução da instrução CREATE DATABASE. Para obter mais informações, consulte "Arquivos de grupos de arquivos do banco de dados" na seção Comentários.  
  
 Os parâmetros SIZE, MAXSIZE e FILEGROWTH podem ser definidos quando um caminho UNC está especificado para o arquivo.  
  
 Se o arquivo estiver em uma partição bruta, *os_file_name* deve especificar somente a letra da unidade de uma partição bruta existente. Apenas um arquivo de dados pode ser criado em cada partição bruta.  
  
 Arquivos de dados não devem ser colocados em sistemas de arquivos compactados a não ser que os arquivos sejam secundários e somente leitura ou que o banco de dados seja somente leitura. Arquivos de log nunca devem ser colocados em sistemas de arquivos compactados.  
  
 **'** *filestream_path* **'**  
 Para um grupo de arquivos FILESTREAM, FILENAME faz referência a um caminho onde dados FILESTREAM serão armazenados. O caminho até a última pasta deve existir e a última pasta não deve existir. Por exemplo, se você especificar o caminho C:\MyFiles\MyFilestreamData, C:\MyFiles deve existir antes da execução de ALTER DATABASE, mas a pasta MyFilestreamData não deve existir.  
  
 O grupo de arquivos e o arquivo (`<filespec>`) devem ser criados na mesma instrução.  
  
 As propriedades SIZE e FILEGROWTH não se aplicam a um grupo de arquivos FILESTREAM.  
  
 TAMANHO *tamanho*  
 Especifica o tamanho do arquivo.  
  
 TAMANHO não pode ser especificado quando o *os_file_name* é especificado como um caminho UNC. SIZE não se aplica a um grupo de arquivos FILESTREAM.  
  
 *tamanho*  
 É o tamanho inicial do arquivo.  
  
 Quando *tamanho* não for fornecido para o arquivo primário, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] usa o tamanho do arquivo primário no banco de dados modelo. O tamanho padrão do modelo é de 8 MB (começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]) ou 1 MB (para versões anteriores). Quando um arquivo de dados secundário ou um arquivo de log for especificado, mas *tamanho* não for especificado para o arquivo, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] faz com que o arquivo de 8 MB (começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]) ou 1 MB (para versões anteriores). O tamanho especificado para o arquivo primário deve ser, no mínimo, tão grande quanto o arquivo primário do banco de dados modelo.  
  
 Os sufixos KB (quilobyte), MB (megabyte), GB (gigabyte) ou TB (terabyte) podem ser usados. O padrão é MB. Especifique um número inteiro; não inclua um decimal. *Tamanho* é um valor inteiro. Para valores maiores que 2147483647, use unidades maiores.  
  
 MAXSIZE *max_size*  
 Especifica o tamanho máximo até o qual o arquivo pode crescer. MAXSIZE não pode ser especificado quando o *os_file_name* é especificado como um caminho UNC.  
  
 *max_size*  
 É o tamanho máximo do arquivo. Os sufixos KB, MB, GB e TB podem ser usados. O padrão é MB. Especifique um número inteiro; não inclua um decimal. Se *max_size* não for especificado, o arquivo cresce até que o disco está cheio. *Max_size* é um valor inteiro. Para valores maiores que 2147483647, use unidades maiores.  
  
 UNLIMITED  
 Especifica que o arquivo crescerá até que o disco esteja cheio. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um arquivo de log especificado com crescimento ilimitado tem um tamanho máximo de 2 TB, e um arquivo de dados tem um tamanho máximo de 16 TB.  
  
> [!NOTE]  
>  Não há nenhum tamanho máximo quando essa opção é especificada para um contêiner FILESTREAM. Ele continua crescendo até que o disco esteja cheio.  
  
 FILEGROWTH *growth_increment*  
 Especifica o incremento de crescimento automático do arquivo. A configuração de FILEGROWTH de um arquivo não pode exceder a configuração de MAXSIZE. FILEGROWTH não pode ser especificado quando o *os_file_name* é especificado como um caminho UNC. FILEGROWTH não se aplica a um grupo de arquivos FILESTREAM.  
  
 *growth_increment*  
 É a quantidade de espaço adicionada ao arquivo sempre que novo espaço é necessário.  
  
 O valor pode ser especificado em MB, KB, GB, TB ou porcentagem (%). Se um número for especificado sem um sufixo MB, KB, ou %, o padrão será MB. Quando % está especificada, o tamanho do incremento de crescimento é a porcentagem especificada do tamanho do arquivo no momento em que ocorre o incremento. O tamanho especificado é arredondado para o mais próximo de 64 KB e o valor mínimo é 64 KB.  
  
 Um valor 0 indica que o crescimento automático está desativado e nenhum espaço adicional é permitido.  
  
 Se FILEGROWTH não for especificado, os valores padrão são:  
  
|Versão|Valores padrão|  
|-------------|--------------------|  
|Início[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|Dados de 64 MB. Os arquivos de log de 64 MB.|  
|Início[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|Dados de 1 MB. Arquivos de log 10%.|  
|Antes de[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|Dados de 10%. Arquivos de log 10%.|  
  
 \<grupo de arquivos >  
 Controla as propriedades do grupo de arquivos. O grupo de arquivos não pode ser especificado em um instantâneo do banco de dados.  
  
 Grupo de arquivos *filegroup_name*  
 É o nome lógico do grupo de arquivos.  
  
 *filegroup_name*  
 *filegroup_name* devem ser exclusivos no banco de dados e não pode ser os fornecido pelo sistema nomes PRIMARY e PRIMARY_LOG. O nome pode ser um caractere ou constante Unicode ou um identificador normal ou delimitado. O nome deve estar em conformidade com as regras de [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
 CONTAINS FILESTREAM  
 Especifica que o grupo de arquivos armazena BLOBs (objetos binários grandes) FILESTREAM no sistema de arquivos.  
  
 CONTAINS MEMORY_OPTIMIZED_DATA  

**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] por meio de[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Especifica que o grupo de arquivos armazena dados memory_optimized no sistema de arquivos. Para obter mais informações, veja [OLTP in-memory &#40;Otimização na memória&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md). Apenas um grupo de arquivos MEMORY_OPTIMIZED_DATA é permitido por banco de dados. Para obter exemplos de código que cria um grupo de arquivos para armazenar dados com otimização de memória, consulte [criando uma tabela com otimização de memória e um procedimento armazenado compilado nativamente](../../relational-databases/in-memory-oltp/creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md).  
  
 DEFAULT  
 Especifica que o grupo de arquivos nomeado é o grupo de arquivos padrão no banco de dados.  
  
 *database_snapshot_name*  
 É o nome do novo instantâneo do banco de dados. Nomes de instantâneos de bancos de dados devem ser exclusivos dentro de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e estar de acordo com as regras de identificadores. *database_snapshot_name* pode ter no máximo 128 caracteres.  
  
 ON **(** nome  **=**  *logical_file_name***,** FILENAME **='**  *os_file_name***')** [ **,**... *n* ]  
 Na criação de um instantâneo do banco de dados, especifica uma lista de arquivos no banco de dados de origem. Para que o instantâneo funcione, todos os arquivos de dados devem ser especificados individualmente. No entanto, arquivos de log não são permitidos para instantâneos do banco de dados. Os grupos de arquivos FILESTREAM não são suportados pelos instantâneos do banco de dados. Se um arquivo de dados FILESTREAM for incluído em uma cláusula CREATE DATABASE ON, a instrução falhará e um erro será gerado.  
  
 Para descrições de NAME e FILENAME e seus valores, consulte as descrições dos equivalente \<filespec > valores.  
  
> [!NOTE]  
>  Quando você cria um instantâneo de banco de dados, o outro \<filespec > Opções e a palavra-chave primária não são permitidas.  
  
 AS SNAPSHOT OF *source_database_name*  
 Especifica que o banco de dados que está sendo criado é um instantâneo de banco de dados do banco de dados de origem especificado por *source_database_name*. O instantâneo e o banco de dados de origem devem estar na mesma instância.  
  
 Para obter mais informações, consulte "Instantâneos do banco de dados" na seção Comentários.  
  
## <a name="remarks"></a>Comentários  
 O [banco de dados mestre](../../relational-databases/databases/master-database.md) deve ser feito sempre que um banco de dados do usuário for criado, modificado ou descartado.  
  
 A instrução CREATE DATABASE deve ser executada em modo de confirmação automática (o modo padrão de gerenciamento de transações) e não é permitida em uma transação explícita ou implícita.  
  
 Você pode usar uma instrução CREATE DATABASE para criar um banco de dados e os arquivos que armazenam o banco de dados. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] implementa a instrução CREATE DATABASE usando as seguintes etapas:  
  
1.  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa uma cópia do [banco de dados modelo](../../relational-databases/databases/model-database.md) para inicializar o banco de dados e seus metadados.  
  
2.  Um GUID do agente de serviço é atribuído ao banco de dados.  
  
3.  Em seguida, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] preenche o restante do banco de dados com páginas vazias, exceto as páginas que têm dados internos que registram como o espaço é usado no banco de dados.  
  
 No máximo 32.767 bancos de dados podem ser especificados em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Cada banco de dados tem um proprietário que pode executar atividades especiais no banco de dados. O proprietário é o usuário que cria o banco de dados. O proprietário do banco de dados pode ser alterado usando [sp_changedbowner](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md).  

Alguns recursos de banco de dados dependem de recursos ou recursos presentes no sistema de arquivos para a funcionalidade completa de um banco de dados. Alguns exemplos de recursos que dependem do conjunto de recursos de sistema de arquivo incluem:
- DBCC CHECKDB
- FileStream
- Uso de instantâneos do VSS e o arquivo de backups online
- Criação de instantâneo do banco de dados
- Grupo de arquivos de dados com otimização de memória
   
## <a name="database-files-and-filegroups"></a>Arquivos e grupos de arquivos do banco de dados  
 Cada banco de dados tem pelo menos dois arquivos, um *arquivo primário* e um *arquivo de log de transação*e pelo menos um grupo de arquivos. Um máximo de 32.767 arquivos e 32.767 grupos de arquivos pode ser especificado para cada banco de dados.  
  
 Ao criar um banco de dados, torne os arquivos de dados tão grandes quanto possível, com base na quantidade máxima de dados que você espera ter no banco de dados  
  
 É recomendável usar uma rede SAN, uma rede baseada em iSCSI ou um disco conectado localmente para o armazenamento dos arquivos de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], pois essa configuração otimiza o desempenho e a confiabilidade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="database-snapshots"></a>Instantâneos do banco de dados  
 Você pode usar a instrução CREATE DATABASE para criar uma exibição somente leitura, estática, um *instantâneo de banco de dados* do *banco de dados de origem*. Um instantâneo do banco de dados é transacionalmente consistente com o banco de dados de origem pois existia no momento da criação do banco de dados. Um banco de dados de origem pode ter vários instantâneos.  
  
> [!NOTE]  
>  Quando você cria um instantâneo do banco de dados, a instrução CREATE DATABASE não pode fazer referência a arquivos de log, arquivos offline, arquivos de restauração e arquivos extintos.  
  
 Se a criação de um instantâneo do banco de dados falhar, o instantâneo se tornará suspeito e deverá ser excluído. Para obter mais informações, consulte [DROP DATABASE &#40; Transact-SQL &#41; ](../../t-sql/statements/drop-database-transact-sql.md).  
  
 Cada instantâneo persiste até que seja excluído usando DROP DATABASE.  
  
 Para obter mais informações, consulte [Instantâneos de banco de dados &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md).  
  
## <a name="database-options"></a>Opções de banco de dados  
 Várias opções de banco de dados são automaticamente definidas sempre que você cria um banco de dados. Para obter uma lista dessas opções, consulte [opções ALTER DATABASE SET &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
## <a name="the-model-database-and-creating-new-databases"></a>Banco de dados modelo e criação de novos bancos de dados  
 Todos os objetos definidos pelo usuário no [banco de dados modelo](../../relational-databases/databases/model-database.md) são copiados para todos os bancos de dados recém-criado. É possível adicionar quaisquer objetos, como tabelas, exibições, procedimentos armazenados, tipos de dados, etc. ao banco de dados modelo para que sejam incluídos em todos os bancos de dados recém-criados.  
  
 Quando um banco de dados criar *database_name* instrução for especificada sem parâmetros adicionais de tamanho, o arquivo de dados primário é feito do mesmo tamanho que o arquivo primário no banco de dados modelo.  
  
 A não ser que FOR ATTACH seja especificado, cada novo banco de dados herda as configurações de opções do banco de dados modelo. Por exemplo, a opção de banco de dados reduzir automaticamente é definida como **true** no modelo e em quaisquer novos bancos de dados que você criar. Se você alterar as opções no banco de dados modelo, essas novas configurações de opções serão usadas em todos os novos bancos de dados criados. A alteração das operações no banco de dados modelo não afeta bancos de dados existentes. Se FOR ATTACH estiver especificado na instrução CREATE DATABASE, o novo banco de dados herdará as configurações de opções do banco de dados original.  
  
## <a name="viewing-database-information"></a>Exibindo informações do banco de dados  
 É possível usar exibições do catálogo, funções do sistema e procedimentos armazenados do sistema para retornar informações sobre bancos de dados, arquivos e grupos de arquivos. Para obter mais informações, veja [Exibições do sistema &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90).  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CREATE DATABASE, CREATE ANY DATABASE ou ALTER ANY DATABASE.  
  
 Para manter controle sobre o uso do disco em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a permissão para criar bancos de dados geralmente é limitada a algumas contas de logon.  
  
 O exemplo a seguir fornece a permissão para criar um banco de dados para o usuário Fay de banco de dados.  
  
```  
USE master;  
GO  
GRANT CREATE DATABASE TO [Fay];  
GO  
```  
  
### <a name="permissions-on-data-and-log-files"></a>Permissões em arquivos de dados e de log  
 Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], determinadas permissões são definidas nos arquivos de dados e de log de cada banco de dados. As permissões a seguir são definidas sempre que as seguintes operações são aplicadas a um banco de dados:  
  
|||  
|-|-|  
|Criado|Modificado para adicionar um novo arquivo|  
|Anexado|O backup|  
|Desanexado|Restaurado|  
  
 As permissões evitam que os arquivos sejam violados acidentalmente caso residam em um diretório com permissões abertas.  
  
> [!NOTE]  
>  O [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)] não define permissões de arquivos de dados e de log.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-a-database-without-specifying-files"></a>A. Criando um banco de dados sem especificar arquivos  
 O exemplo a seguir cria o banco de dados `mytest` e os arquivos primário e de log de transações correspondentes. Porque a instrução não tiver nenhuma \<filespec > itens, o arquivo de banco de dados primário é o tamanho do arquivo primário de banco de dados de modelo. O log de transações é definido como o maior desses valores: 512 KB ou 25% do tamanho do arquivo de dados primário. Como MAXSIZE não é especificado, os arquivos podem crescer até encher todo o espaço em disco disponível. Este exemplo de também demonstra como descartar um banco de dados denominado `mytest`, se ele existir, antes da criação do banco de dados `mytest`.  
  
```  
USE master;  
GO  
IF DB_ID (N'mytest') IS NOT NULL
DROP DATABASE mytest;
GO
CREATE DATABASE mytest;  
GO  
-- Verify the database files and sizes  
SELECT name, size, size*1.0/128 AS [Size in MBs]   
FROM sys.master_files  
WHERE name = N'mytest';  
GO  
  
```  
  
### <a name="b-creating-a-database-that-specifies-the-data-and-transaction-log-files"></a>B. Criando um banco de dados que especifica os arquivos de dados e de log de transações  
 O exemplo a seguir cria o banco de dados `Sales`. Como a palavra-chave PRIMARY não é usado, o primeiro arquivo (`Sales_dat`) se torna o arquivo primário. Como nem MB nem KB é especificado no parâmetro SIZE do arquivo `Sales_dat` , ele usa MB e é alocado em megabytes. O backup do banco de dados `Sales_log` é alocado em megabytes porque o sufixo `MB` é explicitamente declarado no parâmetro `SIZE` .  
  
```tsql  
USE master;  
GO  
CREATE DATABASE Sales  
ON   
( NAME = Sales_dat,  
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\saledat.mdf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 5 )  
LOG ON  
( NAME = Sales_log,  
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\salelog.ldf',  
    SIZE = 5MB,  
    MAXSIZE = 25MB,  
    FILEGROWTH = 5MB ) ;  
GO  
```  
  
### <a name="c-creating-a-database-by-specifying-multiple-data-and-transaction-log-files"></a>C. Criando um banco de dados especificando vários arquivos de dados e de log de transações  
 O exemplo a seguir cria o banco de dados `Archive` que tem três arquivos de dados de `100-MB` e dois arquivos de log de transações de `100-MB`. O arquivo primário é o primeiro arquivo da lista e é especificado explicitamente com a palavra-chave `PRIMARY`. Os arquivos de log de transações são especificados em seguida às palavras-chave `LOG ON`. Observe as extensões usadas para os arquivos na opção `FILENAME`: `.mdf` é usado para arquivos de dados primários, `.ndf` para arquivos de dados secundários e `.ldf` para arquivos de log de transações. Este exemplo coloca o banco de dados na unidade `D:` e não com o banco de dados `master`.  
  
```tsql  
USE master;  
GO  
CREATE DATABASE Archive   
ON  
PRIMARY    
    (NAME = Arch1,  
    FILENAME = 'D:\SalesData\archdat1.mdf',  
    SIZE = 100MB,  
    MAXSIZE = 200,  
    FILEGROWTH = 20),  
    ( NAME = Arch2,  
    FILENAME = 'D:\SalesData\archdat2.ndf',  
    SIZE = 100MB,  
    MAXSIZE = 200,  
    FILEGROWTH = 20),  
    ( NAME = Arch3,  
    FILENAME = 'D:\SalesData\archdat3.ndf',  
    SIZE = 100MB,  
    MAXSIZE = 200,  
    FILEGROWTH = 20)  
LOG ON   
   (NAME = Archlog1,  
    FILENAME = 'D:\SalesData\archlog1.ldf',  
    SIZE = 100MB,  
    MAXSIZE = 200,  
    FILEGROWTH = 20),  
   (NAME = Archlog2,  
    FILENAME = 'D:\SalesData\archlog2.ldf',  
    SIZE = 100MB,  
    MAXSIZE = 200,  
    FILEGROWTH = 20) ;  
GO  
```  
  
### <a name="d-creating-a-database-that-has-filegroups"></a>D. Criando um banco de dados que tem grupos de arquivos  
 O exemplo a seguir cria o banco de dados `Sales` que tem os seguintes grupos de arquivos:  
  
-   O grupo de arquivos primário com os arquivos `Spri1_dat` e `Spri2_dat`. Os incrementos de FILEGROWTH desses arquivos são especificados como `15%`.  
  
-   Um grupo de arquivos denominado `SalesGroup1` com os arquivos `SGrp1Fi1` e `SGrp1Fi2`.  
  
-   Um grupo de arquivos denominado `SalesGroup2` com os arquivos `SGrp2Fi1` e `SGrp2Fi2`.  
  
 Este exemplo coloca os dados e os arquivos de log em discos diferentes para melhorar o desempenho.  
  
```tsql  
USE master;  
GO  
CREATE DATABASE Sales  
ON PRIMARY  
( NAME = SPri1_dat,  
    FILENAME = 'D:\SalesData\SPri1dat.mdf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 15% ),  
( NAME = SPri2_dat,  
    FILENAME = 'D:\SalesData\SPri2dt.ndf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 15% ),  
FILEGROUP SalesGroup1  
( NAME = SGrp1Fi1_dat,  
    FILENAME = 'D:\SalesData\SG1Fi1dt.ndf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 5 ),  
( NAME = SGrp1Fi2_dat,  
    FILENAME = 'D:\SalesData\SG1Fi2dt.ndf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 5 ),  
FILEGROUP SalesGroup2  
( NAME = SGrp2Fi1_dat,  
    FILENAME = 'D:\SalesData\SG2Fi1dt.ndf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 5 ),  
( NAME = SGrp2Fi2_dat,  
    FILENAME = 'D:\SalesData\SG2Fi2dt.ndf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 5 )  
LOG ON  
( NAME = Sales_log,  
    FILENAME = 'E:\SalesLog\salelog.ldf',  
    SIZE = 5MB,  
    MAXSIZE = 25MB,  
    FILEGROWTH = 5MB ) ;  
GO  
```  
  
### <a name="e-attaching-a-database"></a>E. Anexando um banco de dados  
 O exemplo a seguir desanexa o banco de dados `Archive` criado no exemplo D e o anexa usando a cláusula `FOR ATTACH`. `Archive` foi definido para ter vários dados e arquivos de log. No entanto, como o local dos arquivos não foi alterado desde sua criação, apenas o arquivo primário precisa ser especificado na cláusula `FOR ATTACH`. A partir do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], todos os arquivos de texto completo que fazem parte do banco de dados que está sendo anexado serão anexados com o banco de dados.  
  
```tsql  
USE master;  
GO  
sp_detach_db Archive;  
GO  
CREATE DATABASE Archive  
      ON (FILENAME = 'D:\SalesData\archdat1.mdf')   
      FOR ATTACH ;  
GO  
```  
  
### <a name="f-creating-a-database-snapshot"></a>F. Criando um instantâneo do banco de dados  
 O exemplo a seguir cria o instantâneo de banco de dados `sales_snapshot0600`. Como um instantâneo do banco de dados é somente leitura, um arquivo de log não pode ser especificado. Em conformidade com a sintaxe, todo arquivo do banco de dados de origem é especificado e grupos de arquivos não são especificados.  
  
 O banco de dados de origem deste exemplo é o banco de dados `Sales` criado no exemplo D.  
  
```tsql  
USE master;  
GO  
CREATE DATABASE sales_snapshot0600 ON  
    ( NAME = SPri1_dat, FILENAME = 'D:\SalesData\SPri1dat_0600.ss'),  
    ( NAME = SPri2_dat, FILENAME = 'D:\SalesData\SPri2dt_0600.ss'),  
    ( NAME = SGrp1Fi1_dat, FILENAME = 'D:\SalesData\SG1Fi1dt_0600.ss'),  
    ( NAME = SGrp1Fi2_dat, FILENAME = 'D:\SalesData\SG1Fi2dt_0600.ss'),  
    ( NAME = SGrp2Fi1_dat, FILENAME = 'D:\SalesData\SG2Fi1dt_0600.ss'),  
    ( NAME = SGrp2Fi2_dat, FILENAME = 'D:\SalesData\SG2Fi2dt_0600.ss')  
AS SNAPSHOT OF Sales ;  
GO  
```  
  
### <a name="g-creating-a-database-and-specifying-a-collation-name-and-options"></a>G. Criando um banco de dados e especificando um nome e opções de agrupamento  
 O exemplo a seguir cria o banco de dados `MyOptionsTest`. Um nome de agrupamento é especificado e as opções `TRUSTYWORTHY` e `DB_CHAINING` são definidas como `ON`.  
  
```tsql  
USE master;  
GO  
IF DB_ID (N'MyOptionsTest') IS NOT NULL  
DROP DATABASE MyOptionsTest;  
GO  
CREATE DATABASE MyOptionsTest  
COLLATE French_CI_AI  
WITH TRUSTWORTHY ON, DB_CHAINING ON;  
GO  
--Verifying collation and option settings.  
SELECT name, collation_name, is_trustworthy_on, is_db_chaining_on  
FROM sys.databases  
WHERE name = N'MyOptionsTest';  
GO  
  
```  
  
### <a name="h-attaching-a-full-text-catalog-that-has-been-moved"></a>H. Anexando um catálogo de texto completo que foi movido  
 O exemplo a seguir anexa o catálogo de texto completo `AdvWksFtCat` juntamente com os arquivos de dados e de log do `AdventureWorks2012`. Neste exemplo, o catálogo de texto completo é movido de seu local padrão para um novo local `c:\myFTCatalogs`. Os arquivos de dados e de log permanecem em seus locais padrão.  
  
```tsql  
USE master;  
GO  
--Detach the AdventureWorks2012 database  
sp_detach_db AdventureWorks2012;  
GO  
-- Physically move the full text catalog to the new location.  
--Attach the AdventureWorks2012 database and specify the new location of the full-text catalog.  
CREATE DATABASE AdventureWorks2012 ON   
    (FILENAME = 'c:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\AdventureWorks2012_data.mdf'),   
    (FILENAME = 'c:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\AdventureWorks2012_log.ldf'),  
    (FILENAME = 'c:\myFTCatalogs\AdvWksFtCat')  
FOR ATTACH;  
GO  
```  
  
### <a name="i-creating-a-database-that-specifies-a-row-filegroup-and-two-filestream-filegroups"></a>I. Criando um banco de dados que especifica um grupo de arquivos de linha e dois grupos de arquivos FILESTREAM  
 O exemplo a seguir cria o banco de dados `FileStreamDB`. O banco de dados é criado com um grupo de arquivos de linha e dois grupos de arquivos FILESTREAM. Cada grupo de arquivos contém um arquivo:  
  
-   `FileStreamDB_data` contém dados de linha. Ele contém um arquivo, `FileStreamDB_data.mdf` com o caminho padrão.  
  
-   `FileStreamPhotos` contém dados FILESTREAM. Ele contém dois contêineres de dados FILESTREAM, `FSPhotos`, localizado em `C:\MyFSfolder\Photos` e `FSPhotos2`, localizado em `D:\MyFSfolder\Photos`. É marcado como o grupo de arquivos FILESTREAM padrão.  
  
-   `FileStreamResumes` contém dados FILESTREAM. Ele contém um contêiner de dados FILESTREAM, `FSResumes`, localizado em `C:\MyFSfolder\Resumes`.  
  
```tsql  
USE master;  
GO  
-- Get the SQL Server data path.  
DECLARE @data_path nvarchar(256);  
SET @data_path = (SELECT SUBSTRING(physical_name, 1, CHARINDEX(N'master.mdf', LOWER(physical_name)) - 1)  
                  FROM master.sys.master_files  
                  WHERE database_id = 1 AND file_id = 1);  
  
 -- Execute the CREATE DATABASE statement.   
EXECUTE ('CREATE DATABASE FileStreamDB  
ON PRIMARY   
    (  
    NAME = FileStreamDB_data   
    ,FILENAME = ''' + @data_path + 'FileStreamDB_data.mdf''  
    ,SIZE = 10MB  
    ,MAXSIZE = 50MB  
    ,FILEGROWTH = 15%  
    ),  
FILEGROUP FileStreamPhotos CONTAINS FILESTREAM DEFAULT  
    (  
    NAME = FSPhotos  
    ,FILENAME = ''C:\MyFSfolder\Photos''  
-- SIZE and FILEGROWTH should not be specified here.  
-- If they are specified an error will be raised.  
, MAXSIZE = 5000 MB  
    ),  
    (  
      NAME = FSPhotos2  
      , FILENAME = ''D:\MyFSfolder\Photos''  
      , MAXSIZE = 10000 MB  
     ),  
FILEGROUP FileStreamResumes CONTAINS FILESTREAM  
    (  
    NAME = FileStreamResumes  
    ,FILENAME = ''C:\MyFSfolder\Resumes''  
    )   
LOG ON  
    (  
    NAME = FileStream_log  
    ,FILENAME = ''' + @data_path + 'FileStreamDB_log.ldf''  
    ,SIZE = 5MB  
    ,MAXSIZE = 25MB  
    ,FILEGROWTH = 5MB  
    )'  
);  
GO  
```  
  
### <a name="j-creating-a-database-that-has-a-filestream-filegroup-with-multiple-files"></a>J. Criando um banco de dados que tem um grupo de arquivos FILESTREAM com vários arquivos  
 O exemplo a seguir cria o banco de dados `BlobStore1`. O banco de dados é criado com um grupo de arquivos de linha e um grupo de arquivos FILESTREAM, `FS`. O grupo de arquivos FILESTREAM contêm dois arquivos, `FS1` e `FS2`. O banco de dados é alterado adicionando-se um terceiro arquivo, `FS3`, ao grupo de arquivos FILESTREAM.  
  
```tsql  
USE master;  
GO  
  
CREATE DATABASE [BlobStore1]  
CONTAINMENT = NONE  
ON PRIMARY   
(   
    NAME = N'BlobStore1',   
    FILENAME = N'C:\BlobStore\BlobStore1.mdf',  
    SIZE = 100MB,  
    MAXSIZE = UNLIMITED,  
    FILEGROWTH = 1MB  
),   
FILEGROUP [FS] CONTAINS FILESTREAM DEFAULT   
(  
    NAME = N'FS1',  
    FILENAME = N'C:\BlobStore\FS1',  
    MAXSIZE = UNLIMITED  
),   
(  
    NAME = N'FS2',  
    FILENAME = N'C:\BlobStore\FS2',  
    MAXSIZE = 100MB  
)  
LOG ON   
(  
    NAME = N'BlobStore1_log',  
    FILENAME = N'C:\BlobStore\BlobStore1_log.ldf',  
    SIZE = 100MB,  
    MAXSIZE = 1GB,  
    FILEGROWTH = 1MB  
);  
GO  
  
ALTER DATABASE [BlobStore1]  
ADD FILE  
(  
    NAME = N'FS3',  
    FILENAME = N'C:\BlobStore\FS3',  
    MAXSIZE = 100MB  
)  
TO FILEGROUP [FS];  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Anexar e desanexar bancos de dados &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_changedbowner &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)   
 [sp_detach_db &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)   
 [sp_removedbreplication &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)   
 [Instantâneos de banco de dados &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)   
 [Mover arquivos de banco de dados](../../relational-databases/databases/move-database-files.md)   
 [Bancos de dados](../../relational-databases/databases/databases.md)   
 [Objeto binário grande &#40;Blob&#41; Dados &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)  


