---
title: Definir opções de índice | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- ALLOW_ROW_LOCKS option
- SORT_IN_TEMPDB option
- DROP_EXISTING clause
- large data, indexes
- PAD_INDEX
- STATISTICS_NORECOMPUTE
- MAXDOP index option, setting
- index options [SQL Server]
- MAXDOP index option
- IGNORE_DUP_KEY option
- ALLOW_PAGE_LOCKS option
- OPTIMIZE_FOR_SEQUENTIAL_KEY option
- ONLINE
ms.assetid: 7969af33-e94c-41f7-ab89-9d9a2747cd5c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a140906c656b8d0843c4f9ef30092346a1f79804
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67732559"
---
# <a name="set-index-options"></a>Opções Set Index

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Este tópico descreve como modificar as propriedades de um índice no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].

 **Neste artigo**

- **Antes de começar:**

   [Limitações e restrições](#Restrictions)

   [Segurança](#Security)

- **Para modificar as propriedades de um índice usando:**

   [SQL Server Management Studio](#SSMSProcedure)

   [Transact-SQL](#TsqlProcedure)

## <a name="BeforeYouBegin"></a> Antes de começar

### <a name="Restrictions"></a> Limitações e restrições

- As opções a seguir são aplicadas imediatamente ao índice usando a cláusula SET na instrução ALTER INDEX: ALLOW_PAGE_LOCKS, ALLOW_ROW_LOCKS, OPTIMIZE_FOR_SEQUENTIAL_KEY, IGNORE_DUP_KEY e STATISTICS_NORECOMPUTE.
- As seguintes opções podem ser definidas quando você recompila um índice usando ALTER INDEX REBUILD ou CREATE INDEX WITH DROP_EXISTING: PAD_INDEX, FILLFACTOR, SORT_IN_TEMPDB, IGNORE_DUP_KEY, STATISTICS_NORECOMPUTE, ONLINE, ALLOW_ROW_LOCKS, ALLOW_PAGE_LOCKS, MAXDOP e DROP_EXISTING (somente CREATE INDEX).

### <a name="Security"></a> Segurança

#### <a name="Permissions"></a> Permissões

Requer a permissão ALTER na tabela ou exibição.

## <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio

### <a name="to-modify-the-properties-of-an-index-in-table-designer"></a>Para modificar as propriedades de um índice no Designer de Tabela

1. No Pesquisador de Objetos, clique no sinal de adição ao lado do banco de dados que contém a tabela na qual você modificar as propriedades de um índice.
2. Clique no sinal de adição para expandir a pasta **Tabelas** .
3. Clique com o botão direito do mouse na tabela em que você deseja modificar as propriedades de um índice e selecione **Design**.
4. No menu **Designer de Tabela** , clique em **Índices/Chaves**.
5. Selecione o índice a ser modificado. Suas propriedades aparecerão na grade principal.
6. Altere as configurações de alguma ou de todas as propriedades para personalizar o índice.
7. Clique em **Fechar**.
8. No menu **Arquivo** , selecione **Salvar**_table_name_.

### <a name="to-modify-the-properties-of-an-index-in-object-explorer"></a>Para modificar as propriedades de um índice no Pesquisador de Objetos

1. No Pesquisador de Objetos, clique no sinal de adição ao lado do banco de dados que contém a tabela na qual você modificar as propriedades de um índice.
2. Clique no sinal de adição para expandir a pasta **Tabelas** .
3. Clique no sinal de adição para expandir a tabela na qual você deseja modificar as propriedades do índice.
4. Clique no sinal de adição para expandir a pasta **Índices** .
5. Clique com o botão direito do mouse no índice cujas propriedades serão modificadas e selecione **Propriedades**.
6. Em **Selecione uma página**, selecione **Opções**.
7. Altere as configurações de alguma ou de todas as propriedades para personalizar o índice.
8. Para adicionar, remover ou alterar a posição de uma coluna de índice, selecione a página **Geral** na caixa de diálogo **Propriedades do Índice –** _index_name_ . Para obter mais informações, consulte [Index Properties F1 Help](../../relational-databases/indexes/index-properties-f1-help.md).

## <a name="TsqlProcedure"></a> Usando o Transact-SQL

### <a name="to-see-the-properties-of-all-the-indexes-in-a-table"></a>Para ver as propriedades de todos os índices em uma tabela

O exemplo a seguir mostra as propriedades de todos os índices em uma tabela no banco de dados AdventureWorks.

```sql
SELECT i.name AS index_name
   , i.type_desc
   , i.is_unique
   , ds.type_desc AS filegroup_or_partition_scheme
   , ds.name AS filegroup_or_partition_scheme_name
   , i.ignore_dup_key
   , i.is_primary_key
   , i.is_unique_constraint
   , i.fill_factor
   , i.is_padded
   , i.is_disabled
   , i.allow_row_locks
   , i.allow_page_locks
   , i.has_filter
   , i.filter_definition
FROM sys.indexes AS i
   INNER JOIN sys.data_spaces AS ds
      ON i.data_space_id = ds.data_space_id
   WHERE is_hypothetical = 0 AND i.index_id <> 0
       AND i.object_id = OBJECT_ID('HumanResources.Employee')
;
```

#### <a name="to-set-the-properties-of-an-index"></a>Para definir as propriedades de um índice

O exemplo a seguir define as propriedades dos índices em um banco de dados AdventureWorks.

[!code-sql[IndexDDL#AlterIndex4](../../relational-databases/indexes/codesnippet/tsql/set-index-options_1.sql)]

[!code-sql[IndexDDL#AlterIndex2](../../relational-databases/indexes/codesnippet/tsql/set-index-options_2.sql)]

Para obter mais informações, consulte [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md).
