---
title: ALTER TABLE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/31/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- WAIT_AT_LOW_PRIORITY
- ABORT_AFTER_WAIT
- ABORT_AFTER_WAIT_TSQL
- ALTER_TABLE_TSQL
- ALTER TABLE
- WAIT_AT_LOW_PRIORITY_TSQL
- ALTER_COLUMN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- columns [SQL Server], resizing
- changing column size
- MAXDOP index option, ALTER TABLE statement
- table modifications [SQL Server], ALTER TABLE
- ALTER TABLE statement
- modifying tables
- partitioned tables [SQL Server], lock escalation
- resizing columns
- removing columns
- switching partitions
- reassigning partitions
- removing constraints
- triggers [SQL Server], disabling
- columns [SQL Server], adding
- LOCK_ESCALATION option of ALTER TABLE
- constraints [SQL Server], deleting
- constraints [SQL Server], disabling
- triggers [SQL Server], enabling
- re-enabling constraints
- index modifications [SQL Server]
- disabling constraints
- columns [SQL Server], removing
- max degree of parallelism option
- locking [SQL Server], tables
- ONLINE option
- disabling triggers
- constraints [SQL Server], adding
- deleting constraints
- adding constraints
- adding columns
- SWITCH partitions
- partitioned tables [SQL Server], switching
- lock escalation [SQL Server], option of ALTER TABLE
- constraints [SQL Server], enabling
- dropping constraints
- dropping columns
- table changes [SQL Server]
ms.assetid: f1745145-182d-4301-a334-18f799d361d1
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c61329dcaeb7972382e9385b723f5be889470c3c
ms.sourcegitcommit: 335d27d0493ddf4ffb770e13f8fe8802208d25ae
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/09/2020
ms.locfileid: "81002837"
---
# <a name="alter-table-transact-sql"></a>ALTER TABLE (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Modifica uma definição de tabela alterando, adicionando ou descartando colunas e restrições. ALTER TABLE também reatribui e recompila partições ou desabilita e habilita restrições e gatilhos.

Para obter mais informações sobre as convenções de sintaxe, consulte [Convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).

> [!IMPORTANT]
> A sintaxe de ALTER TABLE é diferente para tabelas baseadas em disco e tabelas com otimização de memória. Use os links a seguir para acessar diretamente o bloco de sintaxe adequado para seus tipos de tabela e os exemplos de sintaxe adequados:
>
> - Tabelas baseadas em disco:
>
>   - [Sintaxe](#syntax-for-disk-based-tables)
>   - [Exemplos](#Example_Top)
> - Tabelas com otimização de memória
>
>   - [Sintaxe](#syntax-for-memory-optimized-tables)
>   - [Exemplos](../../relational-databases/in-memory-oltp/altering-memory-optimized-tables.md)

## <a name="syntax-for-disk-based-tables"></a>Sintaxe para tabelas baseadas em disco

```
ALTER TABLE { database_name.schema_name.table_name | schema_name.table_name | table_name }
{
    ALTER COLUMN column_name
    {
        [ type_schema_name. ] type_name
            [ (
                {
                   precision [ , scale ]
                 | max
                 | xml_schema_collection
                }
            ) ]
        [ COLLATE collation_name ]
        [ NULL | NOT NULL ] [ SPARSE ]
      | { ADD | DROP }
          { ROWGUIDCOL | PERSISTED | NOT FOR REPLICATION | SPARSE | HIDDEN }
      | { ADD | DROP } MASKED [ WITH ( FUNCTION = ' mask_function ') ]
    }
    [ WITH ( ONLINE = ON | OFF ) ]
    | [ WITH { CHECK | NOCHECK } ]
  
    | ADD
    {
        <column_definition>
      | <computed_column_definition>
      | <table_constraint>
      | <column_set_definition>
    } [ ,...n ]
      | [ system_start_time_column_name datetime2 GENERATED ALWAYS AS ROW START
                [ HIDDEN ] [ NOT NULL ] [ CONSTRAINT constraint_name ]
            DEFAULT constant_expression [WITH VALUES] ,
                system_end_time_column_name datetime2 GENERATED ALWAYS AS ROW END
                   [ HIDDEN ] [ NOT NULL ][ CONSTRAINT constraint_name ]
            DEFAULT constant_expression [WITH VALUES] ,
        ]
       PERIOD FOR SYSTEM_TIME ( system_start_time_column_name, system_end_time_column_name )
    | DROP
     [ {
         [ CONSTRAINT ][ IF EXISTS ]
         {
              constraint_name
              [ WITH
               ( <drop_clustered_constraint_option> [ ,...n ] )
              ]
          } [ ,...n ]
          | COLUMN [ IF EXISTS ]
          {
              column_name
          } [ ,...n ]
          | PERIOD FOR SYSTEM_TIME
     } [ ,...n ]
    | [ WITH { CHECK | NOCHECK } ] { CHECK | NOCHECK } CONSTRAINT
        { ALL | constraint_name [ ,...n ] }
  
    | { ENABLE | DISABLE } TRIGGER
        { ALL | trigger_name [ ,...n ] }
  
    | { ENABLE | DISABLE } CHANGE_TRACKING
        [ WITH ( TRACK_COLUMNS_UPDATED = { ON | OFF } ) ]
  
    | SWITCH [ PARTITION source_partition_number_expression ]
        TO target_table
        [ PARTITION target_partition_number_expression ]
        [ WITH ( <low_priority_lock_wait> ) ]

    | SET
        (
            [ FILESTREAM_ON =
                { partition_scheme_name | filegroup | "default" | "NULL" } ]
            | SYSTEM_VERSIONING =
                  {
                      OFF
                  | ON
                      [ ( HISTORY_TABLE = schema_name . history_table_name
                          [, DATA_CONSISTENCY_CHECK = { ON | OFF } ]
                          [, HISTORY_RETENTION_PERIOD =
                          {
                              INFINITE | number {DAY | DAYS | WEEK | WEEKS
                  | MONTH | MONTHS | YEAR | YEARS }
                          }
                          ]
                        )
                      ]
                  }
          )

    | REBUILD
      [ [PARTITION = ALL]
        [ WITH ( <rebuild_option> [ ,...n ] ) ]
      | [ PARTITION = partition_number
           [ WITH ( <single_partition_rebuild_option> [ ,...n ] ) ]
        ]
      ]
  
    | <table_option>
    | <filetable_option>
    | <stretch_configuration>
}
[ ; ]
  
-- ALTER TABLE options
  
<column_set_definition> ::=
    column_set_name XML COLUMN_SET FOR ALL_SPARSE_COLUMNS

<drop_clustered_constraint_option> ::=
    {
        MAXDOP = max_degree_of_parallelism
      | ONLINE = { ON | OFF }
      | MOVE TO
         { partition_scheme_name ( column_name ) | filegroup | "default" }
    }
<table_option> ::=
    {
        SET ( LOCK_ESCALATION = { AUTO | TABLE | DISABLE } )
    }
  
<filetable_option> ::=
    {
       [ { ENABLE | DISABLE } FILETABLE_NAMESPACE ]
       [ SET ( FILETABLE_DIRECTORY = directory_name ) ]
    }
  
<stretch_configuration> ::=
    {
      SET (
        REMOTE_DATA_ARCHIVE
        {
            = ON (<table_stretch_options>)
          | = OFF_WITHOUT_DATA_RECOVERY ( MIGRATION_STATE = PAUSED )
          | ( <table_stretch_options> [, ...n] )
        }
            )
    }
  
<table_stretch_options> ::=
    {
     [ FILTER_PREDICATE = { null | table_predicate_function } , ]
       MIGRATION_STATE = { OUTBOUND | INBOUND | PAUSED }
    }
  
<single_partition_rebuild__option> ::=
{
      SORT_IN_TEMPDB = { ON | OFF }
    | MAXDOP = max_degree_of_parallelism
    | DATA_COMPRESSION = { NONE | ROW | PAGE | COLUMNSTORE | COLUMNSTORE_ARCHIVE} }
    | ONLINE = { ON [( <low_priority_lock_wait> ) ] | OFF }
}
  
<low_priority_lock_wait>::=
{
    WAIT_AT_LOW_PRIORITY ( MAX_DURATION = <time> [ MINUTES ],
        ABORT_AFTER_WAIT = { NONE | SELF | BLOCKERS } )
}
```

> [!NOTE]
> Para obter informações adicionais, consulte:
>
> - [ALTER TABLE column_constraint](alter-table-column-constraint-transact-sql.md)
> - [ALTER TABLE column_definition](alter-table-column-definition-transact-sql.md)
> - [ALTER TABLE computed_column_definition](alter-table-computed-column-definition-transact-sql.md)
> - [ALTER TABLE index_option](alter-table-index-option-transact-sql.md)
> - [ALTER TABLE table_constraints](alter-table-table-constraint-transact-sql.md)

## <a name="syntax-for-memory-optimized-tables"></a>Sintaxe para tabelas com otimização de memória

```
ALTER TABLE { database_name.schema_name.table_name | schema_name.table_name | table_name }
{
    ALTER COLUMN column_name
    {
        [ type_schema_name. ] type_name
            [ (
                {
                   precision [ , scale ]
                }
            ) ]
        [ COLLATE collation_name ]
        [ NULL | NOT NULL ]
    }

    | ALTER INDEX index_name
    {
        [ type_schema_name. ] type_name
        REBUILD
        [ [ NONCLUSTERED ] WITH ( BUCKET_COUNT = bucket_count )
        ]
    }

    | ADD
    {
        <column_definition>
      | <computed_column_definition>
      | <table_constraint>
      | <table_index>
      | <column_index>
    } [ ,...n ]
  
    | DROP
     [ {
         CONSTRAINT [ IF EXISTS ]
         {
              constraint_name
          } [ ,...n ]
        | INDEX [ IF EXISTS ]
      {
         index_name
       } [ ,...n ]
          | COLUMN [ IF EXISTS ]
          {
              column_name
          } [ ,...n ]
          | PERIOD FOR SYSTEM_TIME
     } [ ,...n ]
    | [ WITH { CHECK | NOCHECK } ] { CHECK | NOCHECK } CONSTRAINT
        { ALL | constraint_name [ ,...n ] }

    | { ENABLE | DISABLE } TRIGGER
        { ALL | trigger_name [ ,...n ] }
  
    | SWITCH [ [ PARTITION ] source_partition_number_expression ]
        TO target_table
        [ PARTITION target_partition_number_expression ]
        [ WITH ( <low_priority_lock_wait> ) ]
    
}
[ ; ]

-- ALTER TABLE options

< table_constraint > ::=
 [ CONSTRAINT constraint_name ]
{
   {PRIMARY KEY | UNIQUE }
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
{[ NONCLUSTERED ] HASH (column [ ,... n ] ) WITH (BUCKET_COUNT = bucket_count)
  | [ NONCLUSTERED ] (column [ ASC | DESC ] [ ,... n ] )
      [ ON filegroup_name | default ]
  | CLUSTERED COLUMNSTORE [WITH ( COMPRESSION_DELAY = {0 | delay [Minutes]})]
      [ ON filegroup_name | default ]
}

```

```
-- Syntax for Azure Synapse Analytics and Analytics Platform System

ALTER TABLE { database_name.schema_name.source_table_name | schema_name.source_table_name | source_table_name }
{
    ALTER COLUMN column_name
        {
            type_name [ ( precision [ , scale ] ) ]
            [ COLLATE Windows_collation_name ]
            [ NULL | NOT NULL ]
        }
    | ADD { <column_definition> | <column_constraint> FOR column_name} [ ,...n ]
    | DROP { COLUMN column_name | [CONSTRAINT] constraint_name } [ ,...n ]
    | REBUILD {
            [ PARTITION = ALL [ WITH ( <rebuild_option> ) ] ]
          | [ PARTITION = partition_number [ WITH ( <single_partition_rebuild_option> ] ]
      }
    | { SPLIT | MERGE } RANGE (boundary_value)
    | SWITCH [ PARTITION source_partition_number
        TO target_table_name [ PARTITION target_partition_number ] [ WITH ( TRUNCATE_TARGET = ON | OFF )
}
[;]

<column_definition>::=
{
    column_name
    type_name [ ( precision [ , scale ] ) ]
    [ <column_constraint> ]
    [ COLLATE Windows_collation_name ]
    [ NULL | NOT NULL ]
}

<column_constraint>::=
    [ CONSTRAINT constraint_name ] 
    {
        DEFAULT DEFAULT constant_expression
        | PRIMARY KEY (column_name) NONCLUSTERED  NOT ENFORCED -- Applies to Azure Synapse Analytics only
        | UNIQUE (column_name) NOT ENFORCED -- Applies to Azure Synapse Analytics only
    }
<rebuild_option > ::=
{
    DATA_COMPRESSION = { COLUMNSTORE | COLUMNSTORE_ARCHIVE }
        [ ON PARTITIONS ( {<partition_number> [ TO <partition_number>] } [ , ...n ] ) ]
}

<single_partition_rebuild_option > ::=
{
    DATA_COMPRESSION = { COLUMNSTORE | COLUMNSTORE_ARCHIVE }
}
```

## <a name="arguments"></a>Argumentos

*database_name*  
O nome do banco de dados em que a tabela foi criada.

*schema_name*  
O nome do esquema ao qual a tabela pertence.

*table_name*  
O nome da tabela a ser alterada. Se a tabela não estiver no banco de dados atual ou não constar no esquema pertencente ao usuário atual, especifique explicitamente o banco de dados e o esquema.

ALTER COLUMN  
Especifica que a coluna nomeada será alterada ou modificada.

A coluna modificada não pode ser:

- Uma coluna com um tipo de dados **timestamp**.
- O ROWGUIDCOL para a tabela.
- Uma coluna computada ou usada em uma coluna computada.
- Usada em estatísticas geradas pela instrução CREATE STATISTICS. Os usuários precisam executar DROP STATISTICS para remover as estatísticas antes que ALTER COLUMN possa ter êxito.  Execute esta consulta para obter todas as colunas de estatísticas e as estatísticas criadas pelo usuário para uma tabela.

``` sql

SELECT s.name AS statistics_name  
      ,c.name AS column_name  
      ,sc.stats_column_id  
FROM sys.stats AS s  
INNER JOIN sys.stats_columns AS sc   
    ON s.object_id = sc.object_id AND s.stats_id = sc.stats_id  
INNER JOIN sys.columns AS c   
    ON sc.object_id = c.object_id AND c.column_id = sc.column_id  
WHERE s.object_id = OBJECT_ID('<table_name>'); 

```
   > [!NOTE]
   > As estatísticas que são geradas automaticamente pelo otimizador de consulta são descartadas automaticamente por ALTER COLUMN.

- Usada em uma restrição PRIMARY KEY ou [FOREIGN KEY] REFERENCES.
- Usada em uma restrição CHECK ou UNIQUE. Porém, a alteração do comprimento de uma coluna de comprimento variável usada em uma restrição CHECK ou UNIQUE é permitida.
- Associada com uma definição padrão. Entretanto, o comprimento, a precisão e a escala de uma coluna poderão ser alterados se o tipo de dados não for modificado.

O tipo de dados das colunas **text**, **ntext** e **image** pode ser alterado somente das seguintes maneiras:

- **text** a **varchar(max)** , **nvarchar(max)** ou **xml**
- **ntext** a **varchar(max)** , **nvarchar(max)** ou **xml**
- **image** a **varbinary(max)**

Algumas alterações de tipo de dados podem causar uma alteração nos dados. Por exemplo, alterar uma coluna **nchar** ou **nvarchar** para **char** ou **varchar** pode levar à conversão de caracteres estendidos. Para obter mais informações, veja [CAST e CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md). Reduzir a precisão ou escala de uma coluna pode causar o truncamento de dados.

> [!NOTE]
> O tipo de dados de uma coluna em uma tabela particionada não pode ser alterado.
>
> O tipo de dados de colunas incluídos em um índice não poderá ser alterado, a menos que a coluna seja um tipo de dados **varchar**, **nvarchar** ou **varbinary** e o novo tamanho seja igual ou maior que o tamanho anterior.
>
> Uma coluna incluída em uma restrição de chave primária não pode ser alterada de **NOT NULL** para **NULL**.

Ao usar o Always Encrypted (sem enclaves seguros), se a coluna que está sendo modificada estiver criptografada com “ENCRYPTED WITH”, você poderá alterar o tipo de dados para um tipo de dados compatível (como INT para BIGINT), mas não poderá alterar as configurações de criptografia.

Ao usar o Always Encrypted com enclaves seguros, você poderá alterar qualquer configuração de criptografia, se a chave de criptografia de coluna que protege a coluna (e a nova chave de criptografia de coluna, se estiver alterando a chave) for compatível com cálculos de enclave (criptografada com chaves mestras de coluna habilitadas para enclave). Para conhecer detalhes, consulte [Always Encrypted com enclaves seguros](../../relational-databases/security/encryption/always-encrypted-enclaves.md).

*column_name*  
O nome da coluna a ser alterada, adicionada ou removida. O máximo para *nome_da_coluna* é 128 caracteres. Para novas colunas, é possível omitir *nome_da_coluna* para colunas criadas com um tipo de dados **timestamp**. O nome **timestamp** será usado se nenhum *nome_da_coluna* for especificado para uma coluna de tipo de dados **timestamp**.

> [!NOTE]
> Novas colunas são adicionadas após todas as colunas existentes na tabela sendo alterada.

[ _type\_schema\_name_ **.** ] _type\_name_  
O novo tipo de dados da coluna alterada ou o tipo de dados da coluna adicionada. Não é possível especificar *type_name* para colunas de tabelas particionadas existentes. *type_name* pode ser qualquer um dos seguintes tipos:

- Um tipo de dados de sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
- Um tipo de dados do alias com base em um tipo de dados de sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Crie tipos de dados do alias com a instrução CREATE TYPE antes que possam ser usados em uma definição de tabela.
- Um tipo definido pelo usuário [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] e o esquema ao qual ele pertence. Crie tipos de dados definidos pelo usuário com a instrução CREATE TYPE antes que possam ser usados em uma definição de tabela.

Os seguintes são critérios para *type_name* de uma coluna alterada:

- O tipo de dados anterior deve ser implicitamente conversível para o novo tipo de dados.
- *type_name* não pode ser **timestamp**.
- Padrões ANSI_NULL estão sempre ativados para ALTER COLUMN; se não for especificado, a coluna permite valor nulo.
- O preenchimento ANSI_PADDING está sempre ON para ALTER COLUMN.
- Se a coluna modificada for uma coluna de identidade, *new_data_type* deverá ser um tipo de dados compatível com a propriedade de identidade.
- A configuração atual para SET ARITHABORT é ignorada. ALTER TABLE operará como se ARITHABORT estivesse definido como ON.

> [!NOTE]
> Se a cláusula COLLATE não for especificada, a alteração do tipo de dados de uma coluna fará com que uma ordenação seja modificada para a ordenação padrão do banco de dados.

*precisão*  
A precisão do tipo de dados especificado. Para obter mais informações sobre valores de precisão válidos, veja [Precisão, escala e comprimento](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).

*scale*  
A escala do tipo de dados especificado. Para obter mais informações sobre valores de escala válidos, veja [Precisão, escala e comprimento](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).

**max**  
Aplica-se apenas aos tipos de dados **varchar**, **nvarchar** e **varbinary** para armazenar 2^31-1 bytes de caractere, dados binários e dados Unicode.

*xml_schema_collection*  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

Aplica-se apenas ao tipo de dados **xml** para associar um esquema XML ao tipo. Antes de digitar uma coluna **xml** em uma coleção de esquema, crie primeiro a coleção de esquema no banco de dados usando [CREATE XML SCHEMA COLLECTION](../../t-sql/statements/create-xml-schema-collection-transact-sql.md).

COLLATE \< *collation_name* >  
Especifica a nova ordenação para a coluna alterada. Se não for especificado, à coluna será atribuída a ordenação padrão do banco de dados. O nome da ordenação pode ser um nome de ordenação do Windows ou um nome de ordenação SQL. Para obter uma lista e mais informações, veja [Nome da ordenação do Windows](../../t-sql/statements/windows-collation-name-transact-sql.md) e [Nome de ordenação do SQL Server](../../t-sql/statements/sql-server-collation-name-transact-sql.md).

A cláusula COLLATE altera as ordenações somente de colunas dos tipos de dados **char**, **varchar**, **nchar** e **nvarchar**. Para alterar a ordenação de uma coluna de tipo de dados de alias definido pelo usuário, use instruções ALTER TABLE separadas para alterar a coluna para um tipo de dados de sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Depois, altere novamente a coluna e a ordenação para um tipo de dados de alias.

ALTER COLUMN não poderá ter uma alteração de ordenação se ocorrer uma ou mais das condições a seguir:

- Se uma restrição CHECK, FOREIGN KEY ou colunas computadas referenciarem a coluna alterada.
- Se forem criados qualquer índice, estatísticas ou índice de texto completo na coluna. As estatísticas criadas automaticamente na coluna alterada serão descartadas se a ordenação da coluna for alterada.
- Se uma função ou exibição associada a esquema referenciar a coluna.

Para obter mais informações, consulte [COLLATE](~/t-sql/statements/collations.md).

NULL | NOT NULL  
Especifica se a coluna pode aceitar valores nulos. As colunas que não permitem valores nulos podem ser adicionadas com ALTER TABLE apenas se tiverem um padrão especificado ou se a tabela estiver vazia. Será possível especificar NOT NULL para colunas computadas somente se PERSISTED também for especificado. Se a nova coluna permitir valores nulos e você não especificar um padrão, a nova coluna conterá um valor nulo para cada linha da tabela. Se a nova coluna permitir valores nulos e uma definição padrão for adicionada com a nova coluna, você poderá usar WITH VALUES para armazenar o valor padrão na nova coluna para cada linha existente na tabela.

Se a nova coluna não permite valores nulos e a tabela não estiver vazia, será preciso adicionar uma definição DEFAULT com a nova coluna. E a nova coluna será carregada automaticamente com o valor padrão nas novas colunas em cada linha existente.

É possível especificar NULL em ALTER COLUMN para forçar uma coluna NOT NULL a permitir valores nulos, exceto no caso de colunas nas restrições PRIMARY KEY. NOT NULL poderá ser especificado em ALTER COLUMN apenas se a coluna não contiver nenhum valor nulo. Os valores nulos devem ser atualizados para algum valor antes que ALTER COLUMN NOT NULL seja permitido. Por exemplo:

```sql
UPDATE MyTable SET NullCol = N'some_value' WHERE NullCol IS NULL;
ALTER TABLE MyTable ALTER COLUMN NullCOl NVARCHAR(20) NOT NULL;
```

Quando você cria ou altera uma tabela com a instrução CREATE TABLE ou ALTER TABLE, as configurações de banco de dados e de sessão influenciam e, possivelmente, substituem a nulidade do tipo de dados que é usado em uma definição de coluna. Certifique-se de sempre definir explicitamente uma coluna como NULL ou NOT NULL para colunas não computadas.

Se você adicionar uma coluna com um tipo de dados definido pelo usuário, defina a coluna com a mesma nulidade que o tipo de dados definido pelo usuário. Além disso, especifique um valor padrão para a coluna. Para obter mais informações, confira [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md).

> [!NOTE]
> Se NULL ou NOT NULL for especificado com ALTER COLUMN *new_data_type* [(*precision* [, *scale* ])] também deverá ser especificado. Se o tipo de dados, a precisão e a escala não forem alterados, especifique os valores de coluna atuais.

[ {ADD | DROP} ROWGUIDCOL ]  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

Especifica que a propriedade ROWGUIDCOL propriedade é adicionada ou descartada da coluna especificada. ROWGUIDCOL indica que a coluna é uma coluna GUID de linha. Só é possível definir uma coluna **uniqueidentifier** por tabela como a coluna ROWGUIDCOL. E você só pode atribuir a propriedade ROWGUIDCOL a uma coluna **uniqueidentifier**. Não é possível atribuir ROWGUIDCOL a uma coluna de um tipo de dados definido pelo usuário.

ROWGUIDCOL não impõe exclusividade para os valores armazenados na coluna e não gera valores automaticamente para novas linhas inseridas na tabela. Para gerar valores exclusivos para cada coluna, use a função NEWID ou NEWSEQUENTIALID em instruções INSERT. Ou especifique a função NEWID ou NEWSEQUENTIALID como o padrão para a coluna.

[ {ADD | DROP} PERSISTED ]  
Especifica que a propriedade PERSISTED é adicionada ou descartada da coluna especificada. A coluna deve ser uma coluna computada definida com uma expressão determinista. No caso de colunas especificadas como PERSISTED, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] armazenará fisicamente os valores computados na tabela e os atualizará quando qualquer outra coluna, da qual depende a coluna computada, for atualizada. Ao marcar uma coluna computada como PERSISTED, é possível criar índices em colunas computadas definidas em expressões que são determinísticas, mas não precisas. Para obter mais informações, consulte [Indexes on Computed Columns](../../relational-databases/indexes/indexes-on-computed-columns.md).

Qualquer coluna computada usada como coluna de particionamento de uma tabela particionada deve ser explicitamente marcada como PERSISTED.

DROP NOT FOR REPLICATION  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

Especifica que os valores são incrementados em colunas de identidade quando os agentes de replicação executam operações de inserção. Será possível especificar essa cláusula somente se *nome_da_coluna* for uma coluna de identidade.

SPARSE  
Indica que a coluna é uma coluna esparsa. O armazenamento de colunas esparsas é otimizado para obter valores nulos. Não é possível definir as colunas esparsas como NOT NULL. A conversão de uma coluna de esparsa para não esparsa, ou vice-versa, bloqueia a tabela durante a execução do comando. Talvez você precise usar a cláusula REBUILD para reclamar qualquer economia de espaço. Para obter restrições adicionais e mais informações sobre colunas esparsas, consulte [Usar colunas esparsas](../../relational-databases/tables/use-sparse-columns.md).

ADD MASKED WITH ( FUNCTION = ' *mask_function* ')  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

Especifica uma máscara de dados dinâmicos. *mask_function* é o nome da função de mascaramento com os parâmetros apropriados. Três funções estão disponíveis:

- default()
- email()
- partial()
- random()

Para remover uma máscara, use `DROP MASKED`. Para parâmetros de função, consulte [Máscara de Dados Dinâmicos](../../relational-databases/security/dynamic-data-masking.md).

WITH ( ONLINE = ON | OFF) \<conforme se aplica a alterar uma coluna>  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

Permite que muitas ações de alteração de coluna sejam executadas enquanto a tabela permanece disponível. O padrão é OFF. É possível executar a alteração da coluna online para as alterações de coluna relacionadas ao tipo de dados, comprimento da coluna ou precisão, nulidade, dispersão e ordenação.

A alteração online de coluna permite que as estatísticas automáticas e criadas pelo usuário usem como referência a coluna alterada durante a operação ALTER COLUMN, o que permite a execução normal de consultas. No final da operação, as estatísticas automáticas que fazem referência à coluna são descartadas e as estatísticas criadas pelo usuário são invalidadas. O usuário deve atualizar manualmente as estatísticas geradas pelo usuário após a conclusão da operação. Se a coluna fizer parte de uma expressão de filtro para estatísticas ou índices, você não poderá executar uma operação de alteração de coluna.

- Enquanto a operação de alteração online de coluna estiver em execução, todas as operações que dependem da coluna (índice, exibições e assim por diante) serão bloqueadas ou falharão com um erro apropriado. Esse comportamento garante que a alteração online de coluna não falhe devido a dependências introduzidas enquanto a operação estiver em execução.
- A alteração de uma coluna de NOT NULL para NULL não tem suporte como uma operação online quando a coluna alterada é referenciada por índices não clusterizados.
- Não há suporte para alteração online quando a coluna é referenciada por uma restrição de verificação e a operação de alteração está restringindo a precisão da coluna (numérica ou de data e hora).
- A opção `WAIT_AT_LOW_PRIORITY` não pode ser usada com a alteração online de coluna.
- `ALTER COLUMN ... ADD/DROP PERSISTED` não é compatível para a coluna de alteração online.
- `ALTER COLUMN ... ADD/DROP ROWGUIDCOL/NOT FOR REPLICATION` não é afetado pela coluna de alteração online.
- A alteração online de coluna não dá suporte à alteração de uma tabela em que o controle de alterações está habilitado ou é um publicador de replicação de mesclagem.
- A alteração online de coluna não dá suporte à alteração de ou para tipos de dados CLR.
- A alteração online de coluna não dá suporte à alteração para um tipo de dados XML que tem uma coleção de esquema diferente da coleção de esquema atual.
- A alteração online de coluna não reduz as restrições nem determina quando uma coluna pode ser alterada. Referências de índice/estatísticas e assim por diante podem causar falha na alteração.
- A alteração online de coluna não dá para suporte a alteração de mais de uma coluna simultaneamente.
- A alteração online de coluna não tem nenhum efeito no caso da tabela temporal com versão do sistema. A coluna ALTER não é executada online, independentemente de qual valor tenha sido especificado para a opção ONLINE.

A alteração online de coluna tem requisitos, restrições e funcionalidades similares à recompilação de índice online, o que inclui:

- A recompilação de índice online não é compatível quando a tabela contém colunas LOB ou filestream herdadas ou quando a tabela tem um índice columnstore. As mesmas limitações se aplicam à alteração de coluna online.
- Uma coluna existente que está sendo alterada requer duas vezes a alocação de espaço; para a coluna original e para a coluna oculta recém-criada.
- A estratégia de bloqueio durante uma operação de alteração online de coluna segue o mesmo padrão de bloqueio usado para criação de índice online.

WITH CHECK | WITH NOCHECK  
Especifica se os dados na tabela são ou não validados com relação à restrição FOREIGN KEY ou CHECK recentemente adicionada ou reabilitada. Se não especificado, WITH CHECK é considerado para novas restrições e WITH NOCHECK é considerado para restrições reabilitadas.

Se você não quiser verificar novas restrições CHECK ou FOREIGN KEY com relação aos dados existentes, use WITH NOCHECK. Não recomendamos fazer isso, com raríssimas exceções. A nova restrição é avaliada em todas as atualizações de dados posteriores. Qualquer violação que seja suprimida por WITH NOCHECK ao adicionar a restrição pode gerar falha em atualizações futuras caso elas atualizem as linhas com dados que não sigam a restrição.

> [!NOTE]
> O otimizador de consulta não considera restrições definidas WITH NOCHECK. Tais restrições são ignoradas até que sejam reabilitadas, usando `ALTER TABLE table WITH CHECK CHECK CONSTRAINT ALL`.

ALTER INDEX *index_name*  
Especifica que o número de buckets para *index_name* foi alterado ou modificado.

A sintaxe ALTER TABLE... ADD/DROP/ALTER INDEX só tem suporte para tabelas com otimização de memória.

> [!IMPORTANT]
> Sem o uso de uma instrução ALTER TABLE, não há suporte para as instruções [CREATE INDEX](create-index-transact-sql.md), [DROP INDEX](drop-index-transact-sql.md), [ALTER INDEX](alter-index-transact-sql.md) e [PAD_INDEX](alter-table-index-option-transact-sql.md) para índices em tabelas com otimização de memória.

ADD  
Especifica que uma ou mais definições de coluna, definições de coluna computada ou restrições de tabela são adicionadas. Ou as colunas que o sistema usa para controle de versão do sistema são adicionadas. Para tabelas com otimização de memória, é possível adicionar um índice.

> [!NOTE]
> Novas colunas são adicionadas após todas as colunas existentes na tabela sendo alterada.

> [!IMPORTANT]
> Sem o uso de uma instrução ALTER TABLE, não há suporte para as instruções [CREATE INDEX](create-index-transact-sql.md), [DROP INDEX](drop-index-transact-sql.md), [ALTER INDEX](alter-index-transact-sql.md) e [PAD_INDEX](alter-table-index-option-transact-sql.md) para índices em tabelas com otimização de memória.

PERIOD FOR SYSTEM_TIME ( system_start_time_column_name, system_end_time_column_name )  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

Especifica os nomes das colunas que o sistema usará para registrar o período em que um registro é válido. Você pode especificar colunas existentes ou criar novas colunas como parte do argumento ADD PERIOD FOR SYSTEM_TIME. Configure as colunas o datatype de datetime2 e as defina como NOT NULL. Se você definir uma coluna de período como NULL, um erro será gerado. Você pode definir [column_constraint](../../t-sql/statements/alter-table-column-constraint-transact-sql.md) e/ou [Especificar Valores Padrão para Colunas](../../relational-databases/tables/specify-default-values-for-columns.md) para as colunas system_start_time e system_end_time. Consulte o Exemplo A nos exemplos de [Controle de versão do sistema](#system_versioning) a seguir, que demonstram o uso de um valor padrão para a coluna system_end_time.

Use esse argumento com o argumento SET SYSTEM_VERSIONING para habilitar o controle de versão do sistema em uma tabela existente. Para obter mais informações, veja [Tabelas temporais](../../relational-databases/tables/temporal-tables.md) e [Introdução às tabelas temporais no Banco de Dados SQL do Azure](https://azure.microsoft.com/documentation/articles/sql-database-temporal-tables/).

Do [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] em diante, os usuários poderão marcar uma ou ambas as colunas de período com o sinalizador **HIDDEN** para implicitamente ocultar essas colunas, de modo que **SELECT \* FROM \<nome_da_tabela>** não retorne um valor para as colunas. Por padrão, as colunas de período não ficam ocultas. Para serem usadas, colunas ocultas devem ser explicitamente incluídas em todas as consultas que fazem referência direta à tabela temporal.

DROP  
Especifica que uma ou mais definições de coluna, definições de coluna computada ou restrições de tabela são removidas ou remove a especificação das colunas que o sistema usa para controle de versão do sistema.

CONSTRAINT *constraint_name*  
Especifica que *constraint_name* é removida da tabela. Várias restrições podem ser listadas.

O nome definido pelo usuário ou fornecido pelo sistema das restrições pode ser determinado ao consultar as exibições do catálogo **restrição_sys.check**, **restrições_sys.default**, **restrições_sys.key** e **chaves_sys.foreign**.

Uma restrição PRIMARY KEY não poderá ser descartada se um índice XML existir na tabela.

INDEX *index_name*  
Especifica que *index_name* foi removido da tabela.

A sintaxe ALTER TABLE... ADD/DROP/ALTER INDEX só tem suporte para tabelas com otimização de memória.

> [!IMPORTANT]
> Sem o uso de uma instrução ALTER TABLE, não há suporte para as instruções [CREATE INDEX](create-index-transact-sql.md), [DROP INDEX](drop-index-transact-sql.md), [ALTER INDEX](alter-index-transact-sql.md) e [PAD_INDEX](alter-table-index-option-transact-sql.md) para índices em tabelas com otimização de memória.

COLUMN *column_name*  
Especifica que *constraint_name* ou *column_name* é removida da tabela. Várias colunas podem ser listadas.

 Uma coluna não pode ser descartada quando for:

- Usado em um índice, como uma coluna de chave ou um INCLUDE
- Usada em uma restrição CHECK, FOREIGN KEY, UNIQUE ou PRIMARY KEY.
- Associada a um padrão que é definido com a palavra-chave DEFAULT ou associada com um objeto padrão.
- Associada a uma regra.

> [!NOTE]
> Descartar uma coluna não recupera o espaço em disco da coluna. Talvez seja necessário recuperar o espaço em disco de uma coluna descartada quando o tamanho da linha de uma tabela estiver próximo do limite ou o exceder. Recupere o espaço, criando um índice clusterizado da tabela ou recriando um índice clusterizado existente usando [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md). Para obter informações sobre o impacto de remover tipos de dados LOB, consulte esta [entrada de blog CSS](https://blogs.msdn.com/b/psssql/archive/2012/12/03/how-it-works-gotcha-varchar-max-caused-my-queries-to-be-slower.aspx).

PERIOD FOR SYSTEM_TIME  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

Descarta a especificação para as colunas que o sistema usará para controle de versão do sistema.

WITH \<drop_clustered_constraint_option>  
Especifica que há uma ou mais opções de descarte de restrição clusterizada definidas.

MAXDOP = *max_degree_of_parallelism*  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

Substitui a opção de configuração de **grau máximo de paralelismo** apenas para a duração da operação. Para obter mais informações, veja [Configurar a opção max degree of parallelism de configuração de servidor](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).

Use a opção MAXDOP para limitar o número de processadores usados na execução do plano paralelo. O máximo é de 64 processadores.

*max_degree_of_parallelism* pode ser um dos seguintes valores:

1  
Suprime a geração de plano paralelo.

\>1  
Restringe o número máximo de processadores usados em uma operação de índice paralela ao número especificado.

0 (padrão)  
Usa o número real de processadores, ou menos, com base na carga de trabalho atual do sistema.

Para obter mais informações, consulte [Configurar operações de índice paralelo](../../relational-databases/indexes/configure-parallel-index-operations.md).

> [!NOTE]
> As operações de índice paralelas não estão disponíveis em todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para saber mais, confira [Edições e recursos com suporte para o SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md) e [Edições e recursos com suporte para o SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md).

ONLINE **=** { ON | **OFF** } \<conforme se aplica a drop_clustered_constraint_option>  
Especifica se as tabelas subjacentes e os índices associados estão disponíveis para consultas e modificação de dados durante a operação de índice. O padrão é OFF. É possível executar REBUILD como uma operação ONLINE.

ATIVADO  
Bloqueios de tabela de longa duração não são mantidos durante a operação do índice. Durante a fase principal da operação de índice, apenas um bloqueio IS (Tentativa Compartilhada) é mantido na tabela de origem. Esse comportamento permite a continuação de consultas ou atualizações feitas na tabela e nos índices subjacentes. No início da operação, um bloqueio compartilhado (S) é mantido no objeto de origem por um curto período. Ao término da operação, por um curto período, um bloqueio S (Compartilhado) será adquirido na origem se um índice não clusterizado estiver sendo criado. Ou um bloqueio SCH-M (Modificação de Esquema) será adquirido quando um índice clusterizado for criado ou descartado online e quando um índice clusterizado ou não clusterizado estiver sendo recriado. Não será possível definir ONLINE como ON quando um índice estiver sendo criado em uma tabela temporária local. Apenas a operação de reconstrução de heap de thread único é permitida.

Para executar a DDL de **SWITCH** ou a recompilação de índice online, todas as transações de bloqueio ativas em execução em uma tabela específica devem ser concluídas. Durante a execução, **SWITCH** ou a operação de recompilação impede que a nova transação seja iniciada e pode afetar significativamente a taxa de transferência da carga de trabalho e atrasar temporariamente o acesso à tabela subjacente.

OFF  
Os bloqueios de tabela são aplicados enquanto durar a operação de índice. Uma operação de índice offline que cria, recria ou cancela um índice clusterizado ou recria ou cancela um índice não clusterizado, adquire um bloqueio de esquema de modificação (Sch-M) na tabela. Isso impede o acesso de todos os usuários à tabela subjacente enquanto durar a operação. Uma operação de índice offline que cria um índice não clusterizado adquire um bloqueio Compartilhado (S) na tabela. Isso impede atualizações na tabela subjacente, mas permite operações de leitura, como instruções SELECT. Permite operações de reconstrução de heap multi-threaded.

Para obter mais informações, consulte [Como funcionam as operações de índice online](../../relational-databases/indexes/how-online-index-operations-work.md).

> [!NOTE]
> As operações de índice online não estão disponíveis em todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para saber mais, confira [Edições e recursos com suporte para o SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md) e [Edições e recursos com suporte para o SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md).

MOVE TO { _partition\_scheme\_name_ **(** _column\_name_ [ 1 **,** ... *n*] **)**  | *filegroup* |  **"** default **"** }  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

Especifica o local para onde mover as linhas de dados atualmente no nível folha do índice clusterizado. A tabela é movida para o novo local. Esta opção se aplica apenas a restrições que criam um índice clusterizado.

> [!NOTE]
> Nesse contexto, default não é uma palavra-chave. É um identificador do grupo de arquivos padrão e deve ser delimitado, como em MOVE TO **"** default **"** ou MOVE TO **[** default **]** . Se **"** default **"** for especificado, a opção QUOTED_IDENTIFIER deverá ser ON para a sessão atual. Essa é a configuração padrão. Para saber mais, confira [SET QUOTED_IDENTIFIER](../../t-sql/statements/set-quoted-identifier-transact-sql.md).

{ CHECK | NOCHECK } CONSTRAINT  
Especifica que *constraint_name* está habilitado ou desabilitado. Essa opção só pode ser usada com restrições FOREIGN KEY e CHECK. Quando NOCHECK é especificado, a restrição é desabilitada e futuras inserções ou atualizações da coluna não são validadas com relação às condições de restrição. As restrições DEFAULT, PRIMARY KEY e UNIQUE não podem ser desabilitadas.

ALL  
Especifica que todas as restrições são desabilitadas com a opção NOCHECK ou habilitado com a opção CHECK.

{ ENABLE | DISABLE } TRIGGER  
Especifica que *trigger_name* está habilitado ou desabilitado. Quando um gatilho é desabilitado, ele ainda permanece definido para a tabela. Porém, quando a instrução INSERT, UPDATE ou DELETE é executada na tabela, as ações no gatilho não são realizadas até que ele seja reabilitado.

ALL  
Especifica que todos os gatilhos na tabela são habilitados ou desabilitados.

*trigger_name*  
Especifica o nome do gatilho a ser desabilitado ou habilitado.

{ ENABLE | DISABLE } CHANGE_TRACKING  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

Especifica se controle de alterações está habilitado ou desabilitado para a tabela. Por padrão, o controle de alterações está desabilitado.

Essa opção só estará disponível quando o controle de alterações estiver habilitado para o banco de dados. Para obter mais informações, veja [Opções ALTER DATABASE SET (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-set-options.md).

Para habilitar o controle de alterações, a tabela deve ter uma chave primária.

WITH **(** TRACK_COLUMNS_UPDATED **=** { ON | **OFF** } **)**  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

Especifica se o [!INCLUDE[ssDE](../../includes/ssde-md.md)] controla quais colunas com alteração controlada foram atualizadas. O valor padrão é OFF.

SWITCH [ PARTITION *source_partition_number_expression* ] TO [ _schema\_name_ **.** ] *target_table* [ PARTITION *target_partition_number_expression* ]  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

Alterna um bloco de dados em um dos seguintes modos:

- Reatribui todos os dados de uma tabela como uma partição para uma tabela particionada já existente.
- Alterna uma partição de uma tabela particionada para outra.
- Reatribui todos os dados em uma partição de uma tabela particionada para uma tabela não particionada existente.

Se *tabela* for uma tabela particionada, será preciso especificar *expressão_do_número_da_partição_de_origem*. Se *tabela_de_destino* for uma tabela particionada, será preciso especificar *expressão_do_número_da_partição_de_destino*. Na reatribuição dos dados de uma tabela com uma partição para uma tabela particionada já existente ou alternando uma partição de uma tabela particionada para outra, a partição de destino deve existir e estar vazia.

Na reatribuição dos dados de uma partição para formar uma tabela única, a tabela de destino já deve existir e estar vazia. A tabela de origem ou a partição e a tabela de destino ou a partição devem estar localizadas no mesmo grupo de arquivos. Os índices correspondentes ou as partições de índice também devem estar localizadas no mesmo grupo de arquivos. Muitas restrições adicionais são aplicadas para alternância de partições. *tabela* e *tabela_de_destino* não podem ser iguais. *target_table* pode ser um identificador de várias partes.

*source_partition_number_expression* e *target_partition_number_expression* são expressões de constante que podem fazer referência a variáveis e funções. Eles incluem variáveis de tipo definidas pelo usuário e funções definidas pelo usuário. Eles não podem referenciar expressões [!INCLUDE[tsql](../../includes/tsql-md.md)].

Uma tabela particionada com um índice clusterizado columnstore se comporta como um heap particionado:

- A chave primária deve incluir a chave de partição.
- Um índice exclusivo deve incluir a chave de partição. Incluir a chave de partição com um índice exclusivo existente pode alterar a exclusividade.
- Para mudar as partições, todos os índices não clusterizados devem incluir a chave de partição.

Para a restrição **SWITCH** ao usar replicação, consulte [Replicar tabelas e índices particionados](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md).

Índices columnstore não clusterizados criados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 CTP1 e para o Banco de Dados SQL antes da versão V12 estavam em um formato somente leitura. É preciso recompilar índices columnstore não clusterizado para o formato atual (que é atualizável) antes de quaisquer operações de partição serem executadas.

SET **(** FILESTREAM_ON = { *partition_scheme_name* | *filestream_filegroup_name* |  **"** default **"**  |  **"** NULL **"** } **)**  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior). [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] não dá suporte a `FILESTREAM`.

Especifica onde os dados FILESTREAM são armazenados.

ALTER TABLE com a cláusula SET FILESTREAM_ON só terá sucesso se a tabela não tiver nenhuma coluna FILESTREAM. É possível adicionar colunas FILESTREAM usando uma segunda instrução ALTER TABLE.

Se você especificar *partition_scheme_name*, as regras para [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) se aplicarão. A tabela já deve estar particionada para dados de linha e seu esquema de partição usa a mesma função de partição e colunas que o esquema de partição FILESTREAM.

*filestream_filegroup_name* especifica o nome de um grupo de arquivos FILESTREAM. O grupo de arquivos deve ter um arquivo definido para o grupo de arquivos usando uma instrução [CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md?view=sql-server-2017) ou [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md). Caso contrário, será gerado um erro.

**"** default **"** especifica o grupo de arquivos FILESTREAM com a propriedade DEFAULT definida. Se não houver um grupo de arquivos FILESTREAM, ocorrerá um erro.

**"** NULL **"** especifica que sejam removidas todas as referências para grupos de arquivos FILESTREAM para a tabela. Todas as colunas FILESTREAM devem ser descartadas primeiro. Use SET FILESTREAM_ON **="** NULL **"** para excluir todos os dados FILESTREAM associados a uma tabela.

SET **(** SYSTEM_VERSIONING **=** { OFF | ON [ ( HISTORY_TABLE = schema_name. history_table_name [ , DATA_CONSISTENCY_CHECK = { **ON** | OFF } ]) ] } **)**  
 **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

Desabilita ou habilita o controle de versão do sistema de uma tabela. Para habilitar o controle de versão do sistema de uma tabela, o sistema verifica se o tipo de dados, a restrição de nulidade e requisitos de restrição de chave primária para o controle de versão do sistema são atendidos. Se você não usar o argumento HISTORY_TABLE, o sistema gerará uma nova tabela de histórico correspondendo ao esquema da tabela atual, criando um link entre as duas tabelas e permitindo que o sistema registre o histórico de cada registro na tabela atual na tabela de histórico. O nome desta tabela de histórico será `MSSQL_TemporalHistoryFor<primary_table_object_id>`. Se o argumento HISTORY_TABLE for usado para criar um vínculo e usar a tabela de histórico existente, o sistema criará um vínculo entre a tabela atual e a tabela especificada. Ao criar um link para uma tabela de histórico existente, você pode optar por executar uma verificação de consistência de dados. Essa verificação de consistência de dados garante que os registros existentes não se sobreponham. A execução da verificação de consistência dos dados é o padrão. Para saber mais, veja [Temporal Tables](../../relational-databases/tables/temporal-tables.md).

HISTORY_RETENTION_PERIOD = { **INFINITE** | number {DAY | DAYS | WEEK | WEEKS | MONTH | MONTHS | YEAR | YEARS} }  
**Aplica-se a**: [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

Especifica a retenção finita ou infinita para dados históricos em tabela temporais. Se omitido, será presumida retenção infinita.

SET **(** LOCK_ESCALATION = { AUTO | TABLE | DISABLE } **)**  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

Especifica os métodos permitidos de escalonamento de bloqueios para uma tabela.

AUTO  
Essa opção permite que o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] selecione a granularidade do escalonamento de bloqueios apropriado para o esquema da tabela.

- Se a tabela estiver particionada, o escalonamento de bloqueios será permitido para a granularidade HoBT (pilha ou árvore B). Em outras palavras, o escalonamento será permitido no nível da partição. Depois de ser escalonado para o nível de HoBT, o bloqueio não será escalonado posteriormente para a granularidade TABLE.
- Se a tabela não estiver particionada, o escalonamento de bloqueios será feito para a granularidade TABLE.

TABLE  
O escalonamento de bloqueios será feito na granularidade em nível de tabela, esteja a tabela particionada ou não. TABLE é o valor padrão.

DISABLE  
Impede o escalonamento de bloqueios na maioria dos casos. Os bloqueios em nível de tabela não são totalmente desautorizados. Por exemplo, quando você está verificando uma tabela que não tem nenhum índice clusterizado no nível de isolamento serializável, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve usar um bloqueio de tabela para proteger a integridade dos dados.

REBUILD  
Use a sintaxe REBUILD WITH para recriar uma tabela inteira que inclui todas as partições em uma tabela particionada. Se a tabela tiver um índice clusterizado, a opção REBUILD recriará o índice clusterizado. REBUILD pode ser executado como uma operação ONLINE.

Use a sintaxe REBUILD PARTITION para recriar uma única partição em uma tabela particionada.

PARTITION = ALL  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

Recria todas as partições ao alterar as configurações de compactação da partição.

REBUILD WITH ( \<rebuild_option> )  
Todas as opções se aplicam a uma tabela com um índice clusterizado. Se a tabela não tiver um índice clusterizado, a estrutura de heap será afetada somente por algumas opções.

Quando uma configuração de compactação específica não é especificada com a operação REBUILD, a configuração de compactação atual da partição é usada. Para retornar à configuração atual, consulte a coluna **data_compression** na exibição do catálogo **sys.partitions**.

Para obter descrições completas das opções de recompilação, veja [index_option](../../t-sql/statements/alter-table-index-option-transact-sql.md).

DATA_COMPRESSION  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

Especifica a opção de compactação de dados para a tabela, o número de partição ou o intervalo de partições especificado. As opções são as descritas a seguir:

NONE A tabela ou as partições especificadas não são compactadas. Essa opção não se aplica a tabelas columnstore.

ROW A tabela ou as partições especificadas são compactadas usando a compactação de linha. Essa opção não se aplica a tabelas columnstore.

PAGE A tabela ou as partições especificadas são compactadas usando a compactação de página. Essa opção não se aplica a tabelas columnstore.

COLUMNSTORE  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

Aplica-se somente a tabelas columnstore. COLUMNSTORE especifica a descompactação de uma partição compactada com a opção COLUMNSTORE_ARCHIVE. Quando os dados forem restaurados, eles continuarão sendo compactados por meio da compactação columnstore usada em todas as tabelas columnstore.

COLUMNSTORE_ARCHIVE  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

Aplica-se a tabelas columnstore, que são armazenadas com um índice columnstore clusterizado. COLUMNSTORE_ARCHIVE compactará ainda mais a partição especificada para um tamanho menor. Use essa opção para fins de arquivamento ou em outras situações que exijam menos armazenamento e possam dispensar mais tempo para armazenamento e recuperação.

Para recompilar várias partições ao mesmo tempo, veja [index_option](../../t-sql/statements/alter-table-index-option-transact-sql.md). Se a tabela não tiver um índice clusterizado, alterar a compactação de dados recriará o heap e os índices não clusterizados. Para obter mais informações sobre compactação, consulte [Compactação de dados](../../relational-databases/data-compression/data-compression.md).

ONLINE **=** { ON | **OFF** } \<conforme se aplica a single_partition_rebuild_option>  
Especifica se uma única partição das tabelas subjacentes e os índices associados estão disponíveis para consultas e modificação de dados durante a operação de índice. O padrão é OFF. É possível executar REBUILD como uma operação ONLINE.

ATIVADO  
Bloqueios de tabela de longa duração não são mantidos durante a operação do índice. Um bloqueio S na tabela é exigido no início da recompilação de índice e um bloqueio Sch-M na tabela no final da recompilação de índice online. Embora ambos os bloqueios sejam bloqueios de metadados curtos, o bloqueio Sch-M deve esperar que todas as transações de bloqueio sejam concluídas. Durante o tempo de espera, o bloqueio Sch-M bloqueia todas as transações restantes que esperam atrás desse bloqueio ao acessar a mesma tabela.

> [!NOTE]
> A recompilação de índice online pode definir as opções *low_priority_lock_wait* descritas posteriormente nesta seção.

OFF  
Os bloqueios de tabela são aplicados enquanto durar a operação de índice. Isso evita o acesso de todos os usuários à tabela subjacente enquanto durar a operação.

*column_set_name* XML COLUMN_SET FOR ALL_SPARSE_COLUMNS  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

O nome do conjunto de colunas. Um conjunto de colunas é uma representação em XML sem-tipo que combina todas as colunas esparsas de uma tabela em uma saída estruturada. Um conjunto de colunas não pode ser adicionado a uma tabela que contém colunas esparsas. Para obter mais informações sobre conjuntos de colunas, veja [Usar conjuntos de colunas](../../relational-databases/tables/use-column-sets.md).

{ ENABLE | DISABLE } FILETABLE_NAMESPACE  
 **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior).

Habilita ou desabilita as restrições definidas pelo sistema em uma FileTable. Pode ser usado apenas com uma FileTable.

SET ( FILETABLE_DIRECTORY = *directory_name* )  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior). [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] não dá suporte a `FILETABLE`.

Especifica o nome do diretório de FileTable compatível com o Windows. Esse nome deve ser exclusivo entre todos os nomes de diretórios de FileTable no banco de dados. A comparação de exclusividade não diferencia maiúsculas de minúsculas, apesar das configurações de ordenação do SQL. Pode ser usado apenas com uma FileTable.

```sql
 SET (
        REMOTE_DATA_ARCHIVE
        {
            = ON (<table_stretch_options> )
          | = OFF_WITHOUT_DATA_RECOVERY
          ( MIGRATION_STATE = PAUSED ) | ( <table_stretch_options> [, ...n] )
        } )
```

**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] e posterior).

Habilita ou desabilita o Stretch Database para uma tabela. Saiba mais em [Stretch Database](../../sql-server/stretch-database/stretch-database.md).

**Habilitar o Stretch Database para uma tabela**

Quando você habilita Stretch para uma tabela especificando `ON`, também precisa especificar `MIGRATION_STATE = OUTBOUND`, para começar a migração de dados imediatamente, ou `MIGRATION_STATE = PAUSED`, para adiar a migração de dados. O valor padrão é `MIGRATION_STATE = OUTBOUND`. Saiba mais sobre como habilitar o Stretch para uma tabela em [Habilitar o Stretch Database para uma tabela](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md).

**Pré-requisitos**. Antes de habilitar o Stretch para uma tabela, você precisa habilitar o Stretch no servidor e no banco de dados. Saiba mais em [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md).

**Permissões**. Habilitar o Stretch para um banco de dados ou uma tabela exige permissões db_owner. Habilitar o Stretch em uma tabela também requer permissões ALTER na tabela.

**Desabilitando o Stretch Database para uma tabela**

Quando você desabilitar o Stretch para uma tabela, tem duas opções para os dados remotos que já foram migrados para o Azure. Saiba mais em [Desabilitar Stretch Database e trazer de volta dados remotos](../../sql-server/stretch-database/disable-stretch-database-and-bring-back-remote-data.md).

- Para desabilitar o Stretch para uma tabela e copiar os dados remotos para a tabela do Azure de volta para o SQL Server, execute o comando a seguir. Esse comando não pode ser cancelado.

    ```sql
    ALTER TABLE <table_name>
       SET ( REMOTE_DATA_ARCHIVE ( MIGRATION_STATE = INBOUND ) ) ;
    ```

Essa operação incorre em custos de transferência de dados e não pode ser cancelada. Saiba mais em [Detalhes de preços de transferências de dados](https://azure.microsoft.com/pricing/details/data-transfers/).

Depois que todos os dados remotos forem copiados do Azure de volta para o SQL Server, o Stretch será desabilitado para a tabela.

- Para desabilitar o Stretch de uma tabela e abandonar os dados remotos, execute o comando a seguir.

    ```sql
    ALTER TABLE <table_name>
       SET ( REMOTE_DATA_ARCHIVE = OFF_WITHOUT_DATA_RECOVERY ( MIGRATION_STATE = PAUSED ) ) ;
    ```

Depois de desabilitar o Banco de Dados de Stretch de uma tabela, a migração de dados é interrompida e os resultados da consulta já não incluem os resultados da tabela remota.

Desabilitar o Stretch não remove a tabela remota. Se você quiser excluir o banco de dados remoto, descarte-o usando o portal do Azure.

[ FILTER_PREDICATE = { null | *predicate* } ]  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] e posterior).

Opcionalmente, especifique um predicado de filtro para selecionar linhas para migrar de uma tabela que contém dados atuais e históricos. O predicado deve chamar uma função com valor de tabela embutido determinística. Saiba mais em [Habilitar Stretch Database para uma tabela](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md) e [Selecionar linhas a serem migradas usando uma função de filtro – Stretch Database](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md).

> [!IMPORTANT]
> Se você fornecer um predicado de filtro precário, a migração de dados também será precária. O Stretch Database aplica o predicado de filtro à tabela usando o operador CROSS APPLY.

Se você não especificar um predicado de filtro, a tabela inteira será migrada.

Quando você especifica um predicado de filtro, também precisa especificar *MIGRATION_STATE*.

MIGRATION_STATE = { OUTBOUND | INBOUND | PAUSED }  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] e posterior).

- Especifique `OUTBOUND` para migrar dados do SQL Server para o Azure.
- Especifique `INBOUND` para copiar os dados remotos da tabela do Azure de volta para o SQL Server e para desabilitar o Stretch para a tabela. Saiba mais em [Desabilitar Stretch Database e trazer de volta dados remotos](../../sql-server/stretch-database/disable-stretch-database-and-bring-back-remote-data.md).

    Essa operação incorre em custos de transferência de dados e não pode ser cancelada.

- Especifique `PAUSED` para pausar ou adiar a migração de dados. Saiba mais em [Pausar e retomar a migração de dados – Stretch Database](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md).

WAIT_AT_LOW_PRIORITY  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

Uma recriação de índice online precisa aguardar as operações de bloqueio nesta tabela. **WAIT_AT_LOW_PRIORITY** indica que a operação de recompilação do índice online aguarda bloqueios de baixa prioridade, permitindo que outras operações sejam realizadas enquanto a operação de compilação de índice online está aguardando. Omitir a opção **WAIT AT LOW PRIORITY** é o mesmo que `WAIT_AT_LOW_PRIORITY ( MAX_DURATION = 0 minutes, ABORT_AFTER_WAIT = NONE)`.

MAX_DURATION = *time* [**MINUTES** ]  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

O tempo de espera, que é um valor inteiro especificado em minutos, que a opção **SWITCH** ou os bloqueios de recompilação de índice online aguardam com baixa prioridade ao executar o comando DDL. Se a operação for bloqueada por **MAX_DURATION**, uma das ações de **ABORT_AFTER_WAIT** será executada. O tempo **MAX_DURATION** está sempre em minutos, e a palavra **MINUTES** pode ser omitida.

ABORT_AFTER_WAIT = [**NONE** | **SELF** | **BLOCKERS** } ]  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

Nenhuma  
Continue aguardando o bloqueio com prioridade normal.

SELF  
Saia da operação DDL de recompilação de índice online ou **SWITCH** em execução no momento sem realizar nenhuma ação.

BLOCKERS  
Encerre todas as transações de usuário que bloqueiam atualmente a opção **SWITCH** ou a operação DDL de recompilação de índice online para que a operação possa continuar.

Requer a permissão **ALTER ANY CONNECTION**.

IF EXISTS  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

Descartará condicionalmente a coluna ou restrição somente se ela já existir.

## <a name="remarks"></a>Comentários

Para adicionar novas linhas de dados, use [INSERT](../../t-sql/statements/insert-transact-sql.md). Para remover linhas de dados, use [DELETE](../../t-sql/statements/delete-transact-sql.md) ou [TRUNCATE TABLE](../../t-sql/statements/truncate-table-transact-sql.md). Para modificar os valores nas linhas existentes, use [UPDATE](../../t-sql/queries/update-transact-sql.md).

Se houver qualquer plano de execução no cache de procedimento que referencie a tabela, ALTER TABLE o marcará para que seja recompilado na próxima execução.

## <a name="changing-the-size-of-a-column"></a>Alterando o tamanho de uma coluna

É possível alterar o comprimento, a precisão ou a escala de uma coluna, especificando um novo tamanho para o tipo de dados da coluna. Use a cláusula ALTER COLUMN. Se dados existirem na coluna, o novo tamanho não poderá ser menor do que o tamanho máximo dos dados. Além disso, não é possível definir a coluna em um índice, a menos que a coluna seja um tipo de dados **varchar**, **nvarchar** ou **varbinary** e o índice não seja o resultado de uma restrição PRIMARY KEY. Veja o exemplo na seção curta intitulada [Alterar uma definição de coluna](#alter_column).

## <a name="locks-and-alter-table"></a>Bloqueios e ALTER TABLE

As alterações especificadas em ALTER TABLE são implementadas imediatamente. Se as alterações requererem modificações das linhas na tabela, ALTER TABLE atualizará as linhas. ALTER TABLE adquire um bloqueio de modificação de esquema (SCH-M) na tabela para se certificar de que nenhuma outra conexão referencie nem mesmo os metadados da tabela durante a alteração, exceto as operações de índice online que exigem um bloqueio SCH-M curto no final. Em uma operação `ALTER TABLE...SWITCH`, o bloqueio é adquirido em tabelas de origem e de destino. As modificações feitas na tabela são registradas e completamente recuperáveis. As alterações que afetam todas as linhas em tabelas grandes, como descartar uma coluna ou, em algumas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], adicionar uma coluna NOT NULL com um valor padrão, podem demorar muito tempo para serem concluídas e gerar muitos registros de log. Execute essas instruções ALTER TABLE com o mesmo cuidado de outras instruções INSERT, UPDATE ou DELETE que podem afetar várias linhas.

### <a name="adding-not-null-columns-as-an-online-operation"></a>Adicionando colunas NOT NULL como uma operação online

Começando com o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Enterprise Edition, a adição de uma coluna NOT NULL com um valor padrão é uma operação online quando o valor padrão é uma *constante de runtime*. Isso significa que a operação é concluída quase instantaneamente, apesar do número de linhas na tabela. Isso porque as linhas existentes na tabela não são atualizadas durante a operação. Em vez disso, o valor padrão é armazenado somente nos metadados da tabela e o valor é pesquisado conforme necessário em consultas que acessam essas linhas. Esse comportamento é automático. Nenhuma sintaxe adicional é necessária para implementar a operação online, além da sintaxe ADD COLUMN. Uma constante de runtime é uma expressão que gera o mesmo valor no runtime para cada linha na tabela, independentemente de seu determinismo. Por exemplo, a expressão constante "Meus dados temporários" ou a função do sistema GETUTCDATETIME() são constantes de runtime. Por outro lado, as funções `NEWID()` ou `NEWSEQUENTIALID()` não são constantes de runtime porque é gerado um valor exclusivo para cada linha da tabela. A adição de uma coluna NOT NULL com um valor padrão que não é uma constante de runtime é sempre executada offline e um bloqueio exclusivo (SCH-M) é adquirido para a duração da operação.

Enquanto as linhas existentes referenciam o valor armazenado nos metadados, o valor padrão é armazenado na linha para qualquer nova linha inserida e não especifica outro valor para a coluna. O valor padrão armazenado nos metadados é movido para uma linha existente quando a linha é atualizada (mesmo que a coluna real não seja especificada na instrução UPDATE) ou quando a tabela ou o índice clusterizado é recompilado.

Colunas do tipo **varchar(max)** , **nvarchar(max)** , **varbinary(max)** , **xml**, **text**, **ntext**, **image**, **hierarchyid**, **geometry**, **geography** ou CLR UDTS não podem ser adicionadas a uma operação online. Não será possível adicionar uma coluna online se isso fizer o tamanho máximo de linha possível exceder o limite de 8.060 bytes. Nesse caso, a coluna é adicionada como uma operação offline.

## <a name="parallel-plan-execution"></a>Execução de plano paralelo

No [!INCLUDE[ssEnterpriseEd11](../../includes/ssenterpriseed11-md.md)] e superior, o número de processadores empregados para executar uma instrução ALTER TABLE ADD (baseada em índice) CONSTRAINT ou DROP (índice clusterizado) CONSTRAINT é determinado pela opção de configuração **grau máximo de paralelismo** e pela atual carga de trabalho. Se o [!INCLUDE[ssDE](../../includes/ssde-md.md)] detectar que o sistema está ocupado, o grau de paralelismo da operação será automaticamente reduzido antes do início da execução da instrução. É possível configurar manualmente o número de processadores usados para executar a instrução, especificando a opção de índice MAXDOP. Para obter mais informações, veja [Configurar a opção max degree of parallelism de configuração de servidor](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).

## <a name="partitioned-tables"></a>Tabelas particionadas

Além de realizar operações SWITCH que envolvem tabelas particionadas, use ALTER TABLE para alterar o estado de colunas, restrições e gatilhos de uma tabela particionada, exatamente da mesma forma que é usado em tabelas não particionadas. Porém, essa instrução não pode ser usada para alterar o modo que a própria tabela é particionada. Para reparticionar uma tabela particionada, use [ALTER PARTITION SCHEME](../../t-sql/statements/alter-partition-scheme-transact-sql.md) e [ALTER PARTITION FUNCTION](../../t-sql/statements/alter-partition-function-transact-sql.md). Além disso, não é possível alterar o tipo de dados de uma coluna em uma tabela particionada.

## <a name="restrictions-on-tables-with-schema-bound-views"></a>Restrições em tabelas com exibições associadas a esquema

As restrições que se aplicam a instruções ALTER TABLE em tabelas com exibições associadas a esquema são as mesmas atualmente aplicadas ao modificar tabelas com um índice simples. É permitido adicionar uma coluna. Porém, não é permitido remover ou alterar uma coluna que participa de qualquer exibição associada a esquema. Se a instrução ALTER TABLE requerer a alteração de uma coluna usada em uma exibição associada a esquema, ALTER TABLE irá falhar e o [!INCLUDE[ssDE](../../includes/ssde-md.md)] gerará uma mensagem de erro. Para obter mais informações sobre associação de esquema e exibições indexadas, veja [CREATE VIEW](../../t-sql/statements/create-view-transact-sql.md).

A adição ou remoção de gatilhos em tabelas base não é afetada pela criação de uma exibição associada a esquema que referencia tabelas.

## <a name="indexes-and-alter-table"></a>Índices e ALTER TABLE

Os índices criados como parte de uma restrição são descartados quando a restrição é descartada. Os índices criados com CREATE INDEX devem ser descartados com DROP INDEX. Use a instrução ALTER INDEX para recriar uma parte de índice de uma definição de restrição. A restrição não tem que ser descartada e adicionada novamente com ALTER INDEX.

Todos os índices e as restrições com base em uma coluna devem ser removidos antes que a coluna possa ser removida.

Quando uma restrição que cria um índice clusterizado é excluída, as linhas de dados que foram armazenadas no nível folha do índice clusterizado são armazenadas em uma tabela não clusterizada. É possível descartar o índice clusterizado e mover a tabela resultante para outro grupo de arquivos ou esquema de partição em uma única transação, especificando a opção MOVE TO. A opção MOVE TO tem as seguintes restrições:

- MOVE TO não é válido para exibições indexadas ou índices não clusterizados.
- O esquema de partição ou grupo de arquivos já deve existir.
- Se MOVE TO não for especificada, a tabela resultante estará localizada no mesmo esquema de partição ou grupo de arquivos definido para o índice clusterizado.

Ao remover um índice clusterizado, especifique a opção ONLINE **=** ON de modo que a transação DROP INDEX não bloqueie consultas e modificações nos dados subjacentes e índices não clusterizados associados.

ONLINE **=** ON tem as seguintes restrições:

- ONLINE **=** ON é inválido para índices clusterizados que também estão desabilitados. Índices desabilitados devem ser descartados usando ONLINE **=** OFF.
- Apenas um índice pode ser descartado por vez.
- ONLINE **=** ON é inválido para exibições indexadas, índices não clusterizados ou índices em tabelas temporárias locais.
- ONLINE **=** ON é inválido para índices columnstore.

É necessário ter espaço temporário em disco igual ao tamanho do índice clusterizado existente para descartar um índice clusterizado. Esse espaço adicional será liberado assim que a operação for concluída.

> [!NOTE]
> As opções listadas em *\<opção_de_descarte_de_restrição_clusterizada>* aplicam-se a índices clusterizados em tabelas e não podem ser aplicadas a índices clusterizados em exibições ou a índices não clusterizados.

## <a name="replicating-schema-changes"></a>Replicando alterações de esquema

Quando você executa ALTER TABLE em uma tabela publicada no Publicador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], por padrão, essa alteração é propagada para todos os assinantes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa funcionalidade tem algumas restrições. É possível desabilitá-la. Para obter mais informações, consulte [Make Schema Changes on Publication Databases](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md) (Fazer alterações de esquema em bancos de dados de publicação).

## <a name="data-compression"></a>Data Compression

Não é possível habilitar as tabelas do sistema para compactação. Se a tabela for um heap, a operação de reconstrução para o modo ONLINE será um thread único. Use o modo OFFLINE para uma operação de reconstrução de um heap multi-threaded. Para obter mais informações sobre compactação de dados, veja [Compactação de dados](../../relational-databases/data-compression/data-compression.md).

Para avaliar como a alteração do estado de compactação afetará uma tabela, um índice ou uma partição, use o procedimento armazenado [sp_estimate_data_compression_savings](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md) .

As restrições a seguir se aplicam a tabelas particionadas:

- Não será possível alterar a configuração de compactação de uma única partição se a tabela tiver índices não alinhados.
- A sintaxe ALTER TABLE \<table> REBUILD PARTITION... recompila a partição especificada.
- A sintaxe ALTER TABLE \<tabela> REBUILD WITH... recompila todas as partições.

## <a name="dropping-ntext-columns"></a>Removendo colunas NTEXT

Ao remover colunas NTEXT, a limpeza dos dados excluídos ocorre como uma operação serializada em todas as linhas. A limpeza pode exigir uma grande quantidade de tempo. Ao remover uma coluna NTEXT em uma tabela com muitas linhas, primeiro atualize a coluna NTEXT para o valor NULL e, em seguida, remova a coluna. Você pode executar essa opção com operações paralelas e torná-la muito mais rápida.

## <a name="online-index-rebuild"></a>Recriação de índice online

Para executar a instrução DDL de uma recompilação de índice online, todas as transações de bloqueio ativas em execução em uma tabela específica devem ser concluídas. Quando a recompilação de índice online for iniciada, ela bloqueará todas as novas transações que estão prontas para iniciar a execução nessa tabela. Embora a duração do bloqueio da recompilação de índice online seja curta, é possível que a espera pela conclusão de todas as transações abertas em uma tabela específica e o bloqueio das novas transações a serem iniciadas afetem significativamente a taxa de transferência. Isso pode diminuir a velocidade de uma carga de trabalho ou ocasionar o tempo limite dela, bem como limitar consideravelmente o acesso à tabela subjacente. A opção **WAIT_AT_LOW_PRIORITY** permite que os DBAs gerenciem o bloqueio S e os bloqueios Sch-M necessários para recompilações de índice online e permite que selecionem uma das três opções. Nos três casos, se, durante o tempo de espera ( `(MAX_DURATION =n [minutes])` ), não houver nenhuma atividade de bloqueio, a recompilação de índice online será executada imediatamente sem aguardar e a instrução DDL será concluída.

## <a name="compatibility-support"></a>Suporte de compatibilidade

A instrução ALTER TABLE dá suporte apenas a nomes de tabela de duas partes (schema.object). No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], a especificação de uma tabela usando os formatos a seguir falhará em tempo de compilação com o erro 117.

- server.database.schema.table
- .database.schema.table
- ..schema.table

Em versões anteriores, especificar o formato server.database.schema.table retornou o erro 4902. A especificação do formato .database.schema.table ou do formato ..schema.table foi bem-sucedida.

Para resolver o problema, remova o uso de um prefixo de 4 partes.

## <a name="permissions"></a>Permissões

Exige a permissão ALTER na tabela.

As permissões ALTER TABLE se aplicam a ambas as tabelas envolvidas em uma instrução ALTER TABLE SWITCH. Qualquer dado que seja alternado herda a segurança da tabela de destino.

Se você tiver definido alguma coluna da instrução ALTER TABLE como um tipo CLR (Common Language Runtime) definido pelo usuário ou tipo de dados de alias, a permissão REFERENCES será necessária nesse tipo.

Adicionar uma coluna que atualize as linhas da tabela requer a permissão **UPDATE** na tabela. Por exemplo, a adição de uma coluna **NOT NULL** com um valor padrão ou a adição de uma coluna de identidade quando a tabela não está vazia.

## <a name="examples"></a><a name="Example_Top"></a> Exemplos

|Categoria|Elementos de sintaxe em destaque|
|--------------|------------------------------|
|[Adicionando colunas e restrições](#add)|ADD * PRIMARY KEY com opções de índice * colunas esparsas e conjuntos de colunas *|
|[Descartando colunas e restrições](#Drop)|DROP|
|[Alterando uma definição de coluna](#alter_column)|alterar o tipo de dados * alterar o tamanho da coluna * ordenação|
|[Alterando uma definição de tabela](#alter_table)|DATA_COMPRESSION * SWITCH PARTITION * LOCK ESCALATION * controle de alterações|
|[Desabilitando e habilitando restrições e gatilhos](#disable_enable)|CHECK * NO CHECK * ENABLE TRIGGER * DISABLE TRIGGER|
| &nbsp; | &nbsp; |

### <a name="adding-columns-and-constraints"></a><a name="add"></a>Adicionando colunas e restrições

Os exemplos desta seção demonstram a adição de colunas e restrições em uma tabela.

#### <a name="a-adding-a-new-column"></a>a. Adicionando uma nova coluna

O exemplo a seguir adiciona uma coluna que permite valores nulos e que não tem nenhum valor fornecido por uma definição DEFAULT. Na nova coluna, cada linha terá `NULL`.

```sql
CREATE TABLE dbo.doc_exa (column_a INT) ;
GO
ALTER TABLE dbo.doc_exa ADD column_b VARCHAR(20) NULL ;
GO
```

#### <a name="b-adding-a-column-with-a-constraint"></a>B. Adicionando uma coluna com uma restrição

O exemplo a seguir adiciona uma nova coluna com uma restrição `UNIQUE`.

```sql
CREATE TABLE dbo.doc_exc (column_a INT) ;
GO
ALTER TABLE dbo.doc_exc ADD column_b VARCHAR(20) NULL
    CONSTRAINT exb_unique UNIQUE ;
GO
EXEC sp_help doc_exc ;
GO
DROP TABLE dbo.doc_exc ;
GO
```

#### <a name="c-adding-an-unverified-check-constraint-to-an-existing-column"></a>C. Adicionando uma restrição CHECK não verificada a uma coluna existente

O exemplo a seguir adiciona uma restrição a uma coluna existente na tabela. A coluna tem um valor que viola a restrição. Portanto, `WITH NOCHECK` é usado para evitar que a restrição seja validada contra as linhas existentes e para permitir que a restrição seja adicionada.

```sql
CREATE TABLE dbo.doc_exd ( column_a INT) ;
GO
INSERT INTO dbo.doc_exd VALUES (-1) ;
GO
ALTER TABLE dbo.doc_exd WITH NOCHECK
ADD CONSTRAINT exd_check CHECK (column_a > 1) ;
GO
EXEC sp_help doc_exd ;
GO
DROP TABLE dbo.doc_exd ;
GO
```

#### <a name="d-adding-a-default-constraint-to-an-existing-column"></a>D. Adicionando uma restrição DEFAULT a uma coluna existente

O exemplo a seguir cria uma tabela de duas colunas e insere um valor na primeira coluna, sendo que a outra permanece NULL. Depois, uma restrição `DEFAULT` é adicionada à segunda coluna. Para verificar se o padrão está aplicado, outro valor é inserido na primeira coluna e a tabela é consultada.

```sql
CREATE TABLE dbo.doc_exz ( column_a INT, column_b INT) ;
GO
INSERT INTO dbo.doc_exz (column_a)VALUES ( 7 ) ;
GO
ALTER TABLE dbo.doc_exz
  ADD CONSTRAINT col_b_def
  DEFAULT 50 FOR column_b ;
GO
INSERT INTO dbo.doc_exz (column_a) VALUES ( 10 ) ;
GO
SELECT * FROM dbo.doc_exz ;
GO
DROP TABLE dbo.doc_exz ;
GO
```

#### <a name="e-adding-several-columns-with-constraints"></a>E. Adicionando várias colunas com restrições

O exemplo a seguir adiciona várias colunas com restrições definidas com a nova coluna. A primeira coluna nova tem uma propriedade `IDENTITY`. Cada linha na tabela tem novos valores com incremento na coluna de identidade.

```sql
CREATE TABLE dbo.doc_exe ( column_a INT CONSTRAINT column_a_un UNIQUE) ;
GO
ALTER TABLE dbo.doc_exe ADD

-- Add a PRIMARY KEY identity column.
column_b INT IDENTITY
CONSTRAINT column_b_pk PRIMARY KEY,

-- Add a column that references another column in the same table.
column_c INT NULL
CONSTRAINT column_c_fk
REFERENCES doc_exe(column_a),

-- Add a column with a constraint to enforce that
-- nonnull data is in a valid telephone number format.
column_d VARCHAR(16) NULL
CONSTRAINT column_d_chk
CHECK
(column_d LIKE '[0-9][0-9][0-9]-[0-9][0-9][0-9][0-9]' OR
column_d LIKE
'([0-9][0-9][0-9]) [0-9][0-9][0-9]-[0-9][0-9][0-9][0-9]'),

-- Add a nonnull column with a default.
column_e DECIMAL(3,3)
CONSTRAINT column_e_default
DEFAULT .081 ;
GO
EXEC sp_help doc_exe ;
GO
DROP TABLE dbo.doc_exe ;
GO
```

#### <a name="f-adding-a-nullable-column-with-default-values"></a>F. Adicionando uma coluna que permite valor nulo com valores padrão

O exemplo a seguir adiciona uma coluna que permite valor nulo com uma definição `DEFAULT` e usa `WITH VALUES` para fornecer valores para cada linha existente na tabela. Se WITH VALUES não for usado, cada linha terá o valor NULL na nova coluna.

```sql
CREATE TABLE dbo.doc_exf ( column_a INT) ;
GO
INSERT INTO dbo.doc_exf VALUES (1) ;
GO
ALTER TABLE dbo.doc_exf
ADD AddDate smalldatetime NULL
CONSTRAINT AddDateDflt
DEFAULT GETDATE() WITH VALUES ;
GO
DROP TABLE dbo.doc_exf ;
GO
```

#### <a name="g-creating-a-primary-key-constraint-with-index-or-data-compression-options"></a>G. Criando uma restrição PRIMARY KEY com opções de índice ou de compressão de dados

O exemplo a seguir cria a restrição PRIMARY KEY `PK_TransactionHistoryArchive_TransactionID` e especifica as opções `FILLFACTOR`, `ONLINE` e `PAD_INDEX`. O índice clusterizado resultante terá o mesmo nome da restrição.

**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

```sql
USE AdventureWorks;
GO
ALTER TABLE Production.TransactionHistoryArchive WITH NOCHECK
ADD CONSTRAINT PK_TransactionHistoryArchive_TransactionID PRIMARY KEY CLUSTERED (TransactionID)
WITH (FILLFACTOR = 75, ONLINE = ON, PAD_INDEX = ON);
GO
```

Este exemplo semelhante se aplica a compactação de página ao aplicar a chave primária clusterizada.

```sql
USE AdventureWorks;
GO
ALTER TABLE Production.TransactionHistoryArchive WITH NOCHECK
ADD CONSTRAINT PK_TransactionHistoryArchive_TransactionID PRIMARY KEY CLUSTERED (TransactionID)
WITH (DATA_COMPRESSION = PAGE);
GO
```

#### <a name="h-adding-a-sparse-column"></a>H. Adicionando uma coluna esparsa

Os exemplos a seguir mostram a adição e modificação de colunas esparsas na tabela T1. O código para criar a tabela `T1` é o seguinte:

```sql
CREATE TABLE T1
(C1 int PRIMARY KEY,
C2 varchar(50) SPARSE NULL,
C3 int SPARSE NULL,
C4 int ) ;
GO
```

Para adicionar uma outra coluna esparsa `C5`, execute a seguinte instrução:

```sql
ALTER TABLE T1
ADD C5 char(100) SPARSE NULL ;
GO
```

Para converter a coluna não esparsa `C4` a uma coluna esparsa, execute a seguinte instrução:

```sql
ALTER TABLE T1
ALTER COLUMN C4 ADD SPARSE ;
GO
```

Para converter a coluna esparsa `C4` para uma coluna não esparsa, execute a seguinte instrução.

```sql
ALTER TABLE T1
ALTER COLUMN C4 DROP SPARSE;
GO
```

#### <a name="i-adding-a-column-set"></a>I. Adicionando um conjunto de colunas

Os exemplos a seguir mostram a adição de uma coluna à tabela `T2`. Um conjunto de colunas não poderá ser adicionado a uma tabela se ela já contiver colunas esparsas. O código para criar a tabela `T2` é o seguinte:

```sql
CREATE TABLE T2
(C1 int PRIMARY KEY,
C2 varchar(50) NULL,
C3 int NULL,
C4 int ) ;
GO
```

As três instruções a seguir adicionam um conjunto de colunas chamado `CS` e, depois, modificam colunas `C2` e `C3` para `SPARSE`.

```sql
ALTER TABLE T2
ADD CS XML COLUMN_SET FOR ALL_SPARSE_COLUMNS ;
GO

ALTER TABLE T2
ALTER COLUMN C2 ADD SPARSE ;
GO

ALTER TABLE T2
ALTER COLUMN C3 ADD SPARSE ;
GO
```

#### <a name="j-adding-an-encrypted-column"></a>J. Adicionando uma coluna criptografada

A instrução a seguir adiciona uma coluna criptografada denominada `PromotionCode`.

```sql
ALTER TABLE Customers ADD
    PromotionCode nvarchar(100)
    ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = MyCEK,
    ENCRYPTION_TYPE = RANDOMIZED,
    ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') ;
```

### <a name="dropping-columns-and-constraints"></a><a name="Drop"></a>Descartando colunas e restrições

Os exemplos desta seção demonstram o descarte de colunas e restrições.

#### <a name="a-dropping-a-column-or-columns"></a>a. Descartando uma coluna ou colunas

O primeiro exemplo modifica uma tabela para remover uma coluna. O segundo exemplo remove várias colunas.

```sql
CREATE TABLE dbo.doc_exb
    (column_a INT
     ,column_b VARCHAR(20) NULL
     ,column_c datetime
     ,column_d int) ;
GO  
-- Remove a single column.
ALTER TABLE dbo.doc_exb DROP COLUMN column_b ;
GO
-- Remove multiple columns.
ALTER TABLE dbo.doc_exb DROP COLUMN column_c, column_d;
```

#### <a name="b-dropping-constraints-and-columns"></a>B. Descartando restrições e colunas

O primeiro exemplo remove uma restrição `UNIQUE` de uma tabela. O segundo exemplo remove duas restrições e uma única coluna.

```sql
CREATE TABLE dbo.doc_exc ( column_a int NOT NULL CONSTRAINT my_constraint UNIQUE) ;
GO

-- Example 1. Remove a single constraint.
ALTER TABLE dbo.doc_exc DROP my_constraint ;
GO

DROP TABLE dbo.doc_exc;
GO

CREATE TABLE dbo.doc_exc ( column_a int
                          NOT NULL CONSTRAINT my_constraint UNIQUE
                          ,column_b int
                          NOT NULL CONSTRAINT my_pk_constraint PRIMARY KEY) ;
GO

-- Example 2. Remove two constraints and one column
-- The keyword CONSTRAINT is optional. The keyword COLUMN is required.
ALTER TABLE dbo.doc_exc

    DROP CONSTRAINT my_constraint, my_pk_constraint, COLUMN column_b ;
GO
```

#### <a name="c-dropping-a-primary-key-constraint-in-the-online-mode"></a>C. Descartando uma restrição PRIMARY KEY no modo ONLINE

O exemplo a seguir exclui uma restrição PRIMARY KEY com a opção `ONLINE` definida como `ON`.

```sql
ALTER TABLE Production.TransactionHistoryArchive
DROP CONSTRAINT PK_TransactionHistoryArchive_TransactionID
WITH (ONLINE = ON);
GO
```

#### <a name="d-adding-and-dropping-a-foreign-key-constraint"></a>D. Adicionando e descartando uma restrição FOREIGN KEY

O exemplo a seguir cria a tabela `ContactBackup` e, em seguida, altera a tabela, adicionando uma restrição `FOREIGN KEY` que referencia a tabela `Person.Person` e, depois, descartando a restrição `FOREIGN KEY`.

```sql
CREATE TABLE Person.ContactBackup
    (ContactID int) ;
GO

ALTER TABLE Person.ContactBackup
ADD CONSTRAINT FK_ContactBackup_Contact FOREIGN KEY (ContactID)
    REFERENCES Person.Person (BusinessEntityID) ;
GO

ALTER TABLE Person.ContactBackup
DROP CONSTRAINT FK_ContactBackup_Contact ;
GO

DROP TABLE Person.ContactBackup ;
```

![Ícone de seta usado com o link Voltar ao Início](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao Início") [Exemplos](#Example_Top)

### <a name="altering-a-column-definition"></a><a name="alter_column"></a> Alterando uma definição de coluna

#### <a name="a-changing-the-data-type-of-a-column"></a>a. Alteração do tipo de dados de uma coluna

O exemplo a seguir altera uma coluna de uma tabela de `INT` para `DECIMAL`.

```sql
CREATE TABLE dbo.doc_exy (column_a INT ) ;
GO
INSERT INTO dbo.doc_exy (column_a) VALUES (10) ;
GO
ALTER TABLE dbo.doc_exy ALTER COLUMN column_a DECIMAL (5, 2) ;
GO
DROP TABLE dbo.doc_exy ;
GO
```

#### <a name="b-changing-the-size-of-a-column"></a>B. Alterando o tamanho de uma coluna

O exemplo a seguir aumenta o tamanho de uma coluna **varchar** e a precisão e escala de uma coluna **decimal**. Como essas colunas contêm dados, o tamanho da coluna só pode ser aumentado. Além disso, observe que `col_a` está definido como um índice exclusivo. O tamanho de `col_a` ainda pode ser aumentado, pois o tipo de dados é um **varchar** e o índice não é o resultado de uma restrição PRIMARY KEY.

```sql
-- Create a two-column table with a unique index on the varchar column.
CREATE TABLE dbo.doc_exy ( col_a varchar(5) UNIQUE NOT NULL, col_b decimal (4,2));
GO
INSERT INTO dbo.doc_exy VALUES ('Test', 99.99);
GO
-- Verify the current column size.
SELECT name, TYPE_NAME(system_type_id), max_length, precision, scale
FROM sys.columns WHERE object_id = OBJECT_ID(N'dbo.doc_exy');
GO
-- Increase the size of the varchar column.
ALTER TABLE dbo.doc_exy ALTER COLUMN col_a varchar(25);
GO
-- Increase the scale and precision of the decimal column.
ALTER TABLE dbo.doc_exy ALTER COLUMN col_b decimal (10,4);
GO
-- Insert a new row.
INSERT INTO dbo.doc_exy VALUES ('MyNewColumnSize', 99999.9999) ;
GO
-- Verify the current column size.
SELECT name, TYPE_NAME(system_type_id), max_length, precision, scale
FROM sys.columns WHERE object_id = OBJECT_ID(N'dbo.doc_exy');
```

#### <a name="c-changing-column-collation"></a>C. Alterando a ordenação de colunas

Os exemplos a seguir mostram como alterar a ordenação de uma coluna. Primeiro, uma tabela é criada com a ordenação de usuário padrão.

```sql
CREATE TABLE T3
(C1 int PRIMARY KEY,
C2 varchar(50) NULL,
C3 int NULL,
C4 int ) ;
GO
```

Em seguida, a ordenação da coluna `C2` é alterada para Latin1_General_BIN. O tipo de dados é obrigatório, mesmo que não tenha sido alterado.

```sql
ALTER TABLE T3
ALTER COLUMN C2 varchar(50) COLLATE Latin1_General_BIN;
GO
```

#### <a name="d-encrypting-a-column"></a>D. Criptografar uma coluna

O exemplo a seguir mostra como criptografar uma coluna usando [Always Encrypted com enclaves seguros](../../relational-databases/security/encryption/always-encrypted-enclaves.md).

Primeiro, uma tabela é criada sem nenhuma coluna criptografada.

```sql
CREATE TABLE T3
(C1 int PRIMARY KEY,
C2 varchar(50) NULL,
C3 int NULL,
C4 int ) ;
GO
```

Em seguida, a coluna 'C2' é criptografada com uma chave de criptografia de coluna, chamada CEK1, e a criptografia aleatória. Para que a instrução a seguir seja bem-sucedida:

- A chave de criptografia de coluna deve ser habilitada para enclave. Isso significa que ela deve ser criptografada com uma chave mestra de coluna que permita cálculos de enclave.
- A instância do SQL Server de destino dá suporte a Always Encrypted com enclaves seguros.
- A instrução deve ser emitida por uma conexão configurada para Always Encrypted com enclaves seguros e usando um driver de cliente com suporte.
- O aplicativo de chamada deve ter acesso à chave mestra de coluna, protegendo CEK1.

```sql
ALTER TABLE T3
ALTER COLUMN C2 varchar(50) ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NULL;
GO
```

### <a name="altering-a-table-definition"></a><a name="alter_table"></a> Alterando uma definição de tabela

Os exemplos desta seção demonstram como alterar a definição de uma tabela.

#### <a name="a-modifying-a-table-to-change-the-compression"></a>a. Modificando uma tabela para alterar a compactação

O exemplo a seguir altera a compactação de uma tabela não particionada. O heap ou índice clusterizado será recriado. Se a tabela for um heap, todos os índices não clusterizados serão recriados.

```sql
ALTER TABLE T1
REBUILD WITH (DATA_COMPRESSION = PAGE);
```

O exemplo a seguir altera a compactação de uma tabela particionada. A sintaxe `REBUILD PARTITION = 1` faz com que somente o número de partição `1` seja recriado.

**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

```sql
ALTER TABLE PartitionTable1
REBUILD PARTITION = 1 WITH (DATA_COMPRESSION =NONE) ;
GO
```

A mesma operação usando a sintaxe alternada a seguir faz com que todas as partições na tabela sejam recriadas.

**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

```sql
ALTER TABLE PartitionTable1
REBUILD PARTITION = ALL
WITH (DATA_COMPRESSION = PAGE ON PARTITIONS(1) ) ;
```

Para obter exemplos de compactação de dados adicionais, consulte [Compactação de dados](../../relational-databases/data-compression/data-compression.md).

#### <a name="b-modifying-a-columnstore-table-to-change-archival-compression"></a>B. Modificando uma tabela columnstore para alterar a compactação de arquivamento

O exemplo a seguir compacta ainda mais uma partição de tabela columnstore aplicando um algoritmo de compactação adicional. Essa compactação reduz a tabela para um tamanho menor, mas também aumenta o tempo necessário para armazenamento e recuperação. Isso pode ser útil para fins de arquivamento, ou em outras situações que exijam menos espaço e possam dispensar mais tempo para armazenamento e recuperação.

**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

```sql
ALTER TABLE PartitionTable1
REBUILD PARTITION = 1 WITH (DATA_COMPRESSION = COLUMNSTORE_ARCHIVE) ;
GO
```

O exemplo a seguir descompacta uma partição de tabela columnstore compactada com a opção COLUMNSTORE_ARCHIVE. Quando os dados forem restaurados, eles continuarão sendo compactados por meio da compactação columnstore usada em todas as tabelas columnstore.

**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

```sql
ALTER TABLE PartitionTable1
REBUILD PARTITION = 1 WITH (DATA_COMPRESSION =COLUMNSTORE) ;
GO
```

#### <a name="c-switching-partitions-between-tables"></a>C. Alternando partições entre tabelas

O exemplo a seguir cria uma tabela particionada, pressupondo que o esquema de partição `myRangePS1` já esteja criado no banco de dados. Em seguida, uma tabela não particionada é criada com a mesma estrutura de uma tabela particionada e no mesmo grupo de arquivos que `PARTITION 2` da tabela `PartitionTable`. Depois, os dados da `PARTITION 2` da tabela `PartitionTable` são inseridos na tabela `NonPartitionTable`.

```sql
CREATE TABLE PartitionTable (col1 int, col2 char(10))
ON myRangePS1 (col1) ;
GO
CREATE TABLE NonPartitionTable (col1 int, col2 char(10))
ON test2fg ;
GO
ALTER TABLE PartitionTable SWITCH PARTITION 2 TO NonPartitionTable ;
GO
```

#### <a name="d-allowing-lock-escalation-on-partitioned-tables"></a>D. Permitindo escalonamento de bloqueios em tabelas particionadas

O exemplo a seguir habilita o escalonamento de bloqueios no nível de partição em uma tabela particionada. Se a tabela não estiver particionada, o escalonamento de bloqueios será definido no nível TABLE.

**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

```sql
ALTER TABLE dbo.T1 SET (LOCK_ESCALATION = AUTO);
GO
```

#### <a name="e-configuring-change-tracking-on-a-table"></a>E. Configurando o controle de alterações em uma tabela

O exemplo a seguir habilita o controle de alterações na tabela `Person.Person`.

**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

```sql
USE AdventureWorks;
ALTER TABLE Person.Person
ENABLE CHANGE_TRACKING;
```

O exemplo a seguir habilita o controle de alterações e também o controle de colunas que são atualizadas durante uma alteração.

**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.

```sql
USE AdventureWorks;
GO
ALTER TABLE Person.Person
ENABLE CHANGE_TRACKING
WITH (TRACK_COLUMNS_UPDATED = ON)
```

O exemplo a seguir desabilita o controle de alterações na tabela `Person.Person`.

**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

```sql
USE AdventureWorks;
Go
ALTER TABLE Person.Person
DISABLE CHANGE_TRACKING;
```

### <a name="disabling-and-enabling-constraints-and-triggers"></a><a name="disable_enable"></a>Desabilitando e habilitando restrições e gatilhos

#### <a name="a-disabling-and-re-enabling-a-constraint"></a>a. Desabilitando e reabilitando uma restrição

O exemplo a seguir desabilita uma restrição que limita os salários aceitos nos dados. `NOCHECK CONSTRAINT` é usada com `ALTER TABLE` para desabilitar a restrição e permitir uma inserção que normalmente violaria a restrição. `CHECK CONSTRAINT` reabilita a restrição.

```sql
CREATE TABLE dbo.cnst_example
(id INT NOT NULL,
 name VARCHAR(10) NOT NULL,
 salary MONEY NOT NULL
    CONSTRAINT salary_cap CHECK (salary < 100000)
);

-- Valid inserts
INSERT INTO dbo.cnst_example VALUES (1,'Joe Brown',65000);
INSERT INTO dbo.cnst_example VALUES (2,'Mary Smith',75000);

-- This insert violates the constraint.
INSERT INTO dbo.cnst_example VALUES (3,'Pat Jones',105000);

-- Disable the constraint and try again.
ALTER TABLE dbo.cnst_example NOCHECK CONSTRAINT salary_cap;
INSERT INTO dbo.cnst_example VALUES (3,'Pat Jones',105000);

-- Re-enable the constraint and try another insert; this will fail.
ALTER TABLE dbo.cnst_example CHECK CONSTRAINT salary_cap;
INSERT INTO dbo.cnst_example VALUES (4,'Eric James',110000) ;
```

#### <a name="b-disabling-and-re-enabling-a-trigger"></a>B. Desabilitando e reabilitando um gatilho

O exemplo a seguir usa a opção `DISABLE TRIGGER` de `ALTER TABLE` para desabilitar o gatilho e permitir uma inserção que normalmente violaria o gatilho. `ENABLE TRIGGER` é usado para reabilitar o gatilho.

```sql
CREATE TABLE dbo.trig_example
(id INT,
name VARCHAR(12),
salary MONEY) ;
GO
-- Create the trigger.
CREATE TRIGGER dbo.trig1 ON dbo.trig_example FOR INSERT
AS
IF (SELECT COUNT(*) FROM INSERTED
WHERE salary > 100000) > 0
BEGIN
    print 'TRIG1 Error: you attempted to insert a salary > $100,000'
    ROLLBACK TRANSACTION
END ;
GO
-- Try an insert that violates the trigger.
INSERT INTO dbo.trig_example VALUES (1,'Pat Smith',100001) ;
GO
-- Disable the trigger.
ALTER TABLE dbo.trig_example DISABLE TRIGGER trig1 ;
GO
-- Try an insert that would typically violate the trigger.
INSERT INTO dbo.trig_example VALUES (2,'Chuck Jones',100001) ;
GO
-- Re-enable the trigger.
ALTER TABLE dbo.trig_example ENABLE TRIGGER trig1 ;
GO
-- Try an insert that violates the trigger.
INSERT INTO dbo.trig_example VALUES (3,'Mary Booth',100001) ;
GO
```

### <a name="online-operations"></a><a name="online"></a>Operações online

#### <a name="a-online-index-rebuild-using-low-priority-wait-options"></a>a. Recompilação de índice online usando opções de espera de baixa prioridade

O exemplo a seguir mostra como executar uma recompilação de índice online que especifica as opções de espera de baixa prioridade.

**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

```sql
ALTER TABLE T1
REBUILD WITH
(
    PAD_INDEX = ON,
    ONLINE = ON ( WAIT_AT_LOW_PRIORITY ( MAX_DURATION = 4 MINUTES,
                                         ABORT_AFTER_WAIT = BLOCKERS ) )
)
;
```

#### <a name="b-online-alter-column"></a>B. Alteração online de coluna

O exemplo a seguir mostra como executar uma operação de alteração de coluna com a opção ONLINE.

**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

```sql
CREATE TABLE dbo.doc_exy (column_a INT ) ;
GO
INSERT INTO dbo.doc_exy (column_a) VALUES (10) ;
GO
ALTER TABLE dbo.doc_exy
    ALTER COLUMN column_a DECIMAL (5, 2) WITH (ONLINE = ON);
GO
sp_help doc_exy;
DROP TABLE dbo.doc_exy ;
GO
```

### <a name="system-versioning"></a><a name="system_versioning"></a> Controle de versão do sistema

Os quatro exemplos a seguir ajudarão você a se familiarizar com a sintaxe para usar o controle de versão do sistema. Para obter assistência adicional, veja [Introdução às tabelas temporais com controle de versão do sistema](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md).

**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

#### <a name="a-add-system-versioning-to-existing-tables"></a>a. Adicionar o controle de versão do sistema a tabelas existentes

O exemplo a seguir mostra como adicionar o controle de versão do sistema a uma tabela existente e criar uma tabela de histórico futura. Este exemplo presume que há uma tabela existente chamada `InsurancePolicy` com uma chave primária definida. Este exemplo preenche as colunas de período recém-criadas para controle de versão do sistema usando valores padrão para os horários de início e término, porque esses valores não podem ser nulos. Este exemplo usa a cláusula HIDDEN para garantir que não haja nenhum impacto aplicativos existentes que interagem com a tabela atual. Ele também usa HISTORY_RETENTION_PERIOD, que está disponível somente em [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].

```sql
--Alter non-temporal table to define periods for system versioning
ALTER TABLE InsurancePolicy
ADD PERIOD FOR SYSTEM_TIME (SysStartTime, SysEndTime),
SysStartTime datetime2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL
    DEFAULT SYSUTCDATETIME(),
SysEndTime datetime2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL
    DEFAULT CONVERT(DATETIME2, '9999-12-31 23:59:59.99999999');

--Enable system versioning with 1 year retention for historical data
ALTER TABLE InsurancePolicy
SET (SYSTEM_VERSIONING = ON (HISTORY_RETENTION_PERIOD = 1 YEAR));
```

#### <a name="b-migrate-an-existing-solution-to-use-system-versioning"></a>B. Migrar uma solução existente para usar o controle de versão do sistema

O exemplo a seguir mostra como migrar para o controle de versão do sistema de uma solução que usa gatilhos para imitar simular o suporte temporal. O exemplo supõe que há uma solução existente que usa uma tabela `ProjectTask` e uma tabela `ProjectTaskHistory` para sua solução existente, que usa as colunas `Changed Date` e `Revised Date` para seus períodos, que essas colunas de período não usam o datatype `datetime2` e que a tabela `ProjectTask` tem uma chave primária definida.

```sql
-- Drop existing trigger
DROP TRIGGER ProjectTask_HistoryTrigger;

-- Adjust the schema for current and history table
-- Change data types for existing period columns
ALTER TABLE ProjectTask ALTER COLUMN [Changed Date] datetime2 NOT NULL;
ALTER TABLE ProjectTask ALTER COLUMN [Revised Date] datetime2 NOT NULL;
ALTER TABLE ProjectTaskHistory ALTER COLUMN [Changed Date] datetime2 NOT NULL;
ALTER TABLE ProjectTaskHistory ALTER COLUMN [Revised Date] datetime2 NOT NULL;

-- Add SYSTEM_TIME period and set system versioning with linking two existing tables
-- (a certain set of data checks happen in the background)
ALTER TABLE ProjectTask
ADD PERIOD FOR SYSTEM_TIME ([Changed Date], [Revised Date])

ALTER TABLE ProjectTask
SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.ProjectTaskHistory, DATA_CONSISTENCY_CHECK = ON))
```

#### <a name="c-disabling-and-re-enabling-system-versioning-to-change-table-schema"></a>C. Desabilitando e reabilitando o controle de versão do sistema para alterar o esquema de tabela

Este exemplo mostra como desabilitar o controle de versão do sistema na tabela `Department`, adicionar uma coluna e reabilitar o controle de versão do sistema. É necessário desabilitar o controle de versão do sistema para modificar o esquema da tabela. Realize essas etapas em uma transação para impedir atualizações a ambas as tabelas ao atualizar o esquema da tabela, o que permite ao DBA ignorar a verificação de consistência de dados ao habilitar novamente o controle de versão do sistema e obter um benefício de desempenho. Tarefas como criação de estatísticas, alternância de partições ou aplicação de compactação de uma ou ambas as tabelas não exigem a desabilitação do controle de versão do sistema.

```sql
BEGIN TRAN
/* Takes schema lock on both tables */
ALTER TABLE Department
    SET (SYSTEM_VERSIONING = OFF);
/* expand table schema for temporal table */
ALTER TABLE Department  
     ADD Col5 int NOT NULL DEFAULT 0;
/* Expand table schema for history table */
ALTER TABLE DepartmentHistory
    ADD Col5 int NOT NULL DEFAULT 0;
/* Re-establish versioning again*/
ALTER TABLE Department
    SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE=dbo.DepartmentHistory,
                                 DATA_CONSISTENCY_CHECK = OFF));
COMMIT
```

#### <a name="d-removing-system-versioning"></a>D. Removendo o controle de versão do sistema

Este exemplo mostra como remover completamente o controle de versão do sistema da tabela Departamento e remover a tabela `DepartmentHistory`. Opcionalmente, você também pode querer remover as colunas de período usadas pelo sistema para registrar informações de controle de versão do sistema. Não é possível remover as tabelas `Department` ou `DepartmentHistory` enquanto a versão do sistema está habilitada.

```sql
ALTER TABLE Department
    SET (SYSTEM_VERSIONING = OFF);
ALTER TABLE Department
DROP PERIOD FOR SYSTEM_TIME;
DROP TABLE DepartmentHistory;
```

## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

Os exemplos a seguir de A a C usam a tabela `FactResellerSales` no banco de dados [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)].

### <a name="a-determining-if-a-table-is-partitioned"></a>a. Determinando se uma tabela está particionada

A consulta a seguir retornará uma ou mais linhas se a tabela `FactResellerSales` for particionada. Se a tabela não for particionada, nenhuma linha será retornada.

```sql
SELECT * FROM sys.partitions AS p
JOIN sys.tables AS t
    ON p.object_id = t.object_id
WHERE p.partition_id IS NOT NULL
    AND t.name = 'FactResellerSales';
```

### <a name="b-determining-boundary-values-for-a-partitioned-table"></a>B. Determinando os valores de limite para uma tabela particionada

A consulta a seguir retorna os valores de limite para cada partição na tabela `FactResellerSales` .

```sql
SELECT t.name AS TableName, i.name AS IndexName, p.partition_number,
    p.partition_id, i.data_space_id, f.function_id, f.type_desc,
    r.boundary_id, r.value AS BoundaryValue
FROM sys.tables AS t
JOIN sys.indexes AS i
    ON t.object_id = i.object_id
JOIN sys.partitions AS p
    ON i.object_id = p.object_id AND i.index_id = p.index_id
JOIN  sys.partition_schemes AS s
    ON i.data_space_id = s.data_space_id
JOIN sys.partition_functions AS f
    ON s.function_id = f.function_id
LEFT JOIN sys.partition_range_values AS r
    ON f.function_id = r.function_id and r.boundary_id = p.partition_number
WHERE t.name = 'FactResellerSales' AND i.type <= 1
ORDER BY p.partition_number;
```

### <a name="c-determining-the-partition-column-for-a-partitioned-table"></a>C. Determinando a coluna de partição para uma tabela particionada

A consulta a seguir retorna o nome da coluna de particionamento para a tabela. `FactResellerSales`.

```sql
SELECT t.object_id AS Object_ID, t.name AS TableName,
    ic.column_id as PartitioningColumnID, c.name AS PartitioningColumnName
FROM sys.tables AS t
JOIN sys.indexes AS i
    ON t.object_id = i.object_id
JOIN sys.columns AS c
    ON t.object_id = c.object_id
JOIN sys.partition_schemes AS ps
    ON ps.data_space_id = i.data_space_id
JOIN sys.index_columns AS ic
    ON ic.object_id = i.object_id
    AND ic.index_id = i.index_id AND ic.partition_ordinal > 0
WHERE t.name = 'FactResellerSales'
AND i.type <= 1
AND c.column_id = ic.column_id;
```

### <a name="d-merging-two-partitions"></a>D. Mesclando duas partições

O exemplo a seguir mescla duas partições em uma tabela.

A tabela `Customer` tem a seguinte definição:

```sql
CREATE TABLE Customer (
    id int NOT NULL,
    lastName varchar(20),
    orderCount int,
    orderDate date)
WITH
    ( DISTRIBUTION = HASH(id),
    PARTITION ( orderCount RANGE LEFT
    FOR VALUES (1, 5, 10, 25, 50, 100)));
```

O comando a seguir combina os limites de partição 10 e 25.

```sql
ALTER TABLE Customer MERGE RANGE (10);
```

A nova DDL para a tabela é:

```sql
CREATE TABLE Customer (
    id int NOT NULL,
    lastName varchar(20),
    orderCount int,
    orderDate date)
WITH
    ( DISTRIBUTION = HASH(id),
    PARTITION ( orderCount RANGE LEFT
    FOR VALUES (1, 5, 25, 50, 100)));
```

### <a name="e-splitting-a-partition"></a>E. Dividindo uma partição

O exemplo a seguir divide uma partição em uma tabela.

A tabela `Customer` tem a seguinte DDL:

```sql
DROP TABLE Customer;

CREATE TABLE Customer (
    id int NOT NULL,
    lastName varchar(20),
    orderCount int,
    orderDate date)
WITH
    ( DISTRIBUTION = HASH(id),
    PARTITION ( orderCount RANGE LEFT
    FOR VALUES (1, 5, 10, 25, 50, 100 )));
```

O comando a seguir cria um novo o limite de partição com o valor de 75, entre 50 e 100.

```sql
ALTER TABLE Customer SPLIT RANGE (75);
```

A nova DDL para a tabela é:

```sql
CREATE TABLE Customer (
   id int NOT NULL,
   lastName varchar(20),
   orderCount int,
   orderDate date)
   WITH DISTRIBUTION = HASH(id),
   PARTITION ( orderCount (RANGE LEFT
      FOR VALUES (1, 5, 10, 25, 50, 75, 100 )));
```

### <a name="f-using-switch-to-move-a-partition-to-a-history-table"></a>F. Usando SWITCH para mover uma partição para uma tabela de histórico

O exemplo a seguir move os dados em uma partição da tabela `Orders` para uma partição da tabela `OrdersHistory`.

A tabela `Orders` tem a seguinte DDL:

```sql
CREATE TABLE Orders (
    id INT,
    city VARCHAR (25),
    lastUpdateDate DATE,
    orderDate DATE )
WITH
    (DISTRIBUTION = HASH ( id ),
    PARTITION ( orderDate RANGE RIGHT
    FOR VALUES ('2004-01-01', '2005-01-01', '2006-01-01', '2007-01-01' )));
```

Neste exemplo, a tabela `Orders` tem as seguintes partições. Cada partição contém dados.

|Partition|Tem dados?|Intervalo de limite|
|---------------|---------------|--------------------|
|1|Sim|OrderDate < '2004-01-01'|
|2|Sim|'2004-01-01' <= OrderDate < '2005-01-01'|
|3|Sim|'2005-01-01' <= OrderDate< '2006-01-01'|
|4|Sim|'2006-01-01'<= OrderDate < '2007-01-01'|
|5|Sim|'2007-01-01' <= OrderDate|
| &nbsp; | &nbsp; | &nbsp; |

- Partição 1 (tem dados): OrderDate < '2004-01-01'
- Partição 2 (tem dados): '2004-01-01' <= OrderDate < '2005-01-01'
- Partição 3 (tem dados): '2005-01-01' <= OrderDate< '2006-01-01'
- Partição 4 (tem dados): '2006-01-01'<= OrderDate < '2007-01-01'
- Partição 5 (tem dados): '2007-01-01' <= OrderDate

A tabela `OrdersHistory` tem a seguinte DDL, que tem colunas e nomes de coluna idênticos aos da tabela `Orders`. Ambos são distribuídos por hash na coluna `id`.

```sql
CREATE TABLE OrdersHistory (
   id INT,
   city VARCHAR (25),
   lastUpdateDate DATE,
   orderDate DATE )
WITH
    (DISTRIBUTION = HASH ( id ),
    PARTITION ( orderDate RANGE RIGHT
    FOR VALUES ( '2004-01-01' )));
```

Embora as colunas e os nomes de coluna devam ser iguais, os limites de partição não precisam ser. Neste exemplo, a tabela `OrdersHistory` tem as duas partições a seguir, e ambas estão vazias:

- Partição 1 (sem dados): OrderDate < '2004-01-01'
- Partição 2 (vazia): '2004-01-01' <= OrderDate

Para as duas tabelas anteriores, o comando a seguir move todas as linhas com `OrderDate < '2004-01-01'` da tabela `Orders` para a tabela `OrdersHistory`.

```sql
ALTER TABLE Orders SWITCH PARTITION 1 TO OrdersHistory PARTITION 1;
```

Como resultado, a primeira partição `Orders` está vazia e a primeira partição em `OrdersHistory` contém dados. As tabelas agora aparecem da seguinte maneira:

 Tabela `Orders`

- Partição 1 (vazia): OrderDate < '2004-01-01'
- Partição 2 (tem dados): '2004-01-01' <= OrderDate < '2005-01-01'
- Partição 3 (tem dados): '2005-01-01' <= OrderDate< '2006-01-01'
- Partição 4 (tem dados): '2006-01-01'<= OrderDate < '2007-01-01'
- Partição 5 (tem dados): '2007-01-01' <= OrderDate

Tabela `OrdersHistory`

- Partição 1 (tem dados): OrderDate < '2004-01-01'
- Partição 2 (vazia): '2004-01-01' <= OrderDate

Para limpar a tabela `Orders`, você pode remover a partição vazia mesclando partições 1 e 2 da seguinte maneira:

```sql
ALTER TABLE Orders MERGE RANGE ('2004-01-01');
```

Após a mesclagem, a tabela `Orders` tem as seguintes partições:

Tabela `Orders`

- Partição 1 (tem dados): OrderDate < '2005-01-01'
- Partição 2 (tem dados): '2005-01-01' <= OrderDate< '2006-01-01'
- Partição 3 (tem dados): '2006-01-01'<= OrderDate < '2007-01-01'
- Partição 4 (tem dados): '2007-01-01' <= OrderDate

Suponha que se passe outro ano e você esteja pronto para arquivar o ano de 2005. Você pode alocar uma partição vazia para o ano 2005 na tabela `OrdersHistory` dividindo a partição vazia da seguinte maneira:

```sql
ALTER TABLE OrdersHistory SPLIT RANGE ('2005-01-01');
```

Após a divisão, a tabela `OrdersHistory` tem as seguintes partições:

 Tabela `OrdersHistory`

- Partição 1 (tem dados): OrderDate < '2004-01-01'
- Partição 2 (vazia): '2004-01-01' < '2005-01-01'
- Partição 3 (vazia): '2005-01-01' <= OrderDate

## <a name="see-also"></a>Consulte Também

- [sys.tables](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)
- [sp_rename](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)
- [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)
- [DROP TABLE](../../t-sql/statements/drop-table-transact-sql.md)
- [sp_help](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)
- [ALTER PARTITION SCHEME](../../t-sql/statements/alter-partition-scheme-transact-sql.md)
- [ALTER PARTITION FUNCTION](../../t-sql/statements/alter-partition-function-transact-sql.md)
- [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)
