---
title: CREATE DATABASE (Transact-SQL) | Microsoft Docs
description: Sintaxe de criação de banco de dados para SQL Server, Banco de Dados SQL do Azure, Azure Synapse Analytics e Analytics Platform System
ms.custom: ''
ms.date: 07/21/2020
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-current||=azuresqldb-mi-current||=azure-sqldw-latest||>=aps-pdw-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 4738bbf83c73ae8f2e58b10196e1fc1394d43383
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539866"
---
# <a name="create-database"></a>CREATE DATABASE

Cria um novo banco de dados.

Clique em uma das guias a seguir para ver sintaxe, argumentos, comentários, permissões e exemplos de uma versão específica do SQL com a qual você está trabalhando.

Para obter mais informações sobre as convenções de sintaxe, consulte [Convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).

[!INCLUDE[select-product](../../includes/select-product.md)]

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions"

:::row:::
    :::column:::
        **_\* SQL Server \*_** &nbsp;
    :::column-end:::
    :::column:::
        [Banco de Dados SQL](create-database-transact-sql.md?view=azuresqldb-current)
    :::column-end:::
    :::column:::
        [Banco de Dados SQL<br />Instância Gerenciada](create-database-transact-sql.md?view=azuresqldb-mi-current)
    :::column-end:::
    :::column:::
        [Azure Synapse<br />Analytics](create-database-transact-sql.md?view=azure-sqldw-latest)
    :::column-end:::
    :::column:::
        [Analytics Platform<br />System (PDW)](create-database-transact-sql.md?view=aps-pdw-2016)
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="sql-server"></a>SQL Server

## <a name="overview"></a>Visão geral

No SQL Server, essa instrução cria um novo banco de dados e os arquivos usados e seus grupos de arquivos. Também pode ser usado para criar um instantâneo de banco de dados ou anexar arquivos de banco de dados para criar um banco de dados com os arquivos desanexados de outro banco de dados.

## <a name="syntax"></a>Sintaxe

Criar um banco de dados.

```syntaxsql
CREATE DATABASE database_name
[ CONTAINMENT = { NONE | PARTIAL } ]
[ ON
      [ PRIMARY ] <filespec> [ ,...n ]
      [ , <filegroup> [ ,...n ] ]
      [ LOG ON <filespec> [ ,...n ] ]
]
[ COLLATE collation_name ]
[ WITH <option> [,...n ] ]
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
    | PERSISTENT_LOG_BUFFER=ON ( DIRECTORY_NAME='<Filepath to folder on DAX formatted volume>' )
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

Anexar um banco de dados

```syntaxsql
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

Criar um instantâneo do banco de dados

```syntaxsql
CREATE DATABASE database_snapshot_name
    ON
    (
        NAME = logical_file_name,
        FILENAME = 'os_file_name'
    ) [ ,...n ]
    AS SNAPSHOT OF
[;]
```

## <a name="arguments"></a>Argumentos

*database_name* É o nome do novo banco de dados. Nomes de bancos de dados devem ser exclusivos dentro de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e estar de acordo com as regras de [identificadores](../../relational-databases/databases/database-identifiers.md).

*database_name* pode conter um máximo de 128 caracteres, a menos que um nome lógico não esteja especificado para o arquivo de log. Se não for especificado um nome de arquivo de log lógico, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gerará o *logical_file_name* e *os_file_name* para o log acrescentando um sufixo a *database_name*. Isso limita o *database_name* a 123 caracteres de modo que o nome do arquivo lógico gerado não seja maior do que 128 caracteres.

Se o nome do arquivo de dados não for especificado, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usará *database_name* como o *logical_file_name* e como o *os_file_name*. O caminho padrão é obtido do Registro. O caminho padrão pode ser alterado usando as **Propriedades do Servidor (Página Configurações de Banco de Dados)** no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. A alteração do caminho padrão exige o reinício do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

CONTAINMENT = { NONE | PARTIAL }

**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior

Especifica o status de contenção do banco de dados. NONE = banco de dados dependente. PARTIAL = banco de dados parcialmente independente.

ON Especifica que os arquivos em disco usados para armazenar as seções de dados do banco de dados, arquivos de dados, são definidos explicitamente. ON é necessário quando seguido por uma lista de itens \<filespec> separados por vírgula que definem os arquivos de dados para o grupo de arquivos primário. A lista de arquivos no grupo de arquivos primário pode ser seguida por uma lista opcional de itens \<filegroup> separados por vírgula que definem os grupos de arquivos de usuários e seus arquivos.

PRIMARY especifica que a lista \<filespec> associada define o arquivo primário. O primeiro arquivo especificado na entrada \<filespec> no grupo de arquivos primário torna-se o arquivo primário. Um banco de dados pode conter apenas um arquivo primário. Para obter mais informações, consulte [Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md).

Se PRIMARY não estiver especificado, o primeiro arquivo listado na instrução CREATE DATABASE se tornará o arquivo primário.

LOG ON Especifica que os arquivos em disco usados para armazenar o log do banco de dados, os arquivos de log, são definidos explicitamente. LOG ON é seguido por uma lista de itens \<filespec> separados por vírgula que definem os arquivos de log. Se LOG ON não estiver especificado, um arquivo de log será criado automaticamente com um tamanho de 25 por cento da soma dos tamanhos de todos os arquivos de dados do banco de dados ou 512 KB, o que for maior. Esse arquivo é colocado no local padrão de arquivo de log. Para obter informações sobre esse local, veja [Exibir ou alterar os locais padrão de arquivos de log e dados – SSMS](../../database-engine/configure-windows/view-or-change-the-default-locations-for-data-and-log-files.md).

LOG ON não pode ser especificado em um instantâneo do banco de dados.

COLLATE *collation_name* Especifica a ordenação padrão do banco de dados. O nome da ordenação pode ser um nome de ordenação do Windows ou um nome de ordenação SQL. Se não estiver especificado, a ordenação padrão da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será atribuída ao banco de dados. Um nome de ordenação não pode ser especificado em um instantâneo do banco de dados.

Um nome de ordenação não pode ser especificado com as cláusulas FOR ATTACH ou FOR ATTACH_REBUILD_LOG. Para obter informações sobre como alterar a ordenação de um banco de dados anexado, acesse o [site da Microsoft](https://go.microsoft.com/fwlink/?linkid=16419&kbid=325335).

Para saber mais sobre nomes de ordenações Windows e SQL, confira [COLLATE](~/t-sql/statements/collations.md).

> [!NOTE]
> Os bancos de dados independentes são agrupados de maneira diferente dos bancos de dados dependente. Veja [Ordenações de banco de dados independentes](../../relational-databases/databases/contained-database-collations.md) para obter mais informações.

WITH \<option>
 **\<filestream_options>**

NON_TRANSACTED_ACCESS = { **OFF** | READ_ONLY | FULL } **Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.

Especifica o nível de acesso não transacional de FILESTREAM ao banco de dados.

|Valor|Descrição|
|-----------|-----------------|
|OFF|O acesso não transacional está desabilitado.|
|READONLY|Os dados FILESTREAM deste banco de dados podem ser lidos por processos não transacionais.|
|FULL|O acesso não transacional completo a FileTables FILESTREAM está habilitado.|

DIRECTORY_NAME = \<directory_name>
**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior

Um nome de diretório compatível com o Windows. Esse nome deve ser exclusivo entre todos os nomes de Database_Directory na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A comparação de exclusividade não diferencia maiúsculas de minúsculas, independentemente das configurações de ordenação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa opção deve ser definida antes da criação de um FileTable neste banco de dados.

As opções a seguir são permitidas apenas quando CONTAINMENT estiver definido como PARTIAL. Se CONTAINMENT não for definida como NOME, ocorrerão erros.

- **DEFAULT_FULLTEXT_LANGUAGE = \<lcid> | \<language name> | \<language alias>**

  **Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior

  Confira [Configurar a opção de Configuração de Servidor de linguagem de texto completo padrão](../../database-engine/configure-windows/configure-the-default-full-text-language-server-configuration-option.md) para obter uma descrição completa dessa opção.

- **DEFAULT_LANGUAGE = \<lcid> | \<language name> | \<language alias>**

  **Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior

  Confira [Configurar a opção de Configuração de Servidor de idioma padrão](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md) para obter uma descrição completa dessa opção.

- **NESTED_TRIGGERS = { OFF | ON}**

  **Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior

  Confira [Configurar a opção de Configuração de Servidor de gatilhos aninhados](../../database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option.md) para obter uma descrição completa dessa opção.

- **TRANSFORM_NOISE_WORDS = { OFF | ON}**

  **Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior

  Confira [Opção de Configuração de Servidor transformar palavras de ruído](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md) para obter uma descrição completa dessa opção.

- **TWO_DIGIT_YEAR_CUTOFF = { 2049 | \<any year between 1753 and 9999> }**

  Quatro dígitos que representam um ano. 2049 é o valor padrão. Veja [Configurar a opção de Configuração de Servidor de corte de ano com dois dígitos](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md) para obter uma descrição completa dessa opção.

- **DB_CHAINING { OFF | ON }**

  Quando ON estiver especificado, o banco de dados poderá ser a origem ou o destino de um encadeamento de propriedades de bancos de dados.

  Quando OFF, o banco de dados não poderá participar do encadeamento de propriedades de bancos de dados. O padrão é OFF.

  > [!IMPORTANT]
  > A instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reconhecerá essa configuração quando a opção do servidor Encadeamento de Propriedades de Bancos de Dados for 0 (OFF). Quando Encadeamento de Propriedades de BD for 1 (ON), todos os bancos de dados de usuário poderão participar de cadeias de propriedades de bancos de dados, independentemente do valor dessa opção. Essa opção é definida por meio de [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).

  A definição dessa opção requer associação à função de servidor fixa sysadmin. A opção DB_CHAINING não pode ser definida nesses bancos de dados do sistema: mestre, modelo, tempdb.

- **TRUSTWORTHY { OFF | ON }**

  Quando ON estiver especificado, os módulos de banco de dados (por exemplo, exibições, funções definidas pelo usuário ou procedimentos armazenados) que usam um contexto de representação poderão acessar recursos fora do banco de dados.

  Quando OFF, os módulos do banco de dados em um contexto de representação não poderão acessar recursos fora do banco de dados. O padrão é OFF.

  TRUSTWORTHY será definido como OFF sempre que o banco de dados for anexado.

  Por padrão, todos os bancos de dados do sistema, exceto o banco de dados msdb, têm TRUSTWORTHY definido como OFF. O valor não pode ser alterado para os bancos de dados modelo e tempdb. É recomendável nunca definir a opção TRUSTWORTHY como ON para o banco de dados mestre.

- **PERSISTENT_LOG_BUFFER=ON ( DIRECTORY_NAME='' )**

  Quando essa opção é especificada, o buffer de log de transações é criado em um volume que está localizado em um dispositivo de disco apoiado pela Memória de Classe de Armazenamento (armazenamento não volátil NVDIMM-N), também conhecido como buffer de log persistente. Para saber mais, confira [Aceleração de latência de Transação Confirmada usando Memória de Classe de Armazenamento](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/12/02/transaction-commit-latency-acceleration-using-storage-class-memory-in-windows-server-2016sql-server-2016-sp1/). **Aplica-se a**: [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] e posterior.

FOR ATTACH [ WITH \< attach_database_option > ] Especifica que o banco de dados é criado pela [anexação](../../relational-databases/databases/database-detach-and-attach-sql-server.md) de um conjunto existente de arquivos do sistema operacional. Deve haver uma entrada \<filespec> que especifica o arquivo primário. As únicas outras entradas \<filespec> necessárias são as de arquivos que têm um caminho diferente daquele de quando o banco de dados foi criado pela primeira vez ou anexado pela última vez. Uma entrada \<filespec> deve ser especificada para estes arquivos.

FOR ATTACH exige o seguinte:

- Todos os arquivos de dados (MDF e NDF) devem estar disponíveis.
- Se existirem vários arquivos de log, todos eles deverão estar disponíveis.

Se um banco de dados de leitura/gravação tiver um único arquivo de log que não esteja disponível no momento e se o banco de dados foi encerrado sem usuários ou transações abertas antes da operação de anexação, FOR ATTACH reconstruirá automaticamente o arquivo de log e atualizará o arquivo primário. Por outro lado, para um banco de dados somente leitura, o log não pode ser reconstruído porque o arquivo primário não pode ser atualizado. Portanto, ao anexar um banco de dados somente leitura com um log que não está disponível, você deve fornecer os arquivos de log ou os arquivos na cláusula FOR ATTACH.

> [!NOTE]
> Um banco de dados criado por uma versão mais recente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode ser anexado em versões anteriores.

No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], todos os arquivos de texto completo que fazem parte do banco de dados que está sendo anexado serão anexados com o banco de dados. Para especificar um novo caminho do catálogo de texto completo, especifique o novo local sem o nome do arquivo do sistema operacional de texto completo. Para obter mais informações, consulte a seção Exemplos.

A anexação de um banco de dados que contém uma opção de FILESTREAM "Nome de diretório", em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], solicitará que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verifique se o nome de Database_Directory é exclusivo. Se não for, a operação de anexação falhará com o erro "O nome do Database_Directory do FILESTREAM \<name> não é exclusivo nesta instância do SQL Server". Para evitar esse erro, o parâmetro opcional, *directory_name* deve ser passado para essa operação.

FOR ATTACH não pode ser especificado em um instantâneo do banco de dados.

FOR ATTACH pode especificar a opção de RESTRICTED_USER. RESTRICTED_USER permite que somente os membros da função de banco de dados fixa db_owner e das funções de servidor fixas dbcreator e sysadmin conectem-se ao banco de dados, mas não limita seu número. As tentativas de usuários não qualificados são recusadas.

Se o banco de dados usar [!INCLUDE[ssSB](../../includes/sssb-md.md)], use WITH \<service_broker_option> na cláusula FOR ATTACH:

\<service_broker_option> Controla a entrega da mensagem [!INCLUDE[ssSB](../../includes/sssb-md.md)] e o identificador [!INCLUDE[ssSB](../../includes/sssb-md.md)] para o banco de dados. As opções [!INCLUDE[ssSB](../../includes/sssb-md.md)] podem ser especificadas somente quando a cláusula FOR ATTACH é usada.

ENABLE_BROKER Especifica que o [!INCLUDE[ssSB](../../includes/sssb-md.md)] está habilitado para o banco de dados especificado. Ou seja, a entrega das mensagens é iniciada e is_broker_enabled é definido como verdadeiro na exibição do catálogo sys.databases. O banco de dados retém o identificador do [!INCLUDE[ssSB](../../includes/sssb-md.md)] existente.

NEW_BROKER Cria um valor de service_broker_guid no sys.databases e no banco de dados restaurado e encerra todos os pontos de extremidade de conversa com limpeza. O agente está habilitado, mas nenhuma mensagem é enviada aos pontos de extremidade de conversa remotos. Qualquer rota que referencia o antigo identificador do [!INCLUDE[ssSB](../../includes/sssb-md.md)] deve ser recriada novamente com o novo identificador.

ERROR_BROKER_CONVERSATIONS Encerra todas as conversas com um erro que declara que o banco de dados está anexado ou restaurado. O agente é desabilitado até que essa operação seja concluída e, em seguida, é habilitado. O banco de dados retém o identificador do [!INCLUDE[ssSB](../../includes/sssb-md.md)] existente.

Ao anexar um banco de dados replicado que tenha sido copiado, em vez de desanexado, considere o seguinte:

- Se você anexar o banco de dados à mesma instância e versão de servidor como banco de dados original, nenhuma etapa adicional será necessária.
- Se anexar o banco de dados à mesma instância de servidor, mas com uma versão atualizada, você deverá executar [sp_vupgrade_replication](../../relational-databases/system-stored-procedures/sp-vupgrade-replication-transact-sql.md) para atualizar a replicação depois que a operação de anexação tiver sido concluída.
- Se você anexar o banco de dados a uma instância de servidor diferente, independentemente da versão, deverá executar [sp_removedbreplication](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) para remover a replicação depois que a operação de anexação tiver sido concluída.

> [!NOTE]
> A anexação funciona com o formato de armazenamento **vardecimal**, mas o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] deve ser atualizado pelo menos para o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP2. Não é possível anexar um banco de dados que usa formato de armazenamento vardecimal a uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações sobre o formato de armazenamento **vardecimal**, veja [Compactação de dados](../../relational-databases/data-compression/data-compression.md).

Quando um banco de dados é anexado ou restaurado pela primeira vez a uma nova instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], uma cópia da chave mestra de banco de dados (criptografada pela chave mestra de serviço) ainda não está armazenada no servidor. É necessário usar a instrução **OPEN MASTER KEY** para descriptografar a DMK (chave mestra do banco de dados). Após a descriptografia da DMK, você tem a opção de habilitar a descriptografia automática no futuro usando a instrução **ALTER MASTER KEY REGENERATE** para provisionar o servidor com uma cópia da DMK criptografada com a SMK (chave mestra de serviço). Quando um banco de dados for atualizado de uma versão anterior, a DMK deverá ser regenerada para usar o algoritmo AES mais recente. Para obter mais informações sobre como regenerar a DMK, consulte [ALTER MASTER KEY](../../t-sql/statements/alter-master-key-transact-sql.md). O tempo necessário para regenerar a chave DMK para atualizar o AES depende do número de objetos protegidos pela DMK. É necessário regenerar a chave DMK para atualizar o AES somente uma vez, isso não tem impacto sobre regenerações futuras como parte de uma estratégia de rotação de chave. Para obter informações sobre como atualizar um banco de dados usando anexar, veja [Atualizar um banco de dados utilizando desanexar e anexar](../../relational-databases/databases/upgrade-a-database-using-detach-and-attach-transact-sql.md).

> [!IMPORTANT]
> É recomendável não anexar bancos de dados de origens desconhecidas ou não confiáveis. Esses bancos de dados podem conter um código mal-intencionado que pode executar um código [!INCLUDE[tsql](../../includes/tsql-md.md)] inesperado ou provocar erros modificando o esquema ou a estrutura física do banco de dados. Antes de usar um banco de dados de origem desconhecida ou não confiável, execute [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) no banco de dados em um servidor que não seja de produção, e também examine o código, como procedimentos armazenados ou outro código definido pelo usuário, no banco de dados.
> [!NOTE]
> As opções **TRUSTWORTHY** e **DB_CHAINING** não causam nenhum efeito quando um banco de dados é anexado.

FOR ATTACH_REBUILD_LOG Especifica que o banco de dados é criado pela anexação de um conjunto existente de arquivos do sistema operacional. Essa opção é limitada a bancos de dados de leitura/gravação. Deve haver uma entrada *\<filespec>* que especifique o arquivo primário. Se um ou mais arquivos de log de transações estiverem ausentes, o arquivo de log será reconstruído. O ATTACH_REBUILD_LOG cria automaticamente um novo arquivo de log de 1 MB. Esse arquivo é colocado no local padrão de arquivo de log. Para obter informações sobre esse local, veja [Exibir ou alterar os locais padrão de arquivos de log e dados – SSMS](../../database-engine/configure-windows/view-or-change-the-default-locations-for-data-and-log-files.md).

> [!NOTE]
> Se os arquivos de log estiverem disponíveis, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] usará esses arquivos em vez de reconstruir os arquivos de log.

FOR ATTACH_REBUILD_LOG exige o seguinte:

- Um desligamento correto do banco de dados.
- Todos os arquivos de dados (MDF e NDF) devem estar disponíveis.

> [!IMPORTANT]
> Essa operação interrompe a cadeia de backup de log. É recomendável que um backup completo do banco de dados seja executado após a conclusão da operação. Para obter mais informações, consulte [BACKUP](../../t-sql/statements/backup-transact-sql.md).

Normalmente, FOR ATTACH_REBUILD_LOG é usado quando você copia um banco de dados de leitura/gravação com um log grande em outro servidor onde a cópia será usada principalmente, ou apenas, para operações de leitura e, portanto, exige menos espaço de log do que o banco de dados original.

FOR ATTACH_REBUILD_LOG não pode ser especificado em um instantâneo do banco de dados.

Para obter mais informações sobre como anexar e desanexar bancos de dados, veja [Anexação e desanexação de banco de dados](../../relational-databases/databases/database-detach-and-attach-sql-server.md).

\<filespec> Controla as propriedades do arquivo.

NAME *logical_file_name* Especifica o nome lógico do arquivo. NAME é exigido quando FILENAME está especificado, exceto ao especificar uma das cláusulas FOR ATTACH. Um grupo de arquivos FILESTREAM não pode ser denominado PRIMARY.

*logical_file_name* É o nome lógico usado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao fazer referência ao arquivo. *Logical_file_name* deve ser exclusivo no banco de dados e estar de acordo com a regras de [identificadores](../../relational-databases/databases/database-identifiers.md). O nome pode ser um caractere ou constante Unicode ou um identificador normal ou delimitado.

FILENAME { **'** _os\_file\_name_ **'** | **'** _filestream\_path_ **'** } Especifica o nome de arquivo (físico) do sistema operacional.

**'** *os_file_name* **'** É o caminho e o nome do arquivo usados pelo sistema operacional quando o arquivo é criado. O arquivo deve residir em um dos seguintes dispositivos: o servidor local no qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está instalado, uma rede de área de armazenamento [SAN] ou em uma rede baseada em iSCSI. O caminho especificado deve existir antes da execução da instrução CREATE DATABASE. Para obter mais informações, consulte "Arquivos de grupos de arquivos do banco de dados" na seção Comentários.

Os parâmetros SIZE, MAXSIZE e FILEGROWTH podem ser definidos quando um caminho UNC está especificado para o arquivo.

Se o arquivo estiver em uma partição bruta, *os_file_name* deverá especificar apenas a letra da unidade de uma partição bruta existente. Apenas um arquivo de dados pode ser criado em cada partição bruta.

Arquivos de dados não devem ser colocados em sistemas de arquivos compactados a não ser que os arquivos sejam secundários e somente leitura ou que o banco de dados seja somente leitura. Arquivos de log nunca devem ser colocados em sistemas de arquivos compactados.

**'** *filestream_path* **'** Para um grupo de arquivos FILESTREAM, FILENAME faz referência a um caminho em que os dados FILESTREAM serão armazenados. O caminho até a última pasta deve existir e a última pasta não deve existir. Por exemplo, se você especificar o caminho C:\MyFiles\MyFilestreamData, C:\MyFiles deve existir antes da execução de ALTER DATABASE, mas a pasta MyFilestreamData não deve existir.

O grupo de arquivos e o arquivo (`<filespec>`) devem ser criados na mesma instrução.

As propriedades SIZE e FILEGROWTH não se aplicam a um grupo de arquivos FILESTREAM.

SIZE *size* Especifica o tamanho do arquivo.

SIZE não pode ser especificado quando o *os_file_name* for especificado como um caminho UNC. SIZE não se aplica a um grupo de arquivos FILESTREAM.

*size* É o tamanho inicial do arquivo.

Quando o *tamanho* do arquivo primário não é informado, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] usa o tamanho do arquivo primário no modelo de banco de dados. O tamanho padrão do modelo é de 8 MB (começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]) ou 1 MB (para versões anteriores). Quando um arquivo de dados secundário ou um arquivo de log for especificado, mas o *tamanho* não for especificado para o arquivo, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] fará com que o arquivo ter 8 MB (começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]) ou 1 MB (para versões anteriores). O tamanho especificado para o arquivo primário deve ser, no mínimo, tão grande quanto o arquivo primário do banco de dados modelo.

Os sufixos KB (quilobyte), MB (megabyte), GB (gigabyte) ou TB (terabyte) podem ser usados. O padrão é MB. Especifique um número inteiro; não inclua um decimal. *Size* é um valor inteiro. Para valores maiores que 2147483647, use unidades maiores.

MAXSIZE *max_size* Especifica o tamanho máximo até o qual o arquivo pode crescer. MAXSIZE não pode ser especificado quando o *os_file_name* for especificado como um caminho UNC.

*max_size* É o tamanho de arquivo máximo. Os sufixos KB, MB, GB e TB podem ser usados. O padrão é MB. Especifique um número inteiro; não inclua um decimal. Se um *max_size* não for especificado, o arquivo aumentará até que o disco esteja cheio. *Max_size* é um valor inteiro. Para valores maiores que 2147483647, use unidades maiores.

UNLIMITED Especifica que o arquivo crescerá até que o disco esteja cheio. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um arquivo de log especificado com crescimento ilimitado tem um tamanho máximo de 2 TB, e um arquivo de dados tem um tamanho máximo de 16 TB.

> [!NOTE]
> Não há nenhum tamanho máximo quando essa opção é especificada para um contêiner FILESTREAM. Ele continua crescendo até que o disco esteja cheio.

FILEGROWTH *growth_increment* Especifica o incremento de crescimento automático do arquivo. A configuração de FILEGROWTH de um arquivo não pode exceder a configuração de MAXSIZE. FILEGROWTH não pode ser especificado quando o *os_file_name* é especificado como um caminho UNC. FILEGROWTH não se aplica a um grupo de arquivos FILESTREAM.

*growth_increment* É a quantidade de espaço adicionada ao arquivo sempre que novo espaço é necessário.

O valor pode ser especificado em MB, KB, GB, TB ou porcentagem (%). Se um número for especificado sem um sufixo MB, KB, ou %, o padrão será MB. Quando % está especificada, o tamanho do incremento de crescimento é a porcentagem especificada do tamanho do arquivo no momento em que ocorre o incremento. O tamanho especificado é arredondado para os 64 KB mais próximos e o valor mínimo é de 64 KB.

Um valor 0 indica que o crescimento automático está desativado e nenhum espaço adicional é permitido.

Se FILEGROWTH não é especificado, os valores padrão são:

|Versão|Valores padrão|
|-------------|--------------------|
|Iniciando o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|Dados 64 MB. Arquivos de log 64 MB.|
|Iniciando o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|Dados 1 MB. Arquivos de log 10%.|
|Antes do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|Dados 10%. Arquivos de log 10%.|

\<filegroup> Controla as propriedades do grupo de arquivos. O grupo de arquivos não pode ser especificado em um instantâneo do banco de dados.

FILEGROUP *filegroup_name* É o nome lógico do grupo de arquivos.

*filegroup_name*
*filegroup_name* deve ser exclusivo no banco de dados e não pode ser os nomes PRIMARY e PRIMARY_LOG fornecidos pelo sistema. O nome pode ser um caractere ou constante Unicode ou um identificador normal ou delimitado. O nome deve estar de acordo com as regras de [identificadores](../../relational-databases/databases/database-identifiers.md).

CONTAINS FILESTREAM Especifica que o grupo de arquivos armazena BLOBs (objetos binários grandes) FILESTREAM no sistema de arquivos.

CONTAINS MEMORY_OPTIMIZED_DATA

**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior

Especifica que o grupo de arquivos armazena dados memory_optimized no sistema de arquivos. Para obter mais informações, veja [OLTP In-Memory – Otimização In-Memory](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md). Apenas um grupo de arquivos MEMORY_OPTIMIZED_DATA é permitido por banco de dados. Para obter exemplos de códigos que criam um grupo de arquivos para armazenar dados com otimização de memória, veja [Criando uma tabela com otimização de memória e um procedimento armazenado compilado nativamente](../../relational-databases/in-memory-oltp/creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md).

DEFAULT Especifica que o grupo de arquivos nomeado é o grupo de arquivos padrão no banco de dados.

*database_snapshot_name* É o nome do instantâneo de banco de dados. Nomes de instantâneos de bancos de dados devem ser exclusivos dentro de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e estar de acordo com as regras de identificadores. *database_snapshot_name* pode ter no máximo 128 caracteres.

ON **(** NAME **=** _logical\_file\_name_ **,** FILENAME **='** _os\_file\_name_ **')** [ **,** ... *n* ] Na criação de um instantâneo do banco de dados, especifica uma lista de arquivos no banco de dados de origem. Para que o instantâneo funcione, todos os arquivos de dados devem ser especificados individualmente. No entanto, arquivos de log não são permitidos para instantâneos do banco de dados. Os grupos de arquivos FILESTREAM não são suportados pelos instantâneos do banco de dados. Se um arquivo de dados FILESTREAM for incluído em uma cláusula CREATE DATABASE ON, a instrução falhará e um erro será gerado.

Para obter descrições de NAME e FILENAME e seus valores, confira as descrições dos valores \<filespec> equivalentes.

> [!NOTE]
> Quando você cria um instantâneo do banco de dados, as outras opções \<filespec> e a palavra-chave PRIMARY não são permitidas.

AS SNAPSHOT OF *source_database_name* Especifica que o banco de dados que está sendo criado é um instantâneo de banco de dados do banco de dados de origem especificado por *source_database_name*. O instantâneo e o banco de dados de origem devem estar na mesma instância.

Para saber mais, confira [Instantâneos do banco de dados](#database-snapshots) na seção Comentários.

## <a name="remarks"></a>Comentários

O backup do [banco de dados mestre](../../relational-databases/databases/master-database.md) deve ser feito sempre que um banco de dados de usuário é criado, modificado ou descartado.

A instrução `CREATE DATABASE` deve ser executada em modo de confirmação automática (o modo padrão de gerenciamento de transações) e não deve ser permitida em uma transação explícita ou implícita.

É possível usar uma instrução `CREATE DATABASE` para criar um banco de dados e os arquivos que armazenam o banco de dados. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] implementa a instrução CREATE DATABASE usando as seguintes etapas:

1. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa uma cópia do [modelo de banco de dados](../../relational-databases/databases/model-database.md) para inicializar o banco de dados e seu metadados.
2. Um GUID do agente de serviço é atribuído ao banco de dados.
3. Em seguida, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] preenche o restante do banco de dados com páginas vazias, exceto as páginas que têm dados internos que registram como o espaço é usado no banco de dados.

No máximo 32.767 bancos de dados podem ser especificados em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

Cada banco de dados tem um proprietário que pode executar atividades especiais no banco de dados. O proprietário é o usuário que cria o banco de dados. O proprietário do banco de dados pode ser alterado usando [ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md).

Alguns recursos de banco de dados dependem de recursos ou capacidades presentes no sistema de arquivos para a funcionalidade completa de um banco de dados. Alguns exemplos de recursos que dependem do conjunto de recursos de sistema de arquivos incluem:

- DBCC CHECKDB
- FileStream
- Backups online usando instantâneos de arquivo e VSS
- Criação de instantâneo do banco de dados
- Grupo de arquivos de dados com otimização de memória

## <a name="database-files-and-filegroups"></a>Arquivos e grupos de arquivos do banco de dados

Cada banco de dados tem no mínimo dois arquivos, um *arquivo primário* e um *arquivo de log de transações* e pelo menos um grupo de arquivos. Um máximo de 32.767 arquivos e 32.767 grupos de arquivos pode ser especificado para cada banco de dados.

Ao criar um banco de dados, torne os arquivos de dados tão grandes quanto possível, com base na quantidade máxima de dados que você espera ter no banco de dados.

É recomendável usar uma rede SAN, uma rede baseada em iSCSI ou um disco conectado localmente para o armazenamento dos arquivos de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], pois essa configuração otimiza o desempenho e a confiabilidade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

## <a name="database-snapshots"></a>Instantâneos do banco de dados

É possível usar a instrução `CREATE DATABASE` para criar uma exibição estática somente leitura, um *instantâneo do banco de dados* do *banco de dados de origem*. Um instantâneo do banco de dados é transacionalmente consistente com o banco de dados de origem pois existia no momento da criação do banco de dados. Um banco de dados de origem pode ter vários instantâneos.

> [!NOTE]
> Quando você cria um instantâneo do banco de dados, a instrução `CREATE DATABASE` não pode fazer referência a arquivos de log, arquivos offline, arquivos de restauração e arquivos extintos.

Se a criação de um instantâneo do banco de dados falhar, o instantâneo se tornará suspeito e deverá ser excluído. Para obter mais informações, veja [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md).

Cada instantâneo persiste até que seja excluído usando `DROP DATABASE`.

Para obter mais informações, consulte [Instantâneos de banco de dados](../../relational-databases/databases/database-snapshots-sql-server.md).

## <a name="database-options"></a>Opções de banco de dados

Várias opções de banco de dados são automaticamente definidas sempre que você cria um banco de dados. Para obter uma lista dessas opções, veja [Opções ALTER DATABASE SET](../../t-sql/statements/alter-database-transact-sql-set-options.md).

## <a name="the-model-database-and-creating-new-databases"></a>Banco de dados modelo e criação de novos bancos de dados

Todos os objetos definidos pelo usuário no [modelo de banco de dados](../../relational-databases/databases/model-database.md) são copiados para todos os bancos de dados recém-criados. É possível adicionar quaisquer objetos, como tabelas, exibições, procedimentos armazenados, tipos de dados, etc. ao banco de dados modelo para que sejam incluídos em todos os bancos de dados recém-criados.

Quando uma instrução `CREATE DATABASE <database_name>` é especificada sem parâmetros adicionais de tamanho, o arquivo de dados primário se torna do mesmo tamanho que o arquivo primário no modelo de banco de dados.

A não ser que `FOR ATTACH` seja especificado, cada novo banco de dados herda as configurações de opções do modelo de banco de dados. Por exemplo, a opção de reduzir automaticamente do banco de dados é definida como **true** no banco de dados modelo e em todos os novos bancos de dados criados. Se você alterar as opções no banco de dados modelo, essas novas configurações de opções serão usadas em todos os novos bancos de dados criados. A alteração das operações no banco de dados modelo não afeta bancos de dados existentes. Se FOR ATTACH estiver especificado na instrução CREATE DATABASE, o novo banco de dados herdará as configurações de opções do banco de dados original.

## <a name="viewing-database-information"></a>Exibindo informações do banco de dados

É possível usar exibições do catálogo, funções do sistema e procedimentos armazenados do sistema para retornar informações sobre bancos de dados, arquivos e grupos de arquivos. Para obter mais informações, veja [Exibições do sistema](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90).

## <a name="permissions"></a>Permissões

Requer permissão `CREATE DATABASE`, `CREATE ANY DATABASE` ou `ALTER ANY DATABASE`.

Para manter controle sobre o uso do disco em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a permissão para criar bancos de dados geralmente é limitada a algumas contas de logon.

O exemplo a seguir fornece a permissão para criar um banco de dados para o usuário Fay de banco de dados.

```sql
USE master;
GO
GRANT CREATE DATABASE TO [Fay];
GO
```

### <a name="permissions-on-data-and-log-files"></a>Permissões em arquivos de dados e de log

Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], determinadas permissões são definidas nos arquivos de dados e de log de cada banco de dados. As permissões a seguir são definidas sempre que as seguintes operações são aplicadas a um banco de dados:

- Anexado
- Incluído em backup
- Criado
- Desanexado
- Modificado para adicionar um novo arquivo
- Restaurado

As permissões evitam que os arquivos sejam violados acidentalmente caso residam em um diretório com permissões abertas.

> [!NOTE]
> O [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)] não define dados e permissões de arquivos de log.

## <a name="examples"></a>Exemplos

### <a name="a-creating-a-database-without-specifying-files"></a>a. Criando um banco de dados sem especificar arquivos

O exemplo a seguir cria o banco de dados `mytest` e os arquivos primário e de log de transações correspondentes. Como a instrução não tem nenhum item \<filespec>, o arquivo de banco de dados primário é do tamanho do arquivo primário do modelo de banco de dados. O log de transações é definido como o maior destes valores: 512 KB ou 25% do tamanho do arquivo de dados primário. Como MAXSIZE não é especificado, os arquivos podem crescer até encher todo o espaço em disco disponível. Este exemplo de também demonstra como descartar um banco de dados denominado `mytest`, se ele existir, antes da criação do banco de dados `mytest`.

```sql
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

O exemplo a seguir cria o banco de dados `Sales`. Como a palavra-chave PRIMARY não é usada, o primeiro arquivo (`Sales_dat`) torna-se o arquivo primário. Como nem MB nem KB é especificado no parâmetro SIZE do arquivo `Sales_dat` , ele usa MB e é alocado em megabytes. O backup do banco de dados `Sales_log` é alocado em megabytes porque o sufixo `MB` é explicitamente declarado no parâmetro `SIZE` .

```sql
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

```sql
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

- O grupo de arquivos primário com os arquivos `Spri1_dat` e `Spri2_dat`. Os incrementos de FILEGROWTH desses arquivos são especificados como `15%`.
- Um grupo de arquivos denominado `SalesGroup1` com os arquivos `SGrp1Fi1` e `SGrp1Fi2`.
- Um grupo de arquivos denominado `SalesGroup2` com os arquivos `SGrp2Fi1` e `SGrp2Fi2`.

Este exemplo coloca os dados e os arquivos de log em discos diferentes para melhorar o desempenho.

```sql
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

```sql
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

O exemplo a seguir cria o instantâneo do banco de dados `sales_snapshot0600`. Como um instantâneo do banco de dados é somente leitura, um arquivo de log não pode ser especificado. Em conformidade com a sintaxe, todo arquivo do banco de dados de origem é especificado e grupos de arquivos não são especificados.

O banco de dados de origem deste exemplo é o banco de dados `Sales` criado no exemplo D.

```sql
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

### <a name="g-creating-a-database-and-specifying-a-collation-name-and-options"></a>G. Criando um banco de dados e especificando um nome e opções de ordenação

O exemplo a seguir cria o banco de dados `MyOptionsTest`. Um nome de ordenação é especificado e as opções `TRUSTYWORTHY` e `DB_CHAINING` são definidas como `ON`.

```sql
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

```sql
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

- `FileStreamDB_data` contém dados de linha. Ele contém um arquivo, `FileStreamDB_data.mdf` com o caminho padrão.
- `FileStreamPhotos` contém dados FILESTREAM. Ele contém dois contêineres de dados FILESTREAM, `FSPhotos`, localizado em `C:\MyFSfolder\Photos` e `FSPhotos2`, localizado em `D:\MyFSfolder\Photos`. É marcado como o grupo de arquivos FILESTREAM padrão.
- `FileStreamResumes` contém dados FILESTREAM. Ele contém um contêiner de dados FILESTREAM, `FSResumes`, localizado em `C:\MyFSfolder\Resumes`.

```sql
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

```sql
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

## <a name="see-also"></a>Consulte Também

- [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md)
- [Anexar e desanexar bancos de dados](../../relational-databases/databases/database-detach-and-attach-sql-server.md)
- [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)
- [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)
- [ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md)
- [sp_detach_db](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)
- [sp_removedbreplication](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)
- [Instantâneos do banco de dados](../../relational-databases/databases/database-snapshots-sql-server.md)
- [Mover arquivos de banco de dados](../../relational-databases/databases/move-database-files.md)
- [Bancos de dados](../../relational-databases/databases/databases.md)
- [Objeto binário grande – dados de blob](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)

::: moniker-end
::: moniker range="=azuresqldb-current||=sqlallproducts-allversions"

:::row:::
    :::column:::
        [SQL Server](create-database-transact-sql.md?view=sql-server-2017)
    :::column-end:::
    :::column:::
        **_\* Banco de Dados SQL \*_**
    :::column-end:::
    :::column:::
        [Banco de Dados SQL<br />Instância Gerenciada](create-database-transact-sql.md?view=azuresqldb-mi-current)
    :::column-end:::
    :::column:::
        [Azure Synapse<br />Analytics](create-database-transact-sql.md?view=azure-sqldw-latest)
    :::column-end:::
    :::column:::
        [Analytics Platform<br />System (PDW)](create-database-transact-sql.md?view=aps-pdw-2016)
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="sql-database"></a>Banco de Dados SQL

## <a name="overview"></a>Visão geral

No [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], essa instrução pode ser usada com um SQL Server do Azure para criar um banco de dados individual ou um banco de dados em um pool elástico. Com esta instrução, você especifica o nome do banco de dados, a ordenação, o tamanho máximo, a edição e o objetivo de serviço e, se aplicável, o pool elástico para o novo banco de dados. Também pode ser usado para criar o banco de dados em um pool elástico. Além disso, ele pode ser usado para criar uma cópia do banco de dados em outro servidor de Banco de Dados SQL.

## <a name="syntax"></a>Sintaxe

### <a name="create-a-database"></a>Criar um banco de dados

```syntaxsql
CREATE DATABASE database_name [ COLLATE collation_name ]
{
  (<edition_options> [, ...n])
}
[ WITH CATALOG_COLLATION = { DATABASE_DEFAULT | SQL_Latin1_General_CP1_CI_AS }]
[;]

<edition_options> ::=
{

  MAXSIZE = { 100 MB | 250 MB | 500 MB | 1 ... 1024 ... 4096 GB }
  | ( EDITION = { 'Basic' | 'Standard' | 'Premium' | 'GeneralPurpose' | 'BusinessCritical' | 'Hyperscale' }
  | SERVICE_OBJECTIVE =
    { 'Basic' | 'S0' | 'S1' | 'S2' | 'S3' | 'S4'| 'S6'| 'S7'| 'S9'| 'S12'
      | 'P1' | 'P2' | 'P4'| 'P6' | 'P11' | 'P15'
      | 'GP_Gen4_1' | 'GP_Gen4_2' | 'GP_Gen4_3' | 'GP_Gen4_4' | 'GP_Gen4_5' | 'GP_Gen4_6'
      | 'GP_Gen4_7' | 'GP_Gen4_8' | 'GP_Gen4_9' | 'GP_Gen4_10' | 'GP_Gen4_16' | 'GP_Gen4_24'
      | 'GP_Gen5_2' | 'GP_Gen5_4' | 'GP_Gen5_6' | 'GP_Gen5_8' | 'GP_Gen5_10' | 'GP_Gen5_12' | 'GP_Gen5_14'
      | 'GP_Gen5_16' | 'GP_Gen5_18' | 'GP_Gen5_20' | 'GP_Gen5_24' | 'GP_Gen5_32' | 'GP_Gen5_40' | 'GP_Gen5_80'
      | 'GP_Fsv2_8' | 'GP_Fsv2_10' | 'GP_Fsv2_12' | 'GP_Fsv2_14' | 'GP_Fsv2_16' | 'GP_Fsv2_18'
      | 'GP_Fsv2_20' | 'GP_Fsv2_24' | 'GP_Fsv2_32' | 'GP_Fsv2_36' | 'GP_Fsv2_72'
      | 'GP_S_Gen5_1' | 'GP_S_Gen5_2' | 'GP_S_Gen5_4' | 'GP_S_Gen5_6' | 'GP_S_Gen5_8'
      | 'GP_S_Gen5_10' | 'GP_S_Gen5_12' | 'GP_S_Gen5_14' | 'GP_S_Gen5_16'
      | 'GP_S_Gen5_18' | 'GP_S_Gen5_20' | 'GP_S_Gen5_24' | 'GP_S_Gen5_32' | 'GP_S_Gen5_40'
      | 'BC_Gen4_1' | 'BC_Gen4_2' | 'BC_Gen4_3' | 'BC_Gen4_4' | 'BC_Gen4_5' | 'BC_Gen4_6'
      | 'BC_Gen4_7' | 'BC_Gen4_8' | 'BC_Gen4_9' | 'BC_Gen4_10' | 'BC_Gen4_16' | 'BC_Gen4_24'
      | 'BC_Gen5_2' | 'BC_Gen5_4' | 'BC_Gen5_6' | 'BC_Gen5_8' | 'BC_Gen5_10' | 'BC_Gen5_12' | 'BC_Gen5_14'
      | 'BC_Gen5_16' | 'BC_Gen5_18' | 'BC_Gen5_20' | 'BC_Gen5_24' | 'BC_Gen5_32' | 'BC_Gen5_40' | 'BC_Gen5_80'
      | 'BC_M_8' | 'BC_M_10' | 'BC_M_12' | 'BC_M_14' | 'BC_M_16' | 'BC_M_18'
      | 'BC_M_20' | 'BC_M_24' | 'BC_M_32' | 'BC_M_64' | 'BC_M_128'
      | 'HS_GEN4_1' | 'HS_GEN4_2' | 'HS_GEN4_4' | 'HS_GEN4_8' | 'HS_GEN4_16' | 'HS_GEN4_24'
      | 'HS_GEN5_2' | 'HS_GEN5_4' | 'HS_GEN5_8' | 'HS_GEN5_16' | 'HS_GEN5_24' | 'HS_GEN5_32' | 'HS_GEN5_48' | 'HS_GEN5_80'
      | { ELASTIC_POOL(name = <elastic_pool_name>) } })
}
```

### <a name="copy-a-database"></a>Copiar um banco de dados

```syntaxsql
CREATE DATABASE database_name
    AS COPY OF [source_server_name.] source_database_name
    [ ( SERVICE_OBJECTIVE =
      { 'Basic' |'S0' | 'S1' | 'S2' | 'S3'| 'S4'| 'S6'| 'S7'| 'S9'| 'S12'
      | 'P1' | 'P2' | 'P4'| 'P6' | 'P11' | 'P15'
      | 'GP_Gen4_1' | 'GP_Gen4_2' | 'GP_Gen4_3' | 'GP_Gen4_4' | 'GP_Gen4_5' | 'GP_Gen4_6'
      | 'GP_Gen4_7' | 'GP_Gen4_8' | 'GP_Gen4_9' | 'GP_Gen4_10' | 'GP_Gen4_16' | 'GP_Gen4_24'
      | 'GP_Gen5_2' | 'GP_Gen5_4' | 'GP_Gen5_6' | 'GP_Gen5_8' | 'GP_Gen5_10' | 'GP_Gen5_12' | 'GP_Gen5_14'
      | 'GP_Gen5_16' | 'GP_Gen5_18' | 'GP_Gen5_20' | 'GP_Gen5_24' | 'GP_Gen5_32' | 'GP_Gen5_40' | 'GP_Gen5_80'
      | 'GP_Fsv2_8' | 'GP_Fsv2_10' | 'GP_Fsv2_12' | 'GP_Fsv2_14' | 'GP_Fsv2_16' | 'GP_Fsv2_18'
      | 'GP_Fsv2_20' | 'GP_Fsv2_24' | 'GP_Fsv2_32' | 'GP_Fsv2_36' | 'GP_Fsv2_72'
      | 'GP_S_Gen5_1' | 'GP_S_Gen5_2' | 'GP_S_Gen5_4' | 'GP_S_Gen5_6' | 'GP_S_Gen5_8'
      | 'GP_S_Gen5_10' | 'GP_S_Gen5_12' | 'GP_S_Gen5_14' | 'GP_S_Gen5_16'
      | 'GP_S_Gen5_18' | 'GP_S_Gen5_20' | 'GP_S_Gen5_24' | 'GP_S_Gen5_32' | 'GP_S_Gen5_40'
      | 'BC_Gen4_1' | 'BC_Gen4_2' | 'BC_Gen4_3' | 'BC_Gen4_4' | 'BC_Gen4_5' | 'BC_Gen4_6'
      | 'BC_Gen4_7' | 'BC_Gen4_8' | 'BC_Gen4_9' | 'BC_Gen4_10' | 'BC_Gen4_16' | 'BC_Gen4_24'
      | 'BC_Gen5_2' | 'BC_Gen5_4' | 'BC_Gen5_6' | 'BC_Gen5_8' | 'BC_Gen5_10' | 'BC_Gen5_12' | 'BC_Gen5_14'
      | 'BC_Gen5_16' | 'BC_Gen5_18' | 'BC_Gen5_20' | 'BC_Gen5_24' | 'BC_Gen5_32' | 'BC_Gen5_40' | 'BC_Gen5_80'
      | 'BC_M_8' | 'BC_M_10' | 'BC_M_12' | 'BC_M_14' | 'BC_M_16' | 'BC_M_18'
      | 'BC_M_20' | 'BC_M_24' | 'BC_M_32' | 'BC_M_64' | 'BC_M_128'
      | 'HS_GEN4_1' | 'HS_GEN4_2' | 'HS_GEN4_4' | 'HS_GEN4_8' | 'HS_GEN4_16' | 'HS_GEN4_24'
      | 'HS_GEN5_2' | 'HS_GEN5_4' | 'HS_GEN5_8' | 'HS_GEN5_16' | 'HS_GEN5_24' | 'HS_GEN5_32' | 'HS_GEN5_48' | 'HS_GEN5_80'
      | { ELASTIC_POOL(name = <elastic_pool_name>) } })
   ]
[;]
```

## <a name="arguments"></a>Argumentos

*database_name* O nome do novo banco de dados. Este nome deve ser exclusivo no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e deve estar de acordo com a regras do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para identificadores. Para obter mais informações, consulte [Identificadores](https://go.microsoft.com/fwlink/p/?LinkId=180386).

*Collation_name* Especifica a ordenação padrão do banco de dados. O nome da ordenação pode ser um nome de ordenação do Windows ou um nome de ordenação SQL. Se não for especificado, o banco de dados receberá a ordenação padrão, que é SQL_Latin1_General_CP1_CI_AS.

Para obter mais informações sobre nomes de ordenações do Windows e SQL, [COLLATE (Transact-SQL)](../../t-sql/statements/collations.md).

CATALOG_COLLATION Especifica a ordenação padrão do catálogo de metadados. *DATABASE_DEFAULT* especifica que o catálogo de metadados usado para exibições do sistema e tabelas do sistema seja agrupado para corresponder à ordenação padrão do banco de dados. Esse é o comportamento encontrado no SQL Server.

*SQL_Latin1_General_CP1_CI_AS* especifica que o catálogo de metadados usado para exibições do sistema e tabelas seja agrupado em uma ordenação SQL_Latin1_General_CP1_CI_AS fixo. Essa será a configuração padrão no Banco de Dados SQL do Azure, se não for especificado.

EDITION Especifica a camada de serviço do banco de dados.

Bancos de dados individuais e em pool. Os valores disponíveis são: "Básico", "Standard", "Premium","GeneralPurpose", "BusinessCritical" e "Hiperescala".

MAXSIZE Especifica o tamanho máximo do banco de dados. MAXSIZE deve ser válido para a EDIÇÃO especificada (camada de serviço) A seguir, estão os valores com suporte para MAXSIZE e os padrões (D) para as camadas de serviço.

> [!NOTE]
> O argumento **MAXSIZE** não é aplicável a bancos de dados individuais na camada de serviço em hiperescala. Os bancos de dados da camada em hiperescala crescem conforme necessário até 100 TB. O serviço de Banco de Dados SQL adiciona armazenamento automaticamente – não é necessário definir um tamanho máximo.

**Modelo de DTU para bancos de dados individuais e em pool em um servidor do banco de dados SQL**

|**MAXSIZE**|**Basic**|**S0-S2**|**S3-S12**|**P1-P6**| **P11-P15** |
|:---|:---|:---|:---|:---|:---|
|100 MB|√|√|√|√|√|
|250 MB|√|√|√|√|√|
|500 MB|√|√|√|√|√|
|1 GB|√|√|√|√|√|
|2 GB|√ (D)|√|√|√|√|
|5 GB|N/D|√|√|√|√|
|10 GB|N/D|√|√|√|√|
|20 GB|N/D|√|√|√|√|
|30 GB|N/D|√|√|√|√|
|40 GB|N/D|√|√|√|√|
|50 GB|N/D|√|√|√|√|
|100 GB|N/D|√|√|√|√|
|150 GB|N/D|√|√|√|√|
|200 GB|N/D|√|√|√|√|
|250 GB|N/D|√ (D)|√ (D)|√|√|
|300 GB|N/D|N/D|√|√|√|
|400 GB|N/D|N/D|√|√|√|
|500 GB|N/D|N/D|√|√ (D)|√|
|750 GB|N/D|N/D|√|√|√|
|1024 GB|N/D|N/D|√|√|√ (D)|
|De 1024 GB até 4096 GB em incrementos de 256 GB* |N/D|N/D|N/D|N/D|√|√|

\* P11 e P15 permitem MAXSIZE até 4 TB com 1024 GB sendo o tamanho padrão. P11 e P15 podem usar até 4 TB de armazenamento incluído sem custos adicionais. Na camada Premium, um MAXSIZE maior que 1 TB está atualmente disponível nas seguintes regiões: Leste dos EUA 2, Oeste dos EUA, US Gov – Virgínia, Europa Ocidental, Região Central da Alemanha, Sudeste da Ásia, Leste do Japão, Leste da Austrália, Região Central do Canadá e Leste do Canadá. Para obter detalhes adicionais sobre limitações de recursos para o modelo de DTU, veja [Limites de recurso de DTU](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits).

O valor MAXSIZE do modelo de DTU, se especificado, deve ser um valor válido exibido na tabela acima para a camada de serviço especificada.

**modelo vCore**

**Uso Geral – computação provisionada – Gen4 (parte 1)**

|MAXSIZE|GP_Gen4_1|GP_Gen4_2|GP_Gen4_3|GP_Gen4_4|GP_Gen4_5|GP_Gen4_6|
|:----- | ------: |-------: |-------: |-------: |-------: |--------:|
|Tamanho máximo de dados (GB)|1024|1024|1024|1536|1536|1536|

**Uso Geral – computação provisionada – Gen4 (parte 2)**

|MAXSIZE|GP_Gen4_7|GP_Gen4_8|GP_Gen4_9|GP_Gen4_10|GP_Gen4_16|GP_Gen4_24
|:----- | ------: |-------: |-------: |-------: |-------: |--------:|
|Tamanho máximo de dados (GB)|1536|3072|3072|3072|4096|4096|

**Uso Geral – computação provisionada – Gen5 (parte 1)**

|MAXSIZE|GP_Gen5_2|GP_Gen5_4|GP_Gen5_6|GP_Gen5_8|GP_Gen5_10|GP_Gen5_12|GP_Gen5_14|
|:----- | ------: |-------: |-------: |-------: |--------: |---------:|--------: |
|Tamanho máximo de dados (GB)|1024|1024|1024|1536|1536|1536|1536|

**Uso Geral – computação provisionada – Gen5 (parte 2)**

|MAXSIZE|GP_Gen5_16|GP_Gen5_18|GP_Gen5_20|GP_Gen5_24|GP_Gen5_32|GP_Gen5_40|GP_Gen5_80|
|:----- | ------: |-------: |-------: |-------: |--------: |---------:|--------: |
|Tamanho máximo de dados (GB)|3072|3072|3072|4096|4096|4096|4096|

**Uso Geral – computação provisionada – série Fsv2 (parte 1)**

|MAXSIZE|GP_Fsv2_8|GP_Fsv2_10|GP_Fsv2_12|GP_Fsv2_14|GP_Fsv2_16|GP_Fsv2_18|
|:----- | ------: | ------: | ------: | ------: | ------: | ------: |
|Tamanho máximo de dados (GB)|1024|1024|1024|1024|1536|1536|

**Uso Geral – computação provisionada – série Fsv2 (parte 2)**

|MAXSIZE|GP_Fsv2_20|GP_Fsv2_24|GP_Fsv2_32|GP_Fsv2_36|GP_Fsv2_72|
|:----- | ------: | ------: | ------: | ------: | ------: |
|Tamanho máximo de dados (GB)|1536|1536|3072|3072|4096|

**Uso Geral – computação sem servidor – Gen5 (parte 1)**

|MAXSIZE|GP_S_Gen5_1|GP_S_Gen5_2|GP_S_Gen5_4|GP_S_Gen5_6|GP_S_Gen5_8|
|:----- | ------: |-------: |-------: |-------: |--------: |
|Máximo de vCores|1|2|4|6|8|

**Uso Geral – computação sem servidor – Gen5 (parte 2)**

|MAXSIZE|GP_S_Gen5_10|GP_S_Gen5_12|GP_S_Gen5_14|GP_S_Gen5_16|
|:----- | ------: |-------: |-------: |-------: |
|Máximo de vCores|10|12|14|16|

**Uso Geral – computação sem servidor – Gen5 (parte 3)**

|MAXSIZE|GP_S_Gen5_18|GP_S_Gen5_20|GP_S_Gen5_24|GP_S_Gen5_32|GP_S_Gen5_40|
|:----- | ------: |-------: |-------: |-------: |--------: |
|Máximo de vCores|18|20|24|32|40|

**Comercialmente Crítico – computação provisionada – Gen4 (parte 1)**

|Tamanho da computação (objetivo do serviço)|BC_Gen4_1|BC_Gen4_2|BC_Gen4_3|BC_Gen4_4|BC_Gen4_5|BC_Gen4_6|
|:--------------- | ------: |-------: |-------: |-------: |-------: |-------: |
|Tamanho máximo de dados (GB)|1024|1024|1024|1024|1024|1024|

**Comercialmente Crítico – computação provisionada – Gen4 (parte 2)**

|Tamanho da computação (objetivo do serviço)|BC_Gen4_7|BC_Gen4_8|BC_Gen4_9|BC_Gen4_10|BC_Gen4_16|BC_Gen4_24|
|:--------------- | ------: |-------: |-------: |--------: |--------: |--------: |
|Tamanho máximo de dados (GB)|1024|1024|1024|1024|1024|1024|

**Comercialmente Crítico – computação provisionada – Gen5 (parte 1)**

|MAXSIZE|BC_Gen5_2|BC_Gen5_4|BC_Gen5_6|BC_Gen5_8|BC_Gen5_10|BC_Gen5_12|BC_Gen5_14|
|:----- | ------: |-------: |-------: |-------: |---------: |--------:|--------: |
|Tamanho máximo de dados (GB)|1024|1024|1024|1536|1536|1536|1536|

**Comercialmente Crítico – computação provisionada – Gen5 (parte 2)**

|MAXSIZE|BC_Gen5_16|BC_Gen5_18|BC_Gen5_20|BC_Gen5_24|BC_Gen5_32|BC_Gen5_40|BC_Gen5_80|
|:----- | -------: |--------: |--------: |--------: |--------: |---------:|--------: |
|Tamanho máximo de dados (GB)|3072|3072|3072|4096|4096|4096|4096|

**Comercialmente Crítico – computação provisionada – série M (parte 1)**

|MAXSIZE|BC_M_8|BC_M_10|BC_M_12|BC_M_14|BC_M_16|BC_M_18|
|:----- | -------: | -------: | -------: | -------: | -------: | -------: |
|Tamanho máximo de dados (GB)|512|640|768|896|1024|1152|

**Comercialmente crítico – computação provisionada – série M (parte 2)**

|MAXSIZE|BC_M_20|BC_M_24|BC_M_32|BC_M_64|BC_M_128|
|:----- | -------: | -------: | -------: | -------: | -------: |
|Tamanho máximo de dados (GB)|1280|1536|2\.048|4096|4096|

Se nenhum valor `MAXSIZE` for definido ao usar o modelo vCore, o padrão será de 32 GB. Para obter detalhes adicionais sobre limitações de recursos para o modelo de vCore, confira [Limites de recurso de vCore](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits).

As regras a seguir se aplicam aos argumentos MAXSIZE e EDITION:

- Se EDITION for especificado, mas MAXSIZE não for especificado, o valor padrão da edição será usado. Por exemplo, se EDITION for definido como Standard e MAXSIZE não for especificado, então MAXSIZE será automaticamente definido como 250 MB.
- Se nem MAXSIZE nem EDITION forem especificados, EDITION será definido como `GeneralPurpose` e MAXZISE será definido como 32 GB.

SERVICE_OBJECTIVE

- **Para bancos de dados individuais e em pool**

  - Especifica o tamanho da computação (objetivo do serviço). Os valores disponíveis para o objetivo de serviço são: `S0`, `S1`, `S2`, `S3`, `S4`, `S6`, `S7`, `S9`, `S12`, `P1`, `P2`, `P4`, `P6`, `P11`, `P15`, `GP_GEN4_1`, `GP_GEN4_2`, `GP_GEN4_3`, `GP_GEN4_4`, `GP_GEN4_5`, `GP_GEN4_6`, `GP_GEN4_7`, `GP_GEN4_8`, `GP_GEN4_7`, `GP_GEN4_8`, `GP_GEN4_9`, `GP_GEN4_10`, `GP_GEN4_16`, `GP_GEN4_24`, `BC_GEN4_1`, `BC_GEN4_2`, `BC_GEN4_3`, `BC_GEN4_4`, `BC_GEN4_5`, `BC_GEN4_6`, `BC_GEN4_7`, `BC_GEN4_8`, `BC_GEN4_9`, `BC_GEN4_10`, `BC_GEN4_16`, `BC_GEN4_24`, `GP_Gen5_2`, `GP_Gen5_4`, `GP_Gen5_6`, `GP_Gen5_8`, `GP_Gen5_10`, `GP_Gen5_12`, `GP_Gen5_14`, `GP_Gen5_16`, `GP_Gen5_18`, `GP_Gen5_20`, `GP_Gen5_24`, `GP_Gen5_32`, `GP_Gen5_40`, `GP_Gen5_80`, `GP_Fsv2_8`, `GP_Fsv2_10`, `GP_Fsv2_12`, `GP_Fsv2_14`, `GP_Fsv2_16`, `GP_Fsv2_18`, `GP_Fsv2_20`, `GP_Fsv2_24`, `GP_Fsv2_32`, `GP_Fsv2_36`, `GP_Fsv2_72`, `BC_Gen5_2`, `BC_Gen5_4`, `BC_Gen5_6`, `BC_Gen5_8`, `BC_Gen5_10`, `BC_Gen5_12`, `BC_Gen5_14`, `BC_Gen5_16`, `BC_Gen5_18`, `BC_Gen5_20`, `BC_Gen5_24`, `BC_Gen5_32`, `BC_Gen5_40`, `BC_Gen5_80`, `BC_M_8`, `BC_M_10`, `BC_M_12`, `BC_M_14`, `BC_M_16`, `BC_M_18`, `BC_M_20`, `BC_M_24`, `BC_M_32`, `BC_M_64`, `BC_M_128`.

- **Para bancos de dados sem servidor**
- 
  - Especifica o tamanho da computação (objetivo do serviço). Os valores disponíveis para o objetivo do serviço são: `GP_S_Gen5_1`, `GP_S_Gen5_2`, `GP_S_Gen5_4`, `GP_S_Gen5_6`, `GP_S_Gen5_8`, `GP_S_Gen5_10`, `GP_S_Gen5_12`, `GP_S_Gen5_14`, `GP_S_Gen5_16`, `GP_S_Gen5_18`, `GP_S_Gen5_20`, `GP_S_Gen5_24`, `GP_S_Gen5_32` e `GP_S_Gen5_40`.

- **Para bancos de dados individuais na camada de serviço em hiperescala**

  - Especifica o tamanho da computação (objetivo do serviço). Os valores disponíveis para o objetivo do serviço são: `HS_GEN4_1` `HS_GEN4_2` `HS_GEN4_4` `HS_GEN4_8` `HS_GEN4_16`, `HS_GEN4_24`, `HS_Gen5_2`, `HS_Gen5_4`, `HS_Gen5_8`, `HS_Gen5_16`, `HS_Gen5_24`, `HS_Gen5_32`, `HS_Gen5_48`, `HS_Gen5_80`.

Para obter descrições do objetivo de serviço e mais informações sobre o tamanho, as edições e as combinações de objetivos de serviço, confira [Camadas de serviço do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-service-tiers). Se o SERVICE_OBJECTIVE especificado não for compatível com a edição, você receberá um erro. Para alterar o valor SERVICE_OBJECTIVE de uma camada para outra (por exemplo, de S1 para P1), você deve alterar também o valor EDITION. Para obter descrições de objetivos de serviço e mais informações sobre o tamanho, as edições e as combinações de objetivo de serviço, veja [Camadas de serviço e níveis de desempenho do Banco de Dados SQL do Azure](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/), [Limites de recurso de DTU](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits) e [Limites de recurso de vCore](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits). O suporte para objetivos de serviço PRS foi removido. Em caso de dúvidas, use este alias de email: premium-rs@microsoft.com.

ELASTIC_POOL (name = \<elastic_pool_name>) **Aplica-se a:** Somente bancos de dados únicos e em pool. Não é aplicável a bancos de dados na camada de serviço em hiperescala.
Para criar um banco de dados em um pool de banco de dados elástico, defina o SERVICE_OBJECTIVE do banco de dados como ELASTIC_POOL e forneça o nome do pool. Para obter mais informações, confira [Criar e gerenciar um pool elástico do Banco de Dados SQL](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/).

AS COPY OF [source_server_name.]source_database_name **Aplica-se a:** Somente bancos de dados únicos e em pool.
Para copiar um banco de dados para o mesmo servidor [!INCLUDE[ssSDS](../../includes/sssds-md.md)] ou um servidor diferente.

*source_server_name* O nome do servidor [!INCLUDE[ssSDS](../../includes/sssds-md.md)] onde o banco de fonte de origem está localizado. Esse parâmetro é opcional quando o banco de dados de origem e o banco de dados de destino devem estar localizados no mesmo servidor [!INCLUDE[ssSDS](../../includes/sssds-md.md)].

> [!NOTE]
> o argumento `AS COPY OF` não oferece suporte aos nomes de domínio exclusivos totalmente qualificados. Em outras palavras, se o nome de domínio totalmente qualificado do seu servidor for `serverName.database.windows.net`, use somente `serverName` durante a cópia do banco de dados.

*source_database_name*

O nome do banco de dados que deve ser copiado.

## <a name="remarks"></a>Comentários

Os bancos de dados no [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] tem várias configurações padrão que são definidas quando o banco de dados é criado. Para obter mais informações sobre essas configurações padrão, veja a lista de valores em [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md).

`MAXSIZE` fornece a capacidade de limitar o tamanho do banco de dados. Se o tamanho do banco de dados atingir seu `MAXSIZE`, você receberá o código de erro 40544. Quando isso ocorre, você não pode inserir ou atualizar dados nem criar novos objetos (como tabelas, procedimentos armazenados, exibições e funções). No entanto, você ainda pode ler e excluir dados, truncar tabelas, descartar tabelas e índices e reconstruir índices. É possível atualizar `MAXSIZE` para um valor maior que o tamanho atual do banco de dados ou excluir alguns dados para liberar espaço de armazenamento. Pode haver um atraso máximo de quinze minutos para que você possa inserir novos dados.

Para alterar o tamanho, edição ou valores objetivos de serviço posteriormente, use [ALTER DATABASE – Banco de Dados SQL do Azure](../../t-sql/statements/alter-database-transact-sql.md?view=azuresqldb-currentls).

O argumento `CATALOG_COLLATION` só está disponível durante a criação do banco de dados.

## <a name="database-copies"></a>Cópias de banco de dados

**Aplica-se a:** Somente bancos de dados únicos e em pool.

Copiar um banco de dados que usa a instrução `CREATE DATABASE` é uma operação assíncrona. Portanto, uma conexão com o servidor de [!INCLUDE[ssSDS](../../includes/sssds-md.md)] não é necessária para a duração completa do processo de cópia. A instrução `CREATE DATABASE` retornará o controle para o usuário depois que a entrada no sys.databases for criada, mas antes que a operação de cópia de banco de dados seja concluída. Em outras palavras, a instrução `CREATE DATABASE` é retornada com êxito quando a cópia do banco de dados ainda está em andamento.

- Monitoramento do processo de cópia em um servidor [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]: Consulte as colunas `percentage_complete` ou `replication_state_desc` em [dm_database_copies](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md) ou na coluna `state` na exibição **sys.databases**. A exibição [sys.dm_operation_status](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md) pode ser usada e retornará o status das operações de banco de dados, incluindo a cópia do banco de dados.

Quando o processo de cópia é concluído com êxito, o banco de dados de destino fica transacionalmente consistente com o banco de dados de origem.

A seguinte sintaxe e as regras semânticas aplicam-se ao uso do argumento `AS COPY OF`:

- Os nomes do servidor de origem e do servidor para o destino de impressão podem ser iguais ou diferentes. Quando são o mesmo, esse parâmetro é opcional e o contexto do servidor da sessão atual é usado por padrão.
- Os nomes do banco de dados de origem e destino devem ser especificados, exclusivo e estarem em conformidade com as regras do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para identificadores. Para obter mais informações, consulte [Identificadores](https://go.microsoft.com/fwlink/p/?LinkId=180386).
- A instrução `CREATE DATABASE` deve ser executada dentro do contexto do banco de dados mestre do servidor [!INCLUDE[ssSDS](../../includes/sssds-md.md)] em que o novo banco de dados será criado.
- Depois de a cópia ser concluída, o banco de dados de destino deve ser gerenciado como um banco de dados independente. Você pode executar as instruções `ALTER DATABASE` e `DROP DATABASE` no novo banco de dados independentemente do banco de dados de origem. Você também pode copiar o novo banco de dados para outro novo banco de dados.
- O banco de dados de origem pode continuar a ser acessado enquanto a cópia do banco de dados está em andamento.

Para obter mais informações, consulte [Criar uma cópia de um Banco de Dados SQL do Azure usando o Transact-SQL](https://azure.microsoft.com/documentation/articles/sql-database-copy-transact-sql/).

## <a name="permissions"></a>Permissões

Para criar um banco de dados, um logon deve ser um dos seguintes:

- O logon da entidade de segurança no nível do servidor
- O administrador do Azure AD do SQL Server do Azure local
- Um logon que é um membro da função de banco de dados `dbmanager`

**Requisitos adicionais para usar a sintaxe `CREATE DATABASE ... AS COPY OF`:** O logon que executa a instrução no servidor local também deve ter pelo menos o `db_owner` no servidor de origem. Se o logon for baseado na autenticação [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o logon que está executando a instrução no servidor local deverá ter um logon correspondente no servidor [!INCLUDE[ssSDS](../../includes/sssds-md.md)] de origem, com um nome idêntico e senha idênticos.

## <a name="examples"></a>Exemplos

### <a name="simple-example"></a>Exemplo simples

Um exemplo simples para criar um banco de dados.

```sql
CREATE DATABASE TestDB1;
```

### <a name="simple-example-with-edition"></a>Exemplo simples com Edição

Um exemplo simples para criar um banco de dados de uso geral.

```sql
CREATE DATABASE TestDB2
( EDITION = 'GeneralPurpose' );
```

### <a name="example-with-additional-options"></a>Exemplo com opções adicionais

Um exemplo que usa várias opções.

```sql
CREATE DATABASE hito
COLLATE Japanese_Bushu_Kakusu_100_CS_AS_KS_WS
( MAXSIZE = 500 MB, EDITION = 'GeneralPurpose', SERVICE_OBJECTIVE = 'GP_GEN4_8' ) ;
```

### <a name="creating-a-copy"></a>Criando uma cópia

Um exemplo da criação de uma cópia de um banco de dados.

**Aplica-se a:** Somente bancos de dados únicos e em pool.

```sql
CREATE DATABASE escuela
AS COPY OF school;
```

### <a name="creating-a-database-in-an-elastic-pool"></a>Criando um banco de dados em um pool elástico

Cria um novo banco de dados no pool chamado S3M100:

**Aplica-se a:** Somente bancos de dados únicos e em pool.

```sql
CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL ( name = S3M100 ) ) ;
```

### <a name="creating-a-copy-of-a-database-on-another-server"></a>Criando uma cópia de um banco de dados em outro servidor

O exemplo a seguir cria uma cópia do banco de dados db_original, chamada db_copy no tamanho da computação (objetivo do serviço) P2 para um banco de dados individual. Isso será verdadeiro independentemente se o db_original estiver em um pool elástico ou em um tamanho da computação (objetivo do serviço) para um banco de dados individual.

**Aplica-se a:** Somente bancos de dados únicos e em pool.

```sql
CREATE DATABASE db_copy
  AS COPY OF ozabzw7545.db_original ( SERVICE_OBJECTIVE = 'P2' );
```

O exemplo a seguir cria uma cópia do banco de dados db_original, chamada db_copy em um pool elástico chamado ep1. Isso será verdadeiro independentemente se o db_original estiver em um pool elástico ou em um tamanho da computação (objetivo do serviço) para um banco de dados individual. Se db_original estiver em um pool elástico com um nome diferente, então db_copy ainda será criado em ep1.

**Aplica-se a:** Somente bancos de dados únicos e em pool.

```sql
CREATE DATABASE db_copy
  AS COPY OF ozabzw7545.db_original
  (SERVICE_OBJECTIVE = ELASTIC_POOL( name = ep1 ) ) ;
```

### <a name="create-database-with-specified-catalog-collation-value"></a>Criar banco de dados com um valor de ordenação de catálogo especificado

O exemplo a seguir define a ordenação de catálogo como DATABASE_DEFAULT durante a criação do banco de dados, que define a ordenação de catálogo como sendo a mesma que a ordenação de banco de dados.

```sql
CREATE DATABASE TestDB3 COLLATE Japanese_XJIS_140 (MAXSIZE = 100 MB, EDITION = 'Basic')
  WITH CATALOG_COLLATION = DATABASE_DEFAULT
```

## <a name="see-also"></a>Confira também

- [sys.dm_database_copies – Banco de Dados SQL do Azure](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md)
- [ALTER DATABASE – Banco de Dados SQL do Azure](alter-database-transact-sql.md?view=azuresqldb-currentls)

::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"

:::row:::
    :::column:::
        [SQL Server](create-database-transact-sql.md?view=sql-server-2017)
    :::column-end:::
    :::column:::
        [Banco de Dados SQL](create-database-transact-sql.md?view=azuresqldb-current)
    :::column-end:::
    :::column:::
        **_\* Banco de Dados SQL<br />Instância Gerenciada \*_**
    :::column-end:::
    :::column:::
        [Azure Synapse<br />Analytics](create-database-transact-sql.md?view=azure-sqldw-latest)
    :::column-end:::
    :::column:::
        [Analytics Platform<br />System (PDW)](create-database-transact-sql.md?view=aps-pdw-2016)
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="azure-sql-managed-instance"></a>Instância Gerenciada do Azure SQL

## <a name="overview"></a>Visão geral

Na Instância Gerenciada de SQL do Azure, essa instrução é usada para criar um banco de dados. Ao criar um banco de dados em uma instância gerenciada, você deve especificar o nome do banco de dados e a ordenação.

## <a name="syntax"></a>Sintaxe

```syntaxsql
CREATE DATABASE database_name [ COLLATE collation_name ]
[;]
```

> [!IMPORTANT]
> Para adicionar arquivos ou definir a contenção de um banco de dados em uma instância gerenciada, use a instrução [ALTER DATABASE](alter-database-transact-sql.md?view=sqlallproducts-allversions&tabs=sqldbmi).

## <a name="arguments"></a>Argumentos

*database_name* O nome do novo banco de dados. Este nome deve ser exclusivo no servidor SQL e deve estar de acordo com a regras do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para identificadores. Para obter mais informações, consulte [Identificadores](https://go.microsoft.com/fwlink/p/?LinkId=180386).

*Collation_name* Especifica a ordenação padrão do banco de dados. O nome da ordenação pode ser um nome de ordenação do Windows ou um nome de ordenação SQL. Se não for especificado, o banco de dados receberá a ordenação padrão, que é SQL_Latin1_General_CP1_CI_AS.

Para obter mais informações sobre nomes de ordenações do Windows e SQL, [COLLATE (Transact-SQL)](../../t-sql/statements/collations.md).

## <a name="remarks"></a>Comentários

Os bancos de dados no [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] tem várias configurações padrão que são definidas quando o banco de dados é criado. Para obter mais informações sobre essas configurações padrão, veja a lista de valores em [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md).

> [!IMPORTANT]
> A instrução `CREATE DATABASE` deve ser a única instrução em um lote do [!INCLUDE[tsql](../../includes/tsql-md.md)].

A seguir estão as limitações de `CREATE DATABASE`:

- Arquivos e grupos de arquivos não podem ser definidos.
- `WITH`não há suporte para as opções.

  > [!TIP]
  > Como alternativa, use [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md?view=azuresqldb-mi-current). após `CREATE DATABASE` para definir opções de banco de dados e para adicionar arquivos.

## <a name="permissions"></a>Permissões

Para criar um banco de dados, um logon deve ser um dos seguintes:

- O logon da entidade de segurança no nível do servidor
- O administrador do Azure AD do SQL Server do Azure local
- Um logon que é um membro da função de banco de dados `dbcreator`

## <a name="examples"></a>Exemplos

### <a name="simple-example"></a>Exemplo simples

Um exemplo simples para criar um banco de dados.

```sql
CREATE DATABASE TestDB1;
```

## <a name="see-also"></a>Confira também

Confira [ALTER DATABASE](alter-database-transact-sql.md?view=azuresqldb-mi-current)

::: moniker-end
::: moniker range="=azure-sqldw-latest||=sqlallproducts-allversions"

:::row:::
    :::column:::
        [SQL Server](create-database-transact-sql.md?view=sql-server-2017)
    :::column-end:::
    :::column:::
        [Banco de Dados SQL](create-database-transact-sql.md?view=azuresqldb-current)
    :::column-end:::
    :::column:::
        [Banco de Dados SQL<br />Instância Gerenciada](create-database-transact-sql.md?view=azuresqldb-mi-current)
    :::column-end:::
    :::column:::
        **_\* Azure Synapse<br />Analytics \*_**
    :::column-end:::
    :::column:::
        [Analytics Platform<br />System (PDW)](create-database-transact-sql.md?view=aps-pdw-2016)
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="azure-synapse-analytics"></a>Azure Synapse Analytics

## <a name="overview"></a>Visão geral

No Azure Synapse, essa instrução pode ser usada com um servidor do Banco de Dados SQL do Azure para criar um banco de dados de Análise do SQL. Com esta instrução, você especifica o nome do banco de dados, a ordenação, o tamanho máximo, a edição e o objetivo de serviço.

## <a name="syntax"></a>Sintaxe

```syntaxsql
CREATE DATABASE database_name [ COLLATE collation_name ]
(
    [ MAXSIZE = {
          250 | 500 | 750 | 1024 | 5120 | 10240 | 20480 | 30720
        | 40960 | 51200 | 61440 | 71680 | 81920 | 92160 | 102400
        | 153600 | 204800 | 245760
      } GB ,
    ]
    EDITION = 'datawarehouse',
    SERVICE_OBJECTIVE = {
         'DW100' | 'DW200' | 'DW300' | 'DW400' | 'DW500' | 'DW600'
        | 'DW1000' | 'DW1200' | 'DW1500' | 'DW2000' | 'DW3000' | 'DW6000'
        |'DW100c' | 'DW200c' | 'DW300c' | 'DW400c' | 'DW500c'
        | 'DW1000c' | 'DW1500c' | 'DW2000c' | 'DW2500c' | 'DW3000c' | 'DW5000c'
        | 'DW6000c' | 'DW7500c' | 'DW10000c' | 'DW15000c' | 'DW30000c'
    }
)
[;]
```

## <a name="arguments"></a>Argumentos

*database_name* O nome do novo banco de dados. Esse nome deve ser exclusivo no servidor SQL, que pode hospedar os bancos de dados [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] e [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], e ser compatível com as regras [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para identificadores. Para obter mais informações, consulte [Identificadores](https://go.microsoft.com/fwlink/p/?LinkId=180386).

*collation_name* Especifica a ordenação padrão do banco de dados. O nome da ordenação pode ser um nome de ordenação do Windows ou um nome de ordenação SQL. Se não for especificado, o banco de dados receberá a ordenação padrão, que é SQL_Latin1_General_CP1_CI_AS.

Para obter mais informações sobre os nomes de ordenação do Windows e do SQL, consulte [COLLATE (Transact-SQL)](https://msdn.microsoft.com/library/ms184391.aspx).

*EDITION* Especifica a camada de serviço do banco de dados. Para [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], use 'datawarehouse'.

*MAXSIZE* O padrão é 245.760 GB (240 TB).

**Aplica-se a:** Otimizado para Computação Gen1

O tamanho máximo permitido para o banco de dados. O banco de dados não pode ultrapassar o MAXSIZE.

**Aplica-se a:** Otimizado para Computação Gen2

O tamanho máximo permitido para dados de rowstore no banco de dados. Os dados armazenados em tabelas rowstore, um deltastore de um índice columnstore ou um índice não clusterizado em um índice columnstore clusterizado não podem exceder o MAXSIZE. Os dados compactados no formato columnstore não têm um limite de tamanho e não estão restritos pelo MAXSIZE.

SERVICE_OBJECTIVE Especifica o tamanho da computação (objetivo do serviço). Para saber mais sobre os objetivos de serviço para o Azure Synapse, confira [Unidades de Data Warehouse (DWUs)](https://docs.microsoft.com/azure/sql-data-warehouse/what-is-a-data-warehouse-unit-dwu-cdwu).

## <a name="general-remarks"></a>Comentários gerais

Use [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) para ver as propriedades do banco de dados.

Use [ALTER DATABASE – Azure Synapse Analytics](../../t-sql/statements/alter-database-transact-sql.md?view=aps-pdw-2016-au7) para alterar o tamanho máximo ou os valores objetivos de serviço posteriormente.

O Azure Synapse é definido como COMPATIBILITY_LEVEL 130 e não pode ser alterado. Para obter mais detalhes, confira [Improved Query Performance with Compatibility Level 130 in Azure SQL Database](https://azure.microsoft.com/documentation/articles/sql-database-compatibility-level-query-performance-130/) (Melhor desempenho de consulta com o nível de compatibilidade 130 no Banco de Dados SQL do Azure).

## <a name="permissions"></a>Permissões

Permissões necessárias:

- Logon de entidade de segurança de nível de serviço, criado pelo processo de provisionamento ou
- Membro da função de banco de dados `dbmanager`.

## <a name="error-handling"></a>Tratamento de erros

Se o tamanho do banco de dados atingir MAXSIZE, você receberá o código de erro 40544. Quando isso ocorre, não é possível inserir, atualizar dados nem criar novos objetos (como tabelas, procedimentos armazenados, exibições e funções). Ainda é possível ler e excluir dados, truncar tabelas, remover tabelas e índices e recriar índices. Você pode atualizar MAXSIZE para um valor maior que o tamanho atual do banco de dados ou excluir alguns dados para liberar espaço de armazenamento. Pode haver um atraso máximo de quinze minutos para que você possa inserir novos dados.

## <a name="limitations-and-restrictions"></a>Limitações e Restrições

Você deve estar conectado ao banco de dados mestre para criar um novo banco de dados.

A instrução `CREATE DATABASE` deve ser a única instrução em um lote do [!INCLUDE[tsql](../../includes/tsql-md.md)].

Não é possível alterar a ordenação de banco de dados depois que o banco de dados é criado.

## <a name="examples-sssdwfull"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]

### <a name="a-simple-example"></a>a. Exemplo simples
Um exemplo simples para criar um banco de dados de data warehouse. Isso cria o banco de dados com o menor tamanho máximo que é 10240 GB, a ordenação padrão que é SQL_Latin1_General_CP1_CI_AS e a menor potência de computação que é DW100.

```sql
CREATE DATABASE TestDW
(EDITION = 'datawarehouse', SERVICE_OBJECTIVE='DW100');
```

### <a name="b-create-a-data-warehouse-database-with-all-the-options"></a>B. Criar um banco de dados de data warehouse com todas as opções
Um exemplo da criação de um data warehouse de 10 terabytes que usa todas as opções.

```sql
CREATE DATABASE TestDW COLLATE Latin1_General_100_CI_AS_KS_WS
(MAXSIZE = 10240 GB, EDITION = 'datawarehouse', SERVICE_OBJECTIVE = 'DW1000');
```

## <a name="see-also"></a>Consulte Também

- [ALTER DATABASE – Azure Synapse Analytics](../../t-sql/statements/alter-database-transact-sql.md?view=aps-pdw-2016-au7)
- [CREATE TABLE – Azure Synapse Analytics](../../t-sql/statements/create-table-azure-sql-data-warehouse.md)
- [DROP DATABASE – Transact-SQL](../../t-sql/statements/drop-database-transact-sql.md)

::: moniker-end
::: moniker range=">=aps-pdw-2016||=sqlallproducts-allversions"

:::row:::
    :::column:::
        [SQL Server](create-database-transact-sql.md?view=sql-server-2017)
    :::column-end:::
    :::column:::
        [Banco de Dados SQL](create-database-transact-sql.md?view=azuresqldb-current)
    :::column-end:::
    :::column:::
        [Banco de Dados SQL<br />Instância Gerenciada](create-database-transact-sql.md?view=azuresqldb-mi-current)
    :::column-end:::
    :::column:::
        [Azure Synapse<br />Analytics](create-database-transact-sql.md?view=azure-sqldw-latest)
    :::column-end:::
    :::column:::
        **_\* Analytics Platform<br />System (PDW) \*_**
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="analytics-platform-system"></a>Sistema de plataforma de análise

## <a name="overview"></a>Visão geral

No Analytics Platform System, essa instrução é usada para criar um banco de dados em um dispositivo do Analytics Platform System. Use essa instrução para criar todos os arquivos associados a um banco de dados do dispositivo e para definir as opções de tamanho máximo e aumento automático para as tabelas de banco de dados e o log de transações.

## <a name="syntax"></a>Sintaxe

```syntaxsql
CREATE DATABASE database_name
WITH (
    [ AUTOGROW = ON | OFF , ]
    REPLICATED_SIZE = replicated_size [ GB ] ,
    DISTRIBUTED_SIZE = distributed_size [ GB ] ,
    LOG_SIZE = log_size [ GB ] )
[;]
```

## <a name="arguments"></a>Argumentos

*database_name* O nome do novo banco de dados. Para obter mais informações sobre nomes de banco de dados permitidos, consulte "Regras de nomenclatura de objeto" e "Nomes de banco de dados reservados" no [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].

AUTOGROW = ON | **OFF** Especifica se os parâmetros *replicated_size*, *distributed_size* e *log_size* para esse banco de dados aumentarão automaticamente, conforme necessário, além de seus tamanhos especificados. O valor padrão é **OFF**.

Se AUTOGROW for ON, *replicated_size*, *distributed_size* e *log_size* aumentará conforme necessário (não em blocos do tamanho inicial especificado) com cada inserção de dados, atualização ou outra ação que exige mais armazenamento do que já foi alocado.

Se AUTOGROW for OFF, os tamanhos não aumentarão automaticamente. O [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] retornará um erro durante a tentativa de uma ação que exige que *replicated_size*, *distributed_size* ou *log_size* aumente além do valor especificado.

AUTOGROW é ON ou OFF para todos os tamanhos. Por exemplo, não é possível definir AUTOGROW ON para *log_size*, mas não defini-lo para *replicated_size*.

*replicated_size* [GB] Um número positivo. Define o tamanho (em gigabytes de inteiro ou decimal) para o espaço total alocado a tabelas replicadas e os dados correspondentes *em cada nó de Computação*. Para os requisitos de *replicated_size* mínimo e máximo, consulte "Valores mínimos e máximos" no [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].

Se AUTOGROW for ON, as tabelas replicadas terão permissão para aumentar além desse limite.

Se AUTOGROW for OFF, um erro será retornado, caso um usuário tente criar uma nova tabela replicada, inserir dados em uma tabela replicada existente ou atualizar uma tabela replicada existente de uma maneira que aumente o tamanho além de *replicated_size*.

*distributed_size* [GB] Um número positivo. O tamanho, em gigabytes de inteiro ou decimal, para o espaço total alocado para tabelas distribuídas (e os dados correspondentes) *entre o dispositivo*. Para os requisitos de *distributed_size* mínimo e máximo, consulte "Valores mínimos e máximos" no [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].

Se AUTOGROW for ON, as tabelas distribuídas terão permissão para aumentar além desse limite.

Se AUTOGROW for OFF, um erro será retornado, caso um usuário tente criar uma nova tabela distribuída, inserir dados em uma tabela distribuída existente ou atualizar uma tabela distribuída existente de uma maneira que aumente o tamanho além de *distributed_size*.

*log_size* [GB] Um número positivo. O tamanho (em gigabytes de inteiro ou decimal) para o log de transações *entre o dispositivo*.

Para os requisitos de *log_size* mínimo e máximo, consulte "Valores mínimos e máximos" no [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].

Se AUTOGROW for ON, o arquivo de log poderá aumentar além desse limite. Use a instrução [DBCC SHRINKLOG (Azure Synapse Analytics)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md) para reduzir o tamanho dos arquivos de log para seu tamanho original.

Se AUTOGROW for OFF, um erro será retornado para o usuário para qualquer ação que aumente o tamanho do log em um nó de Computação individual para além de *log_size*.

## <a name="permissions"></a>Permissões

Exige a permissão `CREATE ANY DATABASE` no banco de dados mestre ou a associação à função de servidor fixa **sysadmin**.

O exemplo a seguir fornece a permissão para criar um banco de dados para o usuário Fay de banco de dados.

```sql
USE master;
GO
GRANT CREATE ANY DATABASE TO [Fay];
GO
```

## <a name="general-remarks"></a>Comentários gerais

Os bancos de dados são criados com o nível de compatibilidade de banco de dados 120, que é o nível de compatibilidade do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]. Isso garante que o banco de dados poderá usar toda as funcionalidade do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] usada pelo PDW.

## <a name="limitations-and-restrictions"></a>Limitações e Restrições

A instrução CREATE DATABASE não é permitida em uma transação explícita. Para obter mais informações, consulte [Instruções](../../t-sql/statements/statements.md).

Para obter informações sobre restrições mínimas e máximas em bancos de dados, consulte "Valores mínimos e máximos" no [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].

No momento em um banco de dados é criado, deve haver espaço livre suficiente disponível *em cada nó de Computação* para alocar o total combinado dos seguintes tamanhos:

- Banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com tabelas com o tamanho de *replicated_table_size*.
- Banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com tabelas com o tamanho do (*distributed_table_size*/número de nós de Computação).
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] registra em log o tamanho de (*log_size*/número de nós de Computação).

## <a name="locking"></a>Bloqueio

Usa um bloqueio compartilhado no objeto DATABASE.

## <a name="metadata"></a>Metadados

Depois que essa operação for bem-sucedida, uma entrada para esse banco de dados será mostrada nas exibições de metadados [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) e [sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).

## <a name="examples-sspdw"></a>Exemplos: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

### <a name="a-basic-database-creation-examples"></a>a. Exemplos de criação de banco de dados básicos

O exemplo a seguir cria o banco de dados `mytest` com uma alocação de armazenamento de 100 GB por nó de Computação para tabelas replicadas, 500 GB por dispositivo para tabelas distribuídas e 100 GB por dispositivo para o log de transações. Neste exemplo, AUTOGROW está desativado por padrão.

```sql
CREATE DATABASE mytest
  WITH
    (REPLICATED_SIZE = 100 GB,
    DISTRIBUTED_SIZE = 500 GB,
    LOG_SIZE = 100 GB );
```

O exemplo a seguir cria o banco de dados `mytest` com os mesmos parâmetros acima, exceto que AUTOGROW está ativado. Isso permite que o banco de dados aumente para fora dos parâmetros de tamanho especificados.

```sql
CREATE DATABASE mytest
  WITH
    (AUTOGROW = ON,
    REPLICATED_SIZE = 100 GB,
    DISTRIBUTED_SIZE = 500 GB,
    LOG_SIZE = 100 GB);
```

### <a name="b-creating-a-database-with-partial-gigabyte-sizes"></a>B. Criando um banco de dados com tamanhos de gigabyte parcial

O exemplo a seguir cria o banco de dados `mytest`, com AUTOGROW desativado, uma alocação de armazenamento de 1,5 GB por nó de Computação para tabelas replicadas, 5,25 GB por dispositivo para tabelas distribuídas e 10 GB por dispositivo para o log de transações.

```sql
CREATE DATABASE mytest
  WITH
    (REPLICATED_SIZE = 1.5 GB,
    DISTRIBUTED_SIZE = 5.25 GB,
    LOG_SIZE = 10 GB);
```

## <a name="see-also"></a>Consulte Também

- [ALTER DATABASE – Analytics Platform System](../../t-sql/statements/alter-database-transact-sql.md?view=aps-pdw-2016-au7)
- [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)

::: moniker-end
