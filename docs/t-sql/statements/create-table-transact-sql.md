---
title: CREATE TABLE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/24/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FILESTREAM_TSQL
- TABLE
- CREATE_TABLE_TSQL
- CREATE TABLE
- FILESTREAM
- TABLE_TSQL
- FILESTREAM_ON
- FILESTREAM_ON_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CHECK constraints
- global temporary tables [SQL Server]
- local temporary tables [SQL Server]
- size [SQL Server], tables
- UNIQUE constraints [SQL Server], creating
- constraints [SQL Server], columns
- maximum number of indexes per table
- number of tables per database
- number of indexes per table
- table creation [SQL Server], CREATE TABLE
- temporary tables [SQL Server], creating
- table size [SQL Server]
- nullability [SQL Server]
- partitioned tables [SQL Server], creating
- DEFAULT definition
- null values [SQL Server], columns
- number of rows per table
- maximum number of columns per table
- FOREIGN KEY constraints, creating
- PRIMARY KEY constraints
- number of bytes per row
- CREATE TABLE statement
- number of columns per table
- maximum number of bytes per row
ms.assetid: 1e068443-b9ea-486a-804f-ce7b6e048e8b
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5c95568167d1a783ed8d605bc64bc60a135046f0
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "80380667"
---
# <a name="create-table-transact-sql"></a>CREATE TABLE (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Cria uma nova tabela no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e no [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

> [!NOTE]
> Para sintaxe [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], veja [CREATE TABLE (SQL Data Warehouse do Azure)](../../t-sql/statements/create-table-azure-sql-data-warehouse.md).

![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="simple-syntax"></a>Sintaxe simples

```
-- Simple CREATE TABLE Syntax (common if not using options)
CREATE TABLE
    { database_name.schema_name.table_name | schema_name.table_name | table_name }
    ( { <column_definition> } [ ,...n ] )
[ ; ]
```

## <a name="full-syntax"></a>Sintaxe completa

```
-- Disk-Based CREATE TABLE Syntax
CREATE TABLE
    { database_name.schema_name.table_name | schema_name.table_name | table_name }
    [ AS FileTable ]
    ( {   <column_definition>
        | <computed_column_definition>
        | <column_set_definition>
        | [ <table_constraint> ] [ ,... n ]
        | [ <table_index> ] }
          [ ,...n ]
          [ PERIOD FOR SYSTEM_TIME ( system_start_time_column_name
             , system_end_time_column_name ) ]
      )
    [ ON { partition_scheme_name ( partition_column_name )
           | filegroup
           | "default" } ]
    [ TEXTIMAGE_ON { filegroup | "default" } ]
    [ FILESTREAM_ON { partition_scheme_name
           | filegroup
           | "default" } ]
    [ WITH ( <table_option> [ ,...n ] ) ]
[ ; ]
  
<column_definition> ::=
column_name <data_type>
    [ FILESTREAM ]
    [ COLLATE collation_name ]
    [ SPARSE ]
    [ MASKED WITH ( FUNCTION = ' mask_function ') ]
    [ CONSTRAINT constraint_name [ DEFAULT constant_expression ] ]
    [ IDENTITY [ ( seed,increment ) ]
    [ NOT FOR REPLICATION ]
    [ GENERATED ALWAYS AS ROW { START | END } [ HIDDEN ] ]
    [ NULL | NOT NULL ]
    [ ROWGUIDCOL ]
    [ ENCRYPTED WITH
        ( COLUMN_ENCRYPTION_KEY = key_name ,
          ENCRYPTION_TYPE = { DETERMINISTIC | RANDOMIZED } ,
          ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256'
        ) ]
    [ <column_constraint> [, ...n ] ]
    [ <column_index> ]
  
<data_type> ::=
[ type_schema_name . ] type_name
    [ ( precision [ , scale ] | max |
        [ { CONTENT | DOCUMENT } ] xml_schema_collection ) ]
  
<column_constraint> ::=
[ CONSTRAINT constraint_name ]
{     { PRIMARY KEY | UNIQUE }
        [ CLUSTERED | NONCLUSTERED ]
        [
            WITH FILLFACTOR = fillfactor
          | WITH ( < index_option > [ , ...n ] )
        ]
        [ ON { partition_scheme_name ( partition_column_name )
            | filegroup | "default" } ]
  
  | [ FOREIGN KEY ]
        REFERENCES [ schema_name . ] referenced_table_name [ ( ref_column ) ]
        [ ON DELETE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]
        [ ON UPDATE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]
        [ NOT FOR REPLICATION ]
  
  | CHECK [ NOT FOR REPLICATION ] ( logical_expression )
}
  
<column_index> ::=
 INDEX index_name [ CLUSTERED | NONCLUSTERED ]
    [ WITH ( <index_option> [ ,... n ] ) ]
    [ ON { partition_scheme_name (column_name )
         | filegroup_name
         | default
         }
    ]
    [ FILESTREAM_ON { filestream_filegroup_name | partition_scheme_name | "NULL" } ]
  
<computed_column_definition> ::=
column_name AS computed_column_expression
[ PERSISTED [ NOT NULL ] ]
[
    [ CONSTRAINT constraint_name ]
    { PRIMARY KEY | UNIQUE }
        [ CLUSTERED | NONCLUSTERED ]
        [
            WITH FILLFACTOR = fillfactor
          | WITH ( <index_option> [ , ...n ] )
        ]
        [ ON { partition_scheme_name ( partition_column_name )
        | filegroup | "default" } ]
  
    | [ FOREIGN KEY ]
        REFERENCES referenced_table_name [ ( ref_column ) ]
        [ ON DELETE { NO ACTION | CASCADE } ]
        [ ON UPDATE { NO ACTION } ]
        [ NOT FOR REPLICATION ]
  
    | CHECK [ NOT FOR REPLICATION ] ( logical_expression )
]
  
<column_set_definition> ::=
column_set_name XML COLUMN_SET FOR ALL_SPARSE_COLUMNS
  
< table_constraint > ::=
[ CONSTRAINT constraint_name ]
{
    { PRIMARY KEY | UNIQUE }
        [ CLUSTERED | NONCLUSTERED ]
        (column [ ASC | DESC ] [ ,...n ] )
        [
            WITH FILLFACTOR = fillfactor
           |WITH ( <index_option> [ , ...n ] )
        ]
        [ ON { partition_scheme_name (partition_column_name)
            | filegroup | "default" } ]
    | FOREIGN KEY
        ( column [ ,...n ] )
        REFERENCES referenced_table_name [ ( ref_column [ ,...n ] ) ]
        [ ON DELETE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]
        [ ON UPDATE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]
        [ NOT FOR REPLICATION ]
    | CHECK [ NOT FOR REPLICATION ] ( logical_expression )

< table_index > ::=
{  
    {  
      INDEX index_name  [ UNIQUE ] [ CLUSTERED | NONCLUSTERED ]
         (column_name [ ASC | DESC ] [ ,... n ] )
    | INDEX index_name CLUSTERED COLUMNSTORE
    | INDEX index_name [ NONCLUSTERED ] COLUMNSTORE (column_name [ ,... n ] )
    }
    [ WITH ( <index_option> [ ,... n ] ) ]
    [ ON { partition_scheme_name (column_name )
         | filegroup_name
         | default
         }
    ]
    [ FILESTREAM_ON { filestream_filegroup_name | partition_scheme_name | "NULL" } ]
  
}

<table_option> ::=
{  
    [DATA_COMPRESSION = { NONE | ROW | PAGE }
      [ ON PARTITIONS ( { <partition_number_expression> | <range> }
      [ , ...n ] ) ]]
    [ FILETABLE_DIRECTORY = <directory_name> ]
    [ FILETABLE_COLLATE_FILENAME = { <collation_name> | database_default } ]
    [ FILETABLE_PRIMARY_KEY_CONSTRAINT_NAME = <constraint_name> ]
    [ FILETABLE_STREAMID_UNIQUE_CONSTRAINT_NAME = <constraint_name> ]
    [ FILETABLE_FULLPATH_UNIQUE_CONSTRAINT_NAME = <constraint_name> ]
    [ SYSTEM_VERSIONING = ON [ ( HISTORY_TABLE = schema_name . history_table_name
        [, DATA_CONSISTENCY_CHECK = { ON | OFF } ] ) ] ]
    [ REMOTE_DATA_ARCHIVE =
      {
          ON [ ( <table_stretch_options> [,...n] ) ]
        | OFF ( MIGRATION_STATE = PAUSED )
      }
    ]
}
  
<table_stretch_options> ::=
{  
    [ FILTER_PREDICATE = { null | table_predicate_function } , ]
      MIGRATION_STATE = { OUTBOUND | INBOUND | PAUSED }
 }
  
<index_option> ::=
{
    PAD_INDEX = { ON | OFF }
  | FILLFACTOR = fillfactor
  | IGNORE_DUP_KEY = { ON | OFF }
  | STATISTICS_NORECOMPUTE = { ON | OFF }
  | STATISTICS_INCREMENTAL = { ON | OFF }
  | ALLOW_ROW_LOCKS = { ON | OFF }
  | ALLOW_PAGE_LOCKS = { ON | OFF }
  | OPTIMIZE_FOR_SEQUENTIAL_KEY = { ON | OFF }
  | COMPRESSION_DELAY= {0 | delay [Minutes]}
  | DATA_COMPRESSION = { NONE | ROW | PAGE | COLUMNSTORE | COLUMNSTORE_ARCHIVE }
       [ ON PARTITIONS ( { <partition_number_expression> | <range> }
       [ , ...n ] ) ]
}
<range> ::=
<partition_number_expression> TO <partition_number_expression>
```

```
-- Memory optimized CREATE TABLE Syntax
CREATE TABLE
    { database_name.schema_name.table_name | schema_name.table_name | table_name }
    ( { <column_definition>
    | [ <table_constraint> ] [ ,... n ]
    | [ <table_index> ]
      [ ,... n ] }
      [ PERIOD FOR SYSTEM_TIME ( system_start_time_column_name
        , system_end_time_column_name ) ]
)
    [ WITH ( <table_option> [ ,... n ] ) ]
 [ ; ]

<column_definition> ::=
column_name <data_type>
    [ COLLATE collation_name ]
    [ GENERATED ALWAYS AS ROW { START | END } [ HIDDEN ] ]
    [ NULL | NOT NULL ]
[
    [ CONSTRAINT constraint_name ] DEFAULT memory_optimized_constant_expression ]
    | [ IDENTITY [ ( 1, 1 ) ]
]
    [ <column_constraint> ]
    [ <column_index> ]
  
<data_type> ::=
 [type_schema_name . ] type_name [ (precision [ , scale ]) ]

<column_constraint> ::=
 [ CONSTRAINT constraint_name ]
{
  { PRIMARY KEY | UNIQUE }
      {   NONCLUSTERED
        | NONCLUSTERED HASH WITH (BUCKET_COUNT = bucket_count)
      }
  | [ FOREIGN KEY ]
        REFERENCES [ schema_name . ] referenced_table_name [ ( ref_column ) ]
  | CHECK ( logical_expression )
}
  
< table_constraint > ::=
 [ CONSTRAINT constraint_name ]
{
   { PRIMARY KEY | UNIQUE }
     {
       NONCLUSTERED (column [ ASC | DESC ] [ ,... n ])
       | NONCLUSTERED HASH (column [ ,... n ] ) WITH ( BUCKET_COUNT = bucket_count )
                    }
    | FOREIGN KEY
        ( column [ ,...n ] )
        REFERENCES referenced_table_name [ ( ref_column [ ,...n ] ) ]
    | CHECK ( logical_expression )
}

<column_index> ::=
  INDEX index_name
{ [ NONCLUSTERED ] | [ NONCLUSTERED ] HASH WITH (BUCKET_COUNT = bucket_count)}

<table_index> ::=
  INDEX index_name
{   [ NONCLUSTERED ] HASH (column [ ,... n ] ) WITH (BUCKET_COUNT = bucket_count)
  | [ NONCLUSTERED ] (column [ ASC | DESC ] [ ,... n ] )
      [ ON filegroup_name | default ]
  | CLUSTERED COLUMNSTORE [WITH ( COMPRESSION_DELAY = {0 | delay [Minutes]})]
      [ ON filegroup_name | default ]
  
}
  
<table_option> ::=
{  
    MEMORY_OPTIMIZED = ON
  | DURABILITY = {SCHEMA_ONLY | SCHEMA_AND_DATA}
  | SYSTEM_VERSIONING = ON [ ( HISTORY_TABLE = schema_name . history_table_name
        [, DATA_CONSISTENCY_CHECK = { ON | OFF } ] ) ]
  
}
```

## <a name="arguments"></a>Argumentos

*database_name* É o nome do banco de dados no qual a tabela é criada. *database_name* precisa especificar o nome de um banco de dados existente. Caso não seja especificado, *database_name* usará o banco de dados atual como padrão. O logon para a conexão atual precisa estar associado a uma ID de usuário existente no banco de dados especificado por *database_name*, e essa ID de usuário precisa ter permissões CREATE TABLE.

*schema_name* É o nome do esquema ao qual a nova tabela pertence.

*table_name* É o nome da nova tabela. Os nomes de tabela precisam seguir as regras para [identificadores](../../relational-databases/databases/database-identifiers.md). *table_name* pode ter no máximo 128 caracteres, exceto para nomes de tabelas temporárias locais [nomes com o prefixo de sinal numérico (#)], que não podem exceder 116 caracteres.

AS FileTable **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior).

Cria a nova tabela como uma FileTable. Você não especifica colunas porque uma FileTable tem um esquema fixo. Para obter mais informações, confira [FileTables](../../relational-databases/blob/filetables-sql-server.md).

*column_name*
*computed_column_expression* É uma expressão que define o valor de uma coluna computada. Uma coluna computada é uma coluna virtual que não está fisicamente armazenada na tabela, a menos que a coluna esteja marcada como PERSISTED. A coluna é computada a partir de uma expressão que usa outras colunas da mesma tabela. Por exemplo, uma coluna computada pode ter a definição **cost** AS **price** \* **qty**. A expressão pode ser o nome de uma coluna não computada, constante, função, variável e qualquer combinação dessas, conectada por um ou mais operadores. A expressão não pode ser uma subconsulta nem conter um tipo de dados do alias.

As colunas computadas podem ser usadas em listas de seleção, cláusulas WHERE, cláusulas ORDER BY ou em qualquer outro local em que expressões regulares possam ser usadas, com as seguintes exceções:

- As colunas computadas devem ser marcadas como PERSISTED para participar de uma restrição FOREIGN KEY ou CHECK.
- Uma coluna computada poderá ser usada como uma coluna de chave em um índice ou como parte de uma restrição PRIMARY KEY ou UNIQUE, se o valor for definido por uma expressão determinística e o tipo de dados do resultado for permitido nas colunas de índice.

   Por exemplo, se a tabela tiver as colunas de inteiros **a** e **b**, a coluna computada **a+b** poderá ser indexada, mas não a coluna computada **a+DATEPART(dd, GETDATE())** , pois o valor poderá ser alterado em chamadas subsequentes.

- Uma coluna computada não pode ser o destino de uma instrução INSERT ou UPDATE.

> [!NOTE]
> Cada linha de uma tabela pode ter valores diferentes para as colunas envolvidas em uma coluna computada; sendo assim, a coluna computada pode não ter o mesmo valor para cada linha.

Com base nas expressões usadas, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] determina automaticamente a nulidade das colunas computadas. O resultado da maioria das expressões será considerado nulo mesmo se somente colunas não nulas estejam presentes, pois a falta de fluxo ou excesso de fluxo produzirá também resultados NULL. Use a função `COLUMNPROPERTY` com a propriedade **AllowsNull** para investigar a nulidade de qualquer coluna computada de uma tabela. Uma expressão que permite valor nulo pode se tornar uma expressão que não permite valor nulo pela especificação de `ISNULL` com a constante *check_expression*, em que a constante é um valor não nulo substituído para qualquer resultado NULL. A permissão REFERENCES no tipo é necessária para colunas computadas com base em expressões do tipo de dados CLR definido pelo usuário.

PERSISTED Especifica que o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] armazenará fisicamente os valores computados na tabela e atualizará os valores quando for atualizada qualquer outra coluna da qual a coluna computada depende. A marcação de uma coluna computada como `PERSISTED` permite a criação de um índice em uma coluna computada que seja determinística, mas não precisa. Para obter mais informações, consulte [Indexes on Computed Columns](../../relational-databases/indexes/indexes-on-computed-columns.md). As colunas computadas usadas como colunas de particionamento de uma tabela particionada precisam ser explicitamente marcadas como `PERSISTED`. *computed_column_expression* precisa ser determinística quando `PERSISTED` é especificado.

ON { *partition_scheme* | *filegroup* |  **"default"** } Especifica o esquema de partição ou o grupo de arquivos no qual a tabela está armazenada. Se *partition_scheme* for especificado, a tabela será uma tabela particionada cujas partições são armazenadas em um conjunto de um ou mais grupos de arquivos especificados em *partition_scheme*. Se *filegroup* for especificado, a tabela será criada no grupo de arquivos nomeado. O grupo de arquivos deve existir no banco de dados. Se **"default"** for especificado ou se ON não for especificado, a tabela será armazenada no grupo de arquivos padrão. O mecanismo de armazenamento de uma tabela como especificado em CREATE TABLE não pode ser alterado posteriormente.

ON {*partition_scheme* | *filegroup* |  **"default"** } também pode ser especificado em uma restrição PRIMARY KEY ou UNIQUE. Essas restrições criam índices. Se *filegroup* for especificado, o índice será armazenado no grupo de arquivos nomeado. Se **"default"** for especificado ou se ON não for especificado, o índice será armazenado no mesmo grupo de arquivos da tabela. Se a restrição `PRIMARY KEY` ou `UNIQUE` criar um índice clusterizado, as páginas de dados da tabela serão armazenadas no mesmo grupo de arquivos do índice. Se `CLUSTERED` for especificado ou se a restrição de outra forma criar um índice clusterizado e for especificado um *partition_scheme* diferente do *partition_scheme* ou do *filegroup* da definição da tabela ou vice-versa, somente a definição da restrição será respeitada e as demais serão ignoradas.

> [!NOTE]
> Nesse contexto, *default* não é uma palavra-chave. É um identificador para o grupo de arquivos padrão e precisa ser delimitado, como em ON **"default"** ou ON **[** default **]** . Se **"default"** é especificado, a opção `QUOTED_IDENTIFIER` deve ser definida como ON na sessão atual. Essa é a configuração padrão. Para saber mais, confira [SET QUOTED_IDENTIFIER](../../t-sql/statements/set-quoted-identifier-transact-sql.md).
>
> Depois de criar uma tabela particionada, considere a configuração da opção `LOCK_ESCALATION` da tabela como `AUTO`. Isso pode melhorar a simultaneidade ao permitir que os bloqueios escalem para o nível da partição (HoBT) em vez da tabela. Para obter mais informações, consulte [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md).

TEXTIMAGE_ON { *filegroup*|  **"default"** } Indica que **text**, **ntext**, **image**, **xml**, **varchar(max)** , **nvarchar(max)** , **varbinary(max)** e colunas do tipo de dado CLR definido pelo usuário (incluindo geometry e geography) são armazenados no grupo de arquivos especificado.

`TEXTIMAGE_ON` não será permitido se não houver colunas de valor grande na tabela. `TEXTIMAGE_ON` não poderá ser especificado se *partition_scheme* for especificado. Se **"default"** for especificado ou se `TEXTIMAGE_ON` não for especificado, as colunas de valores grandes serão armazenadas no grupo de arquivos padrão. O armazenamento de qualquer dado de coluna de valor grande especificado em `CREATE TABLE` não poderá ser alterado posteriormente.

> [!NOTE]
> Varchar(max), nvarchar(max), varbinary(max), xml e valores UDT grandes são armazenados diretamente na linha de dados, até um limite de 8.000 bytes, desde que o valor caiba no registro. Se o valor não se ajustar ao registro, um ponteiro será armazenado na linha e o restante será armazenado fora da linha no espaço de armazenamento de LOB. 0 é o valor padrão, que indica que todos os valores são armazenados diretamente na linha de dados.
>
> `TEXTIMAGE_ON` somente altera o local do "espaço de armazenamento LOB", não afetando o momento em que os dados são armazenados na linha. Use tipos de valor grande sem a opção de linha de sp_tableoption para armazenar todo o valor LOB fora da linha.
>
> Nesse contexto, default não é uma palavra-chave. É um identificador para o grupo de arquivos padrão e precisa ser delimitado, como em `TEXTIMAGE_ON "default"` ou `TEXTIMAGE_ON [default]`. Se **"default"** é especificado, a opção `QUOTED_IDENTIFIER` deve ser definida como ON na sessão atual. Essa é a configuração padrão. Para saber mais, confira [SET QUOTED_IDENTIFIER](../../t-sql/statements/set-quoted-identifier-transact-sql.md).

FILESTREAM_ON { *partition_scheme_name* | filegroup | **"** default **"** } **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] e posterior). [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] não dá suporte para `FILESTREAM`.

Especifica o grupo de arquivos para obter dados de FILESTREAM.

Se a tabela contiver dados FILESTREAM e estiver particionada, a cláusula FILESTREAM_ON deverá ser incluída e especificar um esquema de partição de grupos de arquivos FILESTREAM. Esse esquema de partição deve usar a mesma função de partição e as colunas de partição do esquema de partição da tabela; caso contrário, ocorrerá um erro.

Se a tabela não estiver particionada, a coluna FILESTREAM não poderá ser particionada. Dados FILESTREAM da tabela devem ser armazenados em um único grupo de arquivos. Esse grupo de arquivos é especificado na cláusula FILESTREAM_ON.

Se a tabela não estiver particionada e a cláusula `FILESTREAM_ON` não for especificada, será usado o grupo de arquivos FILESTREAM cuja propriedade `DEFAULT` está definida. Se não houver um grupo de arquivos FILESTREAM, ocorrerá um erro.

Como ocorre com ON e `TEXTIMAGE_ON`, o valor definido por meio `CREATE TABLE` para `FILESTREAM_ON` não pode ser alterado, exceto nos seguintes casos:

- Uma instrução [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md) converte um heap em um índice clusterizado. Nesse caso, um outro grupo de arquivos FILESTREAM, um esquema de partição ou NULL pode ser especificado.
- Uma instrução [DROP INDEX](../../t-sql/statements/drop-index-transact-sql.md) converte um índice clusterizado em um heap. Neste caso, outro grupo de arquivos FILESTREAM, um esquema de partição ou **"default"** pode ser especificado.

O grupo de arquivos da cláusula `FILESTREAM_ON <filegroup>`, ou cada grupo de arquivos FILESTREAM nomeado no esquema de partição, deve ter um arquivo definido para o grupo de arquivos. Esse arquivo deve ser definido usando uma instrução [CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md?view=sql-server-2017) ou [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md); caso contrário, ocorrerá um erro.

Para tópicos sobre FILESTREAM relacionados, veja [Objeto Binário Grande – Dados de Blob](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md).

[ _type\_schema\_name_ **.** ] *type_name* Especifica o tipo de dados da coluna e o esquema ao qual ele pertence. Para tabelas com base em disco, o tipo de dados pode ser um dos seguintes:

- Um tipo de dados do sistema
- Um tipo de alias com base em um tipo de dados do sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os tipos de dados do alias são criados com a instrução `CREATE TYPE` antes que possam ser usados em uma definição de tabela. A atribuição NULL ou NOT NULL para um tipo de dados do alias pode ser substituída durante a instrução `CREATE TABLE`. Contudo, não é possível alterar a especificação do tamanho; o tamanho de um tipo de dados do alias não pode ser especificado na instrução `CREATE TABLE`.
- Um tipo de dados CLR definido pelo usuário. Os tipos de dados CLR definidos pelo usuário são criados com a instrução `CREATE TYPE` antes que possam ser usados em uma definição de tabela. Para criar uma coluna baseada em um tipo de dados CLR definido pelo usuário, é necessária a permissão REFERENCES para o tipo.

Se *type_schema_name* não for especificado, p [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] fará referência a *type_name* na seguinte ordem:

- O tipo de dados de sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
- O esquema padrão do usuário atual no banco de dados atual.
- O esquema **dbo** no banco de dados atual.

Para tabelas com otimização de memória, veja [Tipos de dados compatíveis para OLTP in-memory](../../relational-databases/in-memory-oltp/supported-data-types-for-in-memory-oltp.md) para obter uma lista dos tipos de sistema compatíveis.

*precision* É a precisão do tipo de dados especificado. Para obter mais informações sobre valores de precisão válidos, veja [Precisão, escala e comprimento](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).

*scale* É a escala do tipo de dados especificado. Para obter mais informações sobre valores de escala válidos, veja [Precisão, escala e comprimento](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).

**max** Aplica-se apenas aos tipos de dados **varchar**, **nvarchar** e **varbinary** para armazenar 2^31 bytes de caractere e dados binários e 2^30 bytes de dados Unicode.

CONTENT Especifica que cada instância do tipo de dados **xml** em *column_name* pode conter vários elementos de nível superior. CONTENT aplica-se apenas a tipo de dados **xml** e poderá ser especificado somente se *xml_schema_collection* também for especificado. Caso não seja especificado, CONTENT será o comportamento padrão.

DOCUMENT Especifica que cada instância do tipo de dados **xml** em *column_name* pode conter apenas um elemento de nível superior. DOCUMENT aplica-se apenas a tipo de dados **xml** e poderá ser especificado somente se *xml_schema_collection* também for especificado.

*xml_schema_collection* Aplica-se apenas ao tipo de dados **xml** para associar uma coleção de esquemas XML ao tipo. Antes de digitar uma coluna **xml** em um esquema, o esquema deve ser criado primeiramente no banco de dados com [CREATE XML SCHEMA COLLECTION](../../t-sql/statements/create-xml-schema-collection-transact-sql.md).

DEFAULT Especifica o valor fornecido para a coluna quando um valor não for fornecido explicitamente durante uma inserção. As definições de DEFAULT podem ser aplicadas a qualquer coluna, com exceção daquelas definidas como **timestamp** ou daquelas com a propriedade `IDENTITY`. Se um valor padrão for especificado para uma coluna de tipo definido pelo usuário, o tipo deverá ser compatível com uma conversão implícita de *constant_expression* para o tipo definido pelo usuário. As definições DEFAULT serão removidas quando a tabela for descartada. Somente um valor constante, como uma cadeia de caracteres, uma função de escalar (seja de sistema, definida pelo usuário ou CLR) ou NULL, pode ser usado como padrão. Para manter a compatibilidade com versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um nome de restrição pode ser atribuído a um DEFAULT.

*constant_expression* É uma constante, NULL ou uma função de sistema usada como o valor padrão da coluna.

*memory_optimized_constant_expression* É uma constante, NULL ou uma função de sistema compatível usada como valor padrão para a coluna. Deve haver suporte nos procedimentos armazenados compilados de modo nativo. Para obter mais informações sobre as funções integradas em procedimentos armazenados compilados nativamente, veja [Recursos compatíveis em módulos T-SQL compilados nativamente](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md).

IDENTITY Indica que a nova coluna é uma coluna de identidade. Quando uma nova linha é adicionada à tabela, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] fornece um valor incremental exclusivo para a coluna. Geralmente, as colunas de identidade são usadas com restrições PRIMARY KEY para servir como o identificador exclusivo de linha para a tabela. A propriedade `IDENTITY` pode ser atribuída às colunas **tinyint**, **smallint**, **int**, **bigint**, **decimal(p,0)** ou **numeric(p,0)** . Apenas uma coluna de identidade pode ser criada por tabela. Padrões associados e restrições DEFAULT não podem ser usados com uma coluna de identidade. Devem ser especificados tanto o valor de semente como o de incremento ou nenhum dos dois. Se nenhum for especificado, o padrão será (1,1).

*seed* É o valor usado para a primeira linha carregada na tabela.

*increment* É o valor de incremento adicionado ao valor de identidade da linha anterior carregada.

NOT FOR REPLICATION Na instrução `CREATE TABLE`, a cláusula `NOT FOR REPLICATION` pode ser especificada para a propriedade IDENTITY e para restrições FOREIGN KEY e CHECK. Se essa cláusula for especificada para a propriedade `IDENTITY`, os valores não serão incrementados em colunas de identidade quando os agentes de replicação executarem inserções. Se essa cláusula for especificada para uma restrição, ela não será aplicada quando os agentes de replicação executarem operações insert, update ou delete.

GENERATED ALWAYS AS ROW { START | END } [ HIDDEN ] [ NOT NULL ] **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

Especifica que uma coluna `datetime2` especificada será usada pelo sistema para registrar a hora de início na qual um registro é válido ou a hora de término na qual um registro é válido. A coluna precisa ser definida como `NOT NULL`. Se você tentar especificá-las como `NULL`, o sistema gerará um erro. Se você não especificar explicitamente NOT NULL para uma coluna de período, o sistema definirá a coluna como `NOT NULL` por padrão. Use esse argumento junto com os argumentos `PERIOD FOR SYSTEM_TIME` e `WITH SYSTEM_VERSIONING = ON` para habilitar o controle de versão do sistema em uma tabela. Para saber mais, veja [Temporal Tables](../../relational-databases/tables/temporal-tables.md).

Você pode marcar uma ou ambas as colunas de período com o sinalizador **HIDDEN** para implicitamente ocultar essas colunas, de modo que **SELECT \* FROM** _`<table>`_ não retorne um valor para essas colunas. Por padrão, as colunas de período não ficam ocultas. Para serem usadas, colunas ocultas devem ser explicitamente incluídas em todas as consultas que fazem referência direta à tabela temporal. Para alterar o atributo **HIDDEN** para uma coluna de período existente, **PERIOD** deve ser descartado e recriado com um sinalizador oculto diferente.

INDEX *index_name* [ CLUSTERED | NONCLUSTERED ] (*column_name* [ ASC | DESC ] [ ,... *n* ] ) **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

Especifica a criação de um índice na tabela. Isso pode ser um índice clusterizado ou um índice não clusterizado. O índice conterá as colunas listadas e classificará os dados em ordem crescente ou decrescente.

INDEX *index_name* CLUSTERED COLUMNSTORE **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

Especifica o armazenamento de toda a tabela em formato de coluna com um índice columnstore clusterizado. Isso sempre inclui todas as colunas na tabela. Os dados não estão classificados em ordem alfabética ou numérica, uma vez que as linhas são organizadas para obter benefícios de compactação de columnstore.

INDEX *index_name* [ NONCLUSTERED ] COLUMNSTORE (*column_name* [ ,... *n* ] ) **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

Especifica a criação de um índice não clusterizado columnstore na tabela. A tabela subjacente pode ser um heap rowstore ou um índice clusterizado, ou pode ser um índice columnstore clusterizado. Em todos os casos, a criação de um índice columnstore não clusterizado em uma tabela armazena uma segunda cópia dos dados para as colunas no índice.

O índice columnstore não clusterizado é armazenado e gerenciado como um índice columnstore clusterizado. Isso é chamado de índice columnstore não clusterizado porque as colunas podem ser limitadas e existem como um índice secundário em uma tabela.

ON _partition\_scheme\_name_ **(** _column\_name_ **)** Especifica o esquema de partição que define os grupos de arquivos nos quais as partições de um índice particionado serão mapeadas. O esquema de partição deve existir no banco de dados com a execução de [CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md) ou [ALTER PARTITION SCHEME](../../t-sql/statements/alter-partition-scheme-transact-sql.md). *column_name* especifica a coluna com relação à qual um índice particionado será particionado. Essa coluna precisa corresponder ao tipo de dados, ao comprimento e à precisão do argumento da função de partição que *partition_scheme_name* está usando. *column_name* não é restrito às colunas na definição de índice. Qualquer coluna da tabela base pode ser especificada, exceto que, ao particionar um índice UNIQUE, *column_name* deve ser escolhido entre aqueles usados como chave exclusiva. Essa restrição permite ao [!INCLUDE[ssDE](../../includes/ssde-md.md)] verificar a exclusividade de valores de chave em uma única partição apenas.

> [!NOTE]
> Ao particionar um índice clusterizado não exclusivo, por padrão, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] adiciona a coluna de particionamento à lista de chaves de índices clusterizados, se ela já não estiver especificada. Ao particionar um índice não clusterizado e não exclusivo, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] adiciona a coluna de particionamento como uma coluna não chave (incluída) do índice, se ela já não estiver especificada.

Se *partition_scheme_name* ou *filegroup* não for especificado e a tabela estiver particionada, o índice será colocado no mesmo esquema de partição, usando a mesma coluna de particionamento que a tabela subjacente.

> [!NOTE]
> Não é possível especificar um esquema de particionamento em um índice XML. Se a tabela base for particionada, o índice XML usará o mesmo esquema de partição que a tabela.

Para obter mais informações sobre particionamento de índices, consulte [Tabelas e índices particionados](../../relational-databases/partitions/partitioned-tables-and-indexes.md).

ON *filegroup_name* Cria o índice especificado no grupo de arquivos especificado. Se nenhum local for especificado e a tabela ou exibição não for particionada, o índice usará o mesmo grupo de arquivos que a tabela ou exibição subjacente. O grupo de arquivos já deve existir.

ON **"default"** Cria o índice especificado no grupo de arquivos padrão.

Nesse contexto, default não é uma palavra-chave. É um identificador para o grupo de arquivos padrão e precisa ser delimitado, como em ON **"default"** ou ON **[default]** . Se "default" é especificado, a opção `QUOTED_IDENTIFIER` deve ser definida como ON na sessão atual. Essa é a configuração padrão. Para saber mais, confira [SET QUOTED_IDENTIFIER](../../t-sql/statements/set-quoted-identifier-transact-sql.md).

[ FILESTREAM_ON { *filestream_filegroup_name* | *partition_scheme_name* | "NULL" } ] **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] e posterior).

Especifica a colocação de dados FILESTREAM para a tabela quando um índice clusterizado é criado. A cláusula FILESTREAM_ON permite mover os dados FILESTREAM para outro grupo de arquivos ou esquema de partição FILESTREAM.

*filestream_filegroup_name* é o nome de um grupo de arquivos FILESTREAM. O grupo de arquivos deve ter um arquivo definido para o grupo de arquivos usando uma instrução [CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md) ou [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md); caso contrário, será gerado um erro.

Se a tabela for particionada, a cláusula `FILESTREAM_ON` precisará ser incluída e especificar um esquema de partição de grupos de arquivos FILESTREAM que use a mesma função de partição e as mesmas colunas de partição do esquema de partição da tabela. Caso contrário, será gerado um erro.

Se a tabela não estiver particionada, a coluna FILESTREAM não poderá ser particionada. Os dados FILESTREAM da tabela precisam ser armazenados em um único grupo de arquivos que é especificado na cláusula `FILESTREAM_ON`.

`FILESTREAM_ON NULL` poderá ser especificado em uma instrução `CREATE INDEX` se um índice clusterizado estiver sendo criado e a tabela não contiver uma coluna FILESTREAM.

Para obter mais informações, veja [FILESTREAM](../../relational-databases/blob/filestream-sql-server.md).

ROWGUIDCOL Indica que a nova coluna é uma coluna GUID de linha. Somente uma coluna **uniqueidentifier** por tabela pode ser designada como a coluna ROWGUIDCOL. A aplicação da propriedade ROWGUIDCOL permite que a coluna seja referenciada usando `$ROWGUID`. A propriedade ROWGUIDCOL pode ser atribuída somente a uma coluna **uniqueidentifier**. As colunas de tipo de dados definido pelo usuário não podem ser designadas com ROWGUIDCOL.

A propriedade ROWGUIDCOL não impõe exclusividade dos valores armazenados na coluna. ROWGUIDCOL também não gera automaticamente valores para novas linhas inseridas na tabela. Para gerar valores exclusivos para cada coluna, use a função [NEWID](../../t-sql/functions/newid-transact-sql.md) ou [NEWSEQUENTIALID](../../t-sql/functions/newsequentialid-transact-sql.md) em instruções [INSERT](../../t-sql/statements/insert-transact-sql.md) ou use essas funções como o padrão para a coluna.

ENCRYPTED WITH Especifica as colunas de criptografia usando o recurso [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md).

COLUMN_ENCRYPTION_KEY = *key_name* Especifica a chave de criptografia de coluna. Para obter mais informações, veja [CREATE COLUMN ENCRYPTION KEY](../../t-sql/statements/create-column-encryption-key-transact-sql.md).

ENCRYPTION_TYPE = { DETERMINISTIC | RANDOMIZED } **Criptografia determinística** usa um método que sempre gera o mesmo valor criptografado para qualquer valor de texto sem formatação. Usar criptografia determinística permite pesquisar usando comparação de igualdade, agrupamento e junção de tabelas usando junções de igualdade baseadas em valores criptografados, mas também pode permitir que usuários não autorizados adivinhem informações sobre valores criptografados examinando padrões na coluna criptografada. A união de duas tabelas em colunas criptografadas de maneira determinística só é possível se ambas as colunas são criptografadas com a mesma chave de criptografia de coluna. A criptografia determinística deve usar uma ordenação de colunas com uma ordem de classificação binary2 para as colunas de caracteres.

**Criptografia aleatória** usa um método que criptografa os dados de uma maneira menos previsível. A criptografia aleatória é mais segura, mas impede que cálculos e indexação sejam feitos em colunas criptografadas, a menos que sua instância do SQL Server tenha suporte para Always Encrypted com enclaves seguros. Veja [Always Encrypted com enclaves seguros](../../relational-databases/security/encryption/always-encrypted-enclaves.md) para obter detalhes.

Se você estiver usando o Always Encrypted (sem enclaves seguros), use a criptografia determinística para colunas que serão pesquisadas com parâmetros ou com parâmetros de agrupamento, por exemplo, um número de identificação do governo. Use criptografia randomizada, para dados como número de cartão de crédito, que não é agrupada a outros registros nem usada para unir tabelas, e não é pesquisada porque você usa outras colunas (como número de transações) para localizar a linha que contém a coluna criptografada de interesse.

Se você está usando o Always Encrypted com enclaves seguros, a criptografia aleatória é um tipo de criptografia recomendado.

As colunas devem ser de um tipo de dados qualificado.

ALGORITHM **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior).

Deve ser **'AEAD_AES_256_CBC_HMAC_SHA_256'** .

Para mais informações, incluindo restrições de recursos, veja [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md).

SPARSE Indica que a coluna é uma coluna esparsa. O armazenamento de colunas esparsas é otimizado para obter valores nulos. Colunas esparsas não podem ser designadas como NOT NULL. Para obter restrições adicionais e mais informações sobre colunas esparsas, consulte [Usar colunas esparsas](../../relational-databases/tables/use-sparse-columns.md).

MASKED WITH ( FUNCTION = ' *mask_function* ') **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior).

Especifica uma máscara de dados dinâmicos. *mask_function* é o nome da função de mascaramento com os parâmetros apropriados. Quatro funções estão disponíveis:

- default()
- email()
- partial()
- random()

Para parâmetros de função, consulte [Máscara de Dados Dinâmicos](../../relational-databases/security/dynamic-data-masking.md).

FILESTREAM **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] e posterior)

Válido somente para colunas **varbinary(max)** . Especifica o armazenamento FILESTREAM para dados de BLOB **varbinary(max)** .

A tabela também deve ter uma coluna do tipo de dados **uniqueidentifier** com o atributo ROWGUIDCOL. Essa coluna não deve permitir valores nulos e deve ter uma restrição de coluna única UNIQUE ou PRIMARY KEY. O valor de GUID da coluna deve ser fornecido por um aplicativo ao inserir dados ou por uma restrição DEFAULT que usa a função NEWID ().

A coluna ROWGUIDCOL não pode ser descartada e as restrições relacionadas não podem ser alteradas enquanto houver uma coluna FILESTREAM definida para a tabela. A coluna ROWGUIDCOL poderá ser descartada somente depois que a última coluna FILESTREAM for descartada.

Quando o atributo de armazenamento FILESTREAM é especificado para uma coluna, todos os valores da coluna são armazenados em um contêiner de dados FILESTREAM no sistema de arquivos.

COLLATE *collation_name* Especifica a ordenação da coluna. O nome da ordenação tanto pode ser um nome de ordenação do Windows como um nome de ordenação SQL. *collation_name* é aplicável somente a colunas dos tipos de dados **char**, **varchar**, **text**, **nchar**, **nvarchar** e **ntext**. Se não for especificado, à coluna será atribuída a ordenação do tipo de dados definido pelo usuário, se a coluna for de um tipo de dados definido pelo usuário, ou a ordenação do banco de dados atual.

Para obter mais informações sobre os nomes de ordenação do Windows e do SQL, consulte [Nome de ordenação do Windows](../../t-sql/statements/windows-collation-name-transact-sql.md) e [Nome de ordenação do SQL](../../t-sql/statements/sql-server-collation-name-transact-sql.md).

Para obter mais informações, consulte [COLLATE](~/t-sql/statements/collations.md).

CONSTRAINT É uma palavra-chave opcional que indica o início da definição de uma restrição PRIMARY KEY, NOT NULL, UNIQUE, FOREIGN KEY ou CHECK.

*constraint_name* É o nome de uma restrição. Nomes de restrição devem ser exclusivos no esquema ao qual a tabela pertence.

NULL | NOT NULL Determinam se são permitidos valores nulos na coluna. NULL não é estritamente uma restrição, mas pode ser especificado simplesmente como NOT NULL. NOT NULL poderá ser especificado para colunas computadas somente se PERSISTED também for especificado.

PRIMARY KEY É uma restrição que impõe integridade de entidade para uma ou mais colunas especificadas por meio de um índice exclusivo. Somente uma restrição PRIMARY KEY pode ser criada por tabela.

UNIQUE É uma restrição que fornece integridade de entidade para uma coluna ou colunas especificadas por meio de um índice exclusivo. Uma tabela pode ter várias restrições UNIQUE.

CLUSTERED | NONCLUSTERED Indica que um índice clusterizado ou não clusterizado será criado para a restrição PRIMARY KEY ou UNIQUE. O padrão das restrições PRIMARY KEY é CLUSTERED e das restrições UNIQUE é NONCLUSTERED.

Em uma instrução `CREATE TABLE`, CLUSTERED pode ser especificado apenas para uma restrição. Se CLUSTERED for especificado para uma restrição UNIQUE e uma restrição PRIMARY KEY também for especificada, PRIMARY KEY adotará o padrão de NONCLUSTERED.

FOREIGN KEY REFERENCES É uma restrição que fornece integridade referencial para os dados na coluna ou colunas. As restrições FOREIGN KEY requerem que cada valor na coluna exista na coluna ou colunas referenciadas correspondentes na tabela referenciada. As restrições FOREIGN KEY podem fazer referência somente a colunas que sejam restrições PRIMARY KEY ou UNIQUE na tabela ou colunas referenciadas em um UNIQUE INDEX na tabela referenciada. As chaves estrangeiras em colunas computadas também devem ser marcadas como PERSISTED.

[ _schema\_name_ **.** ] *referenced_table_name*] É o nome da tabela referenciada pela restrição FOREIGN KEY e o esquema ao qual ela pertence.

**(** *ref_column* [ **,** ... *n* ] **)** É uma coluna, ou lista de colunas, da tabela referenciada pela restrição FOREIGN KEY.

ON DELETE { **NO ACTION** | CASCADE | SET NULL | SET DEFAULT } Especifica qual ação ocorrerá nas linhas da tabela criada se essas linhas tiverem uma relação referencial e a linha referenciada for excluída da tabela pai. O padrão é NO ACTION.

NO ACTION O [!INCLUDE[ssDE](../../includes/ssde-md.md)] gera um erro e a ação de excluir na linha da tabela pai é revertida.

CASCADE As linhas correspondentes serão excluídas da tabela de referência se aquela linha for excluída da tabela pai.

SET NULL Todos os valores que compõem a chave estrangeira serão definidos como NULL se a linha correspondente na tabela pai for excluída. Para que essa restrição seja executada, as colunas de chave estrangeira devem ser anuláveis.

SET DEFAULT Todos os valores que compõem a chave estrangeira serão definidos com seus valores padrão se a linha correspondente na tabela pai for excluída. Para que essa restrição seja executada, todas as colunas de chave estrangeira devem ter definições padrão. Se a coluna for anulável e não houver nenhum valor padrão explícito definido, NULL se tornará o valor padrão implícito para a coluna.

Não especifique CASCADE se a tabela for incluída em uma publicação de mesclagem que usa registros lógicos. Para obter mais informações sobre registros lógicos, consulte [Agrupar alterações em linhas relacionadas com registros lógicos](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).

`ON DELETE CASCADE` não poderá ser definido se um `INSTEAD OF` gatilho `ON DELETE` já existir na tabela.

Por exemplo, no banco de dados do [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)], a tabela **ProductVendor** tem uma relação referencial com a tabela **Vendor**. A chave estrangeira **ProductVendor.BusinessEntityID** referencia a chave primária **Vendor.BusinessEntityID**.

Se uma instrução `DELETE` for executada em uma linha da tabela **Vendor** e uma ação `ON DELETE CASCADE` for especificada para **ProductVendor.BusinessEntityID**, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] verificará se há uma ou mais linhas dependentes na tabela **ProductVendor**. Se existir alguma, as linhas dependentes da tabela **ProductVendor** serão excluídas, além da linha referenciada na tabela **Vendor**.

Por outro lado, se `NO ACTION` for especificado, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] gerará um erro e reverterá a ação de exclusão da linha **Vendor**, caso haja, pelo menos, uma linha na tabela **ProductVendor** que a referencie.

ON UPDATE { **NO ACTION** | CASCADE | SET NULL | SET DEFAULT } Especifica qual ação ocorrerá nas linhas da tabela alterada quando essas linhas tiverem uma relação referencial e a linha referenciada for atualizada na tabela pai. O padrão é NO ACTION.

NO ACTION O [!INCLUDE[ssDE](../../includes/ssde-md.md)] gera um erro, e a ação de atualizar na linha da tabela pai é revertida.

CASCADE As linhas correspondentes são atualizadas na tabela de referência quando aquela linha é atualizada na tabela pai.

SET NULL Todos os valores que compõem a chave estrangeira são definidos como NULL quando a linha correspondente na tabela pai é atualizada. Para que essa restrição seja executada, as colunas de chave estrangeira devem ser anuláveis.

SET DEFAULT Todos os valores que compõem a chave estrangeira são definidos como seus valores padrão quando a linha correspondente na tabela pai é atualizada. Para que essa restrição seja executada, todas as colunas de chave estrangeira devem ter definições padrão. Se a coluna for anulável e não houver nenhum valor padrão explícito definido, NULL se tornará o valor padrão implícito para a coluna.

Não especifique `CASCADE` se a tabela for incluída em uma publicação de mesclagem que usa registros lógicos. Para obter mais informações sobre registros lógicos, consulte [Agrupar alterações em linhas relacionadas com registros lógicos](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).

`ON UPDATE CASCADE`, `SET NULL` ou `SET DEFAULT` não poderá ser definido se um `INSTEAD OF` gatilho `ON UPDATE` já existir na tabela que está sendo alterada.

Por exemplo, no banco de dados do [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)], a tabela **ProductVendor** tem uma relação referencial com a tabela **Vendor**: A chave estrangeira **ProductVendor.BusinessEntity** faz referência à chave primária **Vendor.BusinessEntityID**.

Se uma instrução UPDATE for executada em uma linha da tabela **Vendor** e uma ação ON UPDATE CASCADE for especificada para **ProductVendor.BusinessEntityID**, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] verificará se há uma ou mais linhas dependentes na tabela **ProductVendor**. Se existir alguma, as linhas dependentes da tabela **ProductVendor** serão atualizadas, além da linha referenciada na tabela **Vendor**.

De modo inverso, se NO ACTION for especificada, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] gerará um erro e reverterá a ação de atualização da linha **Vendor** se houver pelo menos uma linha da tabela **ProductVendor** que a referencie.

CHECK É uma restrição que impõe a integridade de domínio limitando os possíveis valores que podem ser inseridos em uma ou mais colunas. As restrições CHECK em colunas computadas também devem ser marcadas como PERSISTED.

*logical_expression* é uma expressão lógica que retorna TRUE ou FALSE. Tipos de dados do alias não podem fazer parte da expressão.

*column* É uma coluna ou uma lista de colunas, entre parênteses, usada em restrições de tabela para indicar as colunas usadas na definição da restrição.

[ **ASC** | DESC ] Especifica a ordem na qual a coluna ou colunas que participam de restrições de tabela são classificadas. O padrão é ASC.

*partition_scheme_name* É o nome do esquema de partição que define os grupos de arquivos sobre os quais as partições de uma tabela particionada serão mapeadas. O esquema de partição deve existir no banco de dados.

[ _partition\_column\_name_ **.** ] Especifica a coluna que servirá de base para o particionamento de uma tabela particionada. A coluna deve corresponder àquela especificada na função de partição que *partition_scheme_name* está usando em termos de tipo de dados, comprimento e precisão. Uma coluna computada que participa de uma função de partição deve ser marcada explicitamente como PERSISTED.

> [!IMPORTANT]
> Recomendamos a especificação de NOT NULL na coluna de particionamento das tabelas particionadas e também de tabelas não particionadas que servem de origem e destino para as operações ALTER TABLE...SWITCH. Isso garante que toda restrição CHECK de colunas de particionamento não terão que verificar se existem valores nulos.

WITH FILLFACTOR **=** _fillfactor_ Especifica o quanto o [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve preencher cada página de índice usada para armazenar os dados de índice. Os valores de *fillfactor* especificados pelo usuário podem ser de 1 a 100. Se um valor não for especificado, o padrão será 0. Os valores de fator de preenchimento 0 e 100 são iguais em todos os aspectos.

> [!IMPORTANT]
> A documentação de WITH FILLFACTOR = *fillfactor* como a única opção de índice aplicável às restrições PRIMARY KEY ou UNIQUE é mantida para fins de compatibilidade com versões anteriores, mas não será documentada dessa maneira em versões futuras.

*column_set_name* XML COLUMN_SET FOR ALL_SPARSE_COLUMNS É o nome da coluna de conjunto. Um conjunto de colunas é uma representação em XML sem-tipo que combina todas as colunas esparsas de uma tabela em uma saída estruturada. Para obter mais informações sobre conjuntos de colunas, veja [Usar conjuntos de colunas](../../relational-databases/tables/use-column-sets.md).

PERIOD FOR SYSTEM_TIME (*system_start_time_column_name* , *system_end_time_column_name* ) **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

Especifica os nomes das colunas que o sistema usará para registrar o período para o qual um registro é válido. Use esse argumento junto com os argumentos GENERATED ALWAYS AS ROW { START | END } e WITH SYSTEM_VERSIONING = ON para habilitar o controle de versão do sistema em uma tabela. Para saber mais, veja [Temporal Tables](../../relational-databases/tables/temporal-tables.md).

COMPRESSION_DELAY **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

Para uma otimização de memória, atraso especifica o número mínimo de minutos que uma linha deve permanecer na tabela, inalterada, antes de ser elegível para compactação no índice columnstore. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seleciona linhas específicas a serem compactadas de acordo com a hora da última atualização. Por exemplo, se as linhas estiverem sendo alteradas com frequência durante um período de duas horas, você poderá definir `COMPRESSION_DELAY = 120 Minutes` para garantir que as atualizações sejam concluídas antes de o SQL Server compactar a linha.

Para uma tabela baseada em disco, o atraso especifica o número mínimo de minutos que um rowgroup delta no estado CLOSED precisa permanecer no rowgroup delta antes que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possa compactá-lo no rowgroup compactado. Como as tabelas baseadas em disco não controlam os tempos de inserção e atualização em linhas individuais, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aplica o atraso aos rowgroups delta no estado CLOSED.

O padrão é 0 minuto.

Para obter recomendações sobre quando usar `COMPRESSION_DELAY`, confira [Introdução ao Columnstore para análise operacional em tempo real](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)

\< table_option> :: = especifica uma ou mais opções de tabela.

DATA_COMPRESSION Especifica a opção de compactação de dados para a tabela, o número de partição ou o intervalo de partições especificado. As opções são as descritas a seguir:

NONE A tabela ou as partições especificadas não são compactadas.

ROW A tabela ou as partições especificadas são compactadas usando a compactação de linha.

PAGE A tabela ou as partições especificadas são compactadas usando a compactação de página.

COLUMNSTORE

**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

Aplica-se somente a índices columnstore, incluindo índices columnstore não clusterizados e clusterizados. COLUMNSTORE especifica para compactar com a compactação columnstore de maior desempenho. Essa é a opção típica.

COLUMNSTORE_ARCHIVE **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

Aplica-se somente a índices columnstore, incluindo índices columnstore não clusterizados e clusterizados. COLUMNSTORE_ARCHIVE compactará ainda mais a tabela ou a partição para um tamanho menor. Isso pode ser usado para fins de arquivamento, ou em outras situações que exijam menos armazenamento e possam dispensar mais tempo para armazenamento e recuperação.

Para saber mais, veja [Data Compression](../../relational-databases/data-compression/data-compression.md).

ON PARTITIONS **(** { `<partition_number_expression>` | [ **,** ...*n* ] **)** Especifica as partições às quais se aplica a configuração DATA_COMPRESSION. Se a tabela não for particionada, o argumento `ON PARTITIONS` ON PARTITIONS gerará um erro. Se a cláusula `ON PARTITIONS` não for fornecida, a opção `DATA_COMPRESSION` será aplicada a todas as partições de uma tabela particionada.

*partition_number_expression* pode ser especificado das seguintes maneiras:

- Forneça o número de uma partição, por exemplo: `ON PARTITIONS (2)`
- Forneça os números de várias partições individuais separados por vírgulas, por exemplo: `ON PARTITIONS (1, 5)`
- Forneça os intervalos e as partições individuais, por exemplo: `ON PARTITIONS (2, 4, 6 TO 8)`

`<range>` pode ser especificado como números de partição separados pela palavra TO, por exemplo: `ON PARTITIONS (6 TO 8)`.

Para definir tipos diferentes de compactação de dados para partições diferentes, especifique a opção `DATA_COMPRESSION` mais de uma vez, por exemplo:

```sql
WITH
(
    DATA_COMPRESSION = NONE ON PARTITIONS (1),
    DATA_COMPRESSION = ROW ON PARTITIONS (2, 4, 6 TO 8),
    DATA_COMPRESSION = PAGE ON PARTITIONS (3, 5)
)
```

\<index_option> ::= Especifica uma ou mais opções de índice. Para obter uma descrição completa dessas opções, consulte [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md).

PAD_INDEX = { ON | **OFF** } Quando ON, o percentual de espaço livre especificada por FILLFACTOR será aplicada às páginas de nível intermediário do índice. Quando OFF ou se o valor de FILLFACTOR não foi especificado, as páginas de nível intermediário são preenchidas até próximo de sua capacidade, deixando espaço suficiente para pelo menos uma linha do tamanho máximo que o índice pode ter, considerando o conjunto de chaves em páginas intermediárias. O padrão é OFF.

FILLFACTOR **=** _fillfactor_ Especifica um percentual que indica quanto [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve preencher o nível folha de cada página de índice durante a criação ou alteração do índice. *fillfactor* deve ser um valor inteiro de 1 a 100. O padrão é 0. Os valores de fator de preenchimento 0 e 100 são iguais em todos os aspectos.

IGNORE_DUP_KEY = { ON | **OFF** } Essa opção especifica a resposta de erro quando uma operação de inserção tenta inserir valores da chave duplicada em um índice exclusivo. A opção IGNORE_DUP_KEY aplica-se apenas a operações de inserção depois que o índice é criado ou recriado. A opção não tem nenhum efeito ao executar [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md), [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) ou [UPDATE](../../t-sql/queries/update-transact-sql.md). O padrão é OFF.

ON Uma mensagem de aviso será exibida quando valores de chave duplicados forem inseridos em um índice exclusivo. Ocorrerá falha somente nas linhas que violarem a restrição de exclusividade.

OFF Ocorrerá uma mensagem de erro quando os valores de chave duplicados forem inseridos em um índice exclusivo. Toda a operação INSERT será revertida.

`IGNORE_DUP_KEY` não pode ser definido como ON para índices criados em uma exibição, índices não exclusivos, índices XML, índices espaciais e índices filtrados.

Para exibir `IGNORE_DUP_KEY`, use [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).

Na sintaxe compatível com versões anteriores, `WITH IGNORE_DUP_KEY` é equivalente a `WITH IGNORE_DUP_KEY = ON`.

STATISTICS_NORECOMPUTE **=** { ON | **OFF** } Quando ON, as estatísticas de índice desatualizadas não são recalculadas automaticamente. Quando OFF, a atualização automática de estatísticas será habilitada. O padrão é OFF.

ALLOW_ROW_LOCKS **=** { **ON** | OFF } Quando ON, bloqueios de linha são permitidos ao acessar o índice. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] determina quando os bloqueios de linha são usados. No caso de OFF, não são usados bloqueios de linha. O padrão é ON.

ALLOW_PAGE_LOCKS **=** { **ON** | OFF } Quando ON, bloqueios de página são permitidos ao acessar o índice. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] determina quando os bloqueios de página são usados. Quando definidos como OFF, os bloqueios de página não são usados. O padrão é ON.

OPTIMIZE_FOR_SEQUENTIAL_KEY = { ON | **OFF** } **Se aplica ao**: [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] e a versões posteriores. <BR>
Especifica se a contenção de inserção de última página será ou não otimizada. O padrão é OFF. Para saber mais, confira a seção [Chaves sequenciais](./create-index-transact-sql.md#sequential-keys) da página CREATE INDEX.

FILETABLE_DIRECTORY = *directory_name*

**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior).

Especifica o nome do diretório FileTable compatível com Windows. Esse nome deve ser exclusivo entre todos os nomes de diretórios de FileTable no banco de dados. A comparação de exclusividade não diferencia maiúsculas de minúsculas, independentemente das configurações de ordenação. Se esse valor não for especificado, o nome de filetable será usado.

FILETABLE_COLLATE_FILENAME = { *collation_name* | database_default }

**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior). [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] não dá suporte para `FILETABLE`.

Especifica o nome da ordenação a ser aplicado à coluna **Name** da FileTable. A ordenação não deve diferenciar maiúsculas de minúsculas para ser compatível com a semântica de nomenclatura de arquivos do sistema operacional Windows. Se esse valor não for especificado, a ordenação padrão do banco de dados será usada. Se a ordenação padrão do banco de dados diferenciar maiúsculas de minúsculas, será gerado um erro e a operação CREATE TABLE falhará.

*collation_name* O nome de uma ordenação que não diferencia maiúsculas de minúsculas.

database_default Especifica que a ordenação padrão do banco de dados deve ser usada. Esse ordenação não deve diferenciar maiúsculas de minúsculas.

FILETABLE_PRIMARY_KEY_CONSTRAINT_NAME = *nome_da_restrição*
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior).

Especifica o nome a ser usado para a restrição de chave primária que é criada automaticamente no FileTable. Se esse valor não for especificado, o sistema gerará um nome para a restrição.

FILETABLE_STREAMID_UNIQUE_CONSTRAINT_NAME = *nome_da_restrição*
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior).

Especifica o nome a ser usado para a restrição exclusiva criada automaticamente na coluna **stream_id** na FileTable. Se esse valor não for especificado, o sistema gerará um nome para a restrição.

FILETABLE_FULLPATH_UNIQUE_CONSTRAINT_NAME = *nome_da_restrição*
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior).

Especifica o nome a ser usado para a restrição exclusiva criada automaticamente nas colunas **parent_path_locator** e **name** na FileTable. Se esse valor não for especificado, o sistema gerará um nome para a restrição.

SYSTEM_VERSIONING **=** ON [ ( HISTORY_TABLE **=** *schema_name* .*history_table_name* [, DATA_CONSISTENCY_CHECK **=** { **ON** | OFF } ] ) ] **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]).

Habilitará o controle de versão do sistema da tabela se o tipo de dados, a restrição de nulidade e os requisitos de restrição de chave primária forem atendidos. Se o argumento `HISTORY_TABLE` não for usado, o sistema gerará uma nova tabela de histórico correspondendo ao esquema da tabela atual no mesmo grupo de arquivos da tabela atual, criando um vínculo entre as duas tabelas e permitindo que o sistema registre o histórico de cada registro da tabela atual na tabela de histórico. O nome desta tabela de histórico será `MSSQL_TemporalHistoryFor<primary_table_object_id>`. Por padrão, a tabela de histórico é **PAGE** compactado. Se o argumento `HISTORY_TABLE` for usado para criar um vínculo e usar uma tabela de histórico existente, o vínculo será criado entre a tabela atual e a tabela especificada. Se a tabela atual estiver particionada, a tabela de histórico será criada no grupo de arquivos padrão porque a configuração de particionamento não será replicada automaticamente da tabela atual para a tabela de histórico. Se o nome de uma tabela de histórico estiver especificado durante a criação da tabela de histórico, você deverá especificar o nome do esquema e da tabela. Ao criar um link para uma tabela de histórico existente, você pode optar por executar uma verificação de consistência de dados. Essa verificação de consistência de dados garante que os registros existentes não se sobreponham. A execução da verificação de consistência dos dados é o padrão. Use esse argumento junto com os argumentos `PERIOD FOR SYSTEM_TIME` e `GENERATED ALWAYS AS ROW { START | END }` para habilitar o controle de versão do sistema em uma tabela. Para saber mais, veja [Temporal Tables](../../relational-databases/tables/temporal-tables.md).

REMOTE_DATA_ARCHIVE = { ON [ ( *table_stretch_options* [,...n] ) ] | OFF ( MIGRATION_STATE = PAUSED ) } **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior).

Cria a nova tabela com o Stretch Database habilitado ou desabilitado. Para obter mais informações, consulte [Stretch Database](../../sql-server/stretch-database/stretch-database.md).

**Habilitar o Stretch Database para uma tabela**

Quando você habilitar Stretch para uma tabela especificando `ON`, pode opcionalmente especificar `MIGRATION_STATE = OUTBOUND` para começar a migração de dados imediatamente ou `MIGRATION_STATE = PAUSED` para adiar a migração de dados. O valor padrão é `MIGRATION_STATE = OUTBOUND`. Para obter mais informações sobre como habilitar o Stretch para uma tabela, consulte [Habilitar o Stretch Database para uma tabela](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md).

**Pré-requisitos**. Antes de habilitar o Stretch para uma tabela, você precisa habilitar o Stretch no servidor e no banco de dados. Para obter mais informações, consulte [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md).

**Permissões**. Habilitar o Stretch para um banco de dados ou uma tabela exige permissões db_owner. Habilitar o Stretch em uma tabela também requer permissões ALTER na tabela.

[ FILTER_PREDICATE = { null | *predicate* } ] **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior).

Opcionalmente, especifique um predicado de filtro para selecionar linhas para migrar de uma tabela que contém dados atuais e históricos. O predicado deve chamar uma função com valor de tabela embutido determinística. Para obter mais informações, veja [Habilitar Stretch Database para uma tabela](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md) e [Selecionar linhas a serem migradas usando uma função de filtro](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md).

> [!IMPORTANT]
> Se você fornecer um predicado de filtro precário, a migração de dados também será precária. O Stretch Database aplica o predicado de filtro à tabela usando o operador CROSS APPLY.

Se você não especificar um predicado de filtro, a tabela inteira será migrada.

Quando você especifica um predicado de filtro, também precisa especificar *MIGRATION_STATE*.

MIGRATION_STATE = { OUTBOUND | INBOUND | PAUSED } **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

- Especifique `OUTBOUND` para migrar dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].
- Especifique `INBOUND` para copiar os dados remotos na tabela do [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] novamente para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e para desabilitar o Stretch na tabela. Para obter mais informações, consulte [Desabilitar Stretch Database e trazer de volta dados remotos](../../sql-server/stretch-database/disable-stretch-database-and-bring-back-remote-data.md).

   Essa operação incorre em custos de transferência de dados e não pode ser cancelada.

- Especifique `PAUSED` para pausar ou adiar a migração de dados. Para obter mais informações, veja [Pausar e retomar a migração de dados – Stretch Database](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md).

MEMORY_OPTIMIZED **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]). A instância gerenciada do [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] não dá suporte a tabelas otimizadas para memória.

O valor ON indica que a tabela é otimizada para memória. Tabelas com otimização de memória são parte do recurso de OLTP in-memory, que é usado para otimização de desempenho do processamento de transações. Para começar com o OLTP in-memory, confira [Início Rápido 1: tecnologias do OLTP in-memory para um desempenho mais rápido do Transact-SQL](../../relational-databases/in-memory-oltp/survey-of-initial-areas-in-in-memory-oltp.md). Para obter informações mais detalhadas sobre as tabelas com otimização de memória, veja [Tabelas com otimização de memória](../../relational-databases/in-memory-oltp/memory-optimized-tables.md).

O valor padrão OFF indica que a tabela é baseada em disco.

DURABILITY **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

O valor de `SCHEMA_AND_DATA` indica que a tabela é durável, o que significa que as alterações são persistidas em disco e sobrevivem à reinicialização ou ao failover. SCHEMA_AND_DATA é o valor padrão.

O valor de `SCHEMA_ONLY` indica que a tabela é não durável. O esquema da tabela é mantido, mas as atualizações de dados não são mantidas após uma reinicialização ou failover do banco de dados. `DURABILITY = SCHEMA_ONLY` só é permitido com `MEMORY_OPTIMIZED = ON`.

> [!WARNING]
> Quando uma tabela for criada com **DURABILITY = SCHEMA_ONLY**, e **READ_COMMITTED_SNAPSHOT** depois forem alterado usando **ALTER DATABASE**, os dados na tabela serão perdidos.

BUCKET_COUNT **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

Indica o número de buckets que devem ser criados no índice de hash. O valor máximo para BUCKET_COUNT em índices de hash é 1.073.741.824. Para obter mais informações sobre o número de buckets, veja [Índices para tabelas com otimização de memória](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md).

Bucket_count é um argumento obrigatório.

INDEX **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

Índices de coluna e tabela podem ser especificados como parte da instrução CREATE TABLE. Para obter detalhes sobre como adicionar e remover índices em tabelas com otimização de memória, confira: [Alterando tabelas com otimização de memória](../../relational-databases/in-memory-oltp/altering-memory-optimized-tables.md)

HASH **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

Indica que um índice de HASH foi criado.

Os índices de hash têm suporte apenas em tabelas com otimização de memória.

## <a name="remarks"></a>Comentários

Para obter informações sobre o número de tabelas, colunas, restrições e índices permitidos, veja [Especificações de capacidade máxima para o SQL Server](../../sql-server/maximum-capacity-specifications-for-sql-server.md).

Geralmente, o espaço é alocado a tabelas e índices em incrementos de uma extensão por vez. Quando a opção `SET MIXED_PAGE_ALLOCATION` de `ALTER DATABASE` é definida como TRUE ou sempre antes de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], quando uma tabela ou um índice é criado, são alocadas páginas de extensões mistas até que haja páginas suficientes para preencher uma extensão uniforme. Quando houver páginas suficiente para preencher um extensão uniforme, outra extensão será alocada sempre que as extensões já alocadas ficarem cheias. Para um obter um relatório sobre a quantidade de espaço alocado e usado por uma tabela, execute `sp_spaceused`.

O [!INCLUDE[ssDE](../../includes/ssde-md.md)] não impõe uma ordem para especificar DEFAULT, IDENTITY, ROWGUIDCOL ou restrições de coluna em uma definição de coluna.

Quando uma tabela é criada, a opção QUOTED IDENTIFIER sempre é armazenada como ON nos metadados da tabela, mesmo que a opção esteja definida como OFF quando a tabela é criada.

## <a name="temporary-tables"></a>Tabelas temporárias

Você pode criar tabelas temporárias locais e globais. Tabelas temporárias locais são visíveis apenas na sessão atual e tabelas temporárias globais são visíveis em todas as sessões. Não é possível particionar tabelas temporárias.

Prefixe os nomes de tabelas temporárias locais usando um único sinal numérico (#*table_name*) e prefixe os nomes de tabelas temporárias globais com dois sinais numéricos (##*table_name*).

As instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] referenciam a tabela temporária usando o valor especificado para *table_name* na instrução `CREATE TABLE`, por exemplo:

```sql
CREATE TABLE #MyTempTable (
    col1 INT PRIMARY KEY
);

INSERT INTO #MyTempTable
VALUES (1);
```

Se mais de uma tabela temporária for criada em um procedimento armazenado ou lote, elas devem ter nomes diferentes.

Se você incluir um *schema_name* quando criar ou acessar uma tabela temporária, ele será ignorado. Todas as tabelas temporárias são criadas no esquema dbo.

Se uma tabela temporária local for criada em um procedimento armazenado ou aplicativo que pode ser executado ao mesmo tempo por vários usuários, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve ser capaz de distinguir as tabelas criadas por usuários distintos. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] faz isso acrescentando internamente um sufixo numérico a cada nome de tabela temporária local. O nome completo de uma tabela temporária como ele foi armazenado na tabela **sysobjects** em **tempdb** é composto pelo nome da tabela especificado na instrução CREATE TABLE e o sufixo numérico gerado pelo sistema. Para permitir o sufixo, o *table_name* especificado para um nome temporário local não pode exceder 116 caracteres.

As tabelas temporárias serão descartadas automaticamente se não se ultrapassarem o escopo, a menos que sejam explicitamente descartadas com o uso de DROP TABLE:

- Uma tabela temporária local criada em um procedimento armazenado será descartada automaticamente quando o procedimento armazenado for encerrado. A tabela pode ser referenciada por qualquer procedimento armazenado aninhado executado pelo procedimento armazenado que criou a tabela. A tabela não pode ser referenciada pelo processo que chamou o procedimento armazenado que criou a tabela.
- Todas as outras tabelas temporárias locais serão descartadas automaticamente ao término da sessão atual.
- As tabelas temporárias globais serão descartadas automaticamente ao término da sessão que criou e quando todas as demais tarefas pararem de fazer referência a ela. A associação entre uma tarefa e uma tabela será mantida apenas enquanto durar uma única instrução [!INCLUDE[tsql](../../includes/tsql-md.md)]. Ou seja, a tabela temporária global será descartada ao término da última instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] que estava referenciando ativamente a tabela ao término da sessão de criação.

Uma tabela temporária local criada em um procedimento armazenado ou gatilho pode ter o mesmo nome de uma tabela temporária que foi criada antes de o procedimento armazenado ou gatilho ser chamado. Contudo, se uma consulta fizer referência a uma tabela temporária e houver duas tabelas temporárias com o mesmo nome, não há definição de qual tabela servirá de base para a consulta. Procedimentos armazenados aninhados também podem criar tabelas temporárias com o mesmo nome de uma tabela temporária que foi criada pelo procedimento armazenado que o chamou. Entretanto, para que modificações sejam resolvidas na tabela que foi criada no procedimento aninhado, a tabela deve ter a mesma estrutura, com os mesmos nomes de colunas, da tabela criada pelo procedimento que o chamou. Isso é mostrado no exemplo a seguir.

```sql
CREATE PROCEDURE dbo.Test2
AS
    CREATE TABLE #t (x INT PRIMARY KEY);
    INSERT INTO #t VALUES (2);
    SELECT Test2Col = x FROM #t;
GO

CREATE PROCEDURE dbo.Test1
AS
    CREATE TABLE #t (x INT PRIMARY KEY);
    INSERT INTO #t VALUES (1);
    SELECT Test1Col = x FROM #t;
    EXEC Test2;
GO

CREATE TABLE #t(x INT PRIMARY KEY);
INSERT INTO #t VALUES (99);
GO

EXEC Test1;
GO
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```
(1 row(s) affected)
Test1Col
-----------
1

(1 row(s) affected)
 Test2Col
 -----------
 2
 ```

Quando você cria tabelas temporárias locais ou globais, a sintaxe `CREATE TABLE` dá suporte a definições de restrição, exceto para restrições FOREIGN KEY. Se for especificada uma restrição FOREIGN KEY em uma tabela temporária, a instrução retornará uma mensagem de aviso informando que a restrição foi ignorada. A tabela ainda será criada sem as restrições FOREIGN KEY. Tabelas temporárias não podem ser referenciadas em restrições FOREIGN KEY.

Se uma tabela temporária for criada com uma restrição nomeada e se for criada dentro do escopo de uma transação definida pelo usuário, somente um usuário de cada vez poderá executar a instrução que cria a tabela temporária. Por exemplo, se um procedimento armazenado criar uma tabela temporária com uma restrição de chave primária nomeada, o procedimento armazenado não poderá ser executado simultaneamente por vários usuários.

## <a name="database-scoped-global-temporary-tables-azure-sql-database"></a>Tabelas temporárias globais no escopo do banco de dados (Banco de Dados SQL do Azure)

Tabelas temporárias globais para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (iniciado com ## nome de tabela) são armazenadas em tempdb e compartilhadas entre as sessões de todos os usuários em toda a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter informações sobre tipos de tabela SQL, veja a seção acima em Criar tabelas.

O [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] é compatível com tabelas temporárias globais que também são armazenadas em tempdb e têm o escopo definido para o nível de banco de dados. Isso significa que as tabelas temporárias globais são compartilhadas para as sessões de todos os usuários no mesmo [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. As sessões de usuário de outros bancos de dados não podem acessar tabelas temporárias globais.

Tabelas temporárias globais para o [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] seguem a mesma sintaxe e a mesma semântica que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa para tabelas temporárias. De modo similar, os procedimentos armazenados temporários globais também têm o escopo definido para o nível do [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Tabelas temporárias locais (iniciadas com # nome da tabela) também são compatíveis com o [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] e seguem a mesma sintaxe e a mesma semântica que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa. Veja a seção acima em [Tabelas temporárias](#temporary-tables).  

> [!IMPORTANT]
> Este recurso está disponível no [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

### <a name="troubleshooting-global-temporary-tables-for-azure-sql-database"></a>Solucionando problemas de tabelas temporárias globais para o Banco de Dados SQL do Azure

Para solucionar problemas do tempdb, confira [Como monitorar o uso do tempdb](../../relational-databases/databases/tempdb-database.md#how-to-monitor-tempdb-use).

> [!NOTE]
> Somente um administrador de servidor pode acessar as DMVs de solução de problemas em [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

### <a name="permissions"></a>Permissões

Qualquer usuário pode criar objetos temporários globais. Os usuários podem acessar somente seus próprios objetos, a menos que recebam permissões adicionais.

## <a name="partitioned-tables"></a>Tabelas particionadas

Antes de criar uma tabela particionada usando CREATE TABLE, crie uma função de partição para especificar como a tabela será particionada. Uma função de partição é criada usando [CREATE PARTITION FUNCTION](../../t-sql/statements/create-partition-function-transact-sql.md). Em seguida, crie um esquema de partição para especificar os grupos de arquivos que manterão as partições indicadas pela função de partição. Um esquema de partição é criado usando [CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md). O uso das restrições PRIMARY KEY ou UNIQUE para separar grupos de arquivos não pode ser especificado para tabelas particionadas. Para saber mais, confira [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).

## <a name="primary-key-constraints"></a>Restrições PRIMARY KEY

- Uma tabela pode conter apenas uma restrição PRIMARY KEY.
- O índice gerado pela restrição PRIMARY KEY não pode fazer com que o número de índices na tabela exceda 999 índices não clusterizados e 1 índice clusterizado.
- Se CLUSTERED ou NONCLUSTERED não estiver especificado para uma restrição PRIMARY KEY, CLUSTERED será usado, se não houver índices clusterizados especificados para restrições UNIQUE.
- Todas as colunas definidas em uma restrição PRIMARY KEY devem ser definidas como NOT NULL. Se a nulidade não for especificada, todas as colunas participantes de uma restrição FOREIGN KEY devem ter sua nulidade definida como NOT NULL.

    > [!NOTE]
    > Para tabelas com otimização de memória, a coluna de chave NULLable é permitida.

- Se a chave primária for definida em uma coluna de tipo CLR definida pelo usuário, a implementação do tipo deverá oferecer suporte a uma ordenação binária. Para obter mais informações, veja [Tipos CLR definidos pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md).

## <a name="unique-constraints"></a>Restrições UNIQUE

- Se CLUSTERIZADO ou NONCLUSTERED não for especificado para uma restrição UNIQUE, NONCLUSTERED será usado por padrão.
- Cada restrição UNIQUE gera um índice. O número de restrições UNIQUE não pode fazer com que o número de índices na tabela exceda 999 índices não clusterizados e 1 índice clusterizado.
- Se a restrição unique for definida em uma coluna de tipo de dados CLR definido pelo usuário, a implementação do tipo deverá oferecer suporte a uma ordenação binária ou com base no operador. Para obter mais informações, veja [Tipos CLR definidos pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md).

## <a name="foreign-key-constraints"></a>Restrições de FOREIGN KEY

- Quando um valor diferente de NULL é inserido na coluna de uma restrição FOREIGN KEY, o valor deve existir na coluna referenciada; caso contrário, será retornada uma mensagem de erro de violação de chave estrangeira.
- Restrições FOREIGN KEY serão aplicadas à coluna precedente, a menos que sejam especificadas colunas de origem.
- As restrições FOREIGN KEY só podem fazer referência a tabelas que estão no mesmo banco de dados e no mesmo servidor. A integridade referencial em todos os bancos de dados deve ser implementada por gatilhos. Para mais informações, veja [CREATE TRIGGER](../../t-sql/statements/create-trigger-transact-sql.md).
- As restrições FOREIGN KEY podem fazer referência a outra coluna da mesma tabela. Isso se chama autorreferência.
- A cláusula REFERENCES de uma restrição FOREIGN KEY no nível de coluna pode listar apenas uma coluna de referência. Essa coluna deve ter o mesmo tipo de dados da coluna na qual a restrição foi definida.
- O número de colunas de referência da cláusula REFERENCES de uma restrição FOREIGN KEY deve ser igual ao número de colunas da lista de colunas de restrição. O tipo de dados de cada coluna de referência também deve ser igual ao da coluna correspondente na lista de colunas. As colunas de referência devem ser especificadas na mesma ordem que foi usada ao especificar as colunas da chave primária ou restrição exclusiva na tabela referenciada.
- CASCADE, SET NULL ou SET DEFAULT não poderão ser especificados se uma coluna do tipo **timestamp** integrar a chave estrangeira ou a chave referenciada.
- CASCADE, SET NULL, SET DEFAULT e NO ACTION podem ser combinados nas tabelas que tenham relacionamentos referenciais entre si. Se o [!INCLUDE[ssDE](../../includes/ssde-md.md)] encontrar NO ACTION, parará e reverterá as ações CASCATA, SET NULL e SET DEFAULT. Quando uma instrução DELETE provoca uma combinação de ações CASCADE, SET NULL, SET DEFAULT e NO ACTION, todas as ações CASCADE, SET NULL e SET DEFAULT são aplicadas antes que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] verifique se existe alguma NO ACTION.
- O [!INCLUDE[ssDE](../../includes/ssde-md.md)] não tem um limite predefinido quanto ao número de restrições FOREIGN KEY que uma tabela pode conter para referenciar outras tabelas nem quanto ao número de restrições FOREIGN KEY que são propriedade de outras tabelas e fazem referência a uma tabela específica.

  Entretanto, o número real de restrições FOREIGN KEY que pode ser usado é limitado pela configuração do hardware e pelo design do banco de dados e do aplicativo. Recomendamos que uma tabela não contenha mais de 253 restrições FOREIGN KEY e que ela não seja referenciada por mais de 253 restrições FOREIGN KEY. O limite real pode depender mais ou menos do aplicativo e do hardware. Considere o custo da imposição de restrições FOREIGN KEY ao criar o banco de dados e os aplicativos.

- As restrições FOREIGN KEY não são impostas a tabelas temporárias.
- As restrições FOREIGN KEY podem fazer referência somente a colunas em restrições PRIMARY KEY ou UNIQUE na tabela ou em uma UNIQUE INDEX na tabela referenciada.
- Se a chave estrangeira for definida em uma coluna de tipo de dados CLR definido pelo usuário, a implementação do tipo deverá oferecer suporte a uma ordenação binária. Para obter mais informações, veja [Tipos CLR definidos pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md).
- As colunas que participam de uma relação de chave estrangeira devem ser definidas com o mesmo comprimento e a mesma escala.

## <a name="default-definitions"></a>definições DEFAULT

- Uma coluna pode ter apenas uma definição DEFAULT.
- Uma definição DEFAULT pode conter valores constantes, funções, funções niladic SQL padrão ou NULL. A tabela a seguir mostra as funções niladic e os valores que elas retornam para o padrão durante uma instrução INSERT.

    |funções niladic SQL-92|Valor retornado|
    |------------------------------|--------------------|
    |CURRENT_TIMESTAMP|Data e hora atuais.|
    |CURRENT_USER|Nome de usuário que está executando uma inserção.|
    |SESSION_USER|Nome de usuário que está executando uma inserção.|
    |SYSTEM_USER|Nome de usuário que está executando uma inserção.|
    |USER|Nome de usuário que está executando uma inserção.|
- *constant_expression* em uma definição DEFAULT não pode fazer referência a uma outra coluna da tabela nem a outras tabelas, exibições ou procedimentos armazenados.
- Não é possível criar definições DEFAULT em colunas com um tipo de dados **timestamp** ou colunas com uma propriedade IDENTITY.
- Não é possível criar definições DEFAULT para colunas com tipos de dados do alias se o tipo de dados do alias estiver associado a um objeto padrão.

## <a name="check-constraints"></a>Restrições CHECK

- Uma coluna pode ter qualquer número de restrições CHECK e os critérios podem incluir diversas expressões lógicas combinadas com AND e OR. Várias restrições CHECK são validadas na ordem de criação.
- A avaliação do critério de pesquisa deve usar uma expressão Booleana como base e não pode fazer referência a outra tabela.
- A restrição CHECK no nível de coluna pode fazer referência somente à coluna restrita, e a restrição CHECK no nível de tabela pode fazer referência somente às colunas da mesma tabela.

  CHECK CONSTRAINTS e regras oferecem a mesma função de validação dos dados durante instruções INSERT e UPDATE.

- Se existirem uma regra e uma ou mais restrições CHECK para uma coluna, ou colunas, todas as restrições serão avaliadas.
- Restrições de verificação não podem ser definidas em colunas **text**, **ntext** ou **image**.

## <a name="additional-constraint-information"></a>Informações adicionais sobre restrições

- Um índice criado para uma restrição não pode ser descartado pelo uso de `DROP INDEX`; a restrição precisa ser descartada com o uso de `ALTER TABLE`. Um índice criado para uma restrição e usado por ela pode ser reconstruído com o uso de `ALTER INDEX ... REBUILD`. Para obter mais informações, veja [Reorganizar e recriar índices](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md).
- Os nomes de restrição devem seguir as regras para [identificadores](../../relational-databases/databases/database-identifiers.md), a não ser que o nome não possa começar com uma tecla jogo da velha (#). Se *constraint_name* não for fornecido, um nome gerado pelo sistema será atribuído à restrição. O nome da restrição aparece em qualquer mensagem de erro sobre violações de restrição.
- Quando uma restrição é violada em uma instrução `INSERT`, `UPDATE` ou `DELETE`, a instrução é encerrada. No entanto, quando `SET XACT_ABORT` é definido como OFF, a transação continuará sendo processada, se a instrução fizer parte de uma transação explícita. Quando `SET XACT_ABORT` é definido como ON, a transação inteira é revertida. Use também a instrução `ROLLBACK TRANSACTION` com a definição de transação verificando a função do sistema `@@ERROR`.
- Quando `ALLOW_ROW_LOCKS = ON` e `ALLOW_PAGE_LOCK = ON`, row-, page- e os bloqueios em nível de linha, página e tabela são permitidos quando você acessa o índice. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] escolhe o bloqueio apropriado e pode escalar o bloqueio de uma linha ou página para um bloqueio de tabela. Quando `ALLOW_ROW_LOCKS = OFF` e `ALLOW_PAGE_LOCK = OFF`, o bloqueio em nível de tabela é permitido quando você acessa o índice.
- Se uma tabela tiver restrições FOREIGN KEY ou CHECK e gatilhos, os critérios da restrição serão avaliados antes da execução do gatilho.

Para obter um relatório em uma tabela e suas colunas, use `sp_help` ou `sp_helpconstraint`. Para renomear uma tabela, use `sp_rename`. Para obter um relatório de exibições e procedimentos armazenados que dependem de uma tabela, use [sys.dm_sql_referenced_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md) e [sys.dm_sql_referencing_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md).

## <a name="nullability-rules-within-a-table-definition"></a>Regras de nulidade em uma definição de tabela

A nulidade de uma coluna determina se ela permite valor nulo (NULL) como dados nessa coluna. NULL não é zero nem em branco: NULL significa que nenhuma entrada foi feita nem um NULL explícito foi fornecido e, normalmente, implica que o valor é desconhecido ou não se aplica.

Quando você usa `CREATE TABLE` ou `ALTER TABLE` para criar ou alterar uma tabela, as configurações de banco de dados e de sessão influenciam e, possivelmente, substituem a nulidade do tipo de dados que é usado em uma definição de coluna. Recomendamos que você sempre defina explicitamente uma coluna como NULL ou NOT NULL para colunas não computadas ou, se usar um tipo de dados definido pelo usuário, permita que a coluna use a nulidade padrão do tipo de dados. Colunas esparsas sempre têm que permitir NULL.

Quando a nulidade da coluna não é especificada explicitamente, ela segue as regras mostradas na tabela a seguir

|Tipo de dados de coluna|Regra|
|----------------------|----------|
|Tipo de dados de alias|O [!INCLUDE[ssDE](../../includes/ssde-md.md)] usa a nulidade especificada durante a criação do tipo de dados. Para determinar a nulidade padrão do tipo de dados, use **sp_help**.|
|tipo de dados CLR definido pelo usuário|A nulidade é determinada de acordo com a definição de coluna.|
|Tipo de dados fornecido pelo sistema|Se o tipo de dados fornecido pelo sistema tiver apenas uma opção, ele prevalece. Tipos de dados **timestamp** devem ser tipos de dados NOT NULL. Quando qualquer configuração de sessão é definida como ON com o uso de SET:<br />**ANSI_NULL_DFLT_ON** = ON, NULL é atribuído. <br />**ANSI_NULL_DFLT_OFF** = ON, NOT NULL é atribuído.<br /><br /> Quando qualquer configuração de banco de dados for configurada com o uso de ALTER DATABASE:<br />**ANSI_NULL_DEFAULT_ON** = ON, NULL é atribuído. <br />**ANSI_NULL_DEFAULT_OFF** = ON, NOT NULL é atribuído.<br /><br /> Para exibir a configuração de banco de dados de ANSI_NULL_DEFAULT, use a exibição do catálogo **sys.databases**|

Quando nenhuma das opções ANSI_NULL_DFLT estiver definida para a sessão e o banco de dados estiver configurado com o padrão (ANSI_NULL_DEFAULT é OFF), o padrão de NOT NULL será atribuído.

Se a coluna for uma coluna computada, seu nulidade sempre será determinada automaticamente pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Para descobrir a nulidade desse tipo de coluna, use a função `COLUMNPROPERTY` com a propriedade **AllowsNull**.

> [!NOTE]
> O driver ODBC e o driver OLE DB do SQL Server usam como padrão ANSI_NULL_DFLT_ON definido como ON. Os usuários de ODBC and OLE DB podem configurar essa opção nas fontes de dados ODBC ou usando os atributos ou as propriedades de conexão definidas pelo aplicativo.

## <a name="data-compression"></a>Data Compression

Não é possível habilitar as tabelas do sistema para compactação. Quando você cria uma tabela, a compactação de dados é definida como NONE, a menos que especificada de outra maneira. Se for especificada uma lista de partições ou uma partição fora do intervalo, um erro será gerado. Para obter mais informações sobre compactação de dados, veja [Compactação de dados](../../relational-databases/data-compression/data-compression.md).

Para avaliar como a alteração do estado de compactação afetará uma tabela, um índice ou uma partição, use o procedimento armazenado [sp_estimate_data_compression_savings](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md) .

## <a name="permissions"></a>Permissões

Exige a permissão `CREATE TABLE` no banco de dados e a permissão `ALTER` no esquema no qual a tabela está sendo criada.

Se uma coluna da instrução `CREATE TABLE` for definida como um tipo definido pelo usuário, a permissão `REFERENCES` no tipo definido pelo usuário será necessária.

Se uma coluna da instrução `CREATE TABLE` for definida como um tipo de dados CLR definido pelo usuário, a propriedade do tipo ou a permissão `REFERENCES` será necessária.

Se uma coluna da instrução `CREATE TABLE` tiver uma coleção de esquemas XML associada a ela, a propriedade da coleção de esquemas XML ou a permissão `REFERENCES` será necessária.

Qualquer usuário pode criar tabelas temporárias no tempdb.

## <a name="examples"></a>Exemplos

### <a name="a-create-a-primary-key-constraint-on-a-column"></a>a. Criar uma restrição PRIMARY KEY em uma coluna

O exemplo a seguir mostra a definição de coluna para uma restrição PRIMARY KEY com um índice clusterizado na coluna `EmployeeID` da tabela `Employee`. Como não foi especificado um nome de restrição, o sistema fornecerá o nome da restrição.

```sql
CREATE TABLE dbo.Employee (
    EmployeeID INT PRIMARY KEY CLUSTERED
);
```

### <a name="b-using-foreign-key-constraints"></a>B. Usando restrições FOREIGN KEY

Uma restrição FOREIGN KEY é usada para fazer referência a outra tabela. Chaves estrangeiras podem ser chaves de coluna única ou chaves de várias colunas. O próximo exemplo mostra uma restrição FOREIGN KEY de coluna única na tabela `SalesOrderHeader` que faz referência à tabela `SalesPerson`. Somente a cláusula REFERENCES é necessária para uma restrição FOREIGN KEY de coluna única.

```sql
SalesPersonID INT NULL REFERENCES SalesPerson(SalesPersonID)
```

Também é possível usar explicitamente a cláusula FOREIGN KEY e declarar novamente o atributo de coluna. Observe que o nome da coluna não tem que ser o mesmo em ambas as tabelas.

```sql
FOREIGN KEY (SalesPersonID) REFERENCES SalesPerson(SalesPersonID)
```

As restrições de chaves de várias colunas são criadas como restrições de tabela. No banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)], a tabela `SpecialOfferProduct` contém uma PRIMARY KEY de várias colunas. O exemplo a seguir mostra como fazer referência a essa chave a partir de outra tabela; um nome de restrição explícito é opcional.

```sql
CONSTRAINT FK_SpecialOfferProduct_SalesOrderDetail
    FOREIGN KEY (ProductID, SpecialOfferID)
    REFERENCES SpecialOfferProduct (ProductID, SpecialOfferID)
```

### <a name="c-using-unique-constraints"></a>C. Usando restrições UNIQUE

As restrições UNIQUE são usadas para impor exclusividade a colunas de chave não primária. O exemplo a seguir impõe uma restrição indicando que a coluna `Name` da tabela `Product` deve ser exclusiva.

```sql
Name NVARCHAR(100) NOT NULL
UNIQUE NONCLUSTERED
```

### <a name="d-using-default-definitions"></a>D. Usando definições DEFAULT

Os padrões fornecem um valor (com as instruções INSERT e UPDATE) quando nenhum valor é fornecido. Por exemplo, o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] poderia conter uma tabela de pesquisa listando os diversos cargos que os funcionários podem ocupar na empresa. Na coluna que descreve cada trabalho, uma cadeia de caracteres padrão poderia fornecer uma descrição se não for inserida explicitamente uma descrição real.

```sql
DEFAULT 'New Position - title not formalized yet'
```

Além de constantes, definições DEFAULT podem incluir funções. Use o exemplo a seguir para obter a data atual para uma entrada.

```sql
DEFAULT (GETDATE())
```

Um exame da função niladic também pode melhorar a integridade dos dados. Para monitorar o usuário que inseriu uma linha, use a função niladic para USER. Não coloque as funções niladic entre parênteses.

```sql
DEFAULT USER
```

### <a name="e-using-check-constraints"></a>E. Usando restrições CHECK

O exemplo a seguir mostra uma restrição composta pelos valores inseridos na coluna `CreditRating` da tabela `Vendor`. A restrição não é nomeada.

```sql
CHECK (CreditRating >= 1 and CreditRating <= 5)
```

Este exemplo mostra uma restrição nomeada com um padrão de restrição nos dados de caracteres inseridos em uma coluna de uma tabela.

```sql
CONSTRAINT CK_emp_id CHECK (
    emp_id LIKE '[A-Z][A-Z][A-Z][1-9][0-9][0-9][0-9][0-9][FM]'
    OR emp_id LIKE '[A-Z]-[A-Z][1-9][0-9][0-9][0-9][0-9][FM]'
)
```

Este exemplo especifica que os valores devem estar em uma lista específica ou seguir o padrão especificado.

```sql
CHECK (
    emp_id IN ('1389', '0736', '0877', '1622', '1756')
    OR emp_id LIKE '99[0-9][0-9]'
)
```

### <a name="f-showing-the-complete-table-definition"></a>F. Mostrando a definição de tabela completa

O próximo exemplo mostra as definições de tabela completas com todas as definições de restrição para a tabela `PurchaseOrderDetail`, criada no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. Observe que para executar a amostra, o esquema de tabela foi alterado para `dbo`.

```sql
CREATE TABLE dbo.PurchaseOrderDetail
(
    PurchaseOrderID int NOT NULL
        REFERENCES Purchasing.PurchaseOrderHeader(PurchaseOrderID),
    LineNumber smallint NOT NULL,
    ProductID int NULL
        REFERENCES Production.Product(ProductID),
    UnitPrice money NULL,
    OrderQty smallint NULL,
    ReceivedQty float NULL,
    RejectedQty float NULL,
    DueDate datetime NULL,
    rowguid uniqueidentifier ROWGUIDCOL NOT NULL
        CONSTRAINT DF_PurchaseOrderDetail_rowguid DEFAULT (NEWID()),
    ModifiedDate datetime NOT NULL
        CONSTRAINT DF_PurchaseOrderDetail_ModifiedDate DEFAULT (GETDATE()),
    LineTotal AS ((UnitPrice*OrderQty)),
    StockedQty AS ((ReceivedQty-RejectedQty)),
    CONSTRAINT PK_PurchaseOrderDetail_PurchaseOrderID_LineNumber
               PRIMARY KEY CLUSTERED (PurchaseOrderID, LineNumber)
               WITH (IGNORE_DUP_KEY = OFF)
)
ON PRIMARY;
```

### <a name="g-creating-a-table-with-an-xml-column-typed-to-an-xml-schema-collection"></a>G. Criando uma tabela com uma coluna de xml digitada para uma coleção de esquemas XML

O exemplo seguinte cria uma tabela com uma coluna `xml` que é digitada para a coleção de esquemas XML `HRResumeSchemaCollection`. A palavra-chave `DOCUMENT` especifica que cada instância do tipo de dados `xml` em *column_name* pode conter apenas um elemento de nível superior.

```sql
CREATE TABLE HumanResources.EmployeeResumes
(
    LName nvarchar(25),
    FName nvarchar(25),
    Resume xml(DOCUMENT HumanResources.HRResumeSchemaCollection)
);
```

### <a name="h-creating-a-partitioned-table"></a>H. Criando uma tabela particionada

O exemplo a seguir cria uma função de partição para dividir uma tabela ou índice em quatro partições. Em seguida, o exemplo cria um esquema de partição que especifica os grupos de arquivos que conterão cada uma das quatro partições. Finalmente, o exemplo cria uma tabela que usa o esquema de partição. Este exemplo supõe que os grupos de arquivos já existam no banco de dados.

```sql
CREATE PARTITION FUNCTION myRangePF1 (int)
    AS RANGE LEFT FOR VALUES (1, 100, 1000);
GO

CREATE PARTITION SCHEME myRangePS1
    AS PARTITION myRangePF1
    TO (test1fg, test2fg, test3fg, test4fg);
GO  
  
CREATE TABLE PartitionTable (col1 int, col2 char(10))
    ON myRangePS1 (col1);
GO
```

Com base nos valores da coluna `col1` de `PartitionTable`, as partições são atribuídas das seguintes maneiras.

|Grupo de arquivos|test1fg|test2fg|test3fg|test4fg|
|---------------|-------------|-------------|-------------|-------------|
|**Partição**|1|2|3|4|
|**Valores**|col 1 \<= 1|col1 > 1 AND col1 \<= 100|col1 > 100 AND col1 \<= 1.000|col1 > 1000|

### <a name="i-using-the-uniqueidentifier-data-type-in-a-column"></a>I. Usando o tipo de dados uniqueidentifier em uma coluna

O exemplo a seguir cria uma tabela com uma coluna `uniqueidentifier`. O exemplo usa uma restrição PRIMARY KEY para proteger a tabela, evitando que os usuários insiram valores duplicados, e usa a função `NEWSEQUENTIALID()` da restrição `DEFAULT` para fornecer valores para novas linhas. A propriedade ROWGUIDCOL é aplicada à coluna `uniqueidentifier` de forma que ela possa ser referenciada pela palavra-chave $ROWGUID.

```sql
CREATE TABLE dbo.Globally_Unique_Data
(
    GUID UNIQUEIDENTIFIER
        CONSTRAINT Guid_Default DEFAULT
        NEWSEQUENTIALID() ROWGUIDCOL,
    Employee_Name VARCHAR(60)
    CONSTRAINT Guid_PK PRIMARY KEY (GUID)
);
```

### <a name="j-using-an-expression-for-a-computed-column"></a>J. Usando uma expressão para uma coluna computada

O exemplo a seguir mostra o uso de uma expressão (`(low + high)/2`) para calcular a coluna computada `myavg`.

```sql
CREATE TABLE dbo.mytable
(
    low INT,
    high INT,
    myavg AS (low + high)/2
);
```

### <a name="k-creating-a-computed-column-based-on-a-user-defined-type-column"></a>K. Criando uma coluna computada com base em uma coluna de tipo de dados definido pelo usuário

O exemplo a seguir cria uma tabela com uma coluna definida como tipo de dados definido pelo usuário `utf8string`, supondo que o assembly do tipo, e o próprio tipo, já foram criados no banco de dados atual. Uma segunda coluna é definida com base em `utf8string` e usa o método `ToString()` de **type(class)** `utf8string` para computar um valor para a coluna.

```sql
CREATE TABLE UDTypeTable
(
    u UTF8STRING,
    ustr AS u.ToString() PERSISTED
);
```

### <a name="l-using-the-user_name-function-for-a-computed-column"></a>L. Usando uma função USER_NAME para uma coluna computada

O exemplo a seguir usa a função `USER_NAME()` na coluna `myuser_name`.

```sql
CREATE TABLE dbo.mylogintable
(
    date_in DATETIME,
    user_id INT,
    myuser_name AS USER_NAME()
);
```

### <a name="m-creating-a-table-that-has-a-filestream-column"></a>M. Criando uma tabela que possui uma coluna FILESTREAM

O exemplo a seguir cria uma tabela com uma coluna `FILESTREAM``Photo`. Se uma tabela tiver uma ou mais colunas `FILESTREAM`, ela deve ter uma coluna `ROWGUIDCOL`.

```sql
CREATE TABLE dbo.EmployeePhoto
(
    EmployeeId INT NOT NULL PRIMARY KEY,
    Photo VARBINARY(MAX) FILESTREAM NULL,
    MyRowGuidColumn UNIQUEIDENTIFIER NOT NULL ROWGUIDCOL UNIQUE DEFAULT NEWID()
);
```

### <a name="n-creating-a-table-that-uses-row-compression"></a>N. Criando uma tabela que usa a compactação de linha

O exemplo a seguir cria uma tabela que usa compactação de linha.

```sql
CREATE TABLE dbo.T1
(
    c1 INT,
    c2 NVARCHAR(200)
)
WITH (DATA_COMPRESSION = ROW);
```

Para obter exemplos de compactação de dados adicionais, consulte [Compactação de dados](../../relational-databases/data-compression/data-compression.md).

### <a name="o-creating-a-table-that-has-sparse-columns-and-a-column-set"></a>O. Criando uma tabela que tem colunas esparsas e um conjunto de colunas

Os exemplos a seguir mostram como criar uma tabela com uma coluna esparsa e uma coluna com duas colunas esparsas e um conjunto de colunas. Os exemplos usam a sintaxe básica. Para obter exemplos mais complexos, veja [Usar colunas esparsas](../../relational-databases/tables/use-sparse-columns.md) e [Usar conjuntos de colunas](../../relational-databases/tables/use-column-sets.md).

Este exemplo cria uma tabela com uma coluna esparsa.

```sql
CREATE TABLE dbo.T1
(
    c1 INT PRIMARY KEY,
    c2 VARCHAR(50) SPARSE NULL
);
```

Este exemplo cria uma tabela com duas colunas esparsas e um conjunto de colunas nomeado `CSet`.

```sql
CREATE TABLE T1
(
    c1 INT PRIMARY KEY,
    c2 VARCHAR(50) SPARSE NULL,
    c3 INT SPARSE NULL,
    CSet XML COLUMN_SET FOR ALL_SPARSE_COLUMNS
);
```

### <a name="p-creating-a-system-versioned-disk-based-temporal-table"></a>P. Criando uma tabela temporal baseada em disco com controle de versão do sistema

**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

Os exemplos a seguir mostram como criar uma tabela temporal vinculada a uma nova tabela de histórico e como criar uma tabela temporal vinculada a uma tabela de histórico existente. Observe que a tabela temporal deve ter uma chave primária definida para ser habilitada para a tabela a ser habilitada para controle de versão do sistema. Para obter exemplos mostrando como adicionar ou remover o controle de versão do sistema em uma tabela existente, veja controle de versão do sistema em [Exemplos](../../t-sql/statements/alter-table-transact-sql.md#Example_Top). Para casos de uso, veja [Tabelas temporais](../../relational-databases/tables/temporal-tables.md).

Este exemplo cria uma nova tabela temporal vinculada a uma nova tabela de histórico.

```sql
CREATE TABLE Department
(
    DepartmentNumber CHAR(10) NOT NULL PRIMARY KEY CLUSTERED,
    DepartmentName VARCHAR(50) NOT NULL,
    ManagerID INT NULL,
    ParentDepartmentNumber CHAR(10) NULL,
    SysStartTime DATETIME2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL,
    SysEndTime DATETIME2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL,
    PERIOD FOR SYSTEM_TIME (SysStartTime, SysEndTime)
)
WITH (SYSTEM_VERSIONING = ON);
```

Este exemplo cria uma nova tabela temporal vinculada a uma tabela de histórico existente.

```sql
-- Existing table
CREATE TABLE Department_History
(
    DepartmentNumber CHAR(10) NOT NULL,
    DepartmentName VARCHAR(50) NOT NULL,
    ManagerID INT NULL,
    ParentDepartmentNumber CHAR(10) NULL,
    SysStartTime DATETIME2 NOT NULL,
    SysEndTime DATETIME2 NOT NULL
);

-- Temporal table
CREATE TABLE Department
(
    DepartmentNumber CHAR(10) NOT NULL PRIMARY KEY CLUSTERED,
    DepartmentName VARCHAR(50) NOT NULL,
    ManagerID INT NULL,
    ParentDepartmentNumber CHAR(10) NULL,
    SysStartTime DATETIME2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL,
    SysEndTime DATETIME2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL,
    PERIOD FOR SYSTEM_TIME (SysStartTime, SysEndTime)
)
WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.Department_History, DATA_CONSISTENCY_CHECK = ON));
```

### <a name="q-creating-a-system-versioned-memory-optimized-temporal-table"></a>Q. Criando uma tabela temporal com otimização de memória e controle de versão do sistema

**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

O exemplo a seguir mostra como criar uma versão do sistema com tabela temporal com otimização de memória vinculada a uma nova tabela de histórico baseada em disco.

Este exemplo cria uma nova tabela temporal vinculada a uma nova tabela de histórico.

```sql
CREATE SCHEMA History;
GO

CREATE TABLE dbo.Department
(
    DepartmentNumber CHAR(10) NOT NULL PRIMARY KEY NONCLUSTERED,
    DepartmentName VARCHAR(50) NOT NULL,
    ManagerID INT NULL,
    ParentDepartmentNumber CHAR(10) NULL,
    SysStartTime DATETIME2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL,
    SysEndTime DATETIME2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL,
    PERIOD FOR SYSTEM_TIME (SysStartTime, SysEndTime)
)
WITH
(
    MEMORY_OPTIMIZED = ON,
    DURABILITY = SCHEMA_AND_DATA,
    SYSTEM_VERSIONING = ON (HISTORY_TABLE = History.DepartmentHistory)
);
```

Este exemplo cria uma nova tabela temporal vinculada a uma tabela de histórico existente.

```sql
-- Existing table
CREATE TABLE Department_History
(
    DepartmentNumber CHAR(10) NOT NULL,
    DepartmentName VARCHAR(50) NOT NULL,
    ManagerID INT NULL,
    ParentDepartmentNumber CHAR(10) NULL,
    SysStartTime DATETIME2 NOT NULL,
    SysEndTime DATETIME2 NOT NULL
);

-- Temporal table
CREATE TABLE Department
(
    DepartmentNumber CHAR(10) NOT NULL PRIMARY KEY CLUSTERED,
    DepartmentName VARCHAR(50) NOT NULL,
    ManagerID INT NULL,
    ParentDepartmentNumber CHAR(10) NULL,
    SysStartTime DATETIME2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL,
    SysEndTime DATETIME2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL,
    PERIOD FOR SYSTEM_TIME (SysStartTime, SysEndTime)
)
WITH
(
    SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.Department_History, DATA_CONSISTENCY_CHECK = ON)
);
```

### <a name="r-creating-a-table-with-encrypted-columns"></a>R. Criando uma tabela com colunas criptografadas

O exemplo a seguir cria uma tabela com duas colunas criptografadas. Para obter mais informações, consulte [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md).

```sql
CREATE TABLE Customers (
    CustName NVARCHAR(60)
        ENCRYPTED WITH (
            COLUMN_ENCRYPTION_KEY = MyCEK,
            ENCRYPTION_TYPE = RANDOMIZED,
            ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256'
        ),
    SSN VARCHAR(11) COLLATE Latin1_General_BIN2
        ENCRYPTED WITH (
            COLUMN_ENCRYPTION_KEY = MyCEK,
            ENCRYPTION_TYPE = DETERMINISTIC ,
            ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256'
        ),
    Age INT NULL
);
```

### <a name="s-create-an-inline-filtered-index"></a>S. Criar um índice filtrado embutido

Cria uma tabela com um índice filtrado embutido.

```sql
CREATE TABLE t1
(
    c1 INT,
    index IX1 (c1) WHERE c1 > 0
);
```

### <a name="t-create-an-inline-index"></a>T. Criar um índice embutido

O seguinte exemplo mostra como usar NONCLUSTERED embutido em tabelas baseadas em disco:

```sql
CREATE TABLE t1
(
    c1 INT,
    INDEX ix_1 NONCLUSTERED (c1)
);

CREATE TABLE t2
(
    c1 INT,
    c2 INT INDEX ix_1 NONCLUSTERED
);

CREATE TABLE t3
(
    c1 INT,
    c2 INT,
    INDEX ix_1 NONCLUSTERED (c1,c2)
);
```

### <a name="u-create-a-temporary-table-with-an-anonymously-named-compound-primary-key"></a>U. Criar uma tabela temporária com a chave primária composta nomeada de forma anônima

Criar uma tabela com a chave primária composta nomeada de forma anônima. Isso é útil para evitar conflitos de tempo de execução em que duas tabelas temporárias com escopo da sessão, cada uma em uma sessão separada, usam o mesmo nome para uma restrição.

```sql
CREATE TABLE #tmp
(
    c1 INT,
    c2 INT,
    PRIMARY KEY CLUSTERED ([c1], [c2])
);
GO
```

Se você nomear explicitamente a restrição, a segunda sessão gerará um erro, como:

```
Msg 2714, Level 16, State 5, Line 1
There is already an object named 'PK_#tmp' in the database.
Msg 1750, Level 16, State 1, Line 1
Could not create constraint or index. See previous errors.
```

O problema é que embora o nome da tabela temporária seja exclusivo, os nomes de restrição não são.

### <a name="v-using-global-temporary-tables-in-azure-sql-database"></a>V. Usando tabelas temporárias globais no Banco de Dados SQL do Azure

A Sessão A cria uma tabela temporária global ##test no [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] testdb1 e adiciona 1 linha

```sql
CREATE TABLE ##test (
    a INT,
    b INT
);

INSERT INTO ##test
VALUES (1, 1);

-- Obtain object ID for temp table ##test
SELECT OBJECT_ID('tempdb.dbo.##test') AS 'Object ID';
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```
1253579504
```

Obter o nome da tabela temporária global para uma ID de objeto especificada 1253579504 em tempdb (2)

```sql
SELECT name FROM tempdb.sys.objects WHERE object_id = 1253579504;
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```sql
##test
```

A Sessão B conecta-se ao [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] testdb1 e pode acessar a tabela ##test criado pela sessão A

```sql
SELECT * FROM ##test;
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```sql
1, 1
```

A Sessão C conecta-se a outro banco de dados no [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] testdb2 e deseja acessar ##test criado em testdb1. Esta seleção falha devido ao escopo do banco de dados para as tabelas temporárias globais

```sql
SELECT * FROM ##test
```

Que gera o seguinte erro:

```
Msg 208, Level 16, State 0, Line 1
Invalid object name '##test'
```

Lidando com um objeto do sistema no [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] tempdb do banco de dados do usuário atual testdb1

```sql
SELECT * FROM tempdb.sys.objects;
SELECT * FROM tempdb.sys.columns;
SELECT * FROM tempdb.sys.database_files;
```

## <a name="next-steps"></a>Próximas etapas

- [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)
- [COLUMNPROPERTY](../../t-sql/functions/columnproperty-transact-sql.md)
- [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md)
- [CREATE VIEW](../../t-sql/statements/create-view-transact-sql.md)
- [Data Types](../../t-sql/data-types/data-types-transact-sql.md)
- [DROP INDEX](../../t-sql/statements/drop-index-transact-sql.md)
- [sys.dm_sql_referenced_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)
- [sys.dm_sql_referencing_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)
- [DROP TABLE](../../t-sql/statements/drop-table-transact-sql.md)
- [CREATE PARTITION FUNCTION](../../t-sql/statements/create-partition-function-transact-sql.md)
- [CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md)
- [CREATE TYPE](../../t-sql/statements/create-type-transact-sql.md)
- [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)
- [sp_help](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)
- [sp_helpconstraint](../../relational-databases/system-stored-procedures/sp-helpconstraint-transact-sql.md)
- [sp_rename](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)
- [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)
