---
title: Criar chaves primárias | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- primary keys [SQL Server], creating
ms.assetid: 85c623ca-4656-4d70-a9db-ee4d897cd214
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e1f9d94f1ddf6f6d3e9a8ce73a263790acc516de
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "76259384"
---
# <a name="create-primary-keys"></a>Criar chaves primárias

[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Você pode definir uma chave primária no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. A criação de uma chave primária cria automaticamente um índice clusterizado correspondente exclusivo ou um índice não clusterizado, caso seja especificado dessa forma.

## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar

### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições

- Uma tabela pode conter apenas uma restrição PRIMARY KEY.

- Todas as colunas definidas em uma restrição PRIMARY KEY devem ser definidas como NOT NULL. Se a nulidade não for especificada, todas as colunas participantes de uma restrição FOREIGN KEY devem ter sua nulidade definida como NOT NULL.

### <a name="security"></a><a name="Security"></a> Segurança

#### <a name="permissions"></a><a name="Permissions"></a> Permissões

A criação de uma nova tabela com uma chave primária requer a permissão CREATE TABLE no banco de dados e a permissão ALTER no esquema no qual a tabela está sendo criada.

Criar uma chave primária em uma tabela existente requer a permissão ALTER na tabela.

## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio

### <a name="to-create-a-primary-key"></a>Para criar uma chave primária

1. No Pesquisador de Objetos, clique com o botão direito do mouse na tabela à qual você deseja adicionar uma restrição exclusiva e clique em **Design**.
2. No **Designer de Tabela**, clique no seletor de linha para a coluna de banco de dados que você deseja definir como chave primária. Se desejar selecionar colunas múltiplas, digite a tecla CTRL enquanto você clica nos seletores de linha para as outras colunas.
3. Clique com o botão direito do mouse no seletor de linha da coluna e selecione **Definir Chave Primária**.

> [!CAUTION]
> Se você quiser redefinir a chave primária, qualquer relação com a chave primária existente deve ser excluída antes que a nova chave primária seja criada. Uma mensagem avisará que as relações existentes serão excluídas automaticamente como parte desse processo.

Uma coluna de chave primária é identificada por um símbolo de chave primária em seu seletor de linha.

Se uma chave primária consistir em mais de uma coluna, serão permitidos valores duplicados em uma coluna, mas cada combinação de valores de todas as colunas na chave primária deve ser única.

Se você definir uma chave combinada, a ordem das colunas na chave primária corresponderá à ordem das colunas, como é mostrado na tabela. Entretanto, você poderá alterar a ordem de colunas depois que a chave primária for criada. Para obter mais informações, veja [Modificar chaves primárias](../../relational-databases/tables/modify-primary-keys.md).

## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL

### <a name="to-create-a-primary-key-in-an-existing-table"></a>Para criar uma chave primária em uma tabela existente

O exemplo a seguir cria uma chave primária na coluna `TransactionID` do banco de dados do AdventureWorks.

```sql
ALTER TABLE Production.TransactionHistoryArchive
   ADD CONSTRAINT PK_TransactionHistoryArchive_TransactionID PRIMARY KEY CLUSTERED (TransactionID);
```

### <a name="to-create-a-primary-key-in-a-new-table"></a>Para criar uma chave primária em uma nova tabela

O exemplo a seguir cria uma tabela e define uma chave primária na coluna `TransactionID` do banco de dados do AdventureWorks.

```sql
CREATE TABLE Production.TransactionHistoryArchive1
   (
      TransactionID int IDENTITY (1,1) NOT NULL
      , CONSTRAINT PK_TransactionHistoryArchive_TransactionID PRIMARY KEY CLUSTERED (TransactionID)
   )
;
```

### <a name="to-create-a-primary-key-with-clustered-index-in-a-new-table"></a>Para criar uma chave primária com um índice clusterizado em uma nova tabela

O exemplo a seguir cria uma tabela e define uma chave primária na coluna `CustomerID` e um índice clusterizado em `TransactionID` no banco de dados do AdventureWorks.

```sql
-- Create table to add the clustered index
CREATE TABLE Production.TransactionHistoryArchive1
   (
      CustomerID uniqueidentifier DEFAULT NEWSEQUENTIALID()
      , TransactionID int IDENTITY (1,1) NOT NULL
      , CONSTRAINT PK_TransactionHistoryArchive1_CustomerID PRIMARY KEY NONCLUSTERED (CustomerID)
   )
;

-- Now add the clustered index
CREATE CLUSTERED INDEX CIX_TransactionID ON Production.TransactionHistoryArchive1 (TransactionID);
```

## <a name="see-also"></a>Consulte Também

- [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)
- [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) 
- [table_constraint](../../t-sql/statements/alter-table-table-constraint-transact-sql.md)
