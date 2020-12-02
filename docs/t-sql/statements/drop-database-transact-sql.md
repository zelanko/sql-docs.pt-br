---
description: DROP DATABASE (Transact-SQL)
title: DROP DATABASE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/21/2019
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP DATABASE
- DROP_DATABASE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- snapshots [SQL Server database snapshots], deleting
- removing databases
- database snapshots [SQL Server], removing
- deleting databases
- dropping databases
- databases [SQL Server], dropping
- DROP DATABASE statement
- database removal [SQL Server], DROP DATABASE statement
ms.assetid: 477396a9-92dc-43c9-9b97-42c8728ede8e
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0ae3af2eb84fa18777c0d0fe55503ea60bf5c303
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96127446"
---
# <a name="drop-database-transact-sql"></a>DROP DATABASE (Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Remove um ou mais bancos de dados de usuário ou instantâneos do banco de dados de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>Sintaxe

```syntaxsql
-- SQL Server Syntax
DROP DATABASE [ IF EXISTS ] { database_name | database_snapshot_name } [ ,...n ] [;]
```

```syntaxsql
-- Azure SQL Database, Azure Synapse Analytics and Analytics Platform System Syntax
DROP DATABASE database_name [;]
```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos

*IF EXISTS*
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ( [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até [versão atual](https://go.microsoft.com/fwlink/p/?LinkId=299658)).

Remove condicionalmente o banco de dados somente se ele já existe.

*database_name* Especifica o nome do banco de dados a ser removido. Para exibir uma lista de bancos de dados, use a exibição de catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).

*database_snapshot_name*
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.

Especifica o nome de um instantâneo do banco de dados a ser removido.

## <a name="general-remarks"></a>Comentários gerais

Um banco de dados pode ser removido independentemente de seu estado: offline, somente leitura, suspeito e assim por diante. Para exibir o estado atual de um banco de dados, use a exibição de catálogo **sys.databases**.

Um banco de dados cancelado poderá ser recriado somente por meio da restauração de um backup. Não é possível efetuar backup de instantâneos do banco de dados, portanto, eles não podem ser restaurados.

Quando um banco de dados é removido, o [banco de dados mestre](../../relational-databases/databases/master-database.md) deve ser copiado em backup.

O descarte de um banco de dados exclui o banco de dados de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e exclui os arquivos de disco físicos usados pelo banco de dados. Se o banco de dados ou qualquer um de seus arquivos estiverem offline quando forem cancelados, os arquivos em disco não serão excluídos. Esses arquivos podem ser excluídos manualmente usando o Windows Explorer. Para remover um banco de dados do servidor atual sem excluir os arquivos do sistema de arquivos, use [sp_detach_db](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md).

> [!WARNING]
> A remoção de um banco de dados que tem backups de FILE_SNAPSHOT associados a ele terá êxito, mas os arquivos de banco de dados que têm instantâneos associados não serão excluídos, para evitar a anulação dos backups que referenciam esses arquivos de banco de dados. O arquivo será truncado, mas não será fisicamente excluído para manter os backups de FILE_SNAPSHOT intactos. Para obter mais informações, consulte [Backup e restauração do SQL Server com o serviço de Armazenamento de Blobs do Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md). **Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] à [versão atual](https://go.microsoft.com/fwlink/p/?LinkId=299658).

### [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

O descarte de um instantâneo de banco de dados o exclui de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e exclui os arquivos físicos esparsos do Sistema de Arquivos NTFS utilizados pelo instantâneo. Para obter informações sobre como usar arquivos esparsos por instantâneos de banco de dados, consulte [Instantâneos de banco de dados](../../relational-databases/databases/database-snapshots-sql-server.md). O cancelamento de um instantâneo do banco de dados limpa o cache de plano para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A limpeza do cache de planos gera uma recompilação de todos os planos de execução subsequentes e pode provocar uma redução repentina e temporária do desempenho de consultas. Para cada armazenamento em cache limpo no cache de planos, o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contém a seguinte mensagem informativa: "[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] encontrou %d ocorrências de liberação de armazenamento em cache para o armazenamento em cache '%s' (parte do cache de planos) devido a operações de reconfiguração ou manutenção do banco de dados". Essa mensagem é registrada a cada cinco minutos, contanto que o cache seja liberado dentro desse intervalo de tempo.

## <a name="interoperability"></a>Interoperabilidade

### <a name="sql-server"></a>SQL Server

Para cancelar um banco de dados publicado para replicação transacional ou publicado ou inscrito para replicação de mesclagem, você deve primeiro remover a replicação do banco de dados. Se um banco de dados estiver danificado ou não for possível remover a replicação primeiro ou ambos, na maioria dos casos você ainda pode cancelar o banco de dados usando ALTER DATABASE para definir o banco de dados offline e depois cancelá-lo.

Se o banco de dados estiver envolvido em envio de logs, remova o envio do log antes de cancelá-lo. Para obter mais informações, consulte [Sobre o Envio de Logs](../../database-engine/log-shipping/about-log-shipping-sql-server.md).

## <a name="limitations-and-restrictions"></a>Limitações e Restrições

Os [bancos de dados do sistema](../../relational-databases/databases/system-databases.md) não podem ser removidos.

Uma instrução DROP DATABASE deve ser executada no modo de confirmação automática e não é permitida uma transação explícita ou implícita. O modo de confirmação automática é o modo padrão de gerenciamento de transações.

Você não pode cancelar um banco de dados que estiver sendo utilizado. Isso significa abrir para leitura ou gravação por qualquer usuário. Uma forma de remover usuários do banco de dados é usar ALTER DATABASE para definir o banco de dados como SINGLE_USER.

> [!WARNING]
> Essa não é uma abordagem à prova de falhas, pois que a primeira conexão consecutiva feita por qualquer thread receberá o thread SINGLE_USER, fazendo com que a conexão falhe. O SQL Server não fornece um modo interno para remover bancos de dados sob carga.

### [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

Qualquer instantâneo de banco de dados em um banco de dados deve ser cancelado antes que o banco de dados seja cancelado.

A remoção de um banco de dados permite que o Stretch Database não remova os dados remotos. Se você deseja excluir os dados remotos, precisa removê-los manualmente.

### [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

Você deve estar conectado ao banco de dados mestre para descartar um banco de dados.

 A instrução DROP DATABASE deve ser a única instrução em um lote de SQL, e você poderá descartar apenas um banco de dados de cada vez.

### [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]

Você deve estar conectado ao banco de dados mestre para descartar um banco de dados.

A instrução DROP DATABASE deve ser a única instrução em um lote de SQL, e você poderá descartar apenas um banco de dados de cada vez.

## <a name="permissions"></a>Permissões

### [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

Exige a permissão **CONTROL** no banco de dados, a permissão **ALTER ANY DATABASE** ou a associação na função de banco de dados fixa **db_owner**.

### [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

Somente o logon da entidade de segurança no nível do servidor (criado pelo processo de provisionamento) ou os membros da função de banco de dados **dbmanager** podem remover um banco de dados.

### [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

Exige a permissão **CONTROL** no banco de dados, a permissão **ALTER ANY DATABASE** ou a associação na função de banco de dados fixa **db_owner**.

## <a name="examples"></a>Exemplos

### <a name="a-dropping-a-single-database"></a>a. Removendo um único banco de dados

O exemplo a seguir remove o nome do banco de dados `Sales`:

```sql
DROP DATABASE Sales;
```

### <a name="b-dropping-multiple-databases"></a>B. Removendo vários bancos de dados

**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.

O exemplo a seguir remove cada um dos bancos de dados listados.

```sql
DROP DATABASE Sales, NewSales;
```

### <a name="c-dropping-a-database-snapshot"></a>C. Removendo um instantâneo de banco de dados

**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.

O exemplo a seguir remove um instantâneo do banco de dados, chamado `sales_snapshot0600`, sem afetar o banco de dados de origem.

```sql
DROP DATABASE sales_snapshot0600;
```

## <a name="see-also"></a>Consulte Também

- [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md)
- [CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md?view=sql-server-2017)
- [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)
- [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)
