---
title: Emular registros e coleções por meio do tipo de dado CLR definido pelo usuário
description: Aborda como o Assistente de Migração do SQL Server (SSMA) para Oracle usa os tipos de dados (UDT) definidos pelo usuário SQL Server CLR (Common Language Runtime) para emular registros e coleções do Oracle.
authors: nahk-ivanov
ms.service: ssma
ms.devlang: sql
ms.topic: article
ms.date: 1/22/2020
ms.author: alexiva
ms.openlocfilehash: 39a7e8d59425db7ce2d7e81083012321caac35ef
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "76762810"
---
# <a name="emulating-records-and-collections-via-clr-udt"></a>Emular registros e coleções por meio do tipo de dado CLR definido pelo usuário

Este artigo aborda como o Assistente de Migração do SQL Server (SSMA) para Oracle usa os tipos de dados (UDT) definidos pelo usuário SQL Server CLR (Common Language Runtime) para emular registros e coleções do Oracle.

## <a name="declaring-record-or-collection-types-and-variables"></a>Declarando tipos de registro ou de coleção e variáveis

O SSMA cria três UDTs baseados em CLR:

* `CollectionIndexInt`
* `CollectionIndexString`
* `Record`

O `CollectionIndexInt` tipo destina-se à emulação de coleções indexadas por inteiro `VARRAY`, como s, tabelas aninhadas e Matrizes associativas baseadas em chave de inteiro. O `CollectionIndexString` tipo é usado para matrizes associativas indexadas por chaves de caracteres. A funcionalidade de registro Oracle é emulada pelo `Record` tipo.

Todas as declarações dos tipos de registro ou coleção são convertidas nesta Declaração Transact-SQL:

```sql
declare @Collection$TYPE varchar(max) = '<type definition>'
```

Aqui `<type definition>` está um texto descritivo que identifica exclusivamente o tipo PL/SQL de origem.

Considere o exemplo a seguir:

```sql
DECLARE
    TYPE Manager IS RECORD
    (
        mgrid integer,
        mgrname varchar2(40),
        hiredate date
    );

    TYPE Manager_table is TABLE OF Manager INDEX BY PLS_INTEGER;

    Mgr_rec Manager;
    Mgr_table_rec Manager_table;
BEGIN
    mgr_rec.mgrid := 1;
    mgr_rec.mgrname := 'Mike';
    mgr_rec.hiredate := sysdate;

    select
        empno,
        ename,
        hiredate
    BULK COLLECT INTO
        mgr_table_rec
    FROM
        emp;
END;
```

Quando convertido usando o SSMA, ele se tornará o seguinte código Transact-SQL:

```sql
BEGIN
    DECLARE
        @CollectionIndexInt$TYPE varchar(max) =
            ' TABLE INDEX BY INT OF ( RECORD ( MGRID INT , MGRNAME STRING , HIREDATE DATETIME ) )'

    DECLARE
        @Mgr_rec$mgrid int,
        @Mgr_rec$mgrname varchar(40),
        @Mgr_rec$hiredate datetime2(0),
        @Mgr_table_rec dbo.CollectionIndexInt =
            dbo.CollectionIndexInt::[Null].SetType(@CollectionIndexInt$TYPE)

    SET @mgr_rec$mgrid = 1
    SET @mgr_rec$mgrname = 'Mike'
    SET @mgr_rec$hiredate = sysdatetime()

    SET @mgr_table_rec = @mgr_table_rec.RemoveAll()
    SET @mgr_table_rec =
        @mgr_table_rec.AssignData(
            ssma_oracle.fn_bulk_collect2CollectionComplex((
                SELECT
                    CAST(EMP.EMPNO AS int) AS mgrid,
                    EMP.ENAME AS mgrname,
                    EMP.HIREDATE AS hiredate
                FROM dbo.EMP
                FOR XML PATH
            ))
        )
END
```

Aqui, como a `Manager` tabela está associada a um índice numérico (`INDEX BY PLS_INTEGER`), a declaração T-SQL correspondente usada é do tipo `@CollectionIndexInt$TYPE`. Se a tabela estiver associada a um índice de conjunto de caracteres `VARCHAR2`, como, a declaração T-SQL correspondente será do `@CollectionIndexString$TYPE`tipo:

```sql
-- Oracle
TYPE Manager_table is TABLE OF Manager INDEX BY VARCHAR2(40);

-- SQL Server
@CollectionIndexString$TYPE varchar(max) =
    ' TABLE INDEX BY STRING OF ( RECORD ( MGRID INT , MGRNAME STRING , HIREDATE DATETIME ) )'
```

A funcionalidade de registro Oracle é emulada somente `Record` pelo tipo.

Cada um dos tipos, `CollectionIndexInt`, `CollectionIndexString`e `Record`, tem uma propriedade `[Null]` estática que retorna uma instância vazia. O `SetType` método é chamado para receber um objeto vazio de um tipo específico (como visto no exemplo acima).

## <a name="constructor-call-conversions"></a>Conversões de chamada de Construtor

A notação de construtor pode ser usada somente para `VARRAY`tabelas aninhadas e s, portanto, todas as chamadas de `CollectionIndexInt` Construtor explícitas são convertidas usando o tipo. Chamadas de Construtor vazias são `SetType` convertidas por chamada invocada na instância nula do `CollectionIndexInt`. A `[Null]` propriedade retorna a instância nula. Se o Construtor contiver uma lista de elementos, as chamadas de método especiais serão aplicadas sequencialmente para adicionar o valor à coleção.

Por exemplo:

```sql
-- Oracle

DECLARE
    TYPE nested_type IS TABLE OF VARCHAR2(20);
    TYPE varray_type IS VARRAY(5) OF INTEGER;

    v1 nested_type;
    v2 varray_type;
BEGIN
   v1 := nested_type('Arbitrary','number','of','strings');
   v2 := varray_type(10, 20, 40, 80, 160);
END;

-- SQL Server

BEGIN
    DECLARE
        @CollectionIndexInt$TYPE varchar(max) = ' VARRAY OF INT',
        @CollectionIndexInt$TYPE$2 varchar(max) = ' TABLE OF STRING',
        @v1 dbo.CollectionIndexInt,
        @v2 dbo.CollectionIndexInt

    SET @v1 =
        dbo.CollectionIndexInt::[Null]
            .SetType(@CollectionIndexInt$TYPE$2)
            .AddString('Arbitrary')
            .AddString('number')
            .AddString('of')
            .AddString('strings')

   SET @v2 =
       dbo.CollectionIndexInt::[Null]
            .SetType(@CollectionIndexInt$TYPE)
            .AddInt(10)
            .AddInt(20)
            .AddInt(40)
            .AddInt(80)
            .AddInt(160)
END
```

## <a name="referencing-and-assigning-record-and-collection-elements"></a>Referenciando e atribuindo elementos de registro e coleção

Cada um dos UDTs tem um conjunto de métodos que funcionam com elementos de vários tipos de dados. Por exemplo, o `SetDouble` método atribui um `float(53)` valor para registro ou coleção e `GetDouble` pode ler esse valor. Aqui está a lista completa de métodos:

```sql
GetCollectionIndexInt(@key <KeyType>) returns CollectionIndexInt;
SetCollectionIndexInt(@key <KeyType>, @value CollectionIndexInt) returns <UDT_type>;
GetCollectionIndexString(@key <KeyType>) returns CollectionIndexString;
SetCollectionIndexString(@key <KeyType>, @value CollectionIndexString) returns <UDT_type>;
Record GetRecord(@key <KeyType>) returns Record;
SetRecord(@key <KeyType>, @value Record) returns <UDT_type>;
GetString(@key <KeyType>) returns nvarchar(max);
SetString(@key <KeyType>, @value nvarchar(max)) returns nvarchar(max);
GetDouble(@key <KeyType>) returns float(53);
SetDouble(@key <KeyType>, @value float(53)) returns <UDT_type>;
GetDatetime(@key <KeyType>) returns datetime;
SetDatetime(@key <KeyType>, @value datetime) returns <UDT_type>;
GetVarbinary(@key <KeyType>) returns varbinary(max);
SetVarbinary(@key <KeyType>, @value varbinary(max)) returns <UDT_type>;
SqlDecimal GetDecimal(@key <KeyType>);
SetDecimal(@key <KeyType>, @value numeric) returns <UDT_type>;
GetXml(@key <KeyType>) returns xml;
SetXml(@key <KeyType>, @value xml) returns <UDT_type>;
GetInt(@key <KeyType>) returns bigint;
SetInt(@key <KeyType>, @value bigint) returns <UDT_type>;
```

Esses métodos são usados ao referenciar ou atribuir um valor a um elemento de uma coleção/registro.

```sql
-- Oracle
a_collection(i) := 'VALUE';

-- SQL Server
SET @a_collection = @a_collection.SetString(@i, 'VALUE');
```

Ao converter instruções de atribuição para coleções ou coleções multidimensionais com elementos de registro, o SSMA adiciona os seguintes métodos para fazer referência a um elemento pai dentro do método Set:

```sql
GetOrCreateCollectionIndexInt(@key <KeyType>) returns CollectionIndexInt;
GetOrCreateCollectionIndexString(@key <KeyType>) returns CollectionIndexString;
GetOrCreateRecord(@key <KeyType>) returns Record;
```

Por exemplo, uma coleção de elementos de registro é criada dessa forma:

```sql
-- Oracle
DECLARE
    TYPE rec_details IS RECORD (id int, name varchar2(20));
    TYPE ntb1 IS TABLE of rec_details index BY binary_integer;
    c ntb1;
BEGIN
    c(1).id := 1;
END;

-- SQL Server
DECLARE
   @CollectionIndexInt$TYPE varchar(max) =
       ' TABLE INDEX BY INT OF ( RECORD ( ID INT , NAME STRING ) )',
   @c dbo.CollectionIndexInt =
       dbo.CollectionIndexInt::[Null].SetType(@CollectionIndexInt$TYPE)

SET @c = @c.SetRecord(1, @c.GetOrCreateRecord(1).SetInt(N'ID', 1))
```

## <a name="collection-built-in-methods"></a>Métodos internos da coleção

O SSMA usa os seguintes métodos UDT para emular métodos internos de coleções PL/SQL.

Métodos de coleção do Oracle | `CollectionIndexInt`e `CollectionIndexString` equivalente
--- | ---
COUNT | `Count returns int`
Delete (excluir) | `RemoveAll() returns <UDT_type>`
EXCLUIR (n) | `Remove(@index int) returns <UDT_type>`
EXCLUIR (m, n) | `RemoveRange(@indexFrom int, @indexTo int) returns <UDT_type>`
EXISTS | `ContainsElement(@index int) returns bit`
ESTENDER | `Extend() returns <UDT_type>`
ESTENDER (n) | `Extend() returns <UDT_type>`
ESTENDER (n, i) | `ExtendDefault(@count int, @def int) returns <UDT_type>`
FIRST | `First() returns int`
LAST | `Last() returns int`
LIMIT | N/D
PRIOR | `Prior(@current int) returns int`
NEXT | `Next(@current int) returns int`
TRIM | `Trim() returns <UDT_type>`
TRIM (n) | `TrimN(@count int) returns <UDT_type>`

## <a name="bulk-collect-operation"></a>Operação de coleta em massa

O SSMA `BULK COLLECT INTO` converte instruções em `SELECT ... FOR XML PATH` SQL Server instrução, cujo resultado é encapsulado em uma das seguintes funções:

* `ssma_oracle.fn_bulk_collect2CollectionSimple`
* `ssma_oracle.fn_bulk_collect2CollectionComplex`

A escolha depende do tipo do objeto de destino. Essas funções retornam valores XML que podem ser analisados `CollectionIndexInt`por `CollectionIndexString` e `Record` tipos. Uma função `AssignData` especial atribui a coleção baseada em XML ao UDT.

O SSMA reconhece três tipos `BULK COLLECT INTO` de instruções.

### <a name="the-collection-contains-elements-with-scalar-types-and-the-select-list-contains-one-column"></a>A coleção contém elementos com tipos escalares e a `SELECT` lista contém uma coluna

```sql
-- Oracle
SELECT column_name_1
BULK COLLECT INTO <collection_name_1>
FROM <data_source>

-- SQL Server
SET @<collection_name_1> =
    @<collection_name_1>.AssignData(
        ssma_oracle.fn_bulk_collect2CollectionSimple(
            (SELECT column_name_1 FROM <data_source> FOR XML PATH)))
```

### <a name="the-collection-contains-elements-with-record-types-and-the-select-list-contains-one-column"></a>A coleção contém elementos com tipos de registro e a `SELECT` lista contém uma coluna

```sql
-- Oracle
SELECT
    column_name_1[, column_name_2...]
BULK COLLECT INTO
    <collection_name_1>
FROM
    <data_source>

-- SQL Server
SET @<collection_name_1> =
    @<collection_name_1>.AssignData(
        ssma_oracle.fn_bulk_collect2CollectionComplex(
            (SELECT
                column_name_1 as [collection_name_1_element_field_name_1],
                column_name_2 as [collection_name_1_element_field_name_2]
            FROM <data_source>
            FOR XML PATH)))
```

### <a name="the-collection-contains-elements-with-scalar-type-and-the-select-list-contains-multiple-columns"></a>A coleção contém elementos com tipo escalar e a `SELECT` lista contém várias colunas

```sql
-- Oracle
SELECT
    column_name_1[, column_name_2 ...]
BULK COLLECT INTO
    <collection_name_1>[, <collection_name_2> ...]
FROM
    <data_source>

-- SQL Server
;WITH bulkC AS (
    SELECT
        column_name_1 [collection_name_1_element_field_name_1],
        column_name_2 [collection_name_1_element_field_name_2]
    FROM
        <data_source>
)
SELECT
    @<collection_name_1> =
        @<collection_name_1>.AssignData(
            ssma_oracle.fn_bulk_collect2CollectionSimple(
                (SELECT
                    [collection_name_1_element_field_name_1]
                FROM
                    bulkC
                FOR XML PATH))),
    @<collection_name_2> =
        @<collection_name_2>.AssignData(
            ssma_oracle.fn_bulk_collect2CollectionSimple(
                (SELECT
                    [collection_name_1_element_field_name_2]
                FROM bulkC
                FOR XML PATH)))
```

## <a name="select-into-record"></a>SELECIONAR no registro

Quando o resultado da consulta Oracle é salvo em uma variável de registro PL/SQL, você tem duas opções dependendo da configuração do SSMA para **converter registro como uma lista de variáveis separadas** (disponível no menu **ferramentas** , **configurações do projeto**e conversão **geral** -> **Conversion**). Se o valor dessa configuração for **Sim** (o padrão), o SSMA não criará uma instância do tipo de registro. Em vez disso, ele divide o registro nos campos que constituem criando uma variável Transact-SQL separada por cada campo de registro. Se a configuração for **não**, o registro será instanciado e cada campo receberá um valor usando `Set` métodos.
