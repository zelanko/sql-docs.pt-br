---
title: COLLATE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- COLLATE
- COLLATE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- collations [SQL Server], COLLATE clause
- COLLATE clause
ms.assetid: 76763ac8-3e0d-4bbb-aa53-f5e7da021daa
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7a706193058256747ba1ec2fa71c7641cdecc4e8
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86011327"
---
# <a name="collate-transact-sql"></a>COLLATE (Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Define uma ordenação de uma coluna de banco de dados ou de tabela ou uma operação de conversão de ordenação quando aplicado a uma expressão de cadeia de caracteres. O nome da ordenação pode ser um nome de ordenação do Windows ou um nome de ordenação SQL. Se ele não for especificado durante a criação do banco de dados, a ordenação padrão da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será atribuída ao banco de dados. Se ele não for especificado durante a criação da coluna de tabela, a ordenação padrão do banco de dados será atribuída à coluna.

![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>Sintaxe

```syntaxsql
COLLATE { <collation_name> | database_default }
<collation_name> :: =
    { Windows_collation_name } | { SQL_collation_name }
```

## <a name="arguments"></a>Argumentos

*collation_name* É o nome da ordenação a ser aplicada à expressão, definição de coluna ou definição de banco de dados. *collation_name* pode ser apenas um *Windows_collation_name* ou um *SQL_collation_name* especificado. *collation_name* deve ser um valor literal. *collation_name* não pode ser representado por uma variável ou expressão.

*Windows_collation_name* é o nome de ordenação de um [Nome de Ordenação do Windows](../../t-sql/statements/windows-collation-name-transact-sql.md).

*SQL_collation_name* é o nome de ordenação de um [Nome de Ordenação do SQL Server](../../t-sql/statements/sql-server-collation-name-transact-sql.md).

**database_default** Faz com que a cláusula COLLATE herde a ordenação do banco de dados atual.

## <a name="remarks"></a>Comentários

A cláusula COLLATE pode ser especificada em vários níveis. Entre elas estão as seguintes:

1. Criando ou alterando um banco de dados.

    Você pode usar a cláusula COLLATE da instrução `CREATE DATABASE` ou `ALTER DATABASE` para especificar a ordenação padrão do banco de dados. Também é possível especificar uma ordenação ao criar um banco de dados usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Se uma ordenação não for especificada, o banco de dados será atribuído à ordenação padrão da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

    > [!NOTE]
    > As ordenações somente Unicode do Windows podem ser usadas com a cláusula COLLATE apenas para aplicar ordenações aos tipos de dados **nchar**, **nvarchar** e **ntext** em dados nos níveis de coluna e de expressão. Elas não podem ser usadas com a cláusula COLLATE para definir ou alterar a ordenação de uma instância de banco de dados ou de servidor.

2. Criando ou alterando uma coluna de tabela.

    Você pode especificar ordenações para cada coluna de cadeia de caracteres usando a cláusula COLLATE da instrução `CREATE TABLE` ou `ALTER TABLE`. Também é possível especificar uma ordenação ao criar uma tabela usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Se uma ordenação não for especificada, a coluna será atribuída à ordenação padrão do banco de dados.

    Também é possível usar a opção `database_default` na cláusula COLLATE para especificar que uma coluna de uma tabela temporária use o padrão de ordenação do banco de dados de usuário atual para a conexão em vez de **tempdb**.

3. Convertendo a ordenação de uma expressão.

    Você pode usar a cláusula COLLATE para aplicar uma expressão de caractere a uma determinada ordenação. Literais de caracteres e variáveis são atribuídos à ordenação padrão do banco de dados atual. Referências de coluna são atribuídas à ordenação de definição da coluna.

A ordenação de um identificador depende do nível em que está definido. Os identificadores de objetos no nível de instância, como logons e nomes de banco de dados, são atribuídos à ordenação padrão da instância. Os identificadores de objetos em um banco de dados, como tabelas, exibições e nomes de coluna, são atribuídos à ordenação padrão do banco de dados. Por exemplo, duas tabelas com nomes que diferem apenas em maiúsculas e minúsculas podem ser criadas em um banco de dados que possui ordenação que diferencia maiúsculas e minúsculas, mas não podem ser criadas em um banco de dados com uma ordenação que não faz essa diferenciação. Para obter mais informações, consulte [Database Identifiers](../../relational-databases/databases/database-identifiers.md).

Variáveis, rótulos GOTO, procedimentos armazenados temporários e tabelas temporárias podem ser criados quando o contexto de conexão é associado a um banco de dados e, em seguida, referenciado quando o contexto é alternado para outro banco de dados. Os identificadores para variáveis, os rótulos GOTO, os procedimentos armazenados temporários e as tabelas temporárias estão na ordenação padrão da instância de servidor.

A cláusula COLLATE pode ser aplicada apenas aos tipos de dados **char**, **varchar**, **text**, **nchar**, **nvarchar** e **ntext**.

COLLATE usa *collate_name* para referenciar o nome da ordenação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do Windows a ser aplicada à expressão, à definição de coluna ou à definição de banco de dados. *collation_name* pode ser somente um *Windows_collation_name* ou *SQL_collation_name* especificado e o parâmetro deve conter um valor literal. *collation_name* não pode ser representado por uma variável ou expressão.

Geralmente, as ordenações são identificadas por um nome de ordenação, exceto na Instalação. Na Instalação, especifique o designador de ordenação raiz (a localidade da ordenação) para ordenações do Windows e, em seguida, especifique opções de classificação que diferenciam ou não maiúsculas e minúsculas ou caracteres com ou sem acentos.

Você pode executar a função de sistema [fn_helpcollations](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md) para recuperar uma lista de todos os nomes de ordenações válidos para ordenações do Windows e SQL Server:

```sql
SELECT name, description
FROM fn_helpcollations();
```

O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] só pode aceitar páginas de código que tenham suporte no sistema operacional subjacente. Quando você executa uma ação que depende de ordenações, a ordenação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usada pelo objeto referenciado deve usar uma página de código com suporte no sistema operacional executado no computador. Essas ações podem incluir o seguinte:

- Especificando uma ordenação padrão para um banco de dados ao criar ou alterar o banco de dados.
- Especificando uma ordenação para uma coluna ao criar ou alterar uma tabela.
- Ao restaurar ou anexar um banco de dados, a ordenação padrão do banco de dados e a ordenação de qualquer coluna ou parâmetro **char**, **varchar** e **text** no banco de dados devem ser compatíveis com o sistema operacional.

> [!NOTE]
> Há suporte para conversões de página de código em tipos de dados **char** e **varchar**, mas não no tipo de dados **text**. A perda de dados durante traduções de página de código não é informada.
>
> Se a ordenação especificada ou a ordenação usada pelo objeto referenciado usar uma página de código não compatível com o Windows, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exibirá um erro.

## <a name="examples"></a>Exemplos

### <a name="a-specifying-collation-during-a-select"></a>a. Especificando a ordenação durante uma instrução SELECT

O exemplo a seguir cria uma tabela simples e insere 4 linhas. Depois, o exemplo aplica duas ordenações ao selecionar dados da tabela, demonstrando como `Chiapas` é classificado de forma diferente.

```sql
CREATE TABLE Locations
(Place varchar(15) NOT NULL);
GO
INSERT Locations(Place) VALUES ('Chiapas'),('Colima')
                             , ('Cinco Rios'), ('California');
GO
--Apply an typical collation
SELECT Place FROM Locations
ORDER BY Place
COLLATE Latin1_General_CS_AS_KS_WS ASC;
GO
-- Apply a Spanish collation
SELECT Place FROM Locations
ORDER BY Place
COLLATE Traditional_Spanish_ci_ai ASC;
GO
```

Estes são os resultados da primeira consulta.

```output
Place
-------------
California
Chiapas
Cinco Rios
Colima
```

Estes são os resultados da segunda consulta.

```output
Place
-------------
California
Cinco Rios
Colima
Chiapas
```

### <a name="b-additional-examples"></a>B. Mais exemplos

Para obter mais exemplos que usam **COLLATE**, confira [CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md?view=sql-server-2017#examples), exemplo **G. Criando um banco de dados e especificando um nome de ordenação e opções** e [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md#alter_column), exemplo **V. Alterando uma ordenação de coluna**.

## <a name="see-also"></a>Consulte Também

- [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)
- [Suporte a ordenações e a Unicode](../../relational-databases/collations/collation-and-unicode-support.md)
- [Precedência de ordenação](../../t-sql/statements/collation-precedence-transact-sql.md)
- [Constantes](../../t-sql/data-types/constants-transact-sql.md)
- [CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md?view=sql-server-2017)
- [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)
- [DECLARE @local_variable](../../t-sql/language-elements/declare-local-variable-transact-sql.md)
- [Tipo de dados de tabela](../../t-sql/data-types/table-transact-sql.md)
